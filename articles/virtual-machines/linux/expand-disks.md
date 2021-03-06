---
title: Vouw de virtuele harde schijven op een Linux-VM in Azure | Microsoft Docs
description: Meer informatie over het uitbreiden van virtuele harde schijven op een Linux-VM met de Azure CLI
services: virtual-machines-linux
documentationcenter: ''
author: roygara
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/15/2018
ms.author: rogarana
ms.openlocfilehash: 62057d3041aa83e0097b688b48386b80f5c4f87e
ms.sourcegitcommit: 17633e545a3d03018d3a218ae6a3e4338a92450d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/22/2018
ms.locfileid: "49637286"
---
# <a name="expand-virtual-hard-disks-on-a-linux-vm-with-the-azure-cli"></a>Vouw de virtuele harde schijven op een Linux-VM met de Azure CLI

In dit artikel wordt beschreven hoe u beheerde schijven voor een Linux-machine (VM) met de Azure CLI uitbreiden. U kunt [gegevensschijven toevoegen](add-disk.md) te voorzien in extra opslag ruimte, en u kunt ook een bestaande gegevensschijf uitbreiden. De standaardgrootte van de virtuele harde schijf voor het besturingssysteem (OS) is doorgaans 30 GB op een Linux-VM in Azure. 

> [!WARNING]
> Zorg ervoor dat altijd dat u maakt u een back-up van uw gegevens voordat u de schijf uitvoert de grootte van bewerkingen. Zie voor meer informatie, [maakt u een Back-up van virtuele Linux-machines in Azure](tutorial-backup-vms.md).

## <a name="expand-an-azure-managed-disk"></a>Een Azure beheerde schijf uitbreiden
Zorg ervoor dat u de meest recente [Azure CLI](/cli/azure/install-az-cli2) geïnstalleerd en bent aangemeld bij een Azure-account met behulp van [az login](/cli/azure/reference-index#az-login).

Dit artikel gebruikmaken van een bestaande virtuele machine in Azure met ten minste één gegevensschijf die is gekoppeld en voorbereid. Als u nog geen een virtuele machine die u kunt gebruiken, raadpleegt u [maken en een virtuele machine met gegevensschijven voorbereiden](tutorial-manage-disks.md#create-and-attach-disks).

Vervang in de volgende voorbeelden voorbeeld parameternamen zoals *myResourceGroup* en *myVM* door uw eigen waarden.

1. Bewerkingen op virtuele harde schijven kunnen niet worden uitgevoerd met de VM wordt uitgevoerd. Toewijzing ongedaan maken van uw virtuele machine met [az vm deallocate](/cli/azure/vm#az-vm-deallocate). Het volgende voorbeeld wordt de virtuele machine met de naam de toewijzing ingetrokken *myVM* in de resourcegroep met de naam *myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > De virtuele machine moet ongedaan worden gemaakt om uit te breiden van de virtuele harde schijf. Stoppen van de virtuele machine met `az vm stop` heeft niet de rekenresources die zijn uitgebracht. Release van compute-resources, gebruikt `az vm deallocate`.

1. Een lijst met beheerde schijven weergeven in een resourcegroep met [az Schijflijst](/cli/azure/disk#az-disk-list). Het volgende voorbeeld wordt een lijst met beheerde schijven in de resourcegroep met de naam *myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    Vouw de benodigde schijfruimte met [az disk update](/cli/azure/disk#az-disk-update). Het volgende voorbeeld wordt de beheerde schijf met de naam *myDataDisk* naar *200* GB:

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > Als u een beheerde schijf uitbreidt, wordt de grootte van de bijgewerkte naar boven afgerond naar de dichtstbijzijnde beheerde schijf. Zie voor een tabel van de grootte van de beschikbare beheerde schijf en lagen [Azure overzicht van Managed Disks - prijzen en facturering](../windows/managed-disks-overview.md#pricing-and-billing).

1. Start de virtuele machine met [az vm start](/cli/azure/vm#az-vm-start). Het volgende voorbeeld wordt de virtuele machine met de naam *myVM* in de resourcegroep met de naam *myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```


## <a name="expand-a-disk-partition-and-filesystem"></a>Vouw een partitie en bestandssysteem
Vouw de onderliggende partitie en bestandssysteem voor het gebruik van een uitgebreide schijf.

1. SSH naar uw virtuele machine met de juiste referenties. U kunt zien dat het openbare IP-adres van uw virtuele machine met [az vm show](/cli/azure/vm#az-vm-show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

1. Vouw de onderliggende partitie en bestandssysteem.

    a. Als de schijf al is gekoppeld, deze ontkoppelen:

    ```bash
    sudo umount /dev/sdc1
    ```

    b. Gebruik `parted` naar schijfinformatie weergeven en het formaat van de partitie:

    ```bash
    sudo parted /dev/sdc
    ```

    Informatie weergeven over de bestaande partitie-indeling met `print`. De uitvoer is vergelijkbaar met het volgende voorbeeld, waarin dat de onderliggende schijf is 215 GB:

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome to GNU Parted! Type 'help' to view a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    c. Vouw de partitie met `resizepart`. Voer het partitienummer *1*, en een grootte voor de nieuwe partitie:

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. Als u wilt afsluiten, voer `quit`.

1. Met de partitie is gewijzigd, controleert u of de consistentie van de partitie met `e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

1. Formaat van het bestandssysteem met `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

1. Koppel de partitie op de gewenste locatie, zoals `/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

1. Gebruiken om te controleren of de besturingssysteemschijf is gewijzigd, `df -h`. De volgende voorbeelduitvoer ziet u het gegevensstation */dev/sdc1* is nu 200 GB:

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>Volgende stappen
* Als u extra opslag nodig hebt, kunt u ook [gegevensschijven toevoegen aan een Linux-VM](add-disk.md). 
* Zie voor meer informatie over schijfversleuteling [schijven op een Linux-VM met de Azure CLI versleutelen](encrypt-disks.md).

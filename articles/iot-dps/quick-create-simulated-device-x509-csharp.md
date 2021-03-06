---
title: Een gesimuleerd X.509-apparaat met C# inrichten voor Azure IoT Hub | Microsoft Docs
description: 'Azure-quickstart: een gesimuleerd X.509-apparaat met de SDK voor C# maken en inrichten voor Azure IoT Hub Device Provisioning Service'
author: wesmc7777
ms.author: wesmc
ms.date: 04/09/18
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: 1d42280935c406a7af0e632434749b2b082ea8b8
ms.sourcegitcommit: 4ecc62198f299fc215c49e38bca81f7eb62cdef3
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/24/2018
ms.locfileid: "47039664"
---
# <a name="create-and-provision-a-simulated-x509-device-using-c-device-sdk-for-iot-hub-device-provisioning-service"></a>Een gesimuleerd X.509-apparaat met de SDK voor C# maken en inrichten voor IoT Hub Device Provisioning Service
[!INCLUDE [iot-dps-selector-quick-create-simulated-device-x509](../../includes/iot-dps-selector-quick-create-simulated-device-x509.md)]

In deze stappen ziet u hoe u met de [SDK voor C# voor Azure IoT Hub](https://github.com/Azure/azure-iot-sdk-csharp) een gesimuleerd X.509-apparaat maakt op een ontwikkelcomputer met Windows OS en het codevoorbeeld gebruikt om dit gesimuleerde apparaat te verbinden met de Device Provisioning Service en uw IoT-hub.

Als u niet bekend bent met het proces van automatische inrichting, bekijk dan ook de [Concepten voor automatische inrichting](concepts-auto-provisioning.md). Controleer ook of u de stappen in [IoT Hub Device Provisioning Service instellen met Azure Portal](./quick-setup-auto-provision.md) hebt voltooid voordat u verdergaat. 

[!INCLUDE [IoT Device Provisioning Service basic](../../includes/iot-dps-basic.md)]

<a id="setupdevbox"></a>
## <a name="prepare-the-development-environment"></a>De ontwikkelomgeving voorbereiden 

1. Zorg ervoor dat de [core-SDK voor .NET](https://www.microsoft.com/net/download/windows) op uw computer geïnstalleerd. 

1. Zorg ervoor dat `git` op de computer wordt geïnstalleerd en toegevoegd aan de omgevingsvariabelen die voor het opdrachtvenster toegankelijk zijn. Zie [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) (Git-clienthulpprogramma's van Software Freedom Conservancy) om de nieuwste versie van `git`-hulpprogramma's te installeren, waaronder **Git Bash**, de opdrachtregel-app die u kunt gebruiken voor interactie met de lokale Git-opslagplaats. 

4. Open een opdrachtprompt of Git Bash. Kloon de GitHub-opslagplaats [Azure IoT SDK voor C#](https://github.com/Azure/azure-iot-sdk-csharp):
    
    ```cmd
    git clone --recursive https://github.com/Azure/azure-iot-sdk-csharp.git
    ```

## <a name="create-a-self-signed-x509-device-certificate-and-individual-enrollment-entry"></a>Een zelfondertekend X.509-certificaat voor apparaten en een vermelding voor afzonderlijke registratie maken

In deze sectie gebruikt u een zelf-ondertekend X.509-certificaat. Het is hierbij belangrijk dat u rekening houdt met het volgende:

* Zelfondertekende certificaten zijn alleen voor testdoeleinden en moeten niet in productieomgevingen worden gebruikt.
* De standaardvervaltermijn voor een zelfondertekend certificaat is één jaar.

U gaat voorbeeldcode van de [Azure IoT C-SDK voor .NET](https://github.com/Azure/azure-iot-sdk-csharp.git) gebruiken om het certificaat te maken dat moet worden gebruikt met de afzonderlijke inschrijvingsvermelding voor het gesimuleerde apparaat.


1. Ga op een opdrachtprompt naar de projectmap met de voorbeeldcode voor het inrichten van het de X.509-apparaat.

    ```cmd
    cd .\azure-iot-sdk-csharp\provisioning\device\samples\ProvisioningDeviceClientX509
    ```

2. De voorbeeldcode is ingesteld voor het gebruik van X.509-certificaten die zijn opgeslagen in een met PKCS12 opgemaakt bestand (certificate.pfx) met wachtwoordbeveiliging. Bovendien hebt u een certificaatbestand met een openbare sleutel (certificate.cer) nodig om later in deze quickstart een afzonderlijke registratie te maken. Voer de volgende opdracht uit om een zelfondertekend certificaat en de bijbehorende CER- en PFX-bestanden te genereren:

    ```cmd
    powershell .\GenerateTestCertificate.ps1
    ```

3. Het script vraagt u om een PFX-wachtwoord. Onthoud dit wachtwoord, want dit moet u gebruiken wanneer u het voorbeeld gaat uitvoeren.

    ![ PFX-wachtwoord invoeren](./media/quick-create-simulated-device-x509-csharp/generate-certificate.png)  


4. Meld u aan bij Azure Portal, klik in het linkermenu op de knop **All resources** en open uw Provisioning-service.

5. Selecteer **Manage enrollments** in de overzichtsblade van Device Provisioning Service. Selecteer het tabblad **Afzonderlijke registraties** en klik vervolgens op de knop **Afzonderlijke inschrijving toevoegen** bovenaan. 

6. Voer onder het deelvenster **Inschrijving toevoegen** de volgende gegevens in:
    - Selecteer **X.509** als *mechanisme* voor identiteitscontrole.
    - Klik onder het *PEM- of CER-bestand van het primaire certificaat* op *Selecteer een bestand* om het certificaatbestand **certificate.cer** te selecteren dat in de vorige stappen is gemaakt.
    - Laat **Apparaat-id** leeg. Uw apparaat wordt ingericht met de apparaat-id ingesteld op de algemene naam (CN) in het X.509-certificaat, **iothubx509device1**. Dit is ook de naam die wordt gebruikt voor de registratie-id voor de vermelding voor de afzonderlijke registratie. 
    - Desgewenst kunt u de volgende informatie verstrekken:
        - Selecteer een IoT-hub die is gekoppeld aan uw inrichtingsservice.
        - Werk de **initiële status van de apparaatdubbel** bij met de gewenste beginconfiguratie voor het apparaat.
    - Klik op de knop **Save** als u klaar bent. 

    [![Afzonderlijke inschrijving voor X.509-attestation toevoegen in de portal](./media/quick-create-simulated-device-x509-csharp/device-enrollment.png)](./media/quick-create-simulated-device-x509-csharp/device-enrollment.png#lightbox)
    
   Als het apparaat is ingeschreven, wordt het X.509-apparaat weergegeven als **iothubx509device1** onder de kolom *Registratie-id* op het tabblad *Afzonderlijke registraties*. 

## <a name="provision-the-simulated-device"></a>Het gesimuleerde apparaat inrichten

1. Ga naar de blade **Overzicht** voor de provisioning-service en noteer de waarde van **_Id-bereik_**.

    ![Device Provisioning Service-eindpuntgegevens uit de portalblade extraheren](./media/quick-create-simulated-device-x509-csharp/copy-scope.png) 


2. Typ de volgende opdracht om de voorbeeldcode voor het X.509-apparaat te bouwen en uit te voeren. Vervang de waarde voor `<IDScope>` door het id-bereik voor uw provisioning-service. 

    ```cmd
    dotnet run <IDScope>
    ```

3. Als dit wordt gevraagd, voert u het wachtwoord in voor het PFX-bestand dat u eerder hebt gemaakt. De gegevens van uw IoT-hub leest u in de berichten die het opstarten van het apparaat en het verbinding maken met Device Provisioning Service simuleren. 

    ![Voorbeelduitvoer van apparaat](./media/quick-create-simulated-device-x509-csharp/sample-output.png) 

4. Controleer of het apparaat is ingericht. Als het gesimuleerde apparaat is ingericht met de IoT-hub die is gekoppeld met de provisioning-service, wordt de apparaat-id weergegeven op de blade **IoT-apparaten** van de hub. 

    ![Apparaat wordt geregistreerd voor de IoT-hub](./media/quick-create-simulated-device-x509-csharp/registration.png) 

    Als u de standaardwaarde van de *initiële status van de apparaatdubbel* hebt gewijzigd in de inschrijvingsvermelding voor uw apparaat, kan de gewenste status van de dubbel uit de hub worden gehaald en er dienovereenkomstig naar worden gehandeld. Zie [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md) (Apparaatdubbelen begrijpen en gebruiken in IoT Hub) voor meer informatie


## <a name="clean-up-resources"></a>Resources opschonen

Als u wilt blijven doorwerken met het voorbeeld van de apparaatclient en deze beter wilt leren kennen, wis de resources die in deze Snelstartgids zijn gemaakt dan niet. Als u niet wilt doorgaan, gebruikt u de volgende stappen om alle resources die via deze Snelstartgids zijn gemaakt, te verwijderen.

1. Sluit het uitvoervenster van het voorbeeld van de apparaatclient op de computer.
1. Sluit het TPM-simulatorvenster op de computer.
1. Klik in het linkermenu in Azure Portal op **All resources** en selecteer uw Device Provisioning-service. Klik bovenaan de blade **Alle resources** op **Verwijderen**.  
1. Klik in het linkermenu in de Azure Portal op **Alle resources** en selecteer vervolgens uw IoT-hub. Klik bovenaan de blade **Alle resources** op **Verwijderen**.  

## <a name="next-steps"></a>Volgende stappen

In deze quickstart hebt u een gesimuleerd X.509-apparaat op uw Windows-computer gemaakt en het ingericht voor uw IoT-hub met de Azure IoT Hub Device Provisioning Service in de portal. Als u wilt weten hoe u uw X.509-apparaat programmatisch kunt registreren, gaat u verder met de quickstart voor programmatische registratie van een X.509-apparaat. 

> [!div class="nextstepaction"]
> [Azure-quickstart: X.509-apparaat inschrijven bij Azure IoT Hub Device Provisioning Service](quick-enroll-device-x509-csharp.md)

---
title: Maken en beheren van Azure Database voor PostgreSQL-VNet-service-eindpunten en regels met behulp van de Azure portal | Microsoft Docs
description: Maken en beheren van Azure Database voor PostgreSQL-VNet-service-eindpunten en regels met behulp van de Azure portal
services: postgresql
author: mbolz
ms.author: mbolz
ms.reviewer: jasonwhowell
ms.service: postgresql
ms.topic: conceptual
ms.date: 10/23/2018
ms.openlocfilehash: b1cdabdf3c4f5355df568e940ed78e392a9c6612
ms.sourcegitcommit: 5c00e98c0d825f7005cb0f07d62052aff0bc0ca8
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/24/2018
ms.locfileid: "49957170"
---
# <a name="create-and-manage-azure-database-for-postgresql-vnet-service-endpoints-and-vnet-rules-by-using-the-azure-portal"></a>Maken en beheren van Azure Database voor PostgreSQL-VNet-service-eindpunten en VNet-regels met behulp van Azure portal
Virtueel netwerk (VNet) services-eindpunten en regels uitbreiden privé-adresruimte van een Virtueelnetwerk met uw Azure Database for PostgreSQL-server. Zie voor een overzicht van Azure Database voor PostgreSQL-VNet-service-eindpunten, met inbegrip van beperkingen, [Azure Database for PostgreSQL-Server VNet-service-eindpunten](concepts-data-access-and-security-vnet.md). VNet-service-eindpunten zijn beschikbaar in alle ondersteunde regio's voor Azure Database for PostgreSQL.

> [!NOTE]
> Ondersteuning voor VNet-service-eindpunten is alleen voor algemeen gebruik en geoptimaliseerd voor geheugen-servers.

## <a name="create-a-vnet-rule-and-enable-service-endpoints-in-the-azure-portal"></a>Een VNet-regel maken en inschakelen van service-eindpunten in Azure portal

1. Op de pagina van de PostgreSQL-server onder de instellingen voor kop, klikt u op **verbindingsbeveiliging** de beveiliging van de verbinding om deelvenster te openen voor Azure Database voor PostgreSQL. Klik op **+ bestaand virtueel netwerk toevoegen**. Als u een bestaand VNet niet hebt, kunt u **+ nieuw virtueel netwerk maken** een te maken. Zie [Snelstartgids: een virtueel netwerk met behulp van de Azure portal maken](../virtual-network/quick-create-portal.md)

   ![Azure-portal: klik op de beveiliging van de verbinding](./media/howto-manage-vnet-using-portal/1-connection-security.png)

2. Voer de naam van een VNet-regel, selecteer het abonnement, virtueel netwerk en subnetnaam en klik vervolgens op **inschakelen**. Hierdoor automatisch VNet-service-eindpunten op het subnet met behulp van de **Microsoft.SQL** servicetag.

   ![Azure portal - VNet configureren](./media/howto-manage-vnet-using-portal/2-configure-vnet.png)

    Het account moet de vereiste machtigingen om het maken van een virtueel netwerk en de service-eindpunt hebben.

    Service-eindpunten kunnen afzonderlijk worden geconfigureerd op de virtuele netwerken, door een gebruiker met schrijftoegang tot het virtuele netwerk.
    
    Voor het Azure-serviceresources aan een VNet, moet de gebruiker machtiging voor 'Microsoft.Network/virtualNetworks/subnets/joinViaServiceEndpoint/' voor de subnetten die worden toegevoegd. Deze machtiging is standaard opgenomen in de ingebouwde service-beheerdersrollen en kan worden gewijzigd door aangepaste rollen te maken.
    
    Meer informatie over [ingebouwde rollen](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) en het toewijzen van specifieke machtigingen voor [aangepaste rollen](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles).
    
    VNets en Azure-serviceresources kunnen in hetzelfde abonnement of in verschillende abonnementen zitten. Als het VNet en Azure-serviceresources in verschillende abonnementen zitten, moeten de resources onder dezelfde Active Directory (AD)-tenant.

   > [!IMPORTANT]
   > Het is raadzaam om te lezen in dit artikel over de service-eindpunt configuraties en overwegingen voor het configureren van service-eindpunten. **Service-eindpunt voor virtueel netwerk:** A [service-eindpunt voor Virtueelnetwerk](../virtual-network/virtual-network-service-endpoints-overview.md) is een subnet met eigenschappen die een of meer formele Azure-service typenamen bevatten. VNet-services-eindpunten gebruikt u de naam van de service type **Microsoft.Sql**, die verwijst naar de Azure-service met de naam SQL-Database. Deze servicetag geldt ook voor de Azure SQL Database, Azure Database for PostgreSQL en MySQL-services. Het is belangrijk te weten bij het toepassen van de **Microsoft.Sql** servicetag naar een VNet-service-eindpunt configureert het verkeer van de service-eindpunt voor alle Azure-Database-services, met inbegrip van Azure SQL Database, Azure Database for PostgreSQL en Azure Database for MySQL-servers op het subnet. 
   > 

3. Eenmaal is ingeschakeld, klikt u op **OK** en u ziet dat de VNet-service-eindpunten zijn ingeschakeld, samen met een VNet-regel.

   ![VNet-service-eindpunten ingeschakeld en VNet-regel gemaakt](./media/howto-manage-vnet-using-portal/3-vnet-service-endpoints-enabled-vnet-rule-created.png)

## <a name="next-steps"></a>Volgende stappen
- Op dezelfde manier, u kunt een script op [inschakelen VNet service-eindpunten en een VNET-regel maken voor Azure Database voor PostgreSQL met behulp van Azure CLI](howto-manage-vnet-using-cli.md).
- Zie voor hulp bij het verbinding maken met een Azure Database for PostgreSQL-server, [verbindingsbibliotheken voor Azure Database for PostgreSQL](./concepts-connection-libraries.md)

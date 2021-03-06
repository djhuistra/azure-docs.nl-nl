---
title: Azure Automation-gegevens beheren
description: In dit artikel bevat meerdere onderwerpen voor het beheren van een Azure Automation-omgeving.  Momenteel omvat het bewaren van gegevens en back-ups van Azure Automation-noodherstel in Azure Automation.
services: automation
ms.service: automation
ms.component: shared-capabilities
author: georgewallace
ms.author: gwallace
ms.date: 03/16/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 05da900e9ddf4cbb99df5c6d62ddb569059e2c4b
ms.sourcegitcommit: 1af4bceb45a0b4edcdb1079fc279f9f2f448140b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/09/2018
ms.locfileid: "42054033"
---
# <a name="managing-azure-automation-data"></a>Azure Automation-gegevens beheren
In dit artikel bevat meerdere onderwerpen voor het beheren van een Azure Automation-omgeving.

## <a name="data-retention"></a>Bewaartijd van gegevens
Wanneer u een resource in Azure Automation verwijdert, wordt wel worden bewaard gedurende 90 dagen voor controledoeleinden voordat wordt permanent verwijderd.  U kan niet zien of de resource gebruiken gedurende deze tijd.  Dit beleid geldt ook voor resources die deel uitmaken van een automation-account dat wordt verwijderd.

Azure Automation wordt automatisch verwijderd en taken die ouder zijn dan 90 dagen permanent verwijderd.

De volgende tabel geeft een overzicht van het bewaarbeleid voor verschillende resources.

| Gegevens | Beleid |
|:--- |:--- |
| Accounts |90 dagen nadat het account is verwijderd door een gebruiker permanent verwijderd. |
| Assets |Negentig dagen na de asset door een gebruiker wordt verwijderd of 90 dagen na het account waarin dat de asset wordt verwijderd door een gebruiker permanent verwijderd. |
| Modules |Negentig dagen na de module wordt verwijderd door een gebruiker of 90 dagen na de rekening met dat de module wordt verwijderd door een gebruiker permanent verwijderd. |
| Runbooks |Negentig dagen na de resource wordt verwijderd door een gebruiker of 90 dagen na het account waarin dat de resource wordt verwijderd door een gebruiker permanent verwijderd. |
| Taken |Verwijderde en permanent verwijderd 90 dagen na de laatste wordt gewijzigd. Dit wordt mogelijk nadat de taak is voltooid, is gestopt of is onderbroken. |
| Knooppunt configuraties/MOF-bestanden |Oude knooppuntconfiguratie wordt definitief verwijderd van 90 dagen na de configuratie van een nieuw knooppunt wordt gegenereerd. |
| DSC-knooppunten |Negentig dagen na het knooppunt ongedaan van Automation-Account met behulp van Azure portal is definitief verwijderd of de [Unregister-AzureRMAutomationDscNode](https://docs.microsoft.com/powershell/module/azurerm.automation/unregister-azurermautomationdscnode) cmdlet in Windows PowerShell. Knooppunten worden 90 dagen na de rekening met dat het knooppunt wordt verwijderd door een gebruiker ook permanent verwijderd. |
| Knooppunt-rapporten |90 dagen nadat een nieuw rapport is gegenereerd voor dat knooppunt permanent verwijderd |

Het bewaarbeleid is van toepassing op alle gebruikers en momenteel niet worden aangepast.

Echter, als u behouden van gegevens voor een langere periode wilt, kunt u doorsturen runbook taaklogboeken met Log Analytics.  Raadpleeg voor meer informatie, [Azure Automation-taakgegevens doorsturen naar Log Analytics](automation-manage-send-joblogs-log-analytics.md).   

## <a name="backing-up-azure-automation"></a>Back-ups maken met Azure Automation
Wanneer u een automation-account in Microsoft Azure verwijdert, worden alle objecten in het account verwijderd inclusief runbooks, modules, configuraties, instellingen, jobs en activa. De objecten kunnen niet worden hersteld nadat het account is verwijderd.  Gebruik de volgende informatie kunt u back-up van de inhoud van uw automation-account voordat deze worden verwijderd. 

### <a name="runbooks"></a>Runbooks
U kunt uw runbooks exporteren naar scriptbestanden met behulp van de Azure portal of de [Get-AzureAutomationRunbookDefinition](https://docs.microsoft.com/powershell/module/servicemanagement/azure/get-azureautomationrunbookdefinition) cmdlet in Windows PowerShell.  Deze scriptbestanden kunnen worden geïmporteerd in een ander automation-account, zoals beschreven in [maken of importeren van een Runbook](https://msdn.microsoft.com/library/dn643637.aspx).

### <a name="integration-modules"></a>Integratiemodules
U kunt integratiemodules exporteren vanuit Azure Automation.  U moet ervoor zorgen dat deze beschikbaar is buiten het automation-account zijn.

### <a name="assets"></a>Assets
U kunt niet exporteren [activa](https://msdn.microsoft.com/library/dn939988.aspx) van Azure Automation.  Met behulp van de Azure-portal, moet u de details van variabelen, -referenties, certificaten, verbindingen en schema's opmerking.  U moet alle activa die worden gebruikt door runbooks die u in een ander automation importeert vervolgens handmatig maken.

U kunt [Azure-cmdlets](https://docs.microsoft.com/powershell/module/azurerm.automation#automation) ophalen van details van activa op niet-versleutelde en een opslaan voor toekomstig gebruik of gelijkwaardige activa in een ander automation-account maken.

U kunt de waarde voor gecodeerde variabelen of het wachtwoordveld van referenties met behulp van cmdlets niet ophalen.  Als u deze waarden niet weet en u ze wel vanuit een runbook met ophalen kunt de [Get-AutomationVariable](https://msdn.microsoft.com/library/dn940012.aspx) en [Get-AutomationPSCredential](https://msdn.microsoft.com/library/dn940015.aspx) activiteiten.

U kunt certificaten exporteren vanuit Azure Automation.  U moet ervoor zorgen dat er geen certificaten beschikbaar buiten Azure zijn.

### <a name="dsc-configurations"></a>DSC-configuraties
U kunt uw configuraties exporteren naar scriptbestanden met behulp van de Azure portal of de [Export-AzureRmAutomationDscConfiguration](https://docs.microsoft.com/powershell/module/azurerm.automation/export-azurermautomationdscconfiguration) cmdlet in Windows PowerShell. Deze configuraties kunnen worden geïmporteerd en gebruikt in een ander automation-account.

## <a name="geo-replication-in-azure-automation"></a>Geo-replicatie in Azure Automation
Geo-replicatie, standaard in Azure Automation-accounts, back-ups van gegevens naar een andere geografische regio voor redundantie. U kunt een primaire regio kiezen bij het instellen van uw account en vervolgens een secundaire regio die is toegewezen aan deze automatisch. De secundaire gegevens gekopieerd van de primaire regio, wordt voortdurend bijgewerkt in het geval van verlies van gegevens.  

De volgende tabel toont de beschikbare primaire en secundaire regiokoppelingen.

| Primair | Secundair |
| --- | --- |
| US - zuid-centraal |US - noord-centraal |
| US - oost 2 |US - centraal |
| Europa -west |Europa - noord |
| Azië - zuidoost |Azië - oost |
| Japan - oost |Japan - west |

In het onwaarschijnlijke geval dat een primaire regiogegevens verloren gegaan zijn, probeert Microsoft om het te herstellen. Als de primaire gegevens kan niet worden hersteld, vervolgens geo-failover wordt uitgevoerd en de betrokken klanten worden ontvangen over dit via hun abonnement.


---
title: Targeting oplossingen in Azure | Microsoft Docs
description: Targeting beheeroplossingen, kunt u oplossingen voor een specifieke set van agents beperken.  Dit artikel wordt beschreven hoe u de configuratie van een scope maken en dit toepassen op een oplossing.
services: monitoring
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: monitoring
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 65585e6c09def23101d9735c8b9c719d213938ac
ms.sourcegitcommit: 870d372785ffa8ca46346f4dfe215f245931dae1
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/08/2018
ms.locfileid: "33887844"
---
# <a name="targeting-management-solutions-in-azure-preview"></a>Doelitems oplossingen in Azure (Preview)
Wanneer u een oplossing voor uw abonnement toevoegt, wordt het automatisch naar alle Windows- en Linux-agents verbonden met uw werkruimte voor logboekanalyse standaard geïmplementeerd.  Mogelijk wilt de kosten beheren en beperken van de hoeveelheid gegevens die door het beperken van het aan een bepaalde set van agents naar een oplossing worden verzameld.  In dit artikel wordt beschreven hoe u **oplossing Targeting** dit is een functie waarmee u een bereik toepassen op uw oplossingen.

## <a name="how-to-target-a-solution"></a>Het doel een oplossing
Er zijn drie stappen voor het doel van een oplossing zoals beschreven in de volgende secties. 


### <a name="1-create-a-computer-group"></a>1. Maak een computergroep
Geef van de computers die u opnemen in een bereik wilt door het maken van een [computergroep](../log-analytics/log-analytics-computer-groups.md) in logboekanalyse.  De computergroep worden op basis van een zoekopdracht logboek of geïmporteerd uit andere bronnen zoals Active Directory of WSUS-groepen. Als [hieronder beschreven](#solutions-and-agents-that-cant-be-targeted), alleen de computers die rechtstreeks zijn verbonden met logboekanalyse worden opgenomen in het bereik.

Eenmaal hebt gemaakt in de werkruimte groep op de computer en vervolgens moet u deze opnemen in de configuratie van een scope die kan worden toegepast op een of meer oplossingen.
 
 
 ### <a name="2-create-a-scope-configuration"></a>2. De configuratie van een scope maken
 Een **scopeconfiguratie** bevat een of meer computergroepen en kan worden toegepast op een of meer oplossingen. 
 
 De configuratie van een bereik met het volgende proces maken.  

 1. Navigeer in de Azure-portal naar **logboekanalyse** en selecteer uw werkruimte.
 2. In de eigenschappen voor de werkruimte **werkruimte gegevensbronnen** Selecteer **bereik configuraties**.
 3. Klik op **toevoegen** om een nieuwe scopeconfiguratie te maken.
 4. Typ een **naam** voor de configuratie van het bereik.
 5. Klik op **Selecteer computergroepen**.
 6. Selecteer de computergroep die u hebt gemaakt en eventueel andere groepen toevoegen aan de configuratie.  Klik op **Selecteren**.  
 6. Klik op **OK** om de scopeconfiguratie te maken. 


 ### <a name="3-apply-the-scope-configuration-to-a-solution"></a>3. De configuratie van het bereik van toepassing op een oplossing.
Zodra u de configuratie van een scope hebt, kunt klikt u vervolgens u toepassen op een of meer oplossingen.  Houd er rekening mee dat tijdens een configuratie met één scope kan worden gebruikt met meerdere oplossingen, elke oplossing alleen één scopeconfiguratie gebruiken kan.

De configuratie van een bereik met het volgende proces toepassen.  

 1. Navigeer in de Azure-portal naar **logboekanalyse** en selecteer uw werkruimte.
 2. Selecteer in de eigenschappen voor de werkruimte **oplossingen**.
 3. Klik op de oplossing die u bereik wilt.
 4. In de eigenschappen voor de oplossing onder **werkruimte gegevensbronnen** Selecteer **oplossing doelen**.  Als de optie niet beschikbaar is vervolgens [deze oplossing kan niet worden gericht](#solutions-and-agents-that-cant-be-targeted).
 5. Klik op **toevoegen scopeconfiguratie**.  Als u al een configuratie op deze oplossing wordt toegepast, wordt deze optie niet beschikbaar.  De bestaande configuratie voordat u een andere toevoegt, moet u verwijderen.
 6. Klik op de scopeconfiguratie die u hebt gemaakt.
 7. Bekijk de **Status** van de configuratie om ervoor te zorgen dat er wordt weergegeven **geslaagd**.  Als de status is een fout aangeeft, klikt u op de knop met weglatingstekens rechts van de configuratie en selecteer **bewerken scopeconfiguratie** wijzigingen aanbrengen.

## <a name="solutions-and-agents-that-cant-be-targeted"></a>Oplossingen en agents die niet worden gericht
Hieronder vindt u de criteria voor agents en oplossingen die met het doel van de oplossing kunnen niet worden gebruikt.

- Oplossing targeting geldt alleen voor oplossingen die op agents implementeren.
- Oplossing die gericht is alleen van toepassing op Microsoft-oplossingen.  Dit geldt niet voor oplossingen [gemaakt door uzelf of partners](monitoring-solutions-creating.md).
- U kunt alleen agents die rechtstreeks verbinding met logboekanalyse maken filter.  Oplossingen implementeren automatisch naar alle agents die deel van een verbonden beheergroep van Operations Manager uitmaken of ze zijn opgenomen in de configuratie van een scope of niet.

### <a name="exceptions"></a>Uitzonderingen
Oplossing als doel kan niet worden gebruikt met de volgende oplossingen ondanks dat ze voldoen aan de opgegeven criteria.

- Evaluatie van agent-status

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over oplossingen met inbegrip van de oplossingen die kunnen worden geïnstalleerd in uw omgeving op [beheeroplossingen voor Azure-logboekanalyse toevoegen aan uw werkruimte](../log-analytics/log-analytics-add-solutions.md).
- Meer informatie over het maken van computergroepen op [computergroepen in logboekanalyse Meld zoekopdrachten](../log-analytics/log-analytics-computer-groups.md).
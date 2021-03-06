---
title: Controleactiviteitenrapporten in Azure Active Directory Portal | Microsoft Docs
description: Ontdek de controleactiviteitenrapporten in de Azure Active Directory Portal
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 04/19/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: b6fa26cb7947658af77496831d7239b4331aa1f2
ms.sourcegitcommit: 1af4bceb45a0b4edcdb1079fc279f9f2f448140b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/09/2018
ms.locfileid: "42056819"
---
# <a name="audit-activity-reports-in-the-azure-active-directory-portal"></a>Controleactiviteitenrapporten in Azure Active Directory Portal 

Met rapporten in Azure Active Directory ontvangt u alle informatie die nodig is om te bepalen hoe het gaat met uw omgeving.

De rapportstructuur in Azure AD bestaat uit de volgende onderdelen:

- **Activiteit** 
    - **Aanmeldactiviteiten**: informatie over het gebruik van beheerde toepassingen en aanmeldactiviteiten van gebruikers
    - **Auditlogboeken**: traceerbaarheid via logboeken voor alle door diverse functies binnen Azure AD uitgevoerde wijzigingen. Voorbeelden van auditlogboekgegevens zijn wijzigingen die worden aangebracht in resources binnen Azure AD, zoals gebruikers, apps, groepen, rollen, beleid, verificaties, enzovoort.
- **Beveiliging** 
    - **Riskante aanmeldingen** - Een riskante aanmelding is een indicator van een aanmeldingspoging die mogelijk is uitgevoerd door iemand die geen rechtmatige eigenaar van een gebruikersaccount is. Zie Riskante aanmeldingen voor meer informatie.
    - **Gebruikers van wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast. Zie Gebruikers van wie wordt aangegeven dat ze risico lopen voor meer informatie.

In dit onderwerp vindt u meer informatie over de controleactiviteiten.
 
## <a name="who-can-access-the-data"></a>Wie heeft er toegang tot de gegevens?
* Gebruikers met de rol Beveiligingsbeheerder of Beveiligingslezer
* Globale beheerders
* Afzonderlijke gebruikers (niet-beheerders) kunnen hun eigen activiteiten zien


## <a name="audit-logs"></a>Controlelogboeken

In de controlelogboeken in Azure Active Directory staan records van systeemactiviteiten voor naleving.  
Uw eerste beginpunt voor alle controlegegevens is **Controlelogboeken** in het gedeelte **Activiteit** van **Azure Active Directory**.

![Controlelogboeken](./media/concept-audit-logs/61.png "Controlelogboeken")

Een controlelogboek heeft een standaardlijstweergave die het volgende laat zien:

- de datum en tijd van de gebeurtenis
- de initiator/actor (*wie*) van een activiteit 
- de activiteit (*wat*) 
- het doel

![Controlelogboeken](./media/concept-audit-logs/18.png "Controlelogboeken")

U kunt de lijstweergave aanpassen door te klikken op **Kolommen** op de werkbalk.

![Controlelogboeken](./media/concept-audit-logs/19.png "Controlelogboeken")

Hiermee kunt u extra velden weergeven of velden verwijderen die al worden weergegeven.

![Controlelogboeken](./media/concept-audit-logs/21.png "Controlelogboeken")


Wanneer u op een item in de lijstweergave klikt, krijgt u er alle beschikbare informatie over te zien.

![Controlelogboeken](./media/concept-audit-logs/22.png "Controlelogboeken")


## <a name="filtering-audit-logs"></a>Controlelogboeken filteren

Als u de gerapporteerde gegevens wilt beperken tot een niveau dat geschikt is voor u, kunt u de controlegegevens filteren met de volgende velden:

- Datumbereik
- Gestart door (actor)
- Categorie
- Resourcetype van activiteit
- Activiteit

![Controlelogboeken](./media/concept-audit-logs/23.png "Controlelogboeken")


Met het filter **datumbereik** kunt u een tijdsbestek opgeven voor de geretourneerde gegevens.  
Mogelijke waarden zijn:

- 1 maand
- 7 dagen
- 24 uur
- Aangepast telefoonnummer

Wanneer u een aangepast tijdsbestek selecteert, kunt u een begintijd en eindtijd configureren.

Met het filter **gestart door** kunt u de naam of UPN (Universal Principal Name) van een actor definiëren.

Met het filter **aanmeldingsstatus** kunt u een van de volgende filters selecteren:

- Alle
- Hoofdcategorie
- Hoofddirectory
- Wachtwoordbeheer via selfservice
- Groepsbeheer via selfservice
- Account inrichten - Automatische wachtwoordoverschakeling
- Uitgenodigde gebruikers
- MIM-service
- Identiteitsbeveiliging
- B2C

Met het filter **type activiteitsresource** kunt u een van de volgende filters selecteren:

- Alle 
- Groep
- Directory
- Gebruiker
- Toepassing
- Beleid
- Apparaat
- Overige

Wanneer u **Groep** selecteert als **type activiteitsresource**, krijgt u een extra filtercategorie waarmee u ook een **Bron** kunt opgeven:

- Azure AD
- O365


Het filter **activiteit** is gebaseerd op de selectie die u maakt voor de categorie en het type activiteitsresource. U kunt een specifieke activiteit of alle activiteiten selecteren. 

U kunt de lijst met alle controleactiviteiten opvragen met behulp van de Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, waarbij u $tenantdomain vervangt door de naam van uw domein. U kunt ook het artikel [Controlerapportgebeurtenissen](concept-audit-logs.md) raadplegen.


## <a name="audit-logs-shortcuts"></a>Snelkoppelingen naar controlelogboeken

Naast **Azure Active Directory** biedt de Azure Portal twee extra beginpunten voor gegevenscontrole:

- Gebruikers en groepen
- Bedrijfstoepassingen

### <a name="users-and-groups-audit-logs"></a>Controlelogboeken voor gebruikers en groepen

Met de controlerapporten op basis van gebruikers en groepen krijgt u antwoord op vragen zoals:

- Welke soorten updates zijn toegepast op de gebruikers?

- Hoeveel gebruikers zijn gewijzigd?

- Hoeveel wachtwoorden zijn gewijzigd?

- Wat heeft een beheerder in een directory gedaan?

- Welke groepen zijn toegevoegd?

- Zijn er groepen met wijzigingen in het lidmaatschap?

- Zijn de eigenaren van een groep gewijzigd?

- Welke licenties zijn toegewezen aan een groep of een gebruiker?

Als u alleen controlegegevens wilt bekijken die aan gebruikers en groepen zijn gerelateerd, kunt u een gefilterde weergave openen via **Controlelogboeken** in het gedeelte **Activiteit** van **Gebruikers en groepen**. Dit beginpunt heeft **Gebruikers en groepen** als vooraf geselecteerd **Type activiteitsresource**.

![Controlelogboeken](./media/concept-audit-logs/93.png "Controlelogboeken")

### <a name="enterprise-applications-audit-logs"></a>Controlelogboeken voor bedrijfstoepassingen

Met de controlerapporten op basis van toepassingen krijgt u antwoord op vragen zoals:

* Welke toepassingen zijn toegevoegd of bijgewerkt?
* Welke toepassingen zijn verwijderd?
* Is de service-principal van een toepassing gewijzigd?
* Zijn de namen van toepassingen gewijzigd?
* Wie heeft toestemming gegeven voor een toepassing?

Als u alleen controlegegevens wilt bekijken die aan uw toepassingen zijn gerelateerd, kunt u een gefilterde weergave openen via **Controlelogboeken** in het gedeelte **Activiteit** van de blade **Bedrijfstoepassingen**. Dit beginpunt heeft **Bedrijfstoepassingen** als vooraf geselecteerd **Type activiteitsresource**.

![Controlelogboeken](./media/concept-audit-logs/134.png "Controlelogboeken")

U kunt deze weergave verder filteren naar alleen **Groepen** of alleen **Gebruikers**.

![Controlelogboeken](./media/concept-audit-logs/25.png "Controlelogboeken")



## <a name="next-steps"></a>Volgende stappen

- Zie [Azure Active Directory-rapportage](overview-reports.md) voor een overzicht van de rapportage.

- Zie [Referentie voor auditactiviteiten van Azure AD](reference-audit-activities.md) voor een volledige lijst van alle auditactiviteiten.


---
title: Test Drive gehost | Microsoft Docs
description: Het instellen van een onderhouden een proefrit Marketplace die worden gehost
services: Azure, Marketplace, Cloud Partner Portal,
documentationcenter: ''
author: pbutlerm
manager: Ricardo.Villalobos
editor: ''
ms.assetid: ''
ms.service: marketplace
ms.workload: ''
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: conceptual
ms.date: 09/13/2018
ms.author: pbutlerm
ms.openlocfilehash: 1ab9fcd50ad7081f8047d62e545287fa75db75e4
ms.sourcegitcommit: 9eaf634d59f7369bec5a2e311806d4a149e9f425
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/05/2018
ms.locfileid: "48810170"
---
# <a name="hosted-test-drive"></a>Gehoste Test Drive

Een gehost Test Drive wordt de complexiteit van de installatie door Microsoft hosting en onderhouden van de service die de gebruiker Test Drive-inrichting en ongedaan maken van inrichting uitvoert. Dit artikel is voor uitgevers die hebben hun aanbieding op AppSource of een nieuwe bouwen en willen aanbieden van een schijf Test die wordt gehost, waarvoor een verbinding maakt met een Dynamics 365 voor Customer Engagement, Dynamics 365 voor Financiën en bewerkingen of Dynamics 365 Business Central het exemplaar.

## <a name="how-to-publish-a-test-drive"></a>Het publiceren van een Test Drive

Navigeer naar de bestaande aanbieding of maak een nieuwe aanbieding.

Selecteer de Test Drive-optie in het menu aan clientzijde.

Selecteer \'Ja\' voor \'inschakelen van een Test Drive\' optie.

Geef de volgende velden in de \'Details\' sectie.

- **Beschrijving**: biedt een overzicht van uw Test Drive. Deze tekst wordt weergegeven aan de gebruiker tijdens de Test Drive wordt ingericht. Dit veld biedt ondersteuning voor HTML-code als u wilt bieden opgemaakte inhoud.
- **Gebruikershandleiding**: een gebruikershandleiding met gedetailleerde (-bestand van type PDF-bestand) waarmee Test Drive-gebruikers te begrijpen hoe u uw App te uploaden.
- **Test Drive Demo Video**: (optioneel) upload een video die uw App worden gepresenteerd.

De machtiging GRANT AppSource te richten en de inrichting van Test Drive-gebruikers in uw tenant met behulp van de instructies die zich [hier](https://github.com/Microsoft/AppSource/blob/patch-1/Microsoft%20Hosted%20Test%20Drive/Setup-your-Azure-subscription-for-Dynamics365-Microsoft-Hosted-Test-Drives.md).

In deze stap, genereert u de \'Azure AD-App-Id\' en \'Azure AD App-sleutel\' waarden die hieronder worden vermeld.

Geef de volgende velden in de \'technische configuratie\' sectie:

- **Type Test Drive**: kies \'Microsoft Hosted (voorbeeld van de Dynamics 365 voor Customer Engagement)' optie. Dit geeft aan dat Microsoft hosten en beheren van de service die de gebruiker Test Drive-inrichting en ongedaan maken van inrichting uitvoert.
- **Maximum aantal gelijktijdige Test Drives**: Stel dit veld in het aantal gelijktijdige gebruikers die een actieve Test Drive op een willekeurig moment tijd wordt opgelost hebben kunnen. Elke gebruiker wordt een Dynamics-licentie gebruiken tijdens de Test Drive actief, is daarom u moet om ervoor te zorgen dat u ten minste dit aantal Dynamics licenties beschikbaar voor gebruikers van Test Drive. Aanbevolen waarde van 3 tot 5.
- **Test Drive duur (uren)**: Stel dit veld in het aantal uren dat de Test Drive is actief voor gebruikers. Na dit aantal uur, wordt de gebruiker uit uw tenant worden beëindigd. Aanbevolen waarde van 2 tot 24 uur, afhankelijk van de complexiteit van uw App. De gebruiker kan een andere Test Drive altijd aanvragen als ze weinig tijd en toegang kunt krijgen tot de Test Drive opnieuw.
- **Instantie-URL**: Geef een URL waar de gebruiker Test Drive wordt in eerste instantie wordt genavigeerd wanneer ze de Test Drive starten. Dit is meestal de URL van uw Dynamics 365-exemplaar waarop uw App en voorbeeldgegevens op geïnstalleerd. Voorbeeldwaarde:https://testdrive.crm.dynamics.com
- **Azure AD-Tenant-ID**: Geef de ID van de Azure-Tenant voor uw exemplaar van Dynamics 365. Voor het ophalen van deze waarde, meld u aan bij Azure portal en gaat u naar \'Azure Active Directory\'  - \> eigenschappen selecteren uit het menu-blade -\> Kopieer de map-ID. Voorbeeldwaarde: 72f988bf-86f1-41af-91ab-2d7cd0111234
- **Azure AD-App-ID**: ID van de Azure AD-App die u hebt gemaakt in stap 7. \ Voorbeeldwaarde: 53852862-a2ae-4e43-9461-faa49650a096
- **Azure AD App Key**: geheim voor de Azure AD-App gemaakt in stap 7. \ Voorbeeldwaarde: IJUgaIOfq9b9LbUjeQmzNBW4VGn6grr1l/n3aMrnfdk =
- **Azure AD-Tenantnaam**: Geef de naam van de Azure-Tenant voor uw exemplaar van Dynamics 365. Gebruik de indeling van \<tenantname.\> onmicrosoft.com. Voorbeeldwaarde: testdrive.onmicrosoft.com
- **Web-API URL-exemplaar**: Geef de URL van de Web-API voor uw exemplaar van Dynamics 365. U kunt deze waarde wordt opgehaald door te melden bij uw Microsoft Dynamics 365-exemplaar en te navigeren naar instelling -\> aanpassing -\> bronnen voor ontwikkelaars -\> exemplaar Web-API (deze URL kopiëren). Voorbeeldwaarde:  https://testdrive.crm.dynamics.com/api/data/v9.0 
- **De naam van rol**: Geef de naam van de aangepaste Dynamics 365 beveiligingsrol die u hebt gemaakt voor Test Drive. Dit is de rol die wordt toegewezen aan gebruikers tijdens de Test Drive. Voorbeeldwaarde: testdriverole

## <a name="next-steps"></a>Volgende stappen

Als u klaar bent **publiceren** uw aanbieding, nadat uw app is verstreken-certificering, hebt u een **preview** van uw aanbieding. Start een Test uit in de gebruikersinterface en controleer of uw Test Drives correct worden uitgevoerd. Als u vertrouwd met de preview-aanbieding, het is nu tijd om **live gaan!**

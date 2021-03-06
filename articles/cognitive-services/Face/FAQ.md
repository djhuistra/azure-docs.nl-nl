---
title: Veelgestelde vragen - Face-API
titlesuffix: Azure Cognitive Services
description: Hier vindt u antwoorden op de meest populaire vragen over de Face-API-Service.
services: cognitive-services
author: SteveMSFT
manager: cgronlun
ms.service: cognitive-services
ms.component: face-api
ms.topic: conceptual
ms.date: 01/26/2017
ms.author: sbowles
ms.openlocfilehash: 9b30fa0fbbd655c03800dadb19cc2568d404204d
ms.sourcegitcommit: f10653b10c2ad745f446b54a31664b7d9f9253fe
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46129553"
---
# <a name="face-api-frequently-asked-questions"></a>Veelgestelde vragen over de Face-API

### <a name="if-you-cant-find-answers-to-your-questions-in-this-faq-try-asking-the-face-api-community-on-stackoverflowhttpsstackoverflowcomquestionstaggedproject-oxfordormicrosoft-cognitive-or-contact-help-and-support-on-uservoicehttpscognitiveuservoicecom"></a>Als u antwoorden op uw vragen niet in deze Veelgestelde vragen vinden, misschien dat de Face-API-community op [StackOverflow](https://stackoverflow.com/questions/tagged/project-oxford+or+microsoft-cognitive) of neem contact op met Help en ondersteuning op [UserVoice](https://cognitive.uservoice.com/).

-----
**Vraag**: welke factoren verminderen nauwkeurigheid van de Face-API voor spraakherkenning, verificatie of vergelijkbare vinden?

**Antwoord**: in het algemeen is het dezelfde gevallen waar mensen ondervindt bij het identificeren van iemand met inbegrip van;
* Blokkering van een of beide ogen obstakels
* Scherp wordt geopend, bijvoorbeeld ernstige achtergrondverlichting voor
* Wijzigingen in haar stijl of videodetectie haar
* Wijzigingen vanwege leeftijd
* Extreme gezichtsuitdrukkingen (bijvoorbeeld Juichende)

Face-API is vaak lukt dit in uitdagende gevallen zoals deze, maar de nauwkeurigheid van de gegevens kan worden verlaagd. Trainen voor spraakherkenning maken die krachtiger en deze problemen aan te pakken, de personen met een foto's die een uiteenlopende hoeken en belichting bevatten.

-----
**Vraag**: ik ben doorgeven van de binaire gegevens in, maar ik krijg de foutmelding 'Ongeldige face installatiekopie'.

**Antwoord**: dit betekent dat de algoritme is een opgetreden bij het parseren van de installatiekopie. Oorzaken zijn:
* De ondersteunde bestandsindelingen voor invoer bevat JPEG, PNG-, GIF-bestand (het eerste frame), BMP.
* De grootte van de installatiekopie-bestand moet niet groter zijn dan 4MB
* Het bereik van de grootte detecteerbare gezicht is 36 x 36 naar 4096 x 4096 pixels. Gezichten buiten dit bereik niet gedetecteerd
* Sommige gezichten worden mogelijk niet gedetecteerd vanwege technische problemen, bijvoorbeeld zeer grote face hoeken (hoofd-houding), grote bedekking. Gezichten voorzijde en in de buurt binnen handbereik hebben de beste resultaten

-----

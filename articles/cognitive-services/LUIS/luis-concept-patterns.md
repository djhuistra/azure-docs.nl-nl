---
title: Informatie over hoe patronen nauwkeurigheid vergroten
titleSuffix: Azure Cognitive Services
description: Patronen zijn ontworpen voor betere nauwkeurigheid wanneer verschillende uitingen vergelijkbaar zijn. Een patroon kunt u meer nauwkeurigheid voor een doel zonder op te geven veel meer uitingen krijgen.
services: cognitive-services
author: diberry
manager: cgronlun
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: conceptual
ms.date: 09/10/2018
ms.author: diberry
ms.openlocfilehash: fbd11eb23b10800e115a63549f233e0239763420
ms.sourcegitcommit: 17633e545a3d03018d3a218ae6a3e4338a92450d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/22/2018
ms.locfileid: "49638139"
---
# <a name="patterns-improve-prediction-accuracy"></a>Patronen verbeteren nauwkeurigheid
Patronen zijn ontworpen voor betere nauwkeurigheid wanneer verschillende uitingen vergelijkbaar zijn.  Een patroon kunt u meer nauwkeurigheid voor een doel zonder op te geven veel meer uitingen krijgen. 

## <a name="patterns-solve-low-intent-confidence"></a>Patronen oplossen lage intentie vertrouwen
Houd rekening met een Human Resources-app die in de organisatie-grafiek ten opzichte van een werknemer-rapporten. Gezien de naam en de relatie van een werknemer, retourneert LUIS de werknemers die betrokken zijn. Houd rekening met een werknemer, Tom, met een manager naam Els en een team van onderliggende niveaus met de naam: Michael Rebecca en Carl.

![Afbeelding van organigram](./media/luis-concept-patterns/org-chart.png)

|Utterances|Bedoeling voorspeld|Intentie score|
|--|--|--|
|Wie is de Tom ondergeschikte?|GetOrgChart|.30|
|Wie is de onderliggend niveau van Tom?|GetOrgChart|.30|

Als een app heeft tussen 10 en 20 uitingen met verschillende lengtes van zin, verschillende woordvolgorde en zelfs verschillende woorden (synoniemen van 'onderliggende', 'beheren', "rapport"), opleveren LUIS met een lage betrouwbaarheidsscore. Om u te helpen begrijpen het belang van de woordvolgorde LUIS, maakt u een patroon. 

Patronen oplossen van de volgende situaties: 

* Wanneer de intentie score is laag
* Wanneer het juiste doel is niet de hoogste score maar te dicht bij de hoogste score. 

## <a name="patterns-are-not-a-guarantee-of-intent"></a>Patronen zijn geen garantie van doel
Patronen gebruiken een combinatie van technologieën voor voorspelling. Instellen van een doel voor de utterance van een sjabloon in een patroon is geen garantie van de intentie voorspelling maar het is een sterk signaal. 

## <a name="patterns-do-not-improve-entity-detection"></a>Patronen de detectie van de entiteit niet zijn verbeteren
Hoewel patronen entiteiten, een patroon helpt niet bij het detecteren van de entiteit. Een patroon is alleen bedoeld om u te helpen bij het voorspellen met intents en rollen.  

## <a name="patterns-use-entity-roles"></a>Patronen entiteit rollen gebruiken
Als twee of meer entiteiten in een patroon contextueel zijn gerelateerd, patronen entiteit gebruiken [rollen](luis-concept-roles.md) contextuele gegevens over entiteiten extraheren. Dit is gelijk aan het hiërarchische entiteit kinderen, maar is **alleen** beschikbaar in de patronen. 

## <a name="prediction-scores-with-and-without-patterns"></a>Voorspelling scores met en zonder patronen
Onvoldoende uitingen voorbeeld gezien, zou LUIS kunnen worden vergroot het vertrouwen van voorspelling geen patronen weergegeven. De betrouwbaarheidsscore verhogen patronen zonder deze op te geven zoveel uitingen.  

## <a name="pattern-matching"></a>Jokertekens
Een patroon wordt op basis van de entiteiten in het patroon eerst detecteren en valideren van de rest van de woorden en de woordvolgorde van het patroon vergeleken. Entiteiten zijn vereist in het patroon voor een patroon voor de overeenkomst. 

## <a name="pattern-syntax"></a>De syntaxis van het patroon
De syntaxis van het patroon is een sjabloon voor een utterance. De sjabloon moet bevatten woorden en entiteiten die u wilt vergelijken en woorden en leestekens die u wilt negeren. Het is **niet** een reguliere expressie. 

Entiteiten in de patronen zijn omgeven door accolades, `{}`. Patronen kunnen bestaan uit entiteiten en entiteiten met functies. Pattern.any is een entiteit die alleen wordt gebruikt in patronen. De syntaxis van de wordt in de volgende secties uitgelegd.

### <a name="syntax-to-add-an-entity-to-a-pattern-template"></a>Syntaxis voor een entiteit toevoegen aan een patroon-sjabloon
Als u wilt toevoegen een entiteit in de sjabloon voor het patroon, zoals de naam van de entiteit met behulp van accolades, rondom `Who does {Employee} manage?`. 

|Patroon met entiteit|
|--|
|`Who does {Employee} manage?`|

### <a name="syntax-to-add-an-entity-and-role-to-a-pattern-template"></a>Syntaxis voor het toevoegen van een entiteit en een rol aan een patroon-sjabloon
De entiteitsrol van een wordt aangeduid als `{entity:role}` met de naam van de entiteit gevolgd door een dubbele punt, gevolgd door de rolnaam. Als u wilt toevoegen een entiteit met een rol in de sjabloon voor het patroon, moet u de naam van de entiteit en de rolnaam met behulp van accolades, zoals `Book a ticket from {Location:Origin} to {Location:Destination}`. 

|Patroon met behulp van entiteit|
|--|
|`Book a ticket from {Location:Origin} to {Location:Destination}`|

### <a name="syntax-to-add-a-patternany-to-pattern-template"></a>Syntaxis voor het toevoegen van een pattern.any aan patroon sjabloon
De entiteit Pattern.any kunt u een entiteit van de verschillende lengten toevoegen aan het patroon. Als de sjabloon patroon wordt gevolgd, mag de pattern.any een willekeurige lengte. 

Om toe te voegen een **Pattern.any** entiteit in de sjabloon patroon rondom de Pattern.any-entiteit met de accolades, zoals `How much does {Booktitle} cost and what format is it available in?`.  

|Patroon met Pattern.any entiteit|
|--|
|`How much does {Booktitle} cost and what format is it available in?`|

|Titels in het patroon|
|--|
|Wat kost **stelen dit boek** kosten, en welke indeling is beschikbaar in?|
|Wat kost **vragen** kosten, en welke indeling is beschikbaar in?|
|Wat kost **de benieuwd Incident van de hond in de nacht-tijd** kosten, en welke indeling is beschikbaar in?| 

In deze voorbeelden van de titel book zijn niet de contextuele woorden van titel van het boek lastig te LUIS. LUIS weet waar de titel van het boek is beëindigd omdat deze in een patroon is en gemarkeerd met een entiteit Pattern.any.

### <a name="explicit-lists"></a>Expliciete lijsten
Als het patroon bevat een Pattern.any, en de syntaxis van de patroon kunt u de mogelijkheid van een onjuist entiteiten extraheren op basis van de utterance, maakt u een [expliciete lijst](https://aka.ms/ExplicitList) via de API-uitzondering toestaan voor schrijven. 

Stel bijvoorbeeld dat u hebt een patroon met beide optioneel syntaxis `[]`, en de syntaxis van de entiteit, `{}`, gecombineerde op een manier om gegevens te extraheren onjuist.

Houd rekening met het patroon [zoeken] e-mail over {subject} [van {persoon}]. In de volgende uitingen de **onderwerp** en **persoon** entiteit correct en niet correct worden opgehaald:

|Utterance|Entiteit|Juiste extractie|
|--|--|:--:|
|e-mail over honden van Chris|onderwerp = honden<br>persoon Chris =|✔|
|per e-mail over de man in de La Mancha|onderwerp = de man<br>persoon La Mancha =|X|

In de voorgaande tabel, de utterance `email about the man from La Mancha`, het onderwerp moet `the man from La Mancha` (titel van een boek), maar omdat het onderwerp de optionele word bevat `from`, de titel onjuist wordt voorspeld. 

U kunt met het oplossen van deze uitzondering op het patroon, toevoegen `the man from la mancha` als een lijst met expliciete-overeenkomst voor de {subject} entiteit met de [API ontwerpen voor expliciete lijst](https://aka.ms/ExplicitList).

### <a name="syntax-to-mark-optional-text-in-a-template-utterance"></a>Syntaxis voor het markeren van optionele tekst in een sjabloon utterance
Optionele tekst in de utterance met behulp van de syntaxis van reguliere expressie vierkant haakje sluiten, markeert `[]`. De optionele tekst kunt vierkante haken maximaal twee vierkante haken nesten.

|Patroon met optionele tekst|
|--|
|`[find] email about {subject} [from {person}]`|

Leestekens zoals `.`, `!`, en `?` kan worden genegeerd met behulp van de vierkante haken. Als u wilt deze markeringen negeren, moet elke is ingeschakeld in een afzonderlijke patroon. De syntaxis van de optionele ondersteunt momenteel geen een item in een lijst van meerdere items worden genegeerd.

## <a name="patterns-only"></a>Alleen patronen
LUIS kunt een app zonder alle uitingen voorbeeld in de bedoeling. Deze informatie is alleen toegestaan als patronen worden gebruikt. Patronen vereist ten minste één entiteit in elk patroon. Voor een alleen-patroon-app, moet het patroon niet machine geleerde entiteiten bevatten omdat deze voorbeeld-uitingen hoeven. 

## <a name="best-practices"></a>Aanbevolen procedures
Informatie over [aanbevolen procedures](luis-concept-best-practices.md).

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Meer informatie over het implementeren van patronen in deze zelfstudie](luis-tutorial-pattern.md)
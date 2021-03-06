---
title: Afbeelding van beheer - Content Moderator
titlesuffix: Azure Cognitive Services
description: Beheer van afbeeldingen op ongepaste afbeeldingen normaal gebruiken
services: cognitive-services
author: sanjeev3
manager: cgronlun
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: conceptual
ms.date: 01/20/2018
ms.author: sajagtap
ms.openlocfilehash: 6c5fed78c67f974a2af11efd133e9a79ec52124b
ms.sourcegitcommit: ad08b2db50d63c8f550575d2e7bb9a0852efb12f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/26/2018
ms.locfileid: "47219648"
---
# <a name="image-moderation"></a>Beheer van afbeeldingen

Gebruik de Content Moderator geautomatiseerd beheer van afbeeldingen en [hulpprogramma voor menselijke beoordeling](Review-Tool-User-Guide/human-in-the-loop.md) tot gemiddelde van installatiekopieën voor erotische en ongepaste inhoud. Scan afbeeldingen voor tekstinhoud en Detecteer gezichten die tekst extraheren. U kunt installatiekopieën met aangepaste lijsten overeenkomen en verdere actie te ondernemen.

## <a name="evaluating-for-adult-and-racy-content"></a>Evalueren voor erotische en ongepaste inhoud

De **evalueren** bewerking wordt een betrouwbaarheidsscore tussen 0 en 1 geretourneerd. Ook wordt Boolean-waarde gelijk is aan true of false. Deze waarden te voorspellen of de installatiekopie van het potentiële volwassenen of ongepaste inhoud bevat. Wanneer u de API aanroept met de installatiekopie (bestand of URL), is het geretourneerde antwoord bevat de volgende informatie:

    "ImageModeration": {
      .............
      "adultClassificationScore": 0.019196987152099609,
      "isImageAdultClassified": false,
      "racyClassificationScore": 0.032390203326940536,
      "isImageRacyClassified": false,
      ............
      ],

> [!NOTE]

> - `isImageAdultClassified` Hiermee geeft u de mogelijke aanwezigheid van installatiekopieën die kunnen worden beschouwd als seksueel expliciet of volwassenen in bepaalde situaties.
> - `isImageRacyClassified` Hiermee geeft u de mogelijke aanwezigheid van installatiekopieën die kunnen worden beschouwd als seksueel suggestieve of volwassen in bepaalde situaties.
> - De scores zijn tussen 0 en 1. Hoe hoger de score, hoe hoger het model is voorspellen van de categorie mogelijk van toepassing zijn. Deze Preview-versie, is afhankelijk van een statistische model in plaats van handmatig gecodeerde resultaten. Het is raadzaam om eerst te testen met uw eigen inhoud om te bepalen hoe elke categorie overeenstemt met uw vereisten.
> - De Booleaanse waarden zijn true of false afhankelijk van de interne score drempelwaarden. Klanten moeten beoordelen of u wilt deze waarde wordt gebruikt of moet u besluiten welke aangepaste drempelwaarden op basis van hun inhoud beleid.
>

## <a name="detecting-text-with-optical-character-recognition-ocr"></a>Tekst met optische tekenherkenning (OCR) detecteren

De **optische tekenherkenning (OCR)** bewerking voorspelt de aanwezigheid van de tekst in een afbeelding en extraheert het voor beheer van tekst, onder andere gebruikt. U kunt de taal opgeven. Als u een taal opgeeft, wordt de detectie standaard in het Engels.

Het antwoord bevat de volgende informatie:
- De oorspronkelijke tekst.
- De gedetecteerde tekstelementen met hun scores vertrouwen.

Voorbeeld extraheren:

    "TextDetection": {
      "status": {
        "code": 3000.0,
        "description": "OK",
        "exception": null
      },
      .........
      "language": "eng",
      "text": "IF WE DID \r\nALL \r\nTHE THINGS \r\nWE ARE \r\nCAPABLE \r\nOF DOING, \r\nWE WOULD \r\nLITERALLY \r\nASTOUND \r\nOURSELVE \r\n",
      "candidates": []
    },


## <a name="detecting-faces"></a>Gezichten detecteren

Gezichten detecteren helpt bij het persoonlijk identificeerbare informatie (PII) zoals gezichten in afbeeldingen detecteren. U detecteren mogelijke gezichten en het aantal mogelijke gezichten in elke afbeelding.

Een antwoord bevat deze informatie:

- Gezichten tellen
- Lijst met locaties van gezichten gedetecteerd

Voorbeeld extraheren:


    "FaceDetection": {
       ......
      "result": true,
      "count": 2,
      "advancedInfo": [
      .....
      ],
      "faces": [
        {
          "bottom": 598,
          "left": 44,
          "right": 268,
          "top": 374
        },
        {
          "bottom": 620,
          "left": 308,
          "right": 532,
          "top": 396
        }
      ]
    }

## <a name="creating-and-managing-custom-lists"></a>Aangepaste lijsten maken en beheren

In veel online community's, nadat gebruikers afbeeldingen of andere typen inhoud uploaden kunnen aanstootgevende items gedeeld meerdere keren via de volgende dagen, weken en maanden. De kosten van het herhaaldelijk scannen en gefilterd op de dezelfde installatiekopie of ook maar enigszins gewijzigde versie van de installatiekopie vanaf meerdere locaties kunnen worden dure en gevoelig voor fouten.

In plaats van toezicht houden op dezelfde installatiekopie meerdere keren, kunt u de aanstootgevende afbeeldingen toevoegen aan uw aangepaste lijst met geblokkeerde inhoud. Op die manier uw systeem inhoudstoezicht vergelijkt binnenkomende afbeeldingen op basis van uw aangepaste lijsten en stopt verdere verwerking.

> [!NOTE]
> Er is een maximumlimiet van **5 image lijsten** met elke lijst **niet meer dan 10.000 afbeeldingen**.
>

De Content Moderator biedt een complete [afbeeldingen lijst Management API](try-image-list-api.md) met bewerkingen voor het beheren van lijsten met aangepaste installatiekopieën. Beginnen met de [afbeelding geeft een lijst van API-Console](try-image-list-api.md) en gebruiken van de REST-API-codevoorbeelden. Lees ook de [installatiekopie lijst .NET snelstartgids](image-lists-quickstart-dotnet.md) als u bekend met Visual Studio en C# bent.

## <a name="matching-against-your-custom-lists"></a>Overeenkomen met uw aangepaste lijsten

De bewerking overeenkomst kunt fuzzy overeenkomst met binnenkomende afbeeldingen van een van uw aangepaste lijsten, maken en beheren met de lijst met bewerkingen.

Als een overeenkomst wordt gevonden, wordt de bewerking retourneert de id en de beheer-labels van de overeenkomende installatiekopie. Het antwoord bevat deze informatie:

- Overeenkomst score (tussen 0 en 1)
- Overeenkomende installatiekopie
- Afbeelding tags (toegewezen tijdens de vorige toezicht)
- Afbeelding labels

Voorbeeld extraheren:

    {
    ..............,
    "IsMatch": true,
    "Matches": [
        {
            "Score": 1.0,
            "MatchId": 169490,
            "Source": "169642",
            "Tags": [],
            "Label": "Sports"
        }
    ],
    ....
    }

## <a name="human-review-tool"></a>Programma voor menselijke beoordeling

Voor meer genuanceerde gevallen gebruikt u de Content Moderator [controlehulpprogramma](Review-Tool-User-Guide/human-in-the-loop.md) en de API aan de oppervlakte van de resultaten van toezicht en de inhoud van de beoordeling van uw menselijke moderators. Ze controleren van de labels machine is toegewezen en hun uiteindelijke beslissingen bevestigen.

![Beoordeling van de installatiekopie van menselijke moderators](images/moderation-reviews-quickstart-dotnet.PNG)

## <a name="next-steps"></a>Volgende stappen

U kunt uitproberen de [installatiekopie toezicht-API-console](try-image-api.md) en gebruiken van de REST-API-codevoorbeelden. Lees ook de [installatiekopie toezicht .NET snelstartgids](image-moderation-quickstart-dotnet.md) als u bekend met Visual Studio en C# bent.

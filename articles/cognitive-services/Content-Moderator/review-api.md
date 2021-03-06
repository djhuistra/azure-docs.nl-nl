---
title: Beheer van taken en human-in-the-loop beoordelingen - Content Moderator
titlesuffix: Azure Cognitive Services
description: Menselijk toezicht van toepassing op de computer-ondersteund toezicht op voor de beste resultaten.
services: cognitive-services
author: sanjeev3
manager: cgronlun
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: conceptual
ms.date: 1/21/2018
ms.author: sajagtap
ms.openlocfilehash: b4a2f62b1c9cefb716cb217baf7389c3e7c790b8
ms.sourcegitcommit: ad08b2db50d63c8f550575d2e7bb9a0852efb12f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/26/2018
ms.locfileid: "47223250"
---
# <a name="moderation-jobs-and-reviews"></a>Beheer van taken en beoordelingen

Geautomatiseerd beheer met human-in-the-loop mogelijkheden te combineren met behulp van het Azure Content Moderator [revisie API](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5) om op te halen van de beste resultaten voor uw bedrijf.

De beoordeling-API biedt de volgende manieren op te nemen van menselijk toezicht in uw inhoudstoezicht-proces:

* `Job` bewerkingen worden gebruikt om het geautomatiseerd beheer en het maken van menselijke beoordeling start als één stap.
* `Review` bewerkingen worden gebruikt voor het maken van menselijke beoordeling, buiten de beheer-stap.
* `Workflow` bewerkingen worden gebruikt voor het beheren van werkstromen automatiseren met drempelwaarden voor het maken van de beoordeling scannen.

De `Job` en `Review` operations accepteren de callback-eindpunten voor het ontvangen van de status en de resultaten.

In dit artikel bevat informatie over de `Job` en `Review` bewerkingen. Lees de [overzicht van werkstromen](workflow-api.md) voor informatie over het maken, bewerken en werkstroomdefinities ophalen.

## <a name="job-operations"></a>Taakbewerkingen

### <a name="start-a-job"></a>Een taak starten
Gebruik de `Job.Create` bewerking om een beheer en de taak voor het maken van menselijke beoordeling te starten. Content Moderator scant de inhoud en evalueert de opgegeven werkstroom. Op basis van de resultaten van de werkstroom, deze beoordelingen gemaakt of wordt de stap overgeslagen. Het verzendt ook de codes na toezicht en na beoordeling voor de callback-eindpunt.

De invoer zijn onder andere de volgende informatie:

- De revisie-id-team.
- De inhoud die moet worden gecontroleerd.
- De naam van de werkstroom. (De standaardwaarde is de werkstroom 'standaard').
- Uw API-callback het serviceverbindingspunt voor meldingen.
 
Het volgende antwoord bevat de id van de taak die is gestart. U kunt de taak-id de taakstatus en krijgt u gedetailleerde informatie.

    {
        "JobId": "2018014caceddebfe9446fab29056fd8d31ffe"
    }

### <a name="get-job-status"></a>Taakstatus

Gebruik de `Job.Get` bewerking en de taak-id voor de details van een taak die wordt uitgevoerd of voltooid. De bewerking retourneert onmiddellijk terwijl voor het beheer van taak asynchroon wordt uitgevoerd. De resultaten worden geretourneerd via de callback-eindpunt.

De invoer zijn onder andere de volgende informatie:

- De revisie team-ID: de taak-id die wordt geretourneerd door de vorige bewerking

Het antwoord bevat de volgende informatie:

- De id van de beoordeling gemaakt. (Deze ID gebruiken om op te halen van de resultaten van de uiteindelijke beoordeling.)
- De status van de taak (voltooid of wordt uitgevoerd): de toegewezen toezicht tags (sleutel / waarde-paren).
- Het rapport van de taak kan worden uitgevoerd.
 
 
        {
            "Id": "2018014caceddebfe9446fab29056fd8d31ffe",
            "TeamName": "some team name",
            "Status": "Complete",
            "WorkflowId": "OCR",
            "Type": "Image",
            "CallBackEndpoint": "",
            "ReviewId": "201801i28fc0f7cbf424447846e509af853ea54",
            "ResultMetaData":[
            {
            "Key": "hasText",
            "Value": "True"
            },
            {
            "Key": "ocrText",
            "Value": "IF WE DID \r\nALL \r\nTHE THINGS \r\nWE ARE \r\nCAPABLE \r\nOF DOING, \r\nWE WOULD \r\nLITERALLY \r\nASTOUND \r\nOURSELVE \r\n"
            }
            ],
            "JobExecutionReport": [
            {
                "Ts": "2018-01-07T00:38:29.3238715",
                "Msg": "Posted results to the Callbackendpoint: https://requestb.in/vxke1mvx"
                },
                {
                "Ts": "2018-01-07T00:38:29.2928416",
                "Msg": "Job marked completed and job content has been removed"
                },
                {
                "Ts": "2018-01-07T00:38:29.0856472",
                "Msg": "Execution Complete"
                },
            {
                "Ts": "2018-01-07T00:38:26.7714671",
                "Msg": "Successfully got hasText response from Moderator"
                },
                {
                "Ts": "2018-01-07T00:38:26.4181346",
                "Msg": "Getting hasText from Moderator"
                },
                {
                "Ts": "2018-01-07T00:38:25.5122828",
                "Msg": "Starting Execution - Try 1"
                }
            ]
        }
 
![Beoordeling van de installatiekopie van menselijke moderators](images/ocr-sample-image.PNG)

## <a name="review-operations"></a>Bewerkingen controleren

### <a name="create-reviews"></a>Beoordelingen maken

Gebruik de `Review.Create` tijdens het maken van de onlinebeoordelingen door mensen. U ze ergens anders gemiddelde of aangepaste logica gebruik de beheer-labels toe te wijzen.

De invoer voor deze bewerking zijn onder andere:

- De inhoud die moet worden gecontroleerd.
- De toegewezen tags (sleutel-waardeparen) voor controle door menselijke moderators.

Het volgende antwoord ziet u de revisie-id:

    [
        "201712i46950138c61a4740b118a43cac33f434",
    ]


### <a name="get-review-status"></a>Controleer de status ophalen
Gebruik de `Review.Get` bewerking worden de resultaten opgehaald nadat een menselijke beoordeling van de gecontroleerde installatiekopie is voltooid. U ontvangt een bericht via de verstrekte callback-eindpunt. 

De bewerking retourneert twee sets met tags: 

* De labels die zijn toegewezen door de service beheer
* De labels nadat de menselijke beoordeling is voltooid

De invoer zijn ten minste:

- De naam van de beoordeling-team
- De revisie-id die wordt geretourneerd door de vorige bewerking

Het antwoord bevat de volgende informatie:

- De status controleren
- De tags (sleutel / waarde-paren) door de revisor van de menselijke bevestigd
- De tags (sleutel / waarde-paren) die is toegewezen door de service beheer

U ziet dat zowel de revisor toegewezen tags (**reviewerResultTags**) en de eerste labels (**metagegevens**) in het volgende voorbeeldantwoord:

    {
        "reviewId": "201712i46950138c61a4740b118a43cac33f434",
        "subTeam": "public",
        "status": "Complete",
        "reviewerResultTags": [
        {
            "key": "a",
            "value": "False"
        },
        {
            "key": "r",
            "value": "True"
        },
        {
            "key": "sc",
            "value": "True"
        }
        ],
        "createdBy": "{teamname}",
        "metadata": [
        {
            "key": "sc",
            "value": "true"
        }
        ],
        "type": "Image",
        "content": "https://reviewcontentprod.blob.core.windows.net/{teamname}/IMG_201712i46950138c61a4740b118a43cac33f434",
        "contentId": "0",
        "callbackEndpoint": "{callbackUrl}"
    }

## <a name="next-steps"></a>Volgende stappen

* U kunt uitproberen de [taak API-console](try-review-api-job.md), en gebruikt u de REST-API-codevoorbeelden. Als u bekend met Visual Studio en C# bent, Lees ook de [Snelstartgids voor .NET-taken](moderation-jobs-quickstart-dotnet.md). 
* Voor beoordelingen, aan de slag met de [revisie API-console](try-review-api-review.md), en gebruikt u de REST-API-codevoorbeelden. Vervolgens ziet de [Snelstartgids voor .NET beoordelingen](moderation-reviews-quickstart-dotnet.md).
* Voor video beoordelingen, gebruikt u de [Video revisie snelstartgids](video-reviews-quickstart-dotnet.md), en leer hoe u [Transcripten toevoegen aan de video beoordeling](video-transcript-reviews-quickstart-dotnet.md).

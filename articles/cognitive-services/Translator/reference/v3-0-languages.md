---
title: Translator Text-API talen methode
titlesuffix: Azure Cognitive Services
description: Gebruik de talen van Translator tekst-API-methode.
services: cognitive-services
author: Jann-Skotdal
manager: cgronlun
ms.service: cognitive-services
ms.component: translator-text
ms.topic: reference
ms.date: 03/29/2018
ms.author: v-jansko
ms.openlocfilehash: 51f15bd9c75f24be0d477d10de55c93a51cfbf3f
ms.sourcegitcommit: f10653b10c2ad745f446b54a31664b7d9f9253fe
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46129638"
---
# <a name="translator-text-api-30-languages"></a>Translator Text-API 3.0: talen

Hiermee haalt u de reeks talen die momenteel worden ondersteund door andere bewerkingen van de Translator Text-API. 

## <a name="request-url"></a>Aanvraag-URL

Verzendt een `GET` aanvragen:
```HTTP
https://api.cognitive.microsofttranslator.com/languages?api-version=3.0
```

## <a name="request-parameters"></a>Aanvraagparameters

Parameters van de aanvraag doorgegeven aan de query-tekenreeks zijn:

<table width="100%">
  <th width="20%">Queryparameter</th>
  <th>Beschrijving</th>
  <tr>
    <td>API-versie</td>
    <td>*Vereiste parameter*.<br/>De versie van de API die is aangevraagd door de client. De waarde moet liggen `3.0`.</td>
  </tr>
  <tr>
    <td>scope</td>
    <td>*Optionele parameter*.<br/>Een door komma's gescheiden lijst met namen van de groep van talen om terug te definiëren. Toegestane namen zijn: `translation`, `transliteration` en `dictionary`. Als er geen bereik is opgegeven, wordt alle groepen worden geretourneerd, die gelijk is aan te geven `scope=translation,transliteration,dictionary`. Om te beslissen welke set ondersteunde talen voor uw scenario geschikt is, Zie de beschrijving van de [antwoordobject](#response-body).</td>
  </tr>
</table> 

Aanvraagheaders zijn:

<table width="100%">
  <th width="20%">Headers</th>
  <th>Beschrijving</th>
  <tr>
    <td>Accepteer taal</td>
    <td>*Optionele aanvraagheader*.<br/>De taal die moet worden gebruikt voor tekenreeksen voor interface. Sommige van de velden in het antwoord zijn namen van talen of namen van de regio's. Gebruik deze parameter voor het definiëren van de taal waarin deze namen worden geretourneerd. De taal die is opgegeven door op te geven van een opgemaakte BCP-47-taalcode. Gebruik bijvoorbeeld de waarde `fr` aan te vragen van namen in het Frans of gebruikt u de waarde `zh-Hant` naar namen van de aanvraag in een traditioneel Chinees.<br/>Namen zijn opgegeven in de Engelse taal als een doeltaal is niet opgegeven of als de lokalisatie is niet beschikbaar.
    </td>
  </tr>
  <tr>
    <td>X-ClientTraceId</td>
    <td>*Optionele aanvraagheader*.<br/>Een client gegenereerde GUID voor het aanduiden van de aanvraag.</td>
  </tr>
</table> 

Verificatie is niet vereist om op te halen van bronnen.

## <a name="response-body"></a>De hoofdtekst van antwoord

Een client gebruikt de `scope` queryparameter om te definiëren welke groepen van talen die het geïnteresseerd in.

* `scope=translation` biedt de talen die worden ondersteund voor het vertalen van tekst in één taal naar een andere taal;

* `scope=transliteration` biedt mogelijkheden voor het converteren van tekst in één taal van één script naar een ander script;

* `scope=dictionary` taal paren biedt waarvoor `Dictionary` bewerkingen als resultaat de gegevens.

Een client kan meerdere groepen tegelijkertijd ophalen door een door komma's gescheiden lijst met namen op te geven. Bijvoorbeeld, `scope=translation,transliteration,dictionary` retourneerde ondersteunde talen voor alle groepen.

Een geslaagde reactie is een JSON-object met één eigenschap voor elke aangevraagde groep:

```json
{
    "translation": {
        //... set of languages supported to translate text (scope=translation)
    },
    "transliteration": {
        //... set of languages supported to convert between scripts (scope=transliteration)
    },
    "dictionary": {
        //... set of languages supported for alternative translations and examples (scope=dictionary)
    }
}
```

De waarde voor elke eigenschap is als volgt.

* `translation` De eigenschap

  De waarde van de `translation` eigenschap is een woordenlijst met (sleutel, waarde) paren. Elke sleutel is een BCP-47-taalcode. Een sleutel identificeert een taal waarvoor tekst kan worden omgezet naar of van vertaald. De waarde die is gekoppeld aan de sleutel is een JSON-object met eigenschappen die de taal die wordt beschreven:

  * `name`: De weergavenaam van de taal in de landinstellingen aangevraagd `Accept-Language` header.

  * `nativeName`: Weergave de naam van de taal in de oorspronkelijke landinstellingen voor deze taal.

  * `dir`: Richting, namelijk `rtl` voor talen van rechts naar links of `ltr` voor talen van links naar rechts.

  Er is een voorbeeld:
          
  ```json
  {
    "translation": {
      ...
      "fr": {
        "name": "French",
        "nativeName": "Français",
        "dir": "ltr"
      },
      ...
    }
  }
  ```

* `transliteration` De eigenschap

  De waarde van de `transliteration` eigenschap is een woordenlijst met (sleutel, waarde) paren. Elke sleutel is een BCP-47-taalcode. Een sleutel identificeert een taal waarvoor tekst kan worden geconverteerd van een script naar een ander script. De waarde die is gekoppeld aan de sleutel is een JSON-object met eigenschappen die de taal en de bijbehorende ondersteunde scripts beschrijven:

  * `name`: De weergavenaam van de taal in de landinstellingen aangevraagd `Accept-Language` header.

  * `nativeName`: Weergave de naam van de taal in de oorspronkelijke landinstellingen voor deze taal.

  * `scripts`: Lijst met scripts te converteren. Elk element van de `scripts` lijst heeft eigenschappen:

    * `code`: Code identificeren van het script.

    * `name`: De weergavenaam van het script in de landinstellingen aangevraagd `Accept-Language` header.

    * `nativeName`: Weergave de naam van de taal in de oorspronkelijke landinstellingen voor de taal.

    * `dir`: Richting, namelijk `rtl` voor talen van rechts naar links of `ltr` voor talen van links naar rechts.

    * `toScripts`: Lijst met scripts die beschikbaar zijn voor het converteren van tekst die moet worden. Elk element van de `toScripts` lijst heeft eigenschappen `code`, `name`, `nativeName`, en `dir` zoals eerder beschreven.

  Er is een voorbeeld:

  ```json
  {
    "transliteration": {
      ...
      "ja": {
        "name": "Japanese",
        "nativeName": "日本語",
        "scripts": [
          {
            "code": "Jpan",
            "name": "Japanese",
            "nativeName": "日本語",
            "dir": "ltr",
            "toScripts": [
              {
                "code": "Latn",
                "name": "Latin",
                "nativeName": "ラテン語",
                "dir": "ltr"
              }
            ]
          },
          {
            "code": "Latn",
            "name": "Latin",
            "nativeName": "ラテン語",
            "dir": "ltr",
            "toScripts": [
              {
                "code": "Jpan",
                "name": "Japanese",
                "nativeName": "日本語",
                "dir": "ltr"
              }
            ]
          }
        ]
      },
      ...
    }
  }
  ```

* `dictionary` De eigenschap

  De waarde van de `dictionary` eigenschap is een woordenlijst met (sleutel, waarde) paren. Elke sleutel is een BCP-47-taalcode. De sleutel identificeert een taal waarvoor alternatieve vertalingen en back-vertalingen beschikbaar zijn. De waarde is een JSON-object waarin de source-taal en de doel-talen met de beschikbare vertalingen worden beschreven:

  * `name`: De weergavenaam van de source-taal in de landinstellingen aangevraagd `Accept-Language` header.

  * `nativeName`: Weergave de naam van de taal in de oorspronkelijke landinstellingen voor deze taal.

  * `dir`: Richting, namelijk `rtl` voor talen van rechts naar links of `ltr` voor talen van links naar rechts.

  * `translations`: Lijst met talen met alternatief vertalingen en voorbeelden voor de query, uitgedrukt in de source-taal. Elk element van de `translations` lijst heeft eigenschappen:

    * `name`: De weergavenaam van de doel-taal in de landinstellingen aangevraagd `Accept-Language` header.

    * `nativeName`: Weergavenaam van de doel-taal in de oorspronkelijke landinstellingen voor de doel-taal.

    * `dir`: Richting, namelijk `rtl` voor talen van rechts naar links of `ltr` voor talen van links naar rechts.
    
    * `code`: De taalcode die de doeltaal te identificeren.

  Er is een voorbeeld:

  ```json
  "es": {
    "name": "Spanish",
    "nativeName": "Español",
    "dir": "ltr",
    "translations": [
      {
        "name": "English",
        "nativeName": "English",
        "dir": "ltr",
        "code": "en"
      }
    ]
  },
  ```

De structuur van het antwoordobject wijzigen niet zonder een wijziging in de versie van de API. Voor de dezelfde versie van de API wijzigen de lijst met beschikbare talen na verloop van tijd omdat Microsoft Translator wordt voortdurend uitgebreid voor de lijst met talen die worden ondersteund door de services.

De lijst van ondersteunde talen verandert niet vaak. Sla de netwerkbandbreedte en het reactievermogen verbeteren, een clienttoepassing moet rekening houden met caching taal resources en de bijbehorende entity-tag (`ETag`). Vervolgens de clienttoepassing kunt regelmatig (bijvoorbeeld, elke 24 uur) query uitvoeren op de service om op te halen van de meest recente set van ondersteunde talen. Doorgeven van de huidige `ETag` waarde in een `If-None-Match` header-veld kan de service voor het optimaliseren van het antwoord. Als de resource is niet gewijzigd, wordt de service-statuscode 304 en de hoofdtekst van een leeg antwoord geretourneerd.

## <a name="response-headers"></a>Antwoordheaders

<table width="100%">
  <th width="20%">Headers</th>
  <th>Beschrijving</th>
  <tr>
    <td>ETag</td>
    <td>Huidige waarde van de entity-tag voor de aangevraagde groepen van ondersteunde talen. Als u de volgende aanvragen efficiënter, verzendt de client kan de `ETag` waarde in een `If-None-Match` header-veld.
    </td>
  </tr>
  <tr>
    <td>X-RequestId</td>
    <td>De waarde die wordt gegenereerd door de service voor het identificeren van de aanvraag. Het wordt gebruikt voor het oplossen van problemen.</td>
  </tr>
</table> 

## <a name="response-status-codes"></a>Antwoord-statuscodes

Hier volgen de mogelijke HTTP-statuscodes die een aanvraag retourneert. 

<table width="100%">
  <th width="20%">Statuscode</th>
  <th>Beschrijving</th>
  <tr>
    <td>200</td>
    <td>Geslaagd.</td>
  </tr>
  <tr>
    <td>304</td>
    <td>De resource is niet gewijzigd sinds de versie die is opgegeven door de aanvraagheaders `If-None-Match`.</td>
  </tr>
  <tr>
    <td>400</td>
    <td>Een van de queryparameters is ontbreekt of is ongeldig. De parameters van de juiste aanvraag voordat opnieuw wordt geprobeerd.</td>
  </tr>
  <tr>
    <td>429</td>
    <td>De aanroeper is te veel aanvragen verzenden.</td>
  </tr>
  <tr>
    <td>500</td>
    <td>Er is een onverwachte fout opgetreden. Als de fout zich blijft voordoen, rapporteren met: datum en tijd van de fout, aanvraag-id van de reactieheader `X-RequestId`, en de client-id van aanvraagheader `X-ClientTraceId`.</td>
  </tr>
  <tr>
    <td>503</td>
    <td>De server is tijdelijk niet beschikbaar. De aanvraag opnieuw. Als de fout zich blijft voordoen, rapporteren met: datum en tijd van de fout, aanvraag-id van de reactieheader `X-RequestId`, en de client-id van aanvraagheader `X-ClientTraceId`.</td>
  </tr>
</table> 

## <a name="examples"></a>Voorbeelden

Het volgende voorbeeld ziet hoe u talen die worden ondersteund voor tekstvertaling ophaalt.

# <a name="curltabcurl"></a>[CURL](#tab/curl)

```
curl "https://api.cognitive.microsofttranslator.com/languages?api-version=3.0&scope=translation"
```

---

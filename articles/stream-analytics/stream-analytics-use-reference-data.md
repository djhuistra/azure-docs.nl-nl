---
title: Referentiegegevens gebruiken voor zoekacties in Azure Stream Analytics
description: In dit artikel wordt beschreven hoe u referentiegegevens gebruiken om te zoeken of correleren van gegevens in het ontwerp van een Azure Stream Analytics-taak query.
services: stream-analytics
author: jseb225
ms.author: jeanb
manager: kfile
ms.reviewer: mamccrea
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 04/25/2018
ms.openlocfilehash: fd912885335b41e3d7ca8ee717b6bb1b9c88e729
ms.sourcegitcommit: c2c279cb2cbc0bc268b38fbd900f1bac2fd0e88f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/24/2018
ms.locfileid: "49984142"
---
# <a name="using-reference-data-for-lookups-in-stream-analytics"></a>Met behulp van referentiegegevens voor zoekacties in Stream Analytics
Referentiegegevens (ook wel bekend als een opzoektabel) is een eindige gegevensset die is statische of langzaam veranderende aard is, gebruikt om uit te voeren een zoekopdracht of om te correleren met de stroom van uw gegevens. Azure Stream Analytics wordt geladen referentiegegevens in het geheugen te controleren van de verwerking van gegevensstromen met lage latentie. Om het gebruik van referentiegegevens in uw Azure Stream Analytics-taak, gebruikt u in het algemeen een [verwijzing gegevens Join](https://msdn.microsoft.com/library/azure/dn949258.aspx) in uw Query. Stream Analytics maakt gebruik van Azure Blob-opslag als de opslaglaag voor referentiegegevens en met Azure Data Factory-verwijzing gegevens kunnen worden getransformeerd en/of gekopieerd naar Azure Blob-opslag, voor gebruik als referentiegegevens, van [een willekeurig aantal cloudgebaseerde en on-premises gegevensarchieven](../data-factory/copy-activity-overview.md). Referentiegegevens is gemodelleerd als een reeks blobs (gedefinieerd in de configuratie van de invoer), in oplopende volgorde van de datum/tijd opgegeven in de blobnaam. Deze **alleen** ondersteunt het toevoegen aan het einde van de reeks met behulp van een datum/tijd **groter** dan de versie die is opgegeven door de laatste blob in de reeks.

Stream Analytics biedt ondersteuning voor referentiegegevens met **maximale grootte van 300 MB**. De limiet van 300 MB van de maximumgrootte van referentiegegevens is alleen met eenvoudige query's. Als de complexiteit van query toeneemt om op te nemen van stateful verwerking, statistische functies in vensters, tijdelijke joins en tijdelijke analysefuncties, zoals is het waarschijnlijk dat de maximale grootte van verwijzing gegevens vermindert wordt ondersteund. Als Azure Stream Analytics kan niet laden van de referentiegegevens en complexe bewerkingen uitvoeren, wordt de taak te weinig geheugen en mislukken. In dergelijke gevallen kunt bereiken SU % gebruik metrische gegevens 100%.    

|**Het aantal Streaming-eenheden**  |**Maximumgrootte van ongeveer ondersteund (in MB)**  |
|---------|---------|
|1   |50   |
|3   |150   |
|6 en hoger   |300   |

Het aantal Streaming-eenheden van een taak dan 6, verhoogt niet de maximale ondersteunde grootte van de referentiegegevens.

Ondersteuning voor compressie is niet beschikbaar voor referentiegegevens. 

## <a name="configuring-reference-data"></a>Referentiegegevens configureren
Voor het configureren van de referentiegegevens, moet u eerst het maken van de invoer die is van het type **referentiegegevens**. De onderstaande tabel wordt uitgelegd dat elke eigenschap die u opgeven moet tijdens het maken van de referentiegegevens invoer met de beschrijving:

|**De naam van eigenschap**  |**Beschrijving**  |
|---------|---------|
|Invoeralias   | Een beschrijvende naam die in de taakquery wordt gebruikt om te verwijzen naar deze invoer.   |
|Opslagaccount   | De naam van het opslagaccount waar uw BLOB's zich bevinden. Als deze zich in hetzelfde abonnement als uw Stream Analytics-taak, kunt u deze selecteren in de vervolgkeuzelijst.   |
|Opslagaccountsleutel   | De geheime sleutel die is gekoppeld aan de storage-account. Dit wordt automatisch ingevuld als het opslagaccount zich in hetzelfde abonnement als uw Stream Analytics-taak.   |
|Storage-Container   | Containers bieden een logische groepering van blobs die zijn opgeslagen in de Microsoft Azure Blob-service. Wanneer u een blob geüpload naar de Blob-service, moet u een container voor die blob opgeven.   |
|Padpatroon   | Het pad dat wordt gebruikt om uw blobs in de opgegeven container te vinden. U kunt kiezen binnen het pad naar een of meer exemplaren van de volgende 2 variabelen opgeven:<BR>{date}, {time}<BR>Voorbeeld 1: products/{date}/{time}/product-list.csv<BR>Voorbeeld 2: products/{date}/product-list.csv<BR><br> Als de blob in het opgegeven pad niet bestaat, wordt de Stream Analytics-taak voor onbepaalde tijd wachten op de blob weer beschikbaar.   |
|[Optioneel] datumnotatie   | Als u {date} binnen het pad-patroon dat u hebt opgegeven gebruikt hebt, kunt u de datumnotatie waarin uw blobs zijn ingedeeld in de vervolgkeuzelijst van de ondersteunde indelingen selecteren.<BR>Bijvoorbeeld: Jjjj/MM/DD MM/DD/JJJJ, enzovoort.   |
|[Optioneel] tijdnotatie   | Als u {time} hebt gebruikt in het pad-patroon dat u hebt opgegeven, kunt u de indeling waarin uw blobs zijn ingedeeld in de vervolgkeuzelijst van de ondersteunde indelingen selecteren.<BR>Voorbeeld: HH, uu mm/of uu: mm.  |
|Serialisatie-indeling voor gebeurtenissen   | Er moet in Stream Analytics zijn aangegeven welke serialisatie-indeling wordt gebruikt voor inkomende gegevensstromen om te controleren of uw query's werken zoals verwacht. Voor referentiegegevens zijn de ondersteunde indelingen CSV en JSON.  |
|Encoding   | Alleen de coderingsindeling UTF-8 wordt momenteel ondersteund.  |

## <a name="static-reference-data"></a>Statische referentiegegevens
Als uw referentiegegevens niet verwacht wordt te wijzigen, klikt u vervolgens ondersteuning voor statische verwijzing gegevens is ingeschakeld door een statische pad op te geven in de configuratie van de invoer. Azure Stream Analytics, neemt de blob uit het opgegeven pad. {date} en {time} vervanging tokens niet vereist. Referentiegegevens is onveranderbaar in Stream Analytics. Daarom wordt overschrijven van een statische referentiegegevens-blob niet aanbevolen.

## <a name="generating-reference-data-on-a-schedule"></a>Referentiegegevens volgens een schema genereren
Als uw referentiegegevens een langzaam veranderende gegevensset is, wordt ondersteund voor het vernieuwen van verwijzing gegevens is ingeschakeld door een padpatroon op te geven in de invoer-configuratie met behulp van de {date} en {time} vervanging tokens. Stream Analytics, neemt de bijgewerkte referentiegegevens-gegevens-definities op basis van dit padpatroon. Bijvoorbeeld, een patroon van `sample/{date}/{time}/products.csv` met datumnotatie **'Jjjj-MM-DD'** en een tijd-indeling van **'HH: mm'** Hiermee geeft u Stream Analytics om op te halen de bijgewerkte blob `sample/2015-04-16/17-30/products.csv` om 17:30 uur op 16 April , 2015 UTC-tijdzone.

Azure Stream Analytics scant automatisch voor vernieuwd referentiegegevens-blobs op basis van een interval van één minuut.

> [!NOTE]
> Stream Analytics-taken bekijken die momenteel voor het vernieuwen van de blob alleen wanneer de tijd op de computer wordt verplaatst naar de tijd die is gecodeerd in de blob-naam. Bijvoorbeeld, de taak wordt gezocht naar `sample/2015-04-16/17-30/products.csv` zo snel mogelijk maar het is niet eerder dan 17:30 uur op 16 April 2015 UTC tijdzone. Het wordt *nooit* zoeken naar een blob met een gecodeerde tijd ouder is dan het laatste item dat is gedetecteerd.
> 
> Bijvoorbeeld Zodra de taak wordt de blob gevonden `sample/2015-04-16/17-30/products.csv` deze bestanden met een gecodeerde datum ouder is dan 5:30 PM 16 April 2015 worden genegeerd als een latere binnenkomen `sample/2015-04-16/17-25/products.csv` blob wordt gemaakt in dezelfde container wordt niet gebruikt door de taak deze.
> 
> Op dezelfde manier als `sample/2015-04-16/17-30/products.csv` alleen om 22:03 uur 16 April 2015 wordt gemaakt, maar geen blob met een eerdere datum in de container aanwezig is, de taak wordt dit bestand begint bij 10:03 PM 16 April 2015 gebruiken en gebruikmaken van de vorige referentiegegevens tot die tijd.
> 
> Een uitzondering hierop is wanneer de taak opnieuw verwerken gegevens terug in tijd moet of wanneer de taak wordt gestart. De taak is tijdens het starten op zoek naar de meest recente blob geproduceerd voordat de taak starten tijd die is opgegeven. Dit wordt gedaan om ervoor te zorgen dat er een **niet-lege** verwijzingsgegevensset voor wanneer de taak wordt gestart. Als er een kan niet worden gevonden, de taak wordt weergegeven met de volgende diagnose: `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) kan worden gebruikt voor het indelen van de taak voor het maken van de bijgewerkte blobs nodig door Stream Analytics voor het bijwerken van definities van de referentie-gegevens. Een Data Factory is een cloudgebaseerde gegevensintegratieservice waarmee de verplaatsing en transformatie van gegevens wordt beheerd en geautomatiseerd. Data Factory ondersteunt [verbinding te maken met een groot aantal van de cloud gebaseerde en on-premises gegevensarchieven](../data-factory/copy-activity-overview.md) en verplaatsen van gegevens eenvoudig een regelmatige die u opgeeft. Voor meer informatie en stapsgewijze instructies over het instellen van een Data Factory-pijplijn voor het genereren van referentiegegevens voor Stream Analytics wordt vernieuwd volgens een vooraf gedefinieerd schema, bekijk deze [GitHub voorbeeld](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Tips voor het vernieuwen van uw verwijzingsgegevens
1. Referentiegegevens-blobs niet overschrijven omdat ze onveranderd zijn.
2. De aanbevolen manier om te vernieuwen referentiegegevens is aan:
    * Gebruik {date} / {time} in het padpatroon
    * Een nieuwe blob gebruikt dezelfde container en het pad patroon dat is gedefinieerd in de taak invoer toevoegen
    * Gebruik van een datum/tijd **groter** dan de versie die is opgegeven door de laatste blob in de reeks.
3. Referentiegegevens-blobs zijn **niet** besteld door van de blob-tijdstip 'Laatst gewijzigd', maar alleen door de tijd en datum die is opgegeven in de blob naam met behulp van de {date} en {time} vervangingen.
3. Om te voorkomen dat u hoeft te groot aantal blobs lijst, overweeg dan het verwijderen van oude blobs waarvoor de verwerking niet meer worden uitgevoerd. Houd er rekening mee dat ASA mogelijk gaan moet een klein bedrag in sommige scenario's zoals opnieuw opstarten opnieuw verwerken.

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Snelstart: Een Stream Analytics-taak maken met behulp van de Azure-portal](stream-analytics-quick-create-portal.md)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: https://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: https://go.microsoft.com/fwlink/?LinkId=517301

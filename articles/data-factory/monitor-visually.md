---
title: Azure data factory's visueel bewaken | Microsoft Docs
description: Meer informatie over het Azure Data Factory's visueel te controleren
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/12/2018
ms.author: shlo
ms.openlocfilehash: 4b3828e1857d17a128de346449d5cf2041709e50
ms.sourcegitcommit: 7208bfe8878f83d5ec92e54e2f1222ffd41bf931
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/14/2018
ms.locfileid: "39041072"
---
# <a name="visually-monitor-azure-data-factories"></a>Azure data factory's visueel bewaken
Azure Data Factory is een cloudgebaseerde gegevensintegratieservice waarmee u gegevensgestuurde werkstromen kunt maken in de cloud. Op deze manier kunt u de verplaatsing en transformatie van gegevens indelen en automatiseren. Met Azure Data Factory kunt u gegevensgestuurde werkstromen (ook wel pijplijnen) maken en plannen die gegevens uit verschillende gegevensarchieven kunnen opnemen en de gegevens kunnen verwerken/transformeren met behulp van rekenservices zoals Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics en Azure Machine Learning. Daarnaast kunt u de uitvoergegevens publiceren naar gegevensarchieven zoals Azure SQL Data Warehouse, zodat BI-toepassingen (business intelligence) ze kunnen gebruiken.
In deze quick start leert u hoe u pijplijnen van data factory v2 visueel bewaken zonder één regel code te schrijven.
Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

## <a name="monitor-data-factory-v2-pipelines"></a>Data factory v2-pijplijnen bewaken

1. Start de webbrowser **Microsoft Edge** of **Google Chrome**. Op dit moment wordt de Data Factory-gebruikersinterface alleen ondersteund in de webbrowsers Microsoft Edge en Google Chrome.
2. Meld u aan bij de [Azure-portal](https://portal.azure.com/).
3. Navigeer naar de gemaakte data factory-blade in Azure portal en klik op de tegel 'Bewaking en beheer'. Hiermee wordt de ADF v2 visual bewakingservaring geopend.

## <a name="list-view-monitoring"></a>Lijstweergave bewaking

De pijplijn bewaken en de activiteit wordt uitgevoerd met een eenvoudige lijstweergave-interface. Alle uitvoeringen worden weergegeven in de lokale tijdzone van de browser. U kunt de tijdzone wijzigen en alle datum-/tijdvelden springen naar de geselecteerde tijdzone.  

#### <a name="monitoring-pipeline-runs"></a>Controleren van Pijplijnuitvoeringen
Lijstweergave geeft elke pijplijnuitvoering voor uw v2-pijplijnen van uw gegevensfactory duidelijk weer. Opgenomen kolommen:

| **De naam van kolom** | **Beschrijving** |
| --- | --- |
| Pijplijnnaam | Naam van de pijplijn. |
| Acties | Één actie beschikbaar om uitvoeringen van activiteit weer te geven. |
| Uitvoering starten | Pijplijn uitvoeren start datum en tijd (MM/DD/JJJJ uu: mm: SS AM/PM) |
| Duur | Uitvoeringsduur (uu: mm:) |
| Geactiveerd door | Handmatige triggers, trigger voor schema |
| Status | Is mislukt, is voltooid, wordt uitgevoerd |
| Parameters | Pijplijnuitvoering parameters (naam, waarde-paren) |
| Fout | Pijplijnuitvoering fout (indien/any) |
| Run-id | Id van de pijplijnuitvoering |

![Pijplijnuitvoeringen controleren](media/monitor-visually/pipeline-runs.png)

#### <a name="monitoring-activity-runs"></a>Uitvoeringen van activiteit controleren
Lijstweergave geeft activiteituitvoeringen weer die corresponderen met elke pijplijnuitvoering. Klik op **'Uitvoeringen van activiteit'** pictogram onder de **'Acties'** kolom om weer te geven van de activiteit wordt uitgevoerd voor elke pijplijn-run. Opgenomen kolommen:

| **De naam van kolom** | **Beschrijving** |
| --- | --- |
| Naam activiteit | Naam van de activiteit in de pijplijn. |
| Type activiteit | Type activiteit dat wil zeggen kopiëren, HDInsightSpark, HDInsightHive enzovoort. |
| Uitvoering starten | Uitvoering van activiteit start datum en tijd (MM/DD/JJJJ uu: mm: SS AM/PM) |
| Duur | Uitvoeringsduur (uu: mm:) |
| Status | Is mislukt, is voltooid, wordt uitgevoerd |
| Invoer | JSON-matrix met een beschrijving van de invoer voor de activiteit |
| Uitvoer | JSON-matrix met een beschrijving van de uitvoer voor activiteiten |
| Fout | Fout (indien/any) de uitvoering van activiteiten |

![Uitvoering van activiteiten controleren](media/monitor-visually/activity-runs.png)

> [!IMPORTANT]
> U moet klikken op **'Vernieuwen'** pictogram bovenaan de lijst van de uitvoering van pijplijn en activiteit te vernieuwen. Automatisch vernieuwen wordt momenteel niet ondersteund.
>

![Vernieuwen](media/monitor-visually/refresh.png)

## <a name="features"></a>Functies

#### <a name="select-a-data-factory-to-monitor"></a>Selecteer een data factory te controleren
Beweeg de muisaanwijzer op de **Data Factory** pictogram links bovenin. Klik op het pictogram 'Pijl' voor een overzicht van azure-abonnementen en gegevensfactory's die u kunt controleren.

![Data factory selecteren](media/monitor-visually/select-datafactory.png)

#### <a name="rich-ordering-and-filtering"></a>Uitgebreid op volgorde plaatsen en filteren

Volgorde pijplijnuitvoeringen in aflopende/oplopende op Run Start en filter pijplijnuitvoeringen door de volgende kolommen:

| **De naam van kolom** | **Beschrijving** |
| --- | --- |
| Pijplijnnaam | Naam van de pijplijn. Opties voor snelle filters bevatten voor 'afgelopen 24 uur', 'Afgelopen week', 'afgelopen 30 dagen' of een aangepaste datum en tijd selecteren. |
| Uitvoering starten | Pijplijnuitvoering starten, datum en tijd |
| Uitvoeringsstatus | Filter wordt uitgevoerd door de status dat wil zeggen is voltooid, is mislukt, wordt uitgevoerd |

![Filteren](media/monitor-visually/filter.png)

#### <a name="addremove-columns-in-list-view"></a>Kolommen in de lijstweergave toevoegen/verwijderen
Klik met de rechtermuisknop op de lijstweergavekop en kies de kolommen die u wilt weergeven in de lijstweergave

![Kolommen](media/monitor-visually/columns.png)

#### <a name="reorder-column-widths-in-list-view"></a>Volgorde van kolombreedtes in lijstweergave
Vergroot of verklein de kolombreedtes in lijstweergave door eenvoudig de muisaanwijzer boven de kolomkop

#### <a name="user-properties"></a>Gebruikerseigenschappen

Zodat deze een entiteit die u kunt controleren, kunt u een eigenschap van een pijplijn activiteit als een eigenschap van het promoveren. Bijvoorbeeld, u kunt verhogen de **bron** en **bestemming** eigenschappen van de kopieeractiviteit in de pijplijn als eigenschappen van de gebruiker. U kunt ook selecteren **automatisch genereren** voor het genereren van de **bron** en **bestemming** gebruikerseigenschappen voor een kopieeractiviteit.

![Eigenschappen van de gebruiker maken](media/monitor-visually/monitor-user-properties-image1.png)

> [!NOTE]
> U kunt maximaal 5 pijplijn activiteitseigenschappen alleen promoveren als eigenschappen van de gebruiker.

Nadat u de eigenschappen van de gebruiker hebt gemaakt, kunt u deze bewaken in de controleweergaven in de lijst. Als de bron voor de kopieerbewerking een tabelnaam wordt opgegeven is, kunt u de naam van de tabel bewaken terwijl een kolom in de activiteit wordt uitgevoerd lijstweergave.

![Lijst zonder gebruikerseigenschappen uitvoeringen van activiteit](media/monitor-visually/monitor-user-properties-image2.png)

![Kolommen voor de eigenschappen van de gebruiker toevoegen aan lijst met uitvoeringen van activiteit](media/monitor-visually/monitor-user-properties-image3.png)

![Uitvoeringen van activiteit lijst met kolommen voor de eigenschappen van de gebruiker](media/monitor-visually/monitor-user-properties-image4.png)

#### <a name="guided-tours"></a>Rondleidingen
Klik op het 'informatiepictogram' linksonder in en klik op rondleidingen begeleide voor stapsgewijze instructies over het bewaken van de uitvoering van uw pijplijn en activiteit.

![Rondleidingen](media/monitor-visually/guided-tours.png)

#### <a name="feedback"></a>Feedback
Klik op het pictogram 'Feedback' om ons feedback over verschillende functies of eventuele problemen die u kunt te maken krijgen.

![Feedback](media/monitor-visually/feedback.png)

## <a name="next-steps"></a>Volgende stappen

Zie [bewaken en beheren van pijplijnen programmatisch](https://docs.microsoft.com/azure/data-factory/monitor-programmatically) artikel voor meer informatie over het controleren en beheren van pijplijnen

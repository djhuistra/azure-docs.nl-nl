---
title: Runtime-uitzonderingen analyseren met behulp van Azure Application Insights | Microsoft Docs
description: Zelfstudie voor het vinden en diagnosticeren van runtime-uitzonderingen in uw toepassing met behulp van Azure Application Insights.
services: application-insights
keywords: ''
author: mrbullwinkle
ms.author: mbullwin
ms.date: 09/19/2017
ms.service: application-insights
ms.custom: mvc
ms.topic: tutorial
manager: carmonm
ms.openlocfilehash: f45cb6a47756fae7b75d8c3df80a0bc754742063
ms.sourcegitcommit: f3bd5c17a3a189f144008faf1acb9fabc5bc9ab7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/10/2018
ms.locfileid: "44298997"
---
# <a name="find-and-diagnose-run-time-exceptions-with-azure-application-insights"></a>Runtime-uitzonderingen vinden en diagnosticeren met behulp van Azure Application Insights

Azure Application Insights verzamelt telemetrie van uw toepassing om runtime-uitzonderingen te identificeren en diagnosticeren.  In deze zelfstudie leert u dit proces met uw toepassing.  In deze zelfstudie leert u procedures om het volgende te doen:

> [!div class="checklist"]
> * Het wijzigen van uw project om het bijhouden van uitzonderingen in te schakelen
> * Het identificeren van uitzonderingen voor verschillende onderdelen van uw toepassing
> * Het weergeven van de details van een uitzondering
> * Het downloaden van een momentopname van de uitzondering naar Visual Studio voor het opsporen van fouten
> * Het analyseren van details van mislukte aanvragen met behulp van een querytaal
> * Het maken van een nieuw werkitem om de foute code te corrigeren


## <a name="prerequisites"></a>Vereisten

Vereisten voor het voltooien van deze zelfstudie:

- Installeer [Visual Studio 2017](https://www.visualstudio.com/downloads/) met de volgende workloads:
    - ASP.NET-ontwikkeling en webontwikkeling
    - Azure-ontwikkeling
- Download en installeer de [Visual Studio Snapshot Debugger](http://aka.ms/snapshotdebugger).
- [Visual Studio Snapshot Debugger](https://docs.microsoft.com/azure/application-insights/app-insights-snapshot-debugger) inschakelen
- Implementeer een .NET-toepassing in Azure en [schakel de Application Insights-SDK](app-insights-asp-net.md)in. 
- De zelfstudie volgt de identificatie van een uitzondering in uw toepassing; wijzig dus uw code in uw ontwikkelings- of testomgeving om een uitzondering te genereren. 

## <a name="log-in-to-azure"></a>Meld u aan bij Azure.
Meld u aan bij de Azure-portal op [https://portal.azure.com](https://portal.azure.com).


## <a name="analyze-failures"></a>Fouten analyseren
Application Insights verzamelt fouten in uw toepassing en laat u zien hoe vaak ze voorkomen in verschillende bewerkingen, om u te helpen uw inspanningen te richten op het verhelpen van de fouten met de meeste impact.  Vervolgens kunt u inzoomen op de details van deze fouten om de hoofdoorzaak te identificeren.   

1. Selecteer **Application Insights** en selecteer vervolgens uw abonnement.  
2. U kunt het deelvenster **Fouten** openen door **Fouten** te selecteren in het menu **Onderzoeken** menu of door op de grafiek **Mislukte aanvragen** te klikken.

    ![Mislukte aanvragen](media/app-insights-tutorial-runtime-exceptions/failed-requests.png)

3. In het deelvenster **Mislukte aanvragen** deelvenster ziet u het aantal mislukte aanvragen en het aantal getroffen gebruikers voor elke bewerking van de toepassing.  Door deze informatie te sorteren op gebruiker kunt u de fouten identificeren die de meeste impact hebben op gebruikers.  In dit voorbeeld zijn **GET Employees/Create** en **GET Customers/Details** goede kandidaten om te onderzoeken, vanwege het hoge aantal fouten en getroffen gebruikers.  Door een bewerking te selecteren wordt meer informatie over deze bewerking zichtbaar in het rechter deelvenster.

    ![Deelvenster Mislukte aanvragen](media/app-insights-tutorial-runtime-exceptions/failed-requests-blade.png)

4. Verklein het tijdvenster om in te zoomen op de periode waar het aantal fouten een piek vertoont.

    ![Venster Mislukte aanvragen](media/app-insights-tutorial-runtime-exceptions/failed-requests-window.png)

5. Zie de gerelateerde steekproeven door te klikken op de knop met het aantal gefilterde resultaten. De 'aanbevolen' steekproeven hebben gerelateerde telemetrie van alle onderdelen, zelfs als er hierin steekproeven zijn genomen. Klik op een zoekresultaat om de details van de fout te bekijken.

    ![Steekproeven van mislukte aanvraag](media/app-insights-tutorial-runtime-exceptions/failed-requests-search.png)

6. In de details van de mislukte aanvraag ziet u het Gantt-diagram waarin wordt aangegeven dat er twee afhankelijkheidsfouten waren in deze transactie, wat heeft gezorgd voor meer dan 50% van de totale duur van de transactie. Deze ervaring bevat alle telemetrie voor alle onderdelen van een gedistribueerde toepassing die zijn gerelateerd aan deze bewerkings-id. [Meer informatie over de nieuwe ervaring](app-insights-transaction-diagnostics.md). U kunt een van de items selecteren om rechts de details te bekijken. 

    ![Details van mislukte aanvraag](media/app-insights-tutorial-runtime-exceptions/failed-request-details.png)

7. De bewerkingsdetails laten ook een FormatException zien, die de fout lijkt te hebben veroorzaakt.  U ziet dat de uitzondering te wijten is aan een ongeldige postcode. U kunt de momentopname voor foutopsporing openen om foutopsporingsgegevens op codeniveau te bekijken in Visual Studio.

    ![Details van uitzondering](media/app-insights-tutorial-runtime-exceptions/failed-requests-exception.png)

## <a name="identify-failing-code"></a>Mislukt code identificeren
De Snapshot Debugger verzamelt momentopnamen van de meest frequente uitzonderingen in uw toepassing om u te helpen bij de diagnose van de onderliggende oorzaak in de productie.  U kunt foutopsporingsmomentopnamen in het portaal bekijken om de aanroepstack te zien en variabelen inspecteren bij elk aanroepstackframe. Vervolgens kunt u fouten in de broncode opsporen door de snapshot te downloaden en te openen in Visual Studio 2017.

1. Klik in de eigenschappen van de uitzondering op **Momentopname voor foutopsporing openen**.
2. Het deelvenster **Debug Snapshot** (fouten opsporen in momentopname) wordt geopend met de aanroepstack voor de aanvraag.  Klik op een methode om de waarden van alle lokale variabelen op het moment van de aanvraag weer te geven.  Te beginnen bij de bovenste methode in dit voorbeeld, zien we lokale variabelen die geen waarde hebben.

    ![Foutopsporingsmomentopname](media/app-insights-tutorial-runtime-exceptions/debug-snapshot-01.png)

4. De eerste aanroep met geldige waarden is **ValidZipCode**, en we zien dat er een postcode is opgegeven met letters die niet kan worden omgezet in een geheel getal.  Dit lijkt de fout in de code te zijn die moet worden gecorrigeerd.

    ![Foutopsporingsmomentopname](media/app-insights-tutorial-runtime-exceptions/debug-snapshot-02.png)

5. Klik op **Momentopname downloaden** om deze momentopname te downloaden naar Visual Studio, waar we de werkelijke code kunnen vinden die moet worden gecorrigeerd.
6. De momentopname wordt geladen in Visual Studio.
7. U kunt nu een foutopsporingssessie uitvoeren in Visual Studio die snel de coderegel identificeert die de uitzondering heeft veroorzaakt.

    ![Uitzondering in code](media/app-insights-tutorial-runtime-exceptions/exception-code.png)


## <a name="use-analytics-data"></a>Analytics-gegevens gebruiken
Alle gegevens die door Application Insights worden verzameld, worden opgeslagen in Azure Log Analytics, dat een uitgebreide querytaal biedt waarmee u de gegevens op verschillende manieren kunt analyseren.  We kunnen deze gegevens gebruiken voor het analyseren van de aanvragen die de uitzondering hebben gegenereerd die we aan het onderzoeken zijn. 

8. Klik op de CodeLens-informatie boven de code om telemetrie van Application Insights te bekijken.

    ![Code](media/app-insights-tutorial-runtime-exceptions/codelens.png)

9. Klik op **Impact analyseren** om Application Insights Analytics te openen.  Het wordt gevuld met enkele query's die details bieden over mislukte aanvragen, zoals getroffen gebruikers, browsers en regio's.<br><br>![Analytische gegevens](media/app-insights-tutorial-runtime-exceptions/analytics.png)<br>

## <a name="add-work-item"></a>Werkitem toevoegen
Als u Application Insights aansluit op een trackingsysteem zoals Azure DevOps of GitHub, kunt u direct vanuit Application Insights een werkitem maken.

1. Ga terug naar het deelvenster **Uitzonderingseigenschappen** in Application Insights.
2. Klik op **Nieuw werkitem**.
3. Het deelvenster **Nieuw werkitem** wordt geopend, waarin al gegevens over de uitzondering zijn ingevuld.  U kunt aanvullende informatie toevoegen voordat u opslaat.

    ![Nieuw werkitem](media/app-insights-tutorial-runtime-exceptions/new-work-item.png)

## <a name="next-steps"></a>Volgende stappen
Nu u hebt geleerd runtime-uitzonderingen te identificeren, kunt u doorgaan naar de volgende zelfstudie om te leren hoe u prestatieproblemen kunt identificeren en diagnosticeren.

> [!div class="nextstepaction"]
> [Prestatieproblemen identificeren](app-insights-tutorial-performance.md)
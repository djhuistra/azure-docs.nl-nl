---
title: Teamontwikkeling met Azure Dev Spaces met behulp van Java en VS Code | Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: stepro
ms.author: stephpr
ms.date: 08/01/2018
ms.topic: tutorial
description: Snelle Kubernetes-ontwikkeling met containers en microservices in Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers
manager: mmontwil
ms.openlocfilehash: b1f05c176c6005a2fda8025b4645813013a30cb3
ms.sourcegitcommit: b7e5bbbabc21df9fe93b4c18cc825920a0ab6fab
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/27/2018
ms.locfileid: "47407175"
---
# <a name="team-development-with-azure-dev-spaces"></a>Teamontwikkeling met Azure Dev Spaces

In deze zelfstudie leert u hoe u gelijktijdig kunt werken in verschillende ontwikkelomgevingen met behulp van meerdere ontwikkelruimten, om het werk gescheiden te houden in afzonderlijke ontwikkelruimten in hetzelfde cluster.

## <a name="call-a-service-running-in-a-separate-container"></a>Een service aanroepen die wordt uitgevoerd in een afzonderlijke container

In deze sectie maakt u een tweede service, `mywebapi`, en laat u deze aanroepen door `webfrontend`. Elke service wordt uitgevoerd in een afzonderlijke container. Vervolgens spoort u fouten op in beide containers.

![Meerdere containers](media/common/multi-container.png)

### <a name="download-sample-code-for-mywebapi"></a>Voorbeeldcode voor *mywebapi* downloaden
Omwille van de tijd downloaden we voorbeeldcode uit een GitHub-opslagplaats. Ga naar https://github.com/Azure/dev-spaces en selecteer **Clone or Download** om de GitHub-opslagplaats te downloaden. De code voor deze sectie bevindt zich in `samples/java/getting-started/mywebapi`.

### <a name="run-mywebapi"></a>*mywebapi* uitvoeren
1. Open de map `mywebapi` in een *afzonderlijk VS Code-venster*.
1. Open het **Opdrachtenpalet** (via het menu **Beeld | Opdrachtenpalet**), en gebruik automatisch aanvullen om te typen en deze opdracht te selecteren: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.
1. Druk op F5 en wacht tot de service is gebouwd en geïmplementeerd. Dit proces is voltooid, zodra de VS Code-balk voor foutopsporing wordt weergegeven.
1. De eindpunt-URL ziet er ongeveer uit als http://localhost:\<portnumber\>. **Tip: op de VS Code-statusbalk wordt een klikbare URL weergegeven.** Het lijkt misschien alsof de container lokaal wordt uitgevoerd, maar dat is niet zo. De container wordt uitgevoerd in onze ontwikkelomgeving in Azure. Het localhost-adres is te zien omdat er nog geen openbare eindpunten zijn gedefinieerd in `mywebapi` en toegang daarom alleen mogelijk is binnen het Kubernetes-exemplaar. Voor uw gemak en om interactie met de privésessie mogelijk te maken vanaf de lokale computer wordt in Azure Dev Spaces een tijdelijke SSH-tunnel gemaakt naar de container die wordt uitgevoerd in Azure.
1. Wanneer `mywebapi` klaar is, opent u de browser naar het localhost-adres.
1. Als alle stappen zijn voltooid, moet er een reactie van de `mywebapi`-service te zien zijn.

### <a name="make-a-request-from-webfrontend-to-mywebapi"></a>Verzend een aanvraag van *webfrontend* naar *mywebapi*
Nu gaan we code schrijven in `webfrontend` waarmee een aanvraag wordt verzonden naar `mywebapi`.
1. Schakel over naar het VS Code-venster voor `webfrontend`.
1. *Voeg* de volgende `import`-instructies toe onder de `package`-instructie:

   ```java
   import java.io.*;
   import java.net.*;
   ```
1. *Vervang* de code voor de begroetingsmethode:

    ```java
    @RequestMapping(value = "/greeting", produces = "text/plain")
    public String greeting(@RequestHeader(value = "azds-route-as", required = false) String azdsRouteAs) throws Exception {
        URLConnection conn = new URL("http://mywebapi/").openConnection();
        conn.setRequestProperty("azds-route-as", azdsRouteAs); // propagate dev space routing header
        try (BufferedReader reader = new BufferedReader(new InputStreamReader(conn.getInputStream())))
        {
            return "Hello from webfrontend and " + reader.lines().reduce("\n", String::concat);
        }
    }
    ```

In het vorige codevoorbeeld wordt de `azds-route-as`-header van de binnenkomende aanvraag doorgestuurd naar de uitgaande aanvraag. Later ziet u hoe dit teamleden helpt om samen te ontwikkelen.

### <a name="debug-across-multiple-services"></a>Foutopsporing in meerdere services
1. Op dit punt moet `mywebapi` nog steeds worden uitgevoerd met het bijgevoegde foutopsporingsprogramma. Als dit niet het geval is, drukt u op F5 in het `mywebapi`-project.
1. Stel een onderbrekingspunt in in de `index()`-methode van het `webapi`-project.
1. Stel in het `webfrontend`-project een onderbrekingspunt in vlak voordat deze een GET-aanvraag verzendt naar `mywebapi`, en wel op de regel die begint met `try`.
1. Druk op F5 in het `webfrontend`-project (of start het foutopsporingsprogramma opnieuw als het op dat moment wordt uitgevoerd).
1. Roep de web-app aan en analyseer de code in beide services.
1. In de web-app wordt nu op de pagina About een bericht weergegeven dat is samengesteld uit de twee services: Hello from webfrontend and Hello from mywebapi.

Dat is dus gelukt. U hebt nu een toepassing met meerdere containers waarin elke container afzonderlijk kan worden ontwikkeld en geïmplementeerd.

## <a name="learn-about-team-development"></a>Meer informatie over teamontwikkeling

[!INCLUDE [](../../includes/team-development-1.md)]

Laten we eens kijken hoe dat in zijn werk gaat. Ga naar het venster van VS Code voor `mywebapi` en bewerk de code op basis van de `String index()`-methode, bijvoorbeeld:

```java
@RequestMapping(value = "/", produces = "text/plain")
public String index() {
    return "Hello from mywebapi says something new";
}
```

[!INCLUDE [](../../includes/team-development-2.md)]

### <a name="well-done"></a>Dat is dus gelukt.
U hebt de introductiehandleiding voltooid! U hebt geleerd hoe u:

> [!div class="checklist"]
> * Azure Dev Spaces instellen met een beheerd Kubernetes-cluster in Azure.
> * Iteratief code ontwikkelen in containers.
> * Twee afzonderlijke services ontwikkelen en de DNS-servicedetectie van Kubernetes gebruiken om een andere service aan te roepen.
> * Uw code op een productieve manier ontwikkelen en testen in een teamomgeving.

Nu u Azure Dev Spaces hebt verkend, kunt u [uw dev-ruimte delen met teamleden](how-to/share-dev-spaces.md) en hen laten zien hoe eenvoudig het is om samen te werken.

## <a name="clean-up"></a>Opruimen
Als u een exemplaar van Azure Dev Spaces in een cluster volledig wilt verwijderen, waaronder alle ontwikkelruimtes en de actieve services die erin worden uitgevoerd, gebruikt u de opdracht `az aks remove-dev-spaces`. Houd er rekening mee dat deze actie niet kan worden teruggedraaid. U kunt later opnieuw ondersteuning voor Azure Dev Spaces toevoegen aan het cluster, maar u moet dan helemaal opnieuw beginnen. Uw oude services en ruimtes worden niet hersteld.

In het volgende voorbeeld worden de Azure Dev Spaces-controllers in uw actieve abonnement vermeld en wordt vervolgens de Azure Dev Spaces-controller die is gekoppeld aan het AKS-cluster 'myaks' in de resourcegroep 'myaks-rg' verwijderd.

```cmd
    azds controller list
    az aks remove-dev-spaces --name myaks --resource-group myaks-rg
```
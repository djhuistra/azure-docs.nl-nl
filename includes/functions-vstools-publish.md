---
title: bestand opnemen
description: bestand opnemen
services: functions
author: ggailey777
ms.service: functions
ms.topic: include
ms.date: 08/26/2018
ms.author: glenga
ms.custom: include file
ms.openlocfilehash: f3fa6c75fdaf30d13231bc3072bd671614c9a668
ms.sourcegitcommit: ccdea744097d1ad196b605ffae2d09141d9c0bd9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/23/2018
ms.locfileid: "49650654"
---
1. Klik in **Solution Explorer** met de rechtermuisknop op het project en selecteer **Publiceren**.

2. Selecteer **Azure-functie-app**, kies **Nieuwe maken** en selecteer vervolgens **Publiceren**.

    ![Kies een publicatiedoel](./media/functions-vstools-publish/functions-visual-studio-publish-profile.png)

    Als u **Uitvoeren vanuit ZIP-bestand** activeert, wordt uw functie-app in Azure rechtstreeks vanuit het implementatiepakket uitgevoerd. Zie voor meer informatie [Uw Azure Functions uitvoeren vanuit een pakketbestand](../articles/azure-functions/run-functions-from-deployment-package.md).

3. Als u Visual Studio nog niet aan uw Azure-account hebt gekoppeld, selecteert u **Een account toevoegen...**.

4. In het dialoogvenster **App-service maken** gebruikt u de **hosting**instellingen zoals weergegeven in de tabel onder de afbeelding:

    ![Het dialoogvenster App Service maken](./media/functions-vstools-publish/functions-visual-studio-publish.png)

    | Instelling      | Voorgestelde waarde  | Beschrijving                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Naam van app** | Wereldwijd unieke naam | Naam waarmee uw nieuwe functie-app uniek wordt aangeduid. |
    | **Abonnement** | Kies uw abonnement | Het te gebruiken Azure-abonnement. |
    | **[Resourcegroep](../articles/azure-resource-manager/resource-group-overview.md)** | myResourceGroup |  Naam van de resourcegroep waarin uw functie-app moet worden gemaakt. Kies **Nieuw** om een nieuwe resourcegroep te maken.|
    | **[App-serviceabonnement](../articles/azure-functions/functions-scale.md)** | Verbruiksabonnement | Zorg ervoor dat u **Verbruik** kiest onder **Grootte** nadat u op **Nieuw** hebt geklikt om een serverloos abonnement te maken. Kies ook een **Locatie** in een [regio](https://azure.microsoft.com/regions/) bij u in de buurt of in de buurt van andere services die door uw functies worden gebruikt. Wanneer u in een abonnement van een ander type dan **Verbruik** werkt, moet u de [schaal van uw functie-app](../articles/azure-functions/functions-scale.md) beheren.  |
    | **[Opslagaccount](../articles/storage/common/storage-quickstart-create-account.md)** | Algemeen opslagaccount | Er is een Azure-opslagaccount vereist voor de Functions-runtime. Klik op **Nieuw** om een algemeen opslagaccount te maken. U kunt ook een bestaand account gebruiken dat voldoet aan de [vereisten voor een opslagaccount](../articles/azure-functions/functions-scale.md#storage-account-requirements).  |

5. Klik op **Maken** om een functie-app en verwante resources met deze instellingen te maken in Azure en implementeer de code voor uw functieproject. 

6. Noteer de **Site-URL** wanneer de implementatie is voltooid. Dit is het adres van uw functie-app in Azure.

    ![Succesbericht publiceren](./media/functions-vstools-publish/functions-visual-studio-publish-complete.png)

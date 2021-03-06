---
title: Lab-accounts in Azure Lab Services beheren | Microsoft Docs
description: Informatie over het maken van een lab-account, alle lab-accounts weergeven of verwijderen van een lab-account in een Azure-abonnement.
services: lab-services
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2018
ms.author: spelluru
ms.openlocfilehash: 6f9b85ec4821ff2454970136b3c8af2cb0f92154
ms.sourcegitcommit: 0f54b9dbcf82346417ad69cbef266bc7804a5f0e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/26/2018
ms.locfileid: "50140820"
---
# <a name="manage-lab-accounts-in-azure-lab-services"></a>Lab-accounts in Azure Lab Services beheren 
Een lab-account is in Azure Lab-Services, een container voor beheerde labs zoals leslokaallabs. Een beheerder stelt u een lab-account met Azure Lab-Services en biedt toegang tot een lab-eigenaren die labs in het account maken kunnen. In dit artikel wordt beschreven hoe u een lab-account maken, alle lab-accounts weergeven of verwijderen van een lab-account.

## <a name="create-a-lab-account"></a>Een lab-account maken
1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Selecteer **Een resource maken** in het hoofdmenu aan de linkerkant.
3. Zoek naar **Lab Services** in Azure Marketplace en selecteer **Lab Services** in de vervolgkeuzelijst. 
4. Selecteer **Lab Services (preview)** in de gefilterde lijst met services. 
5. Selecteer **Maken** in het venster **Een lab-account maken**.
7. Voer in het venster **Lab-account** de volgende acties uit: 
    1. Voer een naam in bij **lab-accountnaam**. 
    2. Selecteer het **Azure-abonnement** waarin u het lab-account wilt maken.
    3. Selecteer voor **Resourcegroep** de optie **Nieuwe maken** en voer een naam in voor de resourcegroep.
    4. Selecteer voor **Locatie** een locatie/regio waarin het lab-account moet worden gemaakt. 
    5. Selecteer **Maken**. 

        ![Venster Een lab-account maken](../media/how-to-manage-lab-accounts/lab-account-settings.png)
5. Als u de pagina voor het lab-account niet ziet, selecteert u de knop **Meldingen** en klikt u vervolgens op de knop **Ga naar resource** in de meldingen. 

    ![Venster Een lab-account maken](../media/how-to-manage-lab-accounts/notification-go-to-resource.png)    
6. U ziet de volgende pagina **lab-account**:

    ![Pagina lab-account](../media/how-to-manage-lab-accounts/lab-account-page.png)

## <a name="add-a-user-to-the-lab-creator-role"></a>Een gebruiker toevoegen aan de rol Labmaker
Om een leslokaallab in een labaccount in te kunnen stellen, moet de gebruiker lid zijn van de rol **Labmaker** in het labaccount. Het account dat u hebt gebruikt voor het maken van het lab-account wordt automatisch toegevoegd aan deze rol. Als u van plan bent een leslokaallab te maken met hetzelfde gebruikersaccount, kunt u deze stap overslaan. Als u een ander gebruikersaccount wilt gebruiken om een leslokaallab te maken, voert u de volgende stappen uit: 

1. Selecteer op de pagina **lab-account** de optie **Toegangsbeheer (IAM)** en klik op **+ Toevoegen** in de werkbalk. 

    ![Pagina lab-account](../media/tutorial-setup-lab-account/access-control.png)
2. Selecteer op de pagina **Machtigingen toevoegen** de optie **Labmaker** als **rol**. Selecteer de gebruiker die u wilt toevoegen aan de rol Labmaker en selecteer **Opslaan**. 

    ![Gebruiker toevoegen aan de rol Labmaker](../media/tutorial-setup-lab-account/add-user-to-lab-creator-role.png)

## <a name="specify-marketplace-images-available-to-lab-owners"></a>Microsoft Azure Marketplace-installatiekopieën die beschikbaar zijn voor eigenaars van een lab opgeven
Als eigenaar van een labaccount kunt u de Marketplace-installatiekopieën opgeven die labmakers kunnen gebruiken in het labaccount. 

1. Selecteer **Marketplace-installatiekopieën** in het menu aan de linkerkant. Standaard ziet u de volledige lijst met installatiekopieën (zowel ingeschakelde als uitgeschakelde). U kunt de lijst filteren om alleen ingeschakelde/uitgeschakelde installatiekopieën te bekijken door de optie **Alleen ingeschakeld**/**Alleen uitgeschakeld** in de vervolgkeuzelijst bovenaan te selecteren. 
    
    ![Pagina Microsoft Azure Marketplace-installatiekopieën](../media/tutorial-setup-lab-account/marketplace-images-page.png)

    De Marketplace-installatiekopieën die worden weergegeven in de lijst, zijn de enige die voldoen aan de volgende voorwaarden:
        
    - Hiermee wordt een enkele VM gemaakt.
    - Maakt gebruik van Azure Resource Manager om VM’s in te richten
    - Hiervoor hoeft u geen extra licentieabonnement aan te schaffen
2. Als u een Microsoft Azure Marketplace-installatiekopie die is ingeschakeld wilt **uitschakelen**, voert u een van de volgende acties uit: 
    1. Selecteer **... (beletselteken)**  in de laatste kolom en selecteer **Installatiekopie uitschakelen**. 

        ![Een installatiekopie uitschakelen](../media/tutorial-setup-lab-account/disable-one-image.png) 
    2. Selecteer een of meer installatiekopieën in de lijst door de selectievakjes bij de namen van de installatiekopieën in de lijst te selecteren en **Geselecteerde installatiekopieën uitschakelen** te selecteren. 

        ![Meerdere installatiekopieën uitschakelen](../media/tutorial-setup-lab-account/disable-multiple-images.png) 
1. Als u een Microsoft Azure Marketplace-installatiekopie wilt **inschakelen**, voert u een van de volgende acties uit: 
    1. Selecteer **... (beletselteken)**  in de laatste kolom en selecteer **Installatiekopie inschakelen**. 
    2. Selecteer een of meer installatiekopieën in de lijst door de selectievakjes bij de namen van de installatiekopieën in de lijst te selecteren en **Geselecteerde installatiekopieën inschakelen** te selecteren. 

## <a name="view-lab-accounts"></a>Lab-accounts weergeven
1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Selecteer **alle resources** in het menu. 
3. Selecteer **Lab Services** voor de **type**. 
    U kunt ook filteren op abonnement, resourcegroep, locaties en tags. 

## <a name="delete-a-lab-account"></a>Een lab-account verwijderen
Volg de instructies uit de vorige sectie die lab-accounts in een lijst weergegeven. Gebruik de volgende instructies om een lab-account te verwijderen: 

1. Selecteer de **lab-account** die u wilt verwijderen. 
2. Selecteer **verwijderen** via de werkbalk. 
3. Type **Ja** ter bevestiging.
4. Selecteer **Verwijderen**. 

## <a name="view-and-manage-labs-in-the-lab-account"></a>Weergeven en labs in het lab-account beheren

1. Op de **Lab-Account** weergeeft, schakelt **Labs** in het menu links.

    ![Labs in het account](../media/how-to-manage-lab-accounts/labs-in-account.png)
1. U ziet een **lijst met labs** in het account met de volgende informatie: 
    1. De naam van het testlab.
    2. De datum waarop het lab is gemaakt. 
    3. E-mailadres van de gebruiker die het lab gemaakt. 
    4. Maximum aantal gebruikers dat is toegestaan in het lab. 
    5. De status van het testlab. 

## <a name="delete-a-lab-in-the-lab-account"></a>Een lab in het lab-account verwijderen
Volg de instructies in de vorige sectie voor een overzicht van de labs in het lab-account.

1. Selecteer **... (ellips)** , en selecteer **verwijderen**. 

    ![Verwijderen van een lab - knop](../media/how-to-manage-lab-accounts/delete-lab-button.png)
2. Selecteer **Ja** op het waarschuwingsbericht staan aangegeven. 



## <a name="next-steps"></a>Volgende stappen
Aan de slag met het installeren van een lab met Azure Lab Services:

- [Een leslokaallab instellen](tutorial-setup-classroom-lab.md)
- [Een lab instellen](../tutorial-create-custom-lab.md)

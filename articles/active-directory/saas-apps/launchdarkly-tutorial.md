---
title: 'Zelfstudie: Azure Active Directory-integratie met LaunchDarkly | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en LaunchDarkly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0e9cb37e-16bf-493b-bfc8-8d9840545a1e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2018
ms.author: jeedes
ms.openlocfilehash: 54bf459f6acd7649f3ad1a546bef1d0429393161
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "39420756"
---
# <a name="tutorial-azure-active-directory-integration-with-launchdarkly"></a>Zelfstudie: Azure Active Directory-integratie met LaunchDarkly

In deze zelfstudie leert u hoe u LaunchDarkly integreren met Azure Active Directory (Azure AD).

LaunchDarkly integreren met Azure AD biedt u de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot LaunchDarkly heeft.
- U kunt uw gebruikers automatisch ophalen aangemeld bij LaunchDarkly (Single Sign-On) met hun Azure AD-accounts inschakelen.
- U kunt uw accounts in één centrale locatie - Azure portal beheren.

Als u wilt graag meer informatie over de integratie van de SaaS-app met Azure AD, Zie [wat is toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met LaunchDarkly, moet u de volgende items:

- Een Azure AD-abonnement
- Een LaunchDarkly eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Als u wilt testen van de stappen in deze zelfstudie, raden we niet met behulp van een productie-omgeving.

Als u wilt testen van de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik uw productie-omgeving, niet als dat nodig is.
- Als u geen een proefversie Azure AD-omgeving hebt, kunt u [een proefversie van één maand krijgen](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u de Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. LaunchDarkly uit de galerie toe te voegen
1. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-launchdarkly-from-the-gallery"></a>LaunchDarkly uit de galerie toe te voegen
Voor het configureren van de integratie van LaunchDarkly in Azure AD, moet u LaunchDarkly uit de galerie toevoegen aan uw lijst met beheerde SaaS-apps.

**Als u wilt toevoegen LaunchDarkly uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het navigatievenster aan de linkerkant op **Azure Active Directory** pictogram. 

    ![De Azure Active Directory-knop][1]

1. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![De blade Enterprise-toepassingen][2]
    
1. Nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![De knop nieuwe toepassing][3]

1. Typ in het zoekvak **LaunchDarkly**, selecteer **LaunchDarkly** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![LaunchDarkly in de lijst met resultaten](./media/launchdarkly-tutorial/tutorial_launchdarkly_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en Azure AD eenmalige aanmelding testen

In deze sectie maakt u configureert en test Azure AD eenmalige aanmelding met LaunchDarkly op basis van een testgebruiker 'Julia steen' genoemd.

Voor eenmalige aanmelding om te werken, moet Azure AD om te weten wat de gebruiker equivalent in LaunchDarkly is aan een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gerelateerde gebruiker in LaunchDarkly tot stand worden gebracht.

Om te configureren en testen van Azure AD eenmalige aanmelding met LaunchDarkly, moet u de volgende bouwstenen voltooien:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
1. **[Maak een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
1. **[Maak een testgebruiker LaunchDarkly](#create-a-launchdarkly-test-user)**  : als u wilt een equivalent van Britta Simon in LaunchDarkly die is gekoppeld aan de Azure AD-weergave van de gebruiker hebben.
1. **[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
1. **[Eenmalige aanmelding testen](#test-single-sign-on)**  : als u wilt controleren of de configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD eenmalige aanmelding configureren

In deze sectie maakt u schakelt Azure AD eenmalige aanmelding in de Azure-portal en configureren van eenmalige aanmelding in uw toepassing LaunchDarkly.

**Voor het configureren van Azure AD eenmalige aanmelding met LaunchDarkly, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **LaunchDarkly** toepassingspagina integratie, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

1. Op de **eenmalige aanmelding** dialoogvenster, selecteer **modus** als **SAML gebaseerde aanmelding** eenmalige aanmelding inschakelen.

    ![In het dialoogvenster voor eenmalige aanmelding](./media/launchdarkly-tutorial/tutorial_launchdarkly_samlbase.png)

1. Op de **LaunchDarkly domein en URL's** sectie, voert u de volgende stappen uit als u wilt configureren van de toepassing in **IDP** modus gestart:

    ![LaunchDarkly domein en URL's, eenmalige aanmelding informatie](./media/launchdarkly-tutorial/tutorial_launchdarkly_url.png)

    a. In de **id (entiteits-ID)** tekstvak typt u de URL: `app.launchdarkly.com`

    b. In de **antwoord-URL** tekstvak, een URL met behulp van het volgende patroon: `https://app.launchdarkly.com/trust/saml2/acs/<customers-unique-id>`
    
    > [!NOTE]
    > De antwoord-URL-waarde is niet echt. U kunt de waarde wordt bijgewerkt met de werkelijke antwoord-URL, die later in de zelfstudie wordt uitgelegd.

1. Controleer **geavanceerde URL-instellingen weergeven** en voer de volgende stap als u wilt configureren van de toepassing in **SP** modus gestart:

    ![LaunchDarkly domein en URL's, eenmalige aanmelding informatie](./media/launchdarkly-tutorial/tutorial_launchdarkly_url1.png)

    In de **aanmeldings-URL** tekstvak typt u de URL: `https://app.launchdarkly.com`

1. Op de **SAML-handtekeningcertificaat** sectie, klikt u op **certificaat (Base64)** en slaat u het certificaatbestand op uw computer.

    ![De downloadkoppeling certificaat](./media/launchdarkly-tutorial/tutorial_launchdarkly_certificate.png) 

1. Klik op **opslaan** knop.

    ![Configureren van eenmalige aanmelding opslaan](./media/launchdarkly-tutorial/tutorial_general_400.png)
    
1. Op de **LaunchDarkly configuratie** sectie, klikt u op **configureren LaunchDarkly** openen **aanmelding configureren** venster. Kopiëren de **Single Sign-On Service URL** uit de **Naslaggids sectie.**

    ![LaunchDarkly configuratie](./media/launchdarkly-tutorial/tutorial_launchdarkly_configure.png)

1. Meld u in een ander browservenster in uw bedrijf LaunchDarkly site als beheerder.

1. Selecteer **Accountinstellingen** in het linkernavigatievenster.

    ![LaunchDarkly configuratie](./media/launchdarkly-tutorial/configure1.png)

1. Klik op **Security** tabblad.

    ![LaunchDarkly configuratie](./media/launchdarkly-tutorial/configure2.png)

1. Klik op **eenmalige aanmelding inschakelen** en vervolgens **SAML-configuratie bewerken**.

    ![LaunchDarkly configuratie](./media/launchdarkly-tutorial/configure3.png)

1. Op de **uw SAML-configuratie bewerken** sectie, voert u de volgende stappen uit:

    ![LaunchDarkly configuratie](./media/launchdarkly-tutorial/configure4.png)

    a. Kopieer de **URL van de SAML** voor uw exemplaar en plak deze in de antwoord-URL-tekstvak in **LaunchDarkly domein en URL's** sectie in Azure portal.

    b. In de **aanmeldings-URL** tekstvak, plak de **Single Sign-On Service URL** waarde die u hebt gekopieerd vanuit Azure portal.

    c. Het gedownloade certificaat vanuit de Azure-portal openen in Kladblok, Kopieer de inhoud en plak deze in de **X.509-certificaat** box of u kunt rechtstreeks upload het certificaat door te klikken op de **eenuploaden**.

    d. Klik op **Opslaan**.

### <a name="create-an-azure-ad-test-user"></a>Maak een testgebruiker Azure AD

Het doel van deze sectie is het maken van een testgebruiker in Azure portal Britta Simon genoemd.

   ![Maak een testgebruiker Azure AD][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de Azure portal, in het linkerdeelvenster klikt u op de **Azure Active Directory** knop.

    ![De Azure Active Directory-knop](./media/launchdarkly-tutorial/create_aaduser_01.png)

1. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/launchdarkly-tutorial/create_aaduser_02.png)

1. Om te openen de **gebruiker** in het dialoogvenster, klikt u op **toevoegen** aan de bovenkant van de **alle gebruikers** in het dialoogvenster.

    ![De knop toevoegen](./media/launchdarkly-tutorial/create_aaduser_03.png)

1. In de **gebruiker** dialoogvenster vak, voer de volgende stappen uit:

    ![Het dialoogvenster gebruiker](./media/launchdarkly-tutorial/create_aaduser_04.png)

    a. In de **naam** in het vak **BrittaSimon**.

    b. In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.

    c. Selecteer de **wachtwoord weergeven** selectievakje en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.

    d. Klik op **Create**.

### <a name="create-a-launchdarkly-test-user"></a>Maak een testgebruiker LaunchDarkly

Het doel van deze sectie is het maken van een gebruiker met de naam van Britta Simon in LaunchDarkly. LaunchDarkly biedt ondersteuning voor just-in-time inrichting, dit is standaard ingeschakeld. Er is geen actie-item voor u in deze sectie. Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot LaunchDarkly als deze nog niet bestaat.
>[!Note]
>Als u maken van een gebruiker handmatig wilt, neem dan contact op met [LaunchDarkly Client ondersteuningsteam](mailto:support@launchdarkly.com).

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie maakt inschakelen u Britta Simon gebruiken Azure eenmalige aanmelding door toegang te verlenen aan LaunchDarkly.

![De de gebruikersrol toewijzen][200] 

**Als u wilt Britta Simon aan LaunchDarkly toewijst, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de mapweergave en Ga naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

1. Selecteer in de lijst met toepassingen, **LaunchDarkly**.

    ![De koppeling LaunchDarkly in de lijst met toepassingen](./media/launchdarkly-tutorial/tutorial_launchdarkly_app.png)  

1. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![De koppeling 'Gebruikers en groepen'][202]

1. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Het deelvenster toewijzing toevoegen][203]

1. Op **gebruikers en groepen** dialoogvenster, selecteer **Britta Simon** in de lijst gebruikers.

1. Klik op **Selecteer** op knop **gebruikers en groepen** dialoogvenster.

1. Klik op **toewijzen** op knop **toevoegen toewijzing** dialoogvenster.

### <a name="test-single-sign-on"></a>Eenmalige aanmelding testen

In deze sectie maakt testen u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.

Wanneer u op de tegel LaunchDarkly in het toegangsvenster, u moet u automatisch aangemeld bij uw toepassing LaunchDarkly.
Zie voor meer informatie over het toegangsvenster, [Inleiding tot het toegangsvenster](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?)



<!--Image references-->

[1]: ./media/launchdarkly-tutorial/tutorial_general_01.png
[2]: ./media/launchdarkly-tutorial/tutorial_general_02.png
[3]: ./media/launchdarkly-tutorial/tutorial_general_03.png
[4]: ./media/launchdarkly-tutorial/tutorial_general_04.png

[100]: ./media/launchdarkly-tutorial/tutorial_general_100.png

[200]: ./media/launchdarkly-tutorial/tutorial_general_200.png
[201]: ./media/launchdarkly-tutorial/tutorial_general_201.png
[202]: ./media/launchdarkly-tutorial/tutorial_general_202.png
[203]: ./media/launchdarkly-tutorial/tutorial_general_203.png


---
title: 'Zelfstudie: Azure Active Directory-integratie met Rally Software | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Rally Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: 2bb9df9fe0cb20cdd50d7ba716ee5cba562f3e1b
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "39448254"
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a>Zelfstudie: Azure Active Directory-integratie met Rally Software

In deze zelfstudie leert u hoe u Rally om Software te integreren met Azure Active Directory (Azure AD).

Software Rally integreren met Azure AD biedt u de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot Rally Software heeft.
- U kunt uw gebruikers automatisch ophalen aangemeld bij Rally Software (Single Sign-On) inschakelen met hun Azure AD-accounts.
- U kunt uw accounts in één centrale locatie - Azure portal beheren.

Als u wilt graag meer informatie over de integratie van de SaaS-app met Azure AD, Zie [wat is toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met Rally Software, moet u de volgende items:

- Een Azure AD-abonnement
- Een Software Rally eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Als u wilt testen van de stappen in deze zelfstudie, raden we niet met behulp van een productie-omgeving.

Als u wilt testen van de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik uw productie-omgeving, niet als dat nodig is.
- Als u geen een proefversie Azure AD-omgeving hebt, kunt u [een proefversie van één maand krijgen](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u de Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Rally Software uit de galerie toe te voegen
1. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-rally-software-from-the-gallery"></a>Rally Software uit de galerie toe te voegen
Voor het configureren van de integratie van Rally Software in Azure AD, moet u Rally Software uit de galerie toevoegen aan uw lijst met beheerde SaaS-apps.

**Als u wilt toevoegen Rally Software uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het navigatievenster aan de linkerkant op **Azure Active Directory** pictogram. 

    ![De Azure Active Directory-knop][1]

1. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![De blade Enterprise-toepassingen][2]
    
1. Nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![De knop nieuwe toepassing][3]

1. Typ in het zoekvak **Rally Software**, selecteer **Rally Software** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Rally Software in de lijst met resultaten](./media/rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en Azure AD eenmalige aanmelding testen

In deze sectie maakt u configureert en test Azure AD eenmalige aanmelding met Rally Software op basis van een testgebruiker 'Julia steen' genoemd.

Voor eenmalige aanmelding om te werken, moet Azure AD om te weten wat de gebruiker equivalent in Rally Software is aan een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gerelateerde gebruiker in Software Rally tot stand worden gebracht.

Wijs in Rally Software, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Als u wilt configureren en Azure AD eenmalige aanmelding met Rally Software testen, moet u uitvoeren van de volgende bouwstenen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
1. **[Maak een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
1. **[Maak een testgebruiker Rally Software](#create-a-rally-software-test-user)**  : als u wilt een equivalent van Britta Simon in Rally Software die is gekoppeld aan de Azure AD-weergave van de gebruiker hebben.
1. **[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
1. **[Eenmalige aanmelding testen](#test-single-sign-on)**  : als u wilt controleren of de configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD eenmalige aanmelding configureren

In deze sectie maakt u schakelt Azure AD eenmalige aanmelding in de Azure-portal en configureren van eenmalige aanmelding in uw toepassing Rally Software.

**Voor het configureren van Azure AD eenmalige aanmelding met Rally Software, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **Rally Software** toepassingspagina integratie, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

1. Op de **eenmalige aanmelding** dialoogvenster, selecteer **modus** als **SAML gebaseerde aanmelding** eenmalige aanmelding inschakelen.
 
    ![In het dialoogvenster voor eenmalige aanmelding](./media/rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

1. Op de **Rally Software domein en URL's** sectie, voert u de volgende stappen uit:

    ![Software-domein en URL's één aanmelding informatie Rally](./media/rally-software-tutorial/tutorial_rallysoftware_url.png)

    a. In de **aanmeldings-URL** tekstvak, een URL met behulp van het volgende patroon: `https://<tenant-name>.rally.com`

    b. In de **id** tekstvak, een URL met behulp van het volgende patroon: `https://<tenant-name>.rally.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Werk deze waarden met de werkelijke aanmeldings-URL en -id. Neem contact op met [softwareclient Rally ondersteuningsteam](https://help.rallydev.com/) om deze waarden te verkrijgen. 
 


1. Op de **SAML-handtekeningcertificaat** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.

    ![De downloadkoppeling certificaat](./media/rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

1. Klik op **opslaan** knop.

    ![Configureren van eenmalige aanmelding opslaan](./media/rally-software-tutorial/tutorial_general_400.png)

1. Op de **softwareconfiguratie Rally** sectie, klikt u op **Rally Software configureren** openen **aanmelding configureren** venster. Kopiëren de **afmelding-URL en SAML entiteit-ID** uit de **Naslaggids sectie.**

    ![De softwareconfiguratie voor Rally](./media/rally-software-tutorial/tutorial_rallysoftware_configure.png) 

1. Meld u aan bij uw **Rally Software** tenant.

1. Klik in de werkbalk bovenaan op **Setup**, en selecteer vervolgens **abonnement**.
   
    ![Abonnement](./media/rally-software-tutorial/ic769531.png "abonnement")

1. Klik op de **actie** knop. Selecteer **bewerken abonnement** op de rechtsboven in de werkbalk.

1. Op de **abonnement** dialoogvenster pagina, voer de volgende stappen uit en klik vervolgens op **opslaan en sluiten**:
   
    ![Verificatie](./media/rally-software-tutorial/ic769542.png "verificatie")
   
    a. Selecteer **Rally of SSO-verificatie** in de vervolgkeuzelijst verificatie.

    b. In de **URL van de id-provider** tekstvak, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure portal. 

    c. In de **SSO Afmelden** tekstvak, plak de waarde van **afmelding URL**, die u hebt gekopieerd vanuit Azure portal.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl het instellen van de app!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de  **Configuratie** sectie aan de onderkant. U kunt meer lezen over de documentatie voor embedded-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Maak een testgebruiker Azure AD

Het doel van deze sectie is het maken van een testgebruiker in Azure portal Britta Simon genoemd.

   ![Maak een testgebruiker Azure AD][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de Azure portal, in het linkerdeelvenster klikt u op de **Azure Active Directory** knop.

    ![De Azure Active Directory-knop](./media/rally-software-tutorial/create_aaduser_01.png)

1. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/rally-software-tutorial/create_aaduser_02.png)

1. Om te openen de **gebruiker** in het dialoogvenster, klikt u op **toevoegen** aan de bovenkant van de **alle gebruikers** in het dialoogvenster.

    ![De knop toevoegen](./media/rally-software-tutorial/create_aaduser_03.png)

1. In de **gebruiker** dialoogvenster vak, voer de volgende stappen uit:

    ![Het dialoogvenster gebruiker](./media/rally-software-tutorial/create_aaduser_04.png)

    a. In de **naam** in het vak **BrittaSimon**.

    b. In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.

    c. Selecteer de **wachtwoord weergeven** selectievakje en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-rally-software-test-user"></a>Maak een testgebruiker Rally Software

Voor Azure AD-gebruikers kunnen zich aanmelden, moeten ze worden ingericht voor de Software Rally-toepassing met behulp van hun Azure Active Directory-gebruikersnamen.

**Als u wilt inrichten van gebruikers configureren, moet u de volgende stappen uitvoeren:**

1. Meld u aan bij uw tenant Rally Software.

1. Ga naar **Setup \> gebruikers**, en klik vervolgens op **+ nieuwe toevoegen**.
   
    ![Gebruikers](./media/rally-software-tutorial/ic781039.png "gebruikers")

1. Typ de naam in het tekstvak van de nieuwe gebruiker en klik vervolgens op **toevoegen met Details**.

1. In de **Create User** sectie, voert u de volgende stappen uit:
   
    ![Gebruiker maken](./media/rally-software-tutorial/ic781040.png "gebruiker maken")

    a. In de **gebruikersnaam** tekstvak typt u de naam van gebruiker, zoals **Brittsimon**.
   
    b. In **e-mailadres** tekstvak, voer het e-mailadres van gebruiker, zoals **brittasimon@contoso.com**.

    c. In **voornaam** tekst voert u de voornaam van de gebruiker, zoals **Julia**.

    d. In **achternaam** tekst voert u de achternaam van de gebruiker, zoals **Simon**.

    e. Klik op **opslaan en sluiten**.

   >[!NOTE]
   >U kunt een andere Software Rally gebruiker-account maken-hulpprogramma's of API's die worden geleverd door Rally Software gebruiken voor het inrichten van gebruikersaccounts van de Azure AD.

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie maakt inschakelen u Britta Simon gebruiken Azure eenmalige aanmelding door toegang te verlenen tot Software Rally.

![De de gebruikersrol toewijzen][200] 

**Als u wilt toewijzen Britta Simon Rally software, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de mapweergave en Ga naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

1. Selecteer in de lijst met toepassingen, **Rally Software**.

    ![De koppeling Rally Software in de lijst met toepassingen](./media/rally-software-tutorial/tutorial_rallysoftware_app.png)  

1. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![De koppeling 'Gebruikers en groepen'][202]

1. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Het deelvenster toewijzing toevoegen][203]

1. Op **gebruikers en groepen** dialoogvenster, selecteer **Britta Simon** in de lijst gebruikers.

1. Klik op **Selecteer** op knop **gebruikers en groepen** dialoogvenster.

1. Klik op **toewijzen** op knop **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Eenmalige aanmelding testen

Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie via het toegangsvenster.

Wanneer u op de tegel Rally Software in het toegangsvenster, u moet u automatisch aangemeld bij uw toepassing Rally Software.

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?)



<!--Image references-->

[1]: ./media/rally-software-tutorial/tutorial_general_01.png
[2]: ./media/rally-software-tutorial/tutorial_general_02.png
[3]: ./media/rally-software-tutorial/tutorial_general_03.png
[4]: ./media/rally-software-tutorial/tutorial_general_04.png

[100]: ./media/rally-software-tutorial/tutorial_general_100.png

[200]: ./media/rally-software-tutorial/tutorial_general_200.png
[201]: ./media/rally-software-tutorial/tutorial_general_201.png
[202]: ./media/rally-software-tutorial/tutorial_general_202.png
[203]: ./media/rally-software-tutorial/tutorial_general_203.png


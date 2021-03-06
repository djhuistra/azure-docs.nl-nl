---
title: 'Zelfstudie: Azure Active Directory-integratie met Cisco Spark | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Cisco Spark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: bebc8d674d7448ea0ce6a1f11b7ae80335df9cdc
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "39431695"
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a>Zelfstudie: Azure Active Directory-integratie met Cisco Spark

In deze zelfstudie leert u hoe u Cisco Spark integreren met Azure Active Directory (Azure AD).

Cisco Spark integreren met Azure AD biedt u de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot Cisco Spark heeft
- U kunt uw gebruikers automatisch ophalen aangemeld bij Cisco Spark (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts in één centrale locatie - Azure portal beheren

Als u wilt graag meer informatie over de integratie van de SaaS-app met Azure AD, Zie [wat is toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met Cisco Spark, moet u de volgende items:

- Een Azure AD-abonnement
- Een Cisco-Spark eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Als u wilt testen van de stappen in deze zelfstudie, raden we niet met behulp van een productie-omgeving.

Als u wilt testen van de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik uw productie-omgeving, niet als dat nodig is.
- Als u geen een proefversie Azure AD-omgeving hebt, krijgt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u de Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Cisco Spark uit de galerie toe te voegen
1. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-cisco-spark-from-the-gallery"></a>Cisco Spark uit de galerie toe te voegen
Voor het configureren van de integratie van Cisco Spark in Azure AD, moet u Cisco Spark uit de galerie toevoegen aan uw lijst met beheerde SaaS-apps.

**Als u wilt toevoegen Cisco Spark uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het navigatievenster aan de linkerkant op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

1. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![Toepassingen][2]
    
1. Nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![Toepassingen][3]

1. Typ in het zoekvak **Cisco Spark**.

    ![Het maken van een Azure AD-testgebruiker](./media/cisco-spark-tutorial/tutorial_ciscospark_search.png)

1. Selecteer in het deelvenster resultaten **Cisco Spark**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Het maken van een Azure AD-testgebruiker](./media/cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Cisco Spark op basis van een testgebruiker met de naam "Britta Simon."

Voor eenmalige aanmelding om te werken, moet Azure AD om te weten wat de gebruiker equivalent in Cisco Spark in Azure AD aan een gebruiker is. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gerelateerde gebruiker in Cisco Spark tot stand worden gebracht.

In Spark van Cisco, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Als u wilt configureren en testen van Azure AD eenmalige aanmelding met Cisco Spark, u nodig hebt voor de volgende bouwstenen:

1. **[Configureren van Azure AD eenmalige aanmelding](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
1. **[Het maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
1. **[Het maken van een testgebruiker Cisco Spark](#creating-a-cisco-spark-test-user)**  : als u wilt een equivalent van Britta Simon in Spark van Cisco die is gekoppeld aan de Azure AD-weergave van de gebruiker hebben.
1. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
1. **[Eenmalige aanmelding testen](#testing-single-sign-on)**  : als u wilt controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD eenmalige aanmelding configureren

In deze sectie maakt u schakelt Azure AD eenmalige aanmelding in de Azure-portal en configureren van eenmalige aanmelding in uw Cisco Spark-toepassing.

**Voor het configureren van Azure AD eenmalige aanmelding met Cisco Spark, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **Cisco Spark** toepassingspagina integratie, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

1. Op de **eenmalige aanmelding** dialoogvenster, selecteer **modus** als **SAML gebaseerde aanmelding** eenmalige aanmelding inschakelen.
 
    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

1. Op de **Cisco Spark domein en URL's** sectie, voert u de volgende stappen uit:

    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_ciscospark_url.png)

    a. In de **aanmeldings-URL** tekstvak, een URL als: `https://web.ciscospark.com/#/signin`

    b. In de **id** tekstvak, een URL met behulp van het volgende patroon: `https://idbroker.webex.com/<companyname>`

    > [!NOTE] 
    > Deze waarde is niet echt. Deze waarde bijwerken met de werkelijke-id. Neem contact op met [Cisco Spark Client ondersteuningsteam](https://support.ciscospark.com/) deze waarde op te halen. 
 
1. Op de **SAML-handtekeningcertificaat** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.

    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

1. Cisco-toepassing voor Spark wordt verwacht dat de SAML-asserties ondertekend naar specifieke kenmerken bevatten. Configureer de volgende kenmerken voor deze toepassing. U kunt de waarden van deze kenmerken vanuit beheren de **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie. De volgende Schermafbeelding toont een voorbeeld voor deze.
    
    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_ciscospark_07.png) 

1. In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de bovenstaande afbeelding en voer de volgende stappen uit:
    
    | Naam kenmerk  | Waarde kenmerk |
    | --------------- | -------------------- |    
    |   UID    | User.userPrincipalName |   

    a. Klik op **kenmerk toevoegen** openen de **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_attribute_05.png)
    
    b. In de **naam** tekstvak typt u de naam van het kenmerk wordt weergegeven voor die rij.
    
    c. Uit de **waarde** weergeven, typt u de waarde van het kenmerk wordt weergegeven voor die rij.
    
    d. Klik op **OK**.

1. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_general_400.png)

1. Aanmelden bij [Cisco samenwerking Cloudbeheer](https://admin.ciscospark.com/) met uw volledige beheerdersreferenties.

1. Selecteer **instellingen** en klikt u onder de **verificatie** sectie, klikt u op **wijzigen**.
   
    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
1. Selecteer **integreren van een 3rd party-id-provider. (Geavanceerd)**  en Ga naar het volgende scherm.

1. Op de **metagegevens van de id-provider importeren** pagina, een van beide slepen en neerzetten van het bestand met de Azure AD-metagegevens naar de pagina of de optie van de browser bestand gebruiken om te zoeken en de Azure AD-metagegevensbestand uploaden. Selecteer **certificaat dat is ondertekend door een certificeringsinstantie in de metagegevens (veiliger) vereisen** en klikt u op **volgende**. 
    
    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_cisco_spark_11.png)

1. Selecteer **SSO-testverbinding**, en wanneer er wordt een nieuw browsertabblad geopend, verifieert u met Azure AD met het aanmelden.

1. Ga terug naar de **Cisco samenwerking Cloudbeheer** browsertabblad. Als de test voltooid is, selecteert u **deze test is geslaagd. Inschakelen van Single Sign-On optie** en klikt u op **volgende**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl het instellen van de app!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de  **Configuratie** sectie aan de onderkant. U kunt meer lezen over de documentatie voor embedded-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Het maken van een Azure AD-testgebruiker
Het doel van deze sectie is het maken van een testgebruiker in Azure portal Britta Simon genoemd.

![Azure AD-gebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.

    ![Het maken van een Azure AD-testgebruiker](./media/cisco-spark-tutorial/create_aaduser_01.png) 

1. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klikt u op **alle gebruikers**.
    
    ![Het maken van een Azure AD-testgebruiker](./media/cisco-spark-tutorial/create_aaduser_02.png) 

1. Om te openen de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.
 
    ![Het maken van een Azure AD-testgebruiker](./media/cisco-spark-tutorial/create_aaduser_03.png) 

1. Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:
 
    ![Het maken van een Azure AD-testgebruiker](./media/cisco-spark-tutorial/create_aaduser_04.png) 

    a. In de **naam** tekstvak, type **BrittaSimon**.

    b. In de **gebruikersnaam** tekstvak, type de **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-cisco-spark-test-user"></a>Het maken van een testgebruiker Cisco Spark

In deze sectie maakt u een gebruiker met de naam van Britta Simon in Cisco Spark. In deze sectie maakt u een gebruiker met de naam van Britta Simon in Cisco Spark.

1. Ga naar de [Cisco samenwerking Cloudbeheer](https://admin.ciscospark.com/) met uw volledige beheerdersreferenties.

1. Klik op **gebruikers** en vervolgens **gebruikers beheren**.
   
    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

1. In de **beheren gebruiker** venster **handmatig toevoegen of wijzigen van gebruikers** en klikt u op **volgende**.

1. Selecteer **namen en e-mailadres**. Vul vervolgens het tekstvak als volgt in:
   
    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    a. In de **voornaam** tekstvak, type **Julia**. 
    
    b. In de **achternaam** tekstvak, type **Simon**.
    
    c. In de **e-mailadres** tekstvak, type **britta.simon@contoso.com**.

1. Klik op het plusteken om toe te voegen Britta Simon. Klik op **Volgende**.

1. In de **Services toevoegen voor gebruikers** venster, klikt u op **opslaan** en vervolgens **voltooien**.

### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen aan de gebruiker van de test Azure AD

In deze sectie maakt inschakelen u Britta Simon gebruiken Azure eenmalige aanmelding door toegang te verlenen tot Cisco Spark.

![Gebruiker toewijzen][200] 

**Als u wilt toewijzen Britta Simon met Cisco Spark, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de mapweergave en Ga naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

1. Selecteer in de lijst met toepassingen, **Cisco Spark**.

    ![Eenmalige aanmelding configureren](./media/cisco-spark-tutorial/tutorial_ciscospark_app.png) 

1. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

1. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

1. Op **gebruikers en groepen** dialoogvenster, selecteer **Britta Simon** in de lijst gebruikers.

1. Klik op **Selecteer** op knop **gebruikers en groepen** dialoogvenster.

1. Klik op **toewijzen** op knop **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Eenmalige aanmelding testen

Het doel van deze sectie is het testen van de configuratie van uw Azure AD-eenmalige aanmelding via het toegangsvenster.

Wanneer u op de Cisco Spark-tegel in het toegangsvenster, u moet u automatisch aangemeld bij uw Cisco Spark-toepassing.

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?)

<!--Image references-->

[1]: ./media/cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/cisco-spark-tutorial/tutorial_general_203.png


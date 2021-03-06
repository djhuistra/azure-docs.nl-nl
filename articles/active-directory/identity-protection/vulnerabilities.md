---
title: Beveiligingsproblemen die worden gedetecteerd door Azure Active Directory Identity Protection | Microsoft Docs
description: Overzicht van de beveiligingsproblemen die worden gedetecteerd door Azure Active Directory Identity Protection.
services: active-directory
keywords: Azure active directory identity protection cloud discovery, toepassingen, beveiliging, risico's, risiconiveau, beveiligingsproblemen, beveiligingsbeleid beheren
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.component: conditional-access
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2018
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 680e52fefd8256b3ac270e8d721f27645ced49eb
ms.sourcegitcommit: d0ea925701e72755d0b62a903d4334a3980f2149
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/09/2018
ms.locfileid: "40004250"
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Beveiligingsproblemen die worden gedetecteerd door Azure Active Directory Identity Protection
Beveiligingslekken in zwakke punten in uw omgeving die kunnen worden misbruikt door een aanvaller zijn. U wordt aangeraden dat u deze beveiligingslekken ter verbetering van de beveiligingsstatus van uw organisatie en te voorkomen dat aanvallers deze misbruikt.


![beveiligingsproblemen](./media/vulnerabilities/101.png "beveiligingsproblemen")



De volgende secties vindt u een overzicht van de beveiligingsproblemen die zijn gerapporteerd door Identity Protection.

## <a name="multi-factor-authentication-registration-not-configured"></a>Registratie met meervoudige verificatie is niet geconfigureerd
Dit beveiligingsprobleem helpt u bij de implementatie van Azure multi-factor Authentication in uw organisatie beheren. 

Verificatie met meerdere factoren van Azure biedt een tweede beveiligingslaag voor verificatie van de gebruiker. Deze om de toegang tot gegevens en toepassingen beveiligen terwijl aan de wensen van gebruikers voor een eenvoudige aanmeldprocedure. Het biedt een robuuste verificatie met een scala aan gebruiksvriendelijke verificatieopties, telefonische oproepen, SMS-berichten of mobiele app notification of verificatie van code en van derden OATH-tokens.

Het is raadzaam dat u Azure multi-factor Authentication voor gebruikersaanmeldingen nodig hebt. Meervoudige verificatie speelt een belangrijke rol in het beleid voor voorwaardelijke toegang op basis van risico beschikbaar via Identity Protection.

Zie voor meer informatie, [wat is Azure multi-factor Authentication?](../authentication/multi-factor-authentication.md)

## <a name="unmanaged-cloud-apps"></a>Onbeheerde cloud-apps
Hierdoor kunt u niet-beheerde cloud-apps in uw organisatie identificeren.

In moderne ondernemingen zijn vaak IT-afdelingen niet op de hoogte van alle cloudtoepassingen die gebruikers in hun organisatie gebruiken om hun werk te doen. Het is gemakkelijk om te zien waarom beheerders zou twijfels hebt over de niet-geautoriseerde toegang tot zakelijke gegevens, mogelijke gegevenslekken en andere beveiligingsrisico's. 

We raden je aan het implementeren van Cloud Discovery voor het detecteren van niet-beheerde cloud-toepassingen, en voor het beheren van deze toepassingen met Azure Active Directory.

Zie voor meer informatie, [Cloud Discovery](/cloud-app-security/set-up-cloud-discovery).

## <a name="security-alerts-from-privileged-identity-management"></a>Beveiligingswaarschuwingen van Privileged Identity Management
Dit beveiligingsprobleem helpt u bij het opsporen en oplossen van waarschuwingen over bevoorrechte identiteiten in uw organisatie.  

Als u wilt dat gebruikers kunnen bevoorrechte bewerkingen uitvoeren, organisaties moeten gebruikers tijdelijk of permanent bevoorrechte toegang verlenen in Azure AD, Azure of Office 365-resources en andere SaaS-apps. Elk van deze gebruikers met bevoegdheden verhoogt de kwetsbaarheid van uw organisatie. Dit beveiligingsprobleem kunt u gebruikers identificeren met onnodige bevoegde toegang en passende actie ondernemen om te verlagen of elimineren van het risico dat ze met zich meebrengen. 

We raden aan dat uw organisatie Azure AD Privileged Identity Management gebruikt te beheren, controleren en monitor identiteiten en hun toegang tot bronnen in Azure AD, evenals andere Microsoft online services zoals Office 365 en Microsoft Intune bevoegde.

Zie voor meer informatie, [Azure AD Privileged Identity Management](../privileged-identity-management/pim-configure.md). 

## <a name="see-also"></a>Zie ook

[Azure Active Directory Identity Protection](../active-directory-identityprotection.md)


---
title: bestand opnemen
description: bestand opnemen
services: batch
author: dlepow
ms.service: batch
ms.topic: include
ms.date: 05/04/2018
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: 62bb91a2e51c39caf31719f72d68a6edab9205bc
ms.sourcegitcommit: 0a84b090d4c2fb57af3876c26a1f97aac12015c5
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2018
ms.locfileid: "38941164"
---
> [!NOTE]
> Wanneer u een Batch-account maakt, kunt u kiezen tussen twee modi voor *groepstoewijzing*: **gebruikersabonnement** en **Batch-service**. In de meeste gevallen zult u de standaardmodus Batch-service gebruiken, waarbij pools achter de schermen worden toegewezen in door Azure beheerde abonnementen. In de alternatieve modus Gebruikersabonnement worden Batch-VM's en andere resources rechtstreeks in uw abonnement gemaakt wanneer er een groep wordt gemaakt. De modus Gebruikersabonnement is vereist als u Batch-wilt maken met behulp van pools [Azure Reserved VM Instances](https://azure.microsoft.com/pricing/reserved-vm-instances/). Voor het maken van een Batch-account in de gebruikersabonnementmodus moet u het account ook bij Azure Batch registreren en aan een Azure Key Vault koppelen.
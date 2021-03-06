---
title: Ondersteunde gastbesturingssystemen voor Azure Stack | Microsoft Docs
description: Deze gastbesturingssystemen kan worden gebruikt in Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2018
ms.author: sethm
ms.reviewer: ''
ms.openlocfilehash: be4d9b3ea7e5715d7c3a4df11b7e8bab4d1d4ca5
ms.sourcegitcommit: b7e5bbbabc21df9fe93b4c18cc825920a0ab6fab
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/27/2018
ms.locfileid: "47405594"
---
# <a name="guest-operating-systems-supported-on-azure-stack"></a>Gastbesturingssystemen die worden ondersteund in Azure Stack

*Is van toepassing op: geïntegreerde Azure Stack-systemen en Azure Stack Development Kit*

## <a name="windows"></a>Windows

Azure Stack biedt ondersteuning voor de Windows-gastbesturingssystemen die worden vermeld in de volgende tabel:

| Besturingssysteem | Beschrijving | Beschikbaar in de Marketplace |
| --- | --- | --- | --- | --- | --- |
| Windows Server, versie 1709 | 64-bits | Core met Containers |
| Windows Server 2016 | 64-bits |  Datacenter, Datacenter-Core, Datacenter met Containers |
| Windows Server 2012 R2 | 64-bits |  Datacenter |
| Windows Server 2012 | 64-bits |  Datacenter |
| Windows Server 2008 R2 SP1 | 64-bits |  Datacenter |
| Windows Server 2008 SP2 | 64-bits |  Uw eigen installatiekopie gebruiken |
| Windows 10 *(Zie Opmerking 1)* | 64-bits, Pro en Enterprise | Uw eigen installatiekopie gebruiken |

> [!NOTE]
> Windows 10-client om besturingssystemen te implementeren in Azure Stack, moet u hebben [Windows per gebruiker-licentieverlening](https://www.microsoft.com/en-us/Licensing/product-licensing/windows10.aspx) of aanschaffen via een gekwalificeerde Multitenant Hoster ([QMTH](https://www.microsoft.com/en-us/CloudandHosting/licensing_sca.aspx)).

Marketplace-installatiekopieën zijn beschikbaar voor betalen als u-gebruik of BYOL (EA/SPLA)-licentieverlening. Gebruik van beide op een enkele instantie van Azure Stack wordt niet ondersteund. Tijdens de implementatie van injects Azure Stack een geschikte versie van de gastagent in de afbeelding.

Datacenter-edities zijn beschikbaar in de marketplace voor het downloaden van; klanten kunnen hun eigen server-installatiekopieën met inbegrip van andere edities meebrengen. Windows-clientinstallatiekopieën zijn niet beschikbaar in de Marketplace.

## <a name="linux"></a>Linux

Linux-distributies die worden vermeld als beschikbaar in de Marketplace bevatten de benodigde Windows Azure Linux Agent (WALA). Als u uw eigen installatiekopie met Azure Stack maken, volgt u de richtlijnen in [toevoegen Linux-installatiekopieën naar Azure Stack](azure-stack-linux.md).

> [!NOTE]
> Aangepaste installatiekopieën moeten worden gebouwd met de meest recente openbare WALA-versie. Versies ouder dan 2.2.18 werkt mogelijk niet juist in Azure Stack.
>
> [cloud-init](https://cloud-init.io/) wordt niet ondersteund in Azure Stack op dit moment.

| Distributie | Beschrijving | Uitgever | Marketplace |
| --- | --- | --- | --- | --- | --- |
| Op basis van centOS 6,9 | 64-bits | Rogue Wave | Ja |
| Op basis van centOS 7.4 | 64-bits | Rogue Wave | Ja |
| ClearLinux | 64-bits | ClearLinux.org | Ja |
| Container-Linux |  64-bits | CoreOS | Stabiel |
| Debian 8 "Jessie" | 64-bits | credativ |  Ja |
| Debian 9 'Stretch" | 64-bits | credativ | Ja |
| Red Hat Enterprise Linux 7.x | 64-bits | Red Hat |Uw eigen installatiekopie gebruiken |
| SLES 11SP4 | 64-bits | SUSE | Ja |
| SLES 12SP3 | 64-bits | SUSE | Ja |
| Ubuntu 14.04-LTS | 64-bits | Canonical | Ja |
| Ubuntu 16.04-LTS | 64-bits | Canonical | Ja |
| Ubuntu 18.04-LTS | 64-bits | Canonical | Ja |

Raadpleeg voor informatie over Red Hat Enterprise Linux, [Red Hat en Azure Stack: veelgestelde vragen over](https://access.redhat.com/articles/3413531).

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over Azure Stack Marketplace, de volgende artikelen:

[Marketplace-items downloaden](azure-stack-download-azure-marketplace-item.md)  
[Een Marketplace-item maken en publiceren](azure-stack-create-and-publish-marketplace-item.md)
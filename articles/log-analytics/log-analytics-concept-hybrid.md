---
title: Gegevens verzamelen in een hybride omgeving met Azure Log Analytics-agent | Microsoft Docs
description: Dit onderwerp helpt u begrijpen hoe u gegevens verzamelen en controleren van computers die worden gehost in uw on-premises of andere cloudomgeving met Log Analytics.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 10/15/2018
ms.author: magoedte
ms.component: ''
ms.openlocfilehash: 03133c6d6518444f8e6fb15cfa425969dbafdedc
ms.sourcegitcommit: 07a09da0a6cda6bec823259561c601335041e2b9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/18/2018
ms.locfileid: "49406871"
---
# <a name="collect-data-in-a-hybrid-environment-with-log-analytics-agent"></a>Gegevens verzamelen in een hybride omgeving met Log Analytics-agent

Azure Log Analytics kunt verzamelen en reageren op gegevens van computers met het besturingssysteem Windows of Linux wordt uitgevoerd in:

* [Virtuele machines van Azure](log-analytics-quick-collect-azurevm.md) met behulp van de VM-extensie van Log Analytics 
* Uw datacenter als fysieke servers of virtuele machines
* Virtuele machines in een cloud-gebaseerde service, zoals Amazon Web Services (AWS)

Computers die worden gehost in uw omgeving kunnen rechtstreeks worden verbonden met Log Analytics, of als u al deze computers met System Center Operations Manager 2012 R2 of hoger controleert, kunt u uw beheergroep Operations beheren integreren met Log Analytics en door te gaan met het onderhouden van uw IT-service operations-processen.  

## <a name="overview"></a>Overzicht

![log-Analytics-agent-Direct-Connect-diagram](media/log-analytics-concept-hybrid/log-analytics-on-prem-comms.png)

Voordat u analyseren en uitvoeren van de verzamelde gegevens, moet u eerst installeren en verbinden-agents voor alle computers die u wilt gegevens verzenden naar de Log Analytics-service. U kunt agents installeren op uw on-premises computers met Setup, vanaf de opdrachtregel, of met Desired State Configuration (DSC) in Azure Automation. 

De agent voor Linux en Windows uitgaande met de Log Analytics-service communiceert via TCP-poort 443, en als de computer verbinding maakt met een firewall of proxy-server om te communiceren via Internet, raadpleegt u onderstaande voorwaarden om te begrijpen van de netwerkconfiguratie Vereist.  Als uw IT-beveiligingsbeleid niet computers op het netwerk verbinding maken met Internet toestaat, kunt u instellen een [Log Analytics gateway](log-analytics-oms-gateway.md) en configureer vervolgens de agent verbinding maken via de gateway naar Log Analytics. De agent vervolgens configuratie-informatie ontvangen en verzenden van gegevens die zijn verzameld, afhankelijk van welke regels voor het verzamelen van gegevens en de oplossingen die u hebt ingeschakeld. 

Als u de computer met System Center Operations Manager 2012 R2 of hoger worden bewaakt, kan zijn bij de Log Analytics-service voor het verzamelen van gegevens en door te sturen naar de service en nog steeds worden bewaakt door multihomed [Operations Manager](log-analytics-om-agents.md). Linux-computers bewaakt door een Operations Manager-beheergroep is geïntegreerd met Log Analytics wordt geen configuratie voor gegevensbronnen en vooruit verzamelde gegevens via de beheergroep. De Windows-agent kan rapporteren dat maximaal vier werkruimten, terwijl de Linux-agent biedt alleen ondersteuning voor rapportage aan één werkruimte.  

De agent voor Linux en Windows-niet alleen voor het verbinden met Log Analytics, het ondersteunt ook Azure Automation voor de functie Hybrid Runbook worker-host en beheeroplossingen, zoals wijzigingen bijhouden en updatebeheer.  Zie voor meer informatie over de Hybrid Runbook Worker-rol, [Azure Automation Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md).  

## <a name="supported-windows-operating-systems"></a>Ondersteunde Windows-besturingssystemen
De volgende versies van het Windows-besturingssysteem worden officieel ondersteund voor de Windows-agent:

* Windows Server 2008 Service Pack 1 (SP1) of hoger
* Windows 7 SP1 en hoger.

## <a name="supported-linux-operating-systems"></a>Ondersteunde Linux-besturingssystemen
In deze sectie bevat informatie over de ondersteunde Linux-distributies.    

Beginnen met versies die na augustus 2018 wordt uitgebracht, maken we de volgende wijzigingen aan ons ondersteuningsmodel:  

* Alleen de server-versies worden ondersteund, een niet-client.  
* Nieuwe versies van [goedgekeurd voor Azure Linux-distributies](../virtual-machines/linux/endorsed-distros.md) altijd worden ondersteund.  
* Alle secundaire versies worden ondersteund voor elke primaire versie weergegeven.
* De versies die zijn geslaagd voor de datum van de fabrikant einde van ondersteuning worden niet ondersteund.  
* Nieuwe versies van AMI worden niet ondersteund.  
* Alleen versies met SSL 1.x standaard worden ondersteund.

Als u een distributie of een versie die wordt momenteel niet ondersteund en wordt niet afgestemd op onze ondersteuningsmodel gebruikt, raden wij dat u deze opslagplaats splitst, waarmee wordt bevestigd dat Microsoft-ondersteuning geen hulp bij gesplitste agent versies geeft.

* Amazon Linux 2017.09 (x 64)
* CentOS Linux 6 (x86/x64) en 7 (x 64)  
* Oracle Linux 6 en 7 (x86/x64) 
* Red Hat Enterprise Linux Server 6 (x86/x64) en 7 (x 64)
* Debian GNU/Linux 8 en 9 (x86/x64)
* Ubuntu 14.04 LTS (x86/x64), 16.04 LTS (x86/x64) en 18.04 LTS (x64)
* SUSE Linux Enterprise Server 12 (x 64)

>[!NOTE]
>OpenSSL 1.1.0 wordt alleen ondersteund op x86_x64 platforms (64-bits) en OpenSSL ouder dan 1.x wordt niet ondersteund op elk platform.
>

## <a name="tls-12-protocol"></a>TLS 1.2-protocol
Als u wilt controleren of de beveiliging van gegevens die onderweg zijn naar Log Analytics, we raden u aan de agent configureren voor het gebruik van ten minste Transport Layer Security (TLS) 1.2. Oudere versies van TLS/Secure Sockets Layer (SSL) kwetsbaar zijn gevonden en hoewel ze op dit moment nog steeds werken om toe te staan achterwaartse compatibiliteit, zijn ze onderling **niet aanbevolen**.  Raadpleeg voor meer informatie, [verzenden van gegevens veilig gebruik TLS 1.2](log-analytics-data-security.md#sending-data-securely-using-tls-12). 

## <a name="network-firewall-requirements"></a>Netwerkvereisten voor de firewall
Gegevens van de onderstaande lijst de proxy- en firewallinstellingen configuratie-informatie voor de agent voor Linux en Windows om te communiceren met Log Analytics vereist.  

|Agentresource|Poorten |Richting |HTTPS-controle overslaan|
|------|---------|--------|--------|   
|*.ods.opinsights.azure.com |Poort 443 |Binnenkomend en uitgaand|Ja |  
|*.oms.opinsights.azure.com |Poort 443 |Binnenkomend en uitgaand|Ja |  
|*.blob.core.windows.net |Poort 443 |Binnenkomend en uitgaand|Ja |  
|*.azure-automation.net |Poort 443 |Binnenkomend en uitgaand|Ja |  


Als u van plan bent de Hybrid Runbook Worker voor Azure Automation gebruiken om te verbinden en registreren bij de service Automation runbooks gebruiken in uw omgeving, moet er toegang tot het poortnummer en de URL's die worden beschreven in [het netwerk configureren voor de Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md#network-planning). 

De Windows- en Linux-agent ondersteunt communiceren via een proxyserver of de Log Analytics-gateway bij de Log Analytics-service met behulp van het HTTPS-protocol.  Zowel eenvoudige als anonieme verificatie (gebruikersnaam en wachtwoord) worden ondersteund.  Voor de Windows-agent rechtstreeks verbonden met de service, de configuratie van de proxy is opgegeven tijdens de installatie of [na de implementatie](log-analytics-agent-manage.md#update-proxy-settings) via het Configuratiescherm of met PowerShell.  

Voor de Linux-agent de proxyserver wordt opgegeven tijdens de installatie of [na de installatie](log-analytics-agent-manage.md#update-proxy-settings) door het wijzigen van het configuratiebestand proxy.conf.  Waarde voor de Linux-agent proxyconfiguratie heeft de volgende syntaxis:

`[protocol://][user:password@]proxyhost[:port]`

> [!NOTE]
> Als uw proxy-server niet vereist is om te verifiëren, moet de Linux-agent nog steeds bieden een pseudo-gebruiker en wachtwoord. Dit kan een gebruikersnaam of het wachtwoord zijn.

|Eigenschap| Beschrijving |
|--------|-------------|
|Protocol | https |
|Gebruiker | Optioneel de gebruikersnaam voor proxy-verificatie |
|wachtwoord | Optionele wachtwoord voor proxy-verificatie |
|proxyhost | Adres of FQDN-naam van de proxy-server/Log Analytics-gateway |
|poort | Optionele poortnummer voor de proxy-server/Log Analytics-gateway |

Bijvoorbeeld: `https://user01:password@proxy01.contoso.com:30443`

> [!NOTE]
> Als u speciale tekens zoals "\@" in uw wachtwoord, ontvangt u een proxy-verbindingsfout omdat de waarde is niet juist geparseerd.  U kunt dit probleem omzeilen, codeert u het wachtwoord in de URL met behulp van een hulpprogramma zoals [URLDecode](https://www.urldecoder.org/).  

## <a name="install-and-configure-agent"></a>Agent installeren en configureren 
Verbinden van uw on-premises computers rechtstreeks met Log Analytics kan worden bewerkstelligd met verschillende methoden, afhankelijk van uw vereisten. De volgende tabel ziet u elke methode om te bepalen welke het beste werkt in uw organisatie.

|Bron | Methode | Beschrijving|
|-------|-------------|-------------|
| Windows-computer|- [Handmatige installatie](log-analytics-agent-windows.md)<br>- [Azure Automation DSC](log-analytics-agent-windows.md#install-the-agent-using-dsc-in-azure-automation)<br>- [Resource Manager-sjabloon met Azure Stack](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/MicrosoftMonitoringAgent-ext-win) |De Microsoft Monitoring agent installeren vanaf de opdrachtregel of met behulp van een geautomatiseerde methode, zoals Azure Automation DSC, [System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/deploy-use/deploy-applications), of met een Azure Resource Manager-sjabloon als u Microsoft hebt geïmplementeerd Azure Stack in uw datacenter.| 
|Linux-computer| [Handmatige installatie](log-analytics-quick-collect-linux-computer.md)|Installeer de agent voor Linux aanroepen van een wrapper-scripts die worden gehost op GitHub. | 
| System Center Operations Manager|[Operations Manager integreert met Log Analytics](log-analytics-om-agents.md) | Configureren van de integratie tussen Operations Manager en de Log Analytics voor het doorsturen van gegevens die worden verzameld van Linux en Windows-computers die rapporteren aan een beheergroep.|  

## <a name="next-steps"></a>Volgende stappen

* Beoordeling [gegevensbronnen](log-analytics-data-sources.md) om te begrijpen van de gegevensbronnen die beschikbaar zijn voor het verzamelen van gegevens van uw Windows- of Linux-systeem. 

* Meer informatie over [zoekopdrachten](log-analytics-log-searches.md) om de gegevens die worden verzameld van gegevensbronnen en oplossingen te analyseren. 

* Meer informatie over [oplossingen](log-analytics-add-solutions.md) die functionaliteit toevoegen aan Log Analytics en ook gegevens verzamelen in Log Analytics-werkruimte.

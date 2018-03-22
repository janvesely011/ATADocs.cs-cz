---
title: "Advanced Threat Analytics prostředky a připravenost roadamp | Microsoft Docs"
description: "Poskytuje seznam ATA prostředků, videa, Začínáme, nasazení a odkazy plán připravenosti."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 42a1a34f-ed6b-4538-befb-452168a30e8c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a56a24a2012239ed05f0a2f214dba345a817df39
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/22/2018
---
*Platí pro: Advanced Threat Analytics verze 1.9*

# <a name="ata-readiness-roadmap"></a>Plán připravenosti ATA 
Tento dokument obsahuje přehled připravenosti, která vám pomůže začít pracovat s Advanced Threat Analytics.

## <a name="understanding-ata"></a>Principy ATA

Řešení ATA (Advanced Threat Analytics) je místní platforma, která chrání podnik před různými typy pokročilých cílových útoků z kyberprostoru a před vnitřními hrozbami. Další informace o ATA použijte v následujících zdrojích informací:

- [Přehled ATA](https://aka.ms/ATAOverview)

- [Video Úvod ATA - krátký](https://aka.ms/ATAShort)

- [ATA úvodní video – úplná](https://aka.ms/ATAVideo) 


## <a name="deployment-decisions"></a>Rozhodnutí o nasazení

ATA se skládá z komponenty ATA Center, které si můžete nainstalovat na server, a komponenty ATA Gateway, které můžete nainstalovat na samostatné počítače nebo pomocí Lightweight Gateway přímo na řadiče domény. Než získáte spuštěná, je důležité zajistit následující rozhodnutí týkající se nasazení:

|KONFIGURACE|ROZHODNUTÍ|
|----|----|
|Typ hardwaru|Fyzicky virtuální, virtuální počítač Azure|
|Pracovní skupině nebo doméně|Pracovní skupiny, domény|
|Nastavení velikosti brány|Úplné brány, Lightweight Gateway|
|Certifikáty|Infrastruktury veřejných KLÍČŮ, podepsaného svým držitelem|

Pokud používáte fyzické servery, měli byste naplánovat kapacitu. Získat pomoc od nástroj pro změnu velikosti k přidělení místa pro ATA:

[Nástroje pro změnu velikosti ATA](http://aka.ms/atasizing) – nástroj pro změnu velikosti automatizuje kolekce objem provozu, ATA potřebuje. Pro ATA Center a ATA Lightweight Gateway automaticky poskytuje možnosti podpory a doporučení prostředků.

[Plánování kapacity ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/ata-capacity-planning)

## <a name="deploy-ata"></a>Nasazení ATA

Tyto prostředky vám pomůže stažení a instalace ATA Center, připojit ke službě Active Directory, stáhněte si balíček ATA Gateway, nastavit shromažďování událostí a volitelně integrovat vaši síť VPN a nastavení účtů honeytokenu a vyloučení.

[Stáhněte si ATA](http://aka.ms/ataeval) – před nasazením ATA, pokud jste neprovedli rozhodnutí o zakoupení ATA, můžete si stáhnout zkušební verze. 

[ATA POC playbook](http://aka.ms/atapoc) – Příručka pro všechny kroky potřebné k úspěšné nasazení ATA testování Koncepce provést.

[Nasazení ATA video](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes) -toto video poskytuje přehled o nasazení ATA kroky za méně než 10 minut.

## <a name="ata-settings"></a>Nastavení ATA

Základní potřebná nastavení ATA jsou nakonfigurovány jako součást Průvodce instalací. Existuje však několik dalších nastavení, která můžete nakonfigurovat a doladit tak ATA které provedou detekce přesnější pro vaše prostředí, jako je například SIEM integrace a nastavení auditu.

[Nastavení auditování](https://aka.ms/ataauditingblog) – auditovat vaše stav řadiče domény, před a po nasazení ATA.

[Obecné dokumentace ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/)

## <a name="work-with-ata"></a>Práce s ATA

Po ATA je spuštěná, bude moci zobrazit podezřelé aktivity, které jsou zjištěna v časové ose útoků. Toto je výchozí cílová stránka, která se vám zobrazí po přihlášení ke konzole ATA. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila. Každá podezřelá aktivita šetření tak, že procházení k podrobnostem entit (počítače, zařízení, uživatelé) pro otevření jejich profil stránek, které poskytují další informace ohledně. Tyto prostředky vám usnadní práci s podezřelé aktivity ATA:

[Playbook podezřelé aktivity ATA](http://aka.ms/ataplaybook) – Tento článek vás provede procesem techniky útoku krádeží přihlašovacích údajů pomocí nástrojů pro snadno dostupné zdroje informací na Internetu. U každého bodu útoku uvidíte, jak ATA pomáhá získat přehled o tyto hrozby.

[Průvodce podezřelé aktivity ATA](http://aka.ms/atasaguide)



## <a name="security-best-practices"></a>Osvědčené postupy zabezpečení

[Osvědčené postupy ATA](https://aka.ms/atasecbestpractices) -osvědčené postupy pro zabezpečení ATA.

[Nejčastější dotazy k ATA](http://aka.ms/atafaq) – Tento článek obsahuje seznam nejčastější dotazy týkající se ATA a poskytuje podrobné informace a odpovědi.

## <a name="additional-resources"></a>Další materiály a zdroje informací

[Stránka Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Zdroje informací a materiály z komunity

[ATA blog](https://aka.ms/ATABlog)
[ATA komunity](https://aka.ms/ATACommunity)
[svůj názor na ATA](https://aka.ms/ATAUserVoice)

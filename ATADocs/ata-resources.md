---
title: Advanced Threat Analytics prostředky a připravenosti roadamp | Dokumentace Microsoftu
description: Obsahuje seznam ATA prostředky, videa, jak začít, nasazení a odkazy plán připravenosti.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/15/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 42a1a34f-ed6b-4538-befb-452168a30e8c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 48756cbde8b288116975c05567beeac76e83a717
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133765"
---
*Platí pro: Advanced Threat Analytics verze 1.9*

# <a name="ata-readiness-roadmap"></a>Plán připravenosti ATA 
Tento dokument vám poskytne plány připravenosti, která vám pomůže začít pracovat s Advanced Threat Analytics.

## <a name="understanding-ata"></a>Principy ATA

Řešení ATA (Advanced Threat Analytics) je místní platforma, která chrání podnik před různými typy pokročilých cílových útoků z kyberprostoru a před vnitřními hrozbami. Další informace o ATA použijte následující prostředky:

- [Přehled ATA](what-is-ata.md)

- [ATA úvodní video - krátké](https://aka.ms/ATAShort)

- [ATA úvodní video – úplná](https://aka.ms/ATAVideo) 


## <a name="deployment-decisions"></a>Rozhodnutí o nasazení

ATA se skládá z komponenty ATA Center, které si můžete nainstalovat na server, a komponenty ATA Gateway, které si můžete nainstalovat na samostatné počítače nebo Lightweight Gateway přímo na řadiče domény. Než můžete začít pracovat, je důležité, aby následující rozhodnutí týkající se nasazení:

|KONFIGURACE|ROZHODNUTÍ|
|----|----|
|Typ hardwaru|Fyzickými, virtuálními virtuálního počítače Azure|
|Pracovní skupině nebo doméně|Pracovní skupině, doméně|
|Velikost brány|Úplné brány Lightweight Gateway|
|Certifikáty|Infrastruktura veřejných KLÍČŮ, podepsaný svým držitelem|

Pokud používáte fyzické servery, měli byste naplánovat kapacitu. Nápovědu získáte z nástroje pro změnu velikosti k přidělení místa pro ATA:

[Nástroje pro změnu velikosti ATA](ata-capacity-planning.md) – nástroj pro změnu velikosti automatizuje kolekce objem přenosů ATA potřebuje. Pro ATA Center a ATA Lightweight Gateway automaticky poskytuje možnosti podpory a doporučení prostředků.

[Plánování kapacity ATA](ata-capacity-planning.md)

## <a name="deploy-ata"></a>Nasazení ATA

Tyto prostředky vám pomůže stáhnout a nainstalovat komponenty ATA Center, připojit ke službě Active Directory, stažení instalačního balíčku ATA Gateway, nastavit shromažďování událostí a volitelně integrovat vaši síť VPN a nastavit vyloučení a účty honeytoken.

[Stáhněte si ATA](http://aka.ms/ataeval) – před nasazením ATA, pokud nebyla provedena rozhodnutí o zakoupení ATA, můžete si stáhnout zkušební verze. 

[Scénáře ATA POC](http://aka.ms/atapoc) – Příručka pro všechny kroky potřebné k úspěšné nasazení ATA POC.

[Nasazení ATA videa](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes) -toto video poskytuje přehled o nasazení ATA kroky za méně než 10 minut.

## <a name="ata-settings"></a>Nastavení ATA

Základní nastavení potřebné v ATA jsou nakonfigurované jako součást Průvodce instalací. Existují však počet dalších nastavení, které můžete nakonfigurovat a doladit ATA, které přesnějšího detekce pro vaše prostředí, jako je například integrace řešení SIEM a auditovat jejich nastavení.

[Nastavení auditu](https://aka.ms/ataauditingblog) – auditovat vaše stav řadiče domény před a po nasazení ATA.

[Obecná dokumentace ATA](https://docs.microsoft.com/advanced-threat-analytics/)

## <a name="work-with-ata"></a>Práce s ATA

Po ATA je spuštěná, budete moci zobrazíte podezřelých aktivit, které jsou zjištěny na časové ose útoku. Toto je výchozí cílová stránka, která se vám zobrazí po přihlášení ke konzole ATA. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila. Zkontrolovat každou podezřelou aktivitu, že procházení k podrobnostem entitách (počítače, zařízení a uživatele) otevřete jejich profilové stránky, které poskytují další informace. Tyto prostředky vám usnadní práci s podezřelými aktivitami ATA:

[Playbook podezřelých aktivit ATA](http://aka.ms/ataplaybook) – Tento článek vás provede technik útoku krádeží přihlašovacích údajů pomocí snadno dostupné výzkumné nástroje na Internetu. U každého bodu útoku uvidíte, jak ATA vám pomůže získat náhled do těchto hrozeb.

[Průvodce prošetřováním podezřelých aktivit ATA](suspicious-activity-guide.md)



## <a name="security-best-practices"></a>Osvědčené postupy zabezpečení

[Osvědčené postupy ATA](https://aka.ms/atasecbestpractices) – osvědčené postupy pro zabezpečení ATA.

[Nejčastější dotazy k ATA](ata-technical-faq.md) – Tento článek obsahuje seznam nejčastějších dotazů týkající se ATA a poskytuje podrobné informace a odpovědi.

## <a name="additional-resources"></a>Další materiály a zdroje informací

[Stránka Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Zdroje informací a materiály z komunity

[ATA blog](https://aka.ms/ATABlog)
[ATA komunity](https://aka.ms/ATACommunity)
[poskytovat zpětnou vazbu k ATA](https://aka.ms/ATAUserVoice)

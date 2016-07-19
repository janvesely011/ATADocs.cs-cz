---
title: "Konfigurace zrcadlení portů | Microsoft Advanced Threat Analytics"
description: "Popisuje možnosti zrcadlení portů a způsob jejich konfigurace pro ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 121f54e6d8da8220f1827188039e9a89c038f7ac
ms.openlocfilehash: a4befce4003951b18a5e1a9d8bc1addf9e7ea255


---

# Konfigurace zrcadlení portů
> [!NOTE] 
> Tento článek se týká jenom nasazení komponent ATA Gateway, nikoli komponent ATA Lightweight Gateway. Pokud chcete určit, jestli potřebujete ATA Gateway, přečtěte si téma [Volba vhodných bran pro vaše nasazení](/advanced-threat-analytics/plan-design/ata-capacity-planning#choosing-the-right-gateway-type-for-your-deployment).
 
Hlavní zdroj dat používaný ATA je hloubková kontrola paketů síťového provozu do a z řadičů domény. Aby bylo možné pomocí ATA sledovat síťový provoz, musíte buď konfigurovat zrcadlení portů, nebo použít síťové odposlouchávání.

Pro zrcadlení portů nakonfigurujte **zrcadlení portů** u každého řadiče domény, který se má monitorovat jako **zdroj** síťového provozu. Při konfiguraci zrcadlení portů budete obvykle spolupracovat s týmem pro sítě nebo virtualizace.
Další informace najdete v dokumentaci dodavatele.

Řadiče domény a komponenty ATA Gateway můžou být buď fyzické, nebo virtuální. Níže jsou uvedeny běžné metody pro zrcadlení portů a některé aspekty. Další informace najdete v dokumentaci k produktu pro váš přepínač nebo virtualizační server. Výrobce přepínače může používat odlišnou terminologii.

**Switched Port Analyzer (SPAN)** – Kopíruje síťový provoz z jednoho nebo několika portů přepínače na jiný port v rámci stejného přepínače. ATA Gateway a řadič domény musí být připojené ke stejnému fyzickému přepínači.

**Remote Switch Port Analyzer (RSPAN)** – Umožňuje sledovat síťový provoz ze zdrojových portů, které jsou rozložené přes víc fyzických přepínačů. RSPAN kopíruje zdrojový provoz do speciální sítě VLAN nakonfigurované pro RSPAN. Tato síť VLAN musí být propojená mezi zahrnutými přepínači kmenovým vedením. RSPAN pracuje na vrstvě 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** – Jedná se o proprietární technologii Cisco pracující na vrstvě 3. ERSPAN umožňuje monitorování provozu přes různé přepínače bez nutnosti kmenových vedení sítě VLAN. ERSPAN používá ke kopírování monitorovaného síťového provozu protokol GRE (Generic Routing Encapsulation). ATA momentálně nemůže přímo přijímat provoz ERSPAN. Aby byla možná spolupráce ATA s provozem ERSPAN, je potřeba jako cíl ERSPAN konfigurovat přepínač nebo směrovač, který bude dekódovat zapouzdřený provoz. Tento přepínač nebo směrovač je pak potřeba konfigurovat tak, aby ho předával ATA Gateway metodou SPAN nebo RSPAN.

> [!NOTE]
> Pokud řadič domény se zrcadlením portů je připojený prostřednictvím linky WAN, zkontrolujte, že linka WAN dokáže zpracovat další zátěž provozu ERSPAN.

## Podporované možnosti zrcadlení portů

|ATA Gateway|Řadič domény|Pravidla|
|---------------|---------------------|------------------|
|Virtuální|Virtuální na stejném hostiteli|Virtuální přepínač musí podporovat zrcadlení portů.<br /><br />Přesunutí jednoho z virtuálních počítačů do jiného hostitele může samo o sobě způsobit nefunkčnost zrcadlení portů.|
|Virtuální|Virtuální na různých hostitelích|Zkontrolujte, že váš virtuální přepínač tento scénář podporuje.|
|Virtuální|Fyzické|Vyžaduje vyhrazený síťový adaptér, v opačném případě ATA uvidí veškerý příchozí i odchozí provoz hostitele, dokonce i provoz, který odesílá do ATA Center.|
|Fyzické|Virtuální|Ujistěte se, že virtuální přepínač podporuje tento scénář a konfiguraci zrcadlení portů na fyzických přepínačích v závislosti na scénáři:<br /><br />Pokud je virtuální hostitel na stejném fyzickém přepínači, budete muset nakonfigurovat SPAN na úrovni přepínače.<br /><br />Pokud je virtuální hostitele na jiném přepínači, budete muset nakonfigurovat RSPAN nebo ERSPAN&#42;.|
|Fyzické|Fyzický na stejném přepínači|Fyzický přepínač musí podporovat SPAN / zrcadlení portů.|
|Fyzické|Fyzický na jiném přepínači|Vyžaduje fyzické přepínače podporující RSPAN nebo ERSPAN&#42;.|
&#42; ERSPAN se podporuje jenom tehdy, pokud je před tím, než je provoz analyzován pomocí ATA, zrušeno zapouzdření.

> [!NOTE]
> Zkontrolujte, že řadiče domény a komponenty ATA Gateway, ke kterým se připojují, jsou vzájemně časově synchronizované (s tolerancí 5 minut).

**Pokud pracujete s virtualizačními clustery:**

-   U každého řadiče domény spuštěného ve virtualizačním clusteru ve virtuálním počítači s ATA Gateway konfigurujte spřažení mezi řadičem domény a ATA Gateway. Tímto způsobem je zajištěno, že pokud se řadič domény přesune do jiného hostitele v clusteru, ATA Gateway ho bude následovat. To funguje dobře, pokud je jen několik řadičů domény.
> [!NOTE]
> Pokud vaše prostředí podporuje proces V2V (Virtual to Virtual) na různých hostitelích (RSPAN), nemusíte si dělat starosti se spřažením.
> 
-   Abyste se ujistili, že komponenty ATA Gateway mají správnou velikost, aby mohly samy zpracovávat sledování všech řadičů domény, zkuste tuto možnost: Nainstalujte virtuální počítač na každého hostitele virtualizace a nainstalujte ATA Gateway na každého hostitele. Nakonfigurujte každou ATA Gateway ke sledování všech řadičů domény, které běží v clusteru. Tímto způsobem bude sledován každý hostitel, na kterém běží řadiče domény.

Po dokončení konfigurace zrcadlení portů a před instalací ATA Gateway ověřte, že zrcadlení portů funguje.

## Viz také
- [Ověření zrcadlení portů](validate-port-mirroring.md)
- [Instalace ATA](install-ata.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO5-->



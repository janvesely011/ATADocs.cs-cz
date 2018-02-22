---
title: "Konfigurace zrcadlení portů při nasazování Azure Advanced Threat Protection | Microsoft Docs"
description: "Popisuje možnosti zrcadlení portů a způsob jejich konfigurace pro Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 9ec7eb4c-3cad-4543-bbf0-b951d8fc8ffe
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1cc622f1a8306530423920873e5efa05e8c87064
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="configure-port-mirroring"></a>Konfigurace zrcadlení portů
> [!NOTE] 
> Tento článek se týká pouze v případě, že nasazení Azure ATP samostatné senzor místo senzor Azure ATP. Pokud chcete zjistit, pokud budete muset použít snímač samostatné Azure ATP, najdete v části [výběr správné snímače pro vaše nasazení](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment).
 
Hlavní zdroj dat používá Azure ATP je hloubková kontrola paketů síťového provozu do a z řadičů domény. Pro Azure ATP sledovat síťový provoz musíte buď konfigurovat zrcadlení portů nebo použít síťové ODPOSLOUCHÁVÁNÍ.

Pro zrcadlení portů nakonfigurujte **zrcadlení portů** u každého řadiče domény, který se má monitorovat jako **zdroj** síťového provozu. Obvykle musíte spolupracovat s týmem podpory sítí nebo virtualizace konfigurace zrcadlení portů.
Další informace najdete v dokumentaci od dodavatele.

Řadiče domény a senzor samostatné Azure ATP může být fyzické nebo virtuální. Níže jsou uvedeny běžné metody pro zrcadlení portů a některé aspekty. Další informace najdete v dokumentaci produktu přepínač nebo virtualizační server. Výrobce přepínače může používat odlišnou terminologii.

**Switched Port Analyzer (SPAN)** – Kopíruje síťový provoz z jednoho nebo několika portů přepínače na jiný port v rámci stejného přepínače. I Azure ATP samostatné senzor a řadič domény připojen ke stejnému fyzickému přepínači.

**Remote Switch Port Analyzer (RSPAN)** – Umožňuje sledovat síťový provoz ze zdrojových portů, které jsou rozložené přes víc fyzických přepínačů. RSPAN kopíruje zdrojový provoz do speciální sítě VLAN nakonfigurované pro RSPAN. Tato síť VLAN musí být propojená mezi zahrnutými přepínači kmenovým vedením. RSPAN pracuje na vrstvě 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** – Jedná se o proprietární technologii Cisco pracující na vrstvě 3. ERSPAN umožňuje monitorování provozu přes různé přepínače bez nutnosti kmenových vedení sítě VLAN. ERSPAN používá ke kopírování monitorovaného síťového provozu protokol GRE (Generic Routing Encapsulation). Azure ATP momentálně nemůže přímo přijímat provoz ERSPAN. Pro Azure ATP pro práci s provozu ERSPAN přepínač nebo směrovač, který provozem musí být nakonfigurován jako cíl ERSPAN, kde provoz se zrušeným zapouzdřením. Pak nakonfigurujte přepínač nebo směrovač přesměrování provozu zrušeným zapouzdřením do samostatné senzoru Azure ATP metodou SPAN nebo RSPAN.

> [!NOTE]
> Pokud řadič domény se zrcadlením portů je připojený prostřednictvím linky WAN, zkontrolujte, že linka WAN dokáže zpracovat další zátěž provozu ERSPAN.
> Azure ATP podporuje pouze provoz monitorování provozu dosáhne stejným způsobem jako síťový adaptér a řadičem domény. Azure ATP nepodporuje monitorování provozu, když je provozu rozdělená do jiné porty.

## <a name="supported-port-mirroring-options"></a>Podporované možnosti zrcadlení portů

|Azure senzor samostatné ATP|Řadič domény|Pravidla|
|---------------|---------------------|------------------|
|Virtuální|Virtuální na stejném hostiteli|Virtuální přepínač musí podporovat zrcadlení portů.<br /><br />Přesunutí jednoho z virtuálních počítačů do jiného hostitele může samo o sobě způsobit nefunkčnost zrcadlení portů.|
|Virtuální|Virtuální na různých hostitelích|Zkontrolujte, že váš virtuální přepínač tento scénář podporuje.|
|Virtuální|Fyzické|Vyžaduje vyhrazený síťový adaptér, jinak hodnota ATP Azure uvidí veškerý provoz přicházející do/z hostitele, dokonce i provoz, který odesílá do cloudové služby Azure ATP.|
|Fyzické|Virtuální|Ujistěte se, že virtuální přepínač podporuje tento scénář a konfiguraci zrcadlení portů na fyzických přepínačích v závislosti na scénáři:<br /><br />Pokud je virtuální hostitel na stejném fyzickém přepínači, budete muset nakonfigurovat span na úrovni přepínače.<br /><br />Pokud je virtuální hostitele na jiném přepínači, budete muset nakonfigurovat RSPAN nebo ERSPAN &#42;.|
|Fyzické|Fyzický na stejném přepínači|Fyzický přepínač musí podporovat SPAN / zrcadlení portů.|
|Fyzické|Fyzický na jiném přepínači|Vyžaduje fyzické přepínače podporující RSPAN nebo ERSPAN&#42;.|
&#42; ERSPAN se podporuje jenom při předtím, než je provoz analyzován pomocí ATP zrušeno zapouzdření.

> [!NOTE]
> Ujistěte se, že řadiče domény a senzor samostatné Azure ATP, ke kterým se připojují jsou časově synchronizované intervalu než pět minut.

**Pokud pracujete s virtualizačními clustery:**

-   U každého řadiče domény spuštěného ve virtualizačním clusteru ve virtuálním počítači s Azure ATP samostatné senzoru nakonfigurujte spřažení mezi řadičem domény a senzor samostatné Azure ATP. Tímto způsobem, pokud řadič domény přesune na jiného hostitele v clusteru Azure ATP samostatné senzoru následujícího. To funguje dobře, pokud je jen několik řadičů domény.

 > [!NOTE]
 > Pokud vaše prostředí podporuje proces V2V (Virtual to Virtual) na různých hostitelích (RSPAN), nemusíte si dělat starosti se spřažením.
 
-   Abyste měli jistotu, senzoru samostatné Azure ATP jsou správnou velikost, aby zpracovávat sledování všech řadičů domény, které samy o sobě, zkuste tuto možnost: Nainstalujte virtuální počítač na každého hostitele virtualizace a nainstalujte Azure ATP samostatné senzor na každém hostiteli. Nakonfigurujte každou samostatnou senzor Azure ATP ke sledování všech řadičů domény, které běží na clusteru. Tímto způsobem je monitorován libovolného hostitele, který běží na řadiče domény.

Po dokončení konfigurace zrcadlení portů, ověřte, že zrcadlení portů funguje před instalací senzoru samostatné Azure ATP.

## <a name="see-also"></a>Viz také
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
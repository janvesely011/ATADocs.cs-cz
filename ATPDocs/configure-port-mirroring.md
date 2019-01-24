---
title: Konfigurace zrcadlení portů při nasazování rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje možnosti zrcadlení portů a způsob jejich konfigurace pro služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/4/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9ec7eb4c-3cad-4543-bbf0-b951d8fc8ffe
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a9b69db461dc322010fcb8aa446a95151b7a276f
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2019
ms.locfileid: "54840535"
---
# <a name="configure-port-mirroring"></a>Konfigurace zrcadlení portů
> [!NOTE] 
> Tento článek je relevantní pouze v případě, že nasazení služby Azure ATP samostatné senzorů místo senzorů ochrany ATP v programu Azure. Pokud chcete zjistit, pokud musíte použít samostatné senzorů ochrany ATP v programu Azure, najdete v článku [výběr správné senzory pro funkce nasazení](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment).
 
Hlavní zdroj dat používají ochrany ATP v programu Azure je hloubková kontrola paketů síťového provozu do a z řadičů domény. Pro služby Azure ATP zobrazíte síťový provoz musí buď konfigurovat zrcadlení portů nebo použít síťové ODPOSLOUCHÁVÁNÍ.

Pro zrcadlení portů nakonfigurujte **zrcadlení portů** u každého řadiče domény, který se má monitorovat jako **zdroj** síťového provozu. Obvykle budete muset spolupracovat s týmem sítí nebo virtualizace ke konfiguraci zrcadlení portů.
Další informace najdete v tématu v dokumentaci od výrobce.

Řadiče domény a služby Azure ATP samostatný senzor, může být fyzické nebo virtuální. Níže jsou uvedeny běžné metody pro zrcadlení portů a některé aspekty. Další informace naleznete v dokumentaci produktu přepínač nebo virtualizační server. Výrobce přepínače může používat odlišnou terminologii.

**Switched Port Analyzer (SPAN)** – Kopíruje síťový provoz z jednoho nebo několika portů přepínače na jiný port v rámci stejného přepínače. Obě ochrany ATP v programu Azure samostatný senzor a řadič domény musí být připojen k stejnému fyzickému přepínači.

**Remote Switch Port Analyzer (RSPAN)** – Umožňuje sledovat síťový provoz ze zdrojových portů, které jsou rozložené přes víc fyzických přepínačů. RSPAN kopíruje zdrojový provoz do speciální sítě VLAN nakonfigurované pro RSPAN. Tato síť VLAN musí být propojená mezi zahrnutými přepínači kmenovým vedením. RSPAN pracuje na vrstvě 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** – Jedná se o proprietární technologii Cisco pracující na vrstvě 3. ERSPAN umožňuje monitorování provozu přes různé přepínače bez nutnosti kmenových vedení sítě VLAN. ERSPAN používá ke kopírování monitorovaného síťového provozu protokol GRE (Generic Routing Encapsulation). Ochrana ATP v programu Azure momentálně nemůže přímo přijímat provoz ERSPAN. Pro služby Azure ATP pro práci s provozem ERSPAN je přepínač nebo směrovač, který provoz je potřeba nakonfigurovat jako cíl ERSPAN se dekódovat zapouzdřený provoz. Pak nakonfigurujte přepínač nebo směrovač pro přesměrování provozu paketem se zrušeným do služby Azure ATP samostatný senzor, metodou SPAN nebo RSPAN.

> [!NOTE]
> Pokud řadič domény se zrcadlením portů je připojený prostřednictvím linky WAN, zkontrolujte, že linka WAN dokáže zpracovat další zátěž provozu ERSPAN.
> Ochrana ATP v programu Azure podporuje pouze sledování provozu, pokud přenosy přicházejí na kartu NIC a řadič domény stejným způsobem. Ochrana ATP v programu Azure nepodporuje sledování provozu, když přenosy rozdělují a směřují na různé porty.

## <a name="supported-port-mirroring-options"></a>Podporované možnosti zrcadlení portů

|Azure ATP samostatný senzor|Řadič domény|Pravidla|
|---------------|---------------------|------------------|
|Virtuální|Virtuální na stejném hostiteli|Virtuální přepínač musí podporovat zrcadlení portů.<br /><br />Přesunutí jednoho z virtuálních počítačů do jiného hostitele může samo o sobě způsobit nefunkčnost zrcadlení portů.|
|Virtuální|Virtuální na různých hostitelích|Zkontrolujte, že váš virtuální přepínač tento scénář podporuje.|
|Virtuální|Fyzické|Vyžaduje vyhrazený síťový adaptér, jinak ochrany ATP v programu Azure uvidí veškerý síťový provoz přicházející do a z hostitele, dokonce i provoz, který odešle ke cloudové službě ochrana ATP v programu Azure.|
|Fyzické|Virtuální|Ujistěte se, že virtuální přepínač podporuje tento scénář a konfiguraci zrcadlení portů na fyzických přepínačích v závislosti na scénáři:<br /><br />Pokud je virtuální hostitel na stejném fyzickém přepínači, budete muset nakonfigurovat span na úrovni přepínače.<br /><br />Pokud je virtuální hostitele na jiném přepínači, budete muset nakonfigurovat RSPAN nebo ERSPAN&#42;.|
|Fyzické|Fyzický na stejném přepínači|Fyzický přepínač musí podporovat SPAN / zrcadlení portů.|
|Fyzické|Fyzický na jiném přepínači|Vyžaduje fyzické přepínače podporující RSPAN nebo ERSPAN&#42;.|

&#42;ERSPAN se podporuje jenom při provedení pokud předtím, než je provoz analyzován pomocí ochrany ATP v programu.

> [!NOTE]
> Ujistěte se, že řadiče domény a služby Azure ATP samostatný senzor, ke kterým se připojují, jsou časově synchronizované do pěti minut od sebe navzájem.

**Pokud pracujete s virtualizačními clustery:**

- U každého řadiče domény spuštěného ve virtualizačním clusteru ve virtuálním počítači pomocí služby Azure ATP samostatný senzor nakonfigurujte spřažení mezi řadičem domény a samostatného senzoru služby Azure ATP. Tímto způsobem, pokud řadič domény přesune na jiného hostitele v clusteru služby Azure ATP samostatný senzor ji následuje. To funguje dobře, pokud je jen několik řadičů domény.

  > [!NOTE]
  > Pokud vaše prostředí podporuje proces V2V (Virtual to Virtual) na různých hostitelích (RSPAN), nemusíte si dělat starosti se spřažením.
 
- Aby se zajistilo samostatný senzor ochrany ATP v programu Azure mají správnou velikost, zpracovávat sledování všech řadičů domény samy o sobě, zkuste tuto možnost: Nainstalujte virtuální počítač na každého hostitele virtualizace a Azure ATP samostatný senzor na každém hostiteli. Nakonfigurujte každý samostatný senzor ochrany ATP v programu Azure ke sledování všech řadičů domény, které běží na clusteru. Tímto způsobem se monitoruje všechny hostitele, které běží na řadiče domény.

Po dokončení konfigurace zrcadlení portů, ověřte, že zrcadlení portů funguje před instalací samostatného senzoru služby Azure ATP.

## <a name="see-also"></a>Viz také
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

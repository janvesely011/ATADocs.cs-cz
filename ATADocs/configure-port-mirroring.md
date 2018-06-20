---
title: Konfigurace zrcadlení portů při nasazování Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje možnosti zrcadlení portů a způsob jejich konfigurace pro ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 9ed585d37363fbae2604fe0ea705a0ea30b9b283
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010291"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="configure-port-mirroring"></a>Konfigurace zrcadlení portů
> [!NOTE] 
> Tento článek se týká jenom nasazení komponent ATA Gateway, nikoli komponent ATA Lightweight Gateway. Pokud chcete určit, jestli potřebujete ATA Gateway, přečtěte si téma [Volba vhodných bran pro vaše nasazení](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment).
 
Hlavní zdroj dat používaný ATA je hloubková kontrola paketů síťového provozu do a z řadičů domény. Aby bylo možné pomocí ATA sledovat síťový provoz, musíte buď konfigurovat zrcadlení portů, nebo použít síťové odposlouchávání.

Pro zrcadlení portů nakonfigurujte **zrcadlení portů** u každého řadiče domény, který se má monitorovat jako **zdroj** síťového provozu. Obvykle musíte spolupracovat s týmem podpory sítí nebo virtualizace konfigurace zrcadlení portů.
Další informace najdete v dokumentaci od dodavatele.

Řadiče domény a komponenty ATA Gateway můžou být buď fyzické, nebo virtuální. Níže jsou uvedeny běžné metody pro zrcadlení portů a některé aspekty. Další informace najdete v dokumentaci produktu přepínač nebo virtualizační server. Výrobce přepínače může používat odlišnou terminologii.

**Switched Port Analyzer (SPAN)** – Kopíruje síťový provoz z jednoho nebo několika portů přepínače na jiný port v rámci stejného přepínače. ATA Gateway a řadič domény musí být připojené ke stejnému fyzickému přepínači.

**Remote Switch Port Analyzer (RSPAN)** – Umožňuje sledovat síťový provoz ze zdrojových portů, které jsou rozložené přes víc fyzických přepínačů. RSPAN kopíruje zdrojový provoz do speciální sítě VLAN nakonfigurované pro RSPAN. Tato síť VLAN musí být propojená mezi zahrnutými přepínači kmenovým vedením. RSPAN pracuje na vrstvě 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** – Jedná se o proprietární technologii Cisco pracující na vrstvě 3. ERSPAN umožňuje monitorování provozu přes různé přepínače bez nutnosti kmenových vedení sítě VLAN. ERSPAN používá ke kopírování monitorovaného síťového provozu protokol GRE (Generic Routing Encapsulation). ATA momentálně nemůže přímo přijímat provoz ERSPAN. Pro řešení ATA fungovat s provozu ERSPAN přepínač nebo směrovač, který provozem musí být nakonfigurován jako cíl ERSPAN, kde provoz se zrušeným zapouzdřením. Pak nakonfigurujte přepínač nebo směrovač pro přenos dat zrušeným zapouzdřením komponentě ATA Gateway metodou SPAN nebo RSPAN.

> [!NOTE]
> Pokud řadič domény se zrcadlením portů je připojený prostřednictvím linky WAN, zkontrolujte, že linka WAN dokáže zpracovat další zátěž provozu ERSPAN.
> ATA podporuje sledování provozu, jen pokud přenosy přicházejí na kartu NIC a řadič domény stejným způsobem. ATA sledování provozu nepodporuje, pokud se přenosy rozdělují a směřují na různé porty.

## <a name="supported-port-mirroring-options"></a>Podporované možnosti zrcadlení portů

|ATA Gateway|Řadič domény|Pravidla|
|---------------|---------------------|------------------|
|Virtuální|Virtuální na stejném hostiteli|Virtuální přepínač musí podporovat zrcadlení portů.<br /><br />Přesunutí jednoho z virtuálních počítačů do jiného hostitele může samo o sobě způsobit nefunkčnost zrcadlení portů.|
|Virtuální|Virtuální na různých hostitelích|Zkontrolujte, že váš virtuální přepínač tento scénář podporuje.|
|Virtuální|Fyzické|Vyžaduje vyhrazený síťový adaptér opačném případě ATA uvidí veškerý síťový provoz na příchozí i odchozí hostitele, dokonce i provoz, který odesílá do ATA Center.|
|Fyzické|Virtuální|Ujistěte se, že virtuální přepínač podporuje tento scénář a konfiguraci zrcadlení portů na fyzických přepínačích v závislosti na scénáři:<br /><br />Pokud je virtuální hostitel na stejném fyzickém přepínači, budete muset nakonfigurovat span na úrovni přepínače.<br /><br />Pokud je virtuální hostitele na jiném přepínači, budete muset nakonfigurovat RSPAN nebo ERSPAN&#42;.|
|Fyzické|Fyzický na stejném přepínači|Fyzický přepínač musí podporovat SPAN / zrcadlení portů.|
|Fyzické|Fyzický na jiném přepínači|Vyžaduje fyzické přepínače podporující RSPAN nebo ERSPAN&#42;.|
&#42; ERSPAN se podporuje jenom tehdy, pokud je před tím, než je provoz analyzován pomocí ATA, zrušeno zapouzdření.

> [!NOTE]
> Ujistěte se, že řadiče domény a komponenty ATA Gateway, ke kterým se připojují jsou časově synchronizované intervalu než pět minut.

**Pokud pracujete s virtualizačními clustery:**

-   U každého řadiče domény spuštěného ve virtualizačním clusteru ve virtuálním počítači s ATA Gateway konfigurujte spřažení mezi řadičem domény a ATA Gateway. Tímto způsobem, pokud se řadič domény přesune na jiného hostitele v clusteru, ATA Gateway následujícího. To funguje dobře, pokud je jen několik řadičů domény.
> [!NOTE]
> Pokud vaše prostředí podporuje proces V2V (Virtual to Virtual) na různých hostitelích (RSPAN), nemusíte si dělat starosti se spřažením.
> 
-   Abyste se ujistili, že komponenty ATA Gateway mají správnou velikost, aby mohly samy zpracovávat sledování všech řadičů domény, zkuste tuto možnost: Nainstalujte virtuální počítač na každého hostitele virtualizace a nainstalujte ATA Gateway na každého hostitele. Nakonfigurujte každou ATA Gateway ke sledování všech řadičů domény, které běží v clusteru. Tímto způsobem je monitorován libovolného hostitele, který běží na řadiče domény.

Po dokončení konfigurace zrcadlení portů a před instalací ATA Gateway ověřte, že zrcadlení portů funguje.

## <a name="see-also"></a>Viz také
- [Ověření zrcadlení portů](validate-port-mirroring.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

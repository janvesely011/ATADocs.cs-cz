---
title: Co je nového v Azure ATP | Microsoft Docs
description: Popisuje nejnovější verze Azure ATP a poskytuje informace o tom, co je nového v každé verzi.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/8/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6d794e2d30b51d78bd3e4af76d8bd4a48b2d413f
ms.sourcegitcommit: 8472f3f46fc90da7471cd1065cdb2f6a1d5a9f69
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/08/2018
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="whats-new-in-azure-atp"></a>Co je nového v Azure ATP 



## <a name="azure-atp-release-231"></a>Azure ATP verze 2.31

Vydané 6 může 2018
 
- Vylepšení byly provedeny pro překlad názvů. V rámci této snahy kromě active řešení RPC a rozhraní NetBIOS, senzoru vystavovat paket TLS klienta Hello pro koncový bod RDP portu (3389). 
- Tato verze obsahuje opravy a vylepšení pro víc problémy. 

## <a name="azure-atp-release-230"></a>Azure ATP verze 2.30

Vydané 29. dubna 2018
 
- Šifrování přechod na starší verzi podezřelých aktivit nyní zadat důkaz oddíl popisuje detekovaných službou Azure ATP příznaky, které způsobit, že předpokládat, že, k čemu aktivitu přechod na starší verzi šifrování. 
-   Azure ATP teď používá Azure e-mailu Orchestrator pro všechny e-mailů odeslaný Azure ATP, včetně podezřelé aktivity, monitorování výstrah a sestav. Zobrazí se, že tyto e-mailová oznámení teď můžete pomocí konzistentní formát pro snadné použití a souborů aplikace Excel bude propojen v e-mailu ke stažení z konzoly.
 
 

## <a name="azure-atp-release-229"></a>Azure ATP verze 2.29

Vydané 22 duben 2018
 
- Tato verze obsahuje opravy a vylepšení pro víc problémy. 
 
 
## <a name="azure-atp-release-228"></a>Azure ATP verze 2.28

Vydané 15 duben 2018
 
-   Uživatelé, kteří jsou členy skupin rolí uživatelům ATP Azure a Azure ATP prohlížeče nyní mají oprávnění k zobrazení výstrahy monitorování.
- Tato verze obsahuje opravy a vylepšení pro víc problémy. 


## <a name="azure-atp-release-227"></a>Azure ATP verze 2,27

Vydané 8. dubna 2018

- Nyní máte možnost k poskytnutí zpětné vazby uživatele z horním navigačním panelu. Kliknutím na tlačítko emotikony v panelu nabídek umožňuje odesílat e-mailu týmu Azure Advanced Threat Protection s váš názor.

- Tato verze obsahuje opravy a vylepšení pro víc problémy. 
 

## <a name="azure-atp-release-226"></a>Azure ATP verze 2.26

Vydané 25 března 2018

- Pokud Azure ATP upozorňuje podezřelé aktivity, které identifikujete jako neškodné kladnou (legitimní akce, který není podezřelou aktivitu) máte možnost vyloučit počítače a IP adresy pro další detekce, včetně: šifrování přechod na starší verzi, LDAP Útok hrubou silou, Forged PAC, hrubou silou a Pass-the-hash.
-   Byl vylepšen výkon senzor Azure ATP.
-   Novou oblast pro nasazení pracovního prostoru, přidala se teď můžete nasadit pracovního prostoru v Asii. 


## <a name="azure-atp-release-225"></a>Azure ATP verze 2.25

Vydané 18 března 2018

- Vícefaktorové ověřování (MFA) se teď podporuje v Azure ATP. Klienty pomocí vícefaktorového ověřování můžete nyní přejít na portál Azure ATP.
- Azure ATP má teď [ **stav systému** ](https://health.atp.azure.com/) stránky, kde přinášejí informace o tom, jestli portálu pro správu pracovního prostoru je nahoru a aktivní, pokud dochází k potížím s detekcí a pokud je možné odesílat senzoru přenosy dat do cloudu. Dostanete **stav systému** z řádku nabídek Azure ATP.


## <a name="azure-atp-release-224"></a>Azure ATP verze 2,24

Vydané 11 března 2018

**Nové a aktualizované detekce**
  - Vytvoření podezřelé služby – útočníci se pokusí spustit podezřelé services ve vaší síti. Azure ATP nyní vyvolá výstrahu, pokud rozpozná, že někdo v určitém počítači běží novou službu, která vypadá podezřelé. Toto zjišťování je na základě událostí (ne síťový provoz) a je na všech řadičích domény v síti, která je pro předávání událostí 7045, Azure ATP. Další informace najdete v článku [Průvodce podezřelou aktivitu](suspicious-activity-guide.md).

**Vylepšené šetření**
  - Azure ATP zahrnuje provádět rozšířené [profil entity](entity-profiles.md). Profil entity poskytuje platformu, která je určená pro přímý podrobnější prošetření aktivit uživatele patří sem materiály, které k nim přistupovat, počítačů, které budou přihlášený a mnoho dalších. Profil entity také poskytuje data adresáře a umožňuje identifikovat potenciální cesty laterální pohyb do nebo z entity, které další informace o potenciálních porušení ve vaší organizaci.

  - ATP vám umožňuje ručně značky entity jako *citlivé* k vylepšení detekce a monitorování. Toto značení má dopad na mnoho detekce Azure ATP, jako je například změna detekce citlivou skupinu a [laterální pohyb cesta](use-case-lateral-movement-path.md), které spoléhají na entity, které se považují za citlivé.

**Nové sestavy, který vám pomůže prozkoumat**
  - [Zveřejněné hesla v nešifrovaném textu sestavy](reports.md) umožňuje rozpoznat, kdy služby odeslat přihlašovací údaje účtu se odesílají v prostém textu. To umožňuje prozkoumat služby a zvýšit úroveň zabezpečení sítě. Tato sestava nahrazuje výstrahy podezřelé aktivity ve formě prostého textu.
  - [Pomoci odhalit laterální pohyb cesty k sestavě citlivé účty](reports.md) uvádí citlivé účty, které jsou zveřejňovány prostřednictvím cesty laterální pohyb. To umožňuje zmírnit tyto cesty a posilovat jejich zabezpečení sítě s cílem minimalizovat riziko útoku prostor. To vám umožňuje zabránit laterální pohyb tak, aby útočníci nelze přesunout ve vaší síti mezi uživatelé a počítače, dokud se dosáhl jackpotu virtuální zabezpečení: přihlašovací údaje účtu citlivé správce.

- Můžete teď snadno poskytnout přístup k dokumentaci pomocí odkazu v rámci upozornění na podezřelou aktivitu Chcete-li zobrazit [šetření kroky, které můžete provést](suspicious-activity-guide.md). 

**Vylepšení výkonu**
 -  Senzor infrastruktury Azure ATP byl vylepšen výkonu: agregovaná zobrazení provozu umožňuje optimalizace procesoru a paket kanálu a opětovně používá sockets na řadičích domény, chcete-li minimalizovat relací SSL na řadič domény.

## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
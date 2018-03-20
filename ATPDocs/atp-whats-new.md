---
title: "Co je nového v Azure ATP | Microsoft Docs"
description: "Popisuje nejnovější verze Azure ATP a poskytuje informace o tom, co je nového v každé verzi."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/18/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6b3c9ddd1873b3139009a44e9c1f7a85ea3b6901
ms.sourcegitcommit: adfa7a3a3918518b6b14b94d3c0a9f899142196a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/19/2018
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="whats-new-in-azure-atp"></a>Co je nového v Azure ATP 

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
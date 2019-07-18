---
title: Architektura rozšířené ochrany před internetovými útoky Azure | Microsoft Docs
description: Popisuje architekturu Azure Advanced Threat Analytics (ATP).
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/17/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 38a1790194d739ac31c66df60cf0d9c2911344c7
ms.sourcegitcommit: b7b3d4a401faaa3edb4bd669a1a003a6d21a4322
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2019
ms.locfileid: "68298896"
---
# <a name="azure-atp-architecture"></a>Architektura ATP Azure

Azure ATP monitoruje řadiče domény zachytáváním a analýzou síťového provozu a využitím událostí Windows přímo z řadičů domény a pak analyzuje data pro útoky a hrozby. Využití profilování, deterministické detekce, strojového učení a behaviorálních algoritmů chování Azure ATP o vaší síti, umožňuje detekci anomálií a upozorňuje vás na podezřelé aktivity.

Architektura rozšířené ochrany před internetovými útoky Azure:

![Diagram topologie architektury Azure ATP](media/atp-architecture-topology.png)

V této části se dozvíte, jak funguje tok služby Azure ATP a zachytávání událostí a podrobněji popisuje funkce hlavních součástí: portál Azure ATP, senzor Azure ATP a cloudová služba Azure ATP. 

Senzor ATP Azure, který je nainstalovaný přímo na řadičích domény, přistupuje k protokolům událostí, které vyžaduje přímo z řadiče domény. Po analýze protokolů a síťového provozu senzorem Azure ATP pošle do cloudové služby Azure ATP jenom analyzované informace (pošle se jenom procento protokolů). 

## <a name="azure-atp-components"></a>Komponenty ATP Azure
ATP v Azure se skládá z následujících součástí:

-   **Portál Azure ATP** <br>
Portál Azure ATP umožňuje vytvoření instance ATP Azure, zobrazuje data získaná ze senzorů ATP Azure a umožňuje monitorovat, spravovat a zkoumat hrozby ve vašem síťovém prostředí.  
-   **Senzor ATP Azure**<br>
Senzory Azure ATP se instalují přímo na řadiče domény. Senzor přímo monitoruje provoz řadiče domény bez nutnosti vyhrazeného serveru nebo konfigurace zrcadlení portů.

-   **Cloudová služba Azure ATP**<br>
Cloudová služba Azure ATP běží v infrastruktuře Azure a je aktuálně nasazená v USA, Evropě a Asii. Cloudová služba Azure ATP je připojená k inteligentnímu grafu zabezpečení Microsoftu. 

## <a name="azure-atp-portal"></a>Portál Azure ATP 
Použijte portál Azure ATP k těmto akcím:
- Vytvoření instance služby Azure ATP
- Integrace s dalšími službami zabezpečení společnosti Microsoft 
- Správa nastavení konfigurace senzoru ATP Azure 
- Zobrazit data přijatá ze senzorů Azure ATP
- Monitorování zjistilo podezřelé aktivity a podezřelé útoky na základě modelu dezaktivačního řetězu útoků.
- **Volitelné**: portál se dá nakonfigurovat taky pro posílání e-mailů a událostí, když se zjistí výstrahy zabezpečení nebo problémy se stavem.

> [!NOTE]
> - Pokud do vaší instance služby Azure ATP během 60 dnů není nainstalovaný žádný senzor, může být instance odstraněna a budete ji muset znovu vytvořit.

## <a name="azure-atp-sensor"></a>Senzor ATP Azure
Senzor Azure ATP má následující základní funkce:
- Zaznamenání a Kontrola síťového provozu řadiče domény (místní provoz řadiče domény)
- Příjem událostí systému Windows přímo z řadičů domény 
- Získat informace o monitorování účtů RADIUS od poskytovatele sítě VPN
- Získávají data o uživatelích a počítačích z domény Active Directory.
- Provádějí rozpoznání síťových entit (uživatelů, skupin a počítačů).
- Přenos relevantních dat do cloudové služby Azure ATP

 
## <a name="azure-atp-sensor-features"></a>Funkce snímače ATP Azure

Senzor ATP Azure čte události místně bez nutnosti kupovat a udržovat další hardware nebo konfigurace. Senzor ATP Azure také podporuje trasování událostí pro Windows (ETW), které poskytuje informace protokolu pro více zjišťování. Detekce založené na ETW zahrnují podezřelé útoky DCShadow pomocí požadavků na replikaci řadiče domény a povýšení řadiče domény.

### <a name="domain-synchronizer-process"></a>Proces synchronizátoru domény

Proces synchronizátoru domény zodpovídá za proaktivní synchronizaci všech entit z konkrétní domény služby Active Directory (podobně jako mechanismus používaný řadiči domény samotný pro replikaci). Jeden senzor se automaticky vybere náhodně ze všech vašich oprávněných senzorů, aby mohl sloužit jako synchronizátor domény. 

Pokud je synchronizátor domény offline po dobu delší než 30 minut, vybere se místo toho automaticky jiný snímač. 
    
### <a name="resource-limitations"></a>Omezení prostředků

Senzor ATP Azure zahrnuje monitorovací komponentu, která vyhodnocuje dostupnou výpočetní a paměťovou kapacitu na řadiči domény, na kterém běží. Proces monitorování se spouští každých 10 sekund a dynamicky aktualizuje kvótu využití procesoru a paměti v procesu senzoru ATP Azure. Proces monitorování zajišťuje, že řadič domény má vždy alespoň 15% volných výpočetních prostředků a dostupných prostředků paměti.

Bez ohledu na to, co se děje na řadiči domény, proces monitorování průběžně uvolňuje prostředky, aby se zajistilo, že základní funkce řadiče domény nebudou nikdy ovlivněny.

Pokud proces monitorování způsobí, že senzor služby Azure ATP vyčerpá prostředky, monitoruje se jenom částečný provoz a na stránce Stav portálu Azure ATP se zobrazí výstraha monitorování "vynechané síťové přenosy se zrcadlením portů".

### <a name="windows-events"></a>Události systému Windows

Aby bylo možné vylepšit detekci ATP v Azure, je nutné, aby se při podezřelých chybách ověřování, změnách citlivých skupin, vytváření podezřelých služeb a Honeytokenu typů útoků provádělo podezření na neúspěšnou autentizaci. protokoly následujících událostí systému Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 a 7045. Tyto události jsou automaticky čteny senzory Azure ATP se správnými [nastaveními zásad auditu](atp-advanced-audit-policy.md). 

## <a name="next-steps"></a>Další kroky

- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/trisizingtool)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

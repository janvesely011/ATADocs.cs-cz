---
title: Architektura služby Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Popisuje architekturu z Azure Advanced Threat Analytics (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/27/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 34717315eb1c2d705679210c1114287cfc5a389b
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674992"
---
# <a name="azure-atp-architecture"></a>Architektura služby Azure ATP

Ochrana ATP v programu Azure monitoruje řadiče domény tak, že zachycení a parsování síťového provozu a využití události Windows přímo z řadičů domény a pak analyzuje data útoky a hrozbami. Využitím profilace deterministickou detekci, strojové učení a behaviorální algoritmy, které služby Azure ATP učí o síti, umožňuje detekovat anomálie a upozorní vás na podezřelé aktivity.

Architektura služby Azure Advanced Threat Protection:

![Diagram topologie architektury Azure ATP](media/atp-architecture-topology.png)

Tato část popisuje, jak funguje toku sítě a zaznamenávání událostí služby Azure ATP a operací k podrobnému popisu funkce základních komponent: ochrana ATP v programu Azure portal, senzoru služby Azure ATP a cloudové služby Azure ATP. 

Nainstalovat přímo na řadiče domény, senzoru služby Azure ATP přistupuje k protokoly událostí, které vyžaduje přímo z řadiče domény. Po protokoly a přenosech v síti jsou analyzovány pomocí senzor, ochrana ATP v programu Azure odesílá pouze analyzované informace ke cloudové službě ochrana ATP v programu Azure (pouze procento protokoly jsou odeslány). 

## <a name="azure-atp-components"></a>Komponenty služby Azure ATP
Ochrana ATP v programu Azure se skládá z následujících součástí:

-   **Portál Azure ATP** <br>
Ochrana ATP v programu Azure portal umožňuje vytvoření instance služby Azure ATP, zobrazí data přijatá ze senzorů ochrany ATP v programu Azure a umožňuje monitorovat, spravovat a prozkoumejte hrozby ve vašem síťovém prostředí.  
-   **Senzoru služby Azure ATP**<br>
Azure ATP senzorů instalují přímo na řadiče domény. Senzor monitoruje přímo provoz na řadiči domény, bez nutnosti vyhrazený server nebo konfigurovat zrcadlení portů.

-   **Cloudovou službu Azure ATP**<br>
Cloudovou službu Azure ATP běží na infrastrukturu Azure a je aktuálně nasazené v USA, Evropa a Asie. Cloudovou službu Azure ochrany ATP v programu je připojený ke společnosti Microsoft intelligent security graph. 

## <a name="azure-atp-portal"></a>Portál Azure ATP 
Pomocí portálu ochrany ATP v programu Azure:
- Vytvoření instance služby Azure ATP
- Integrace s jinými službami zabezpečení Microsoftu 
- Spravovat nastavení konfigurace senzoru služby Azure ATP 
- Zobrazit data přijatá ze senzorů služby Azure ATP
- Monitorování detekované podezřelé aktivity a podezřelé útoků na základě modelu kill řetězu útoku
- **Volitelné**: na portálu můžete také nakonfigurovat na odesílání e-mailů a událostí při zjištění zabezpečení výstrahy nebo problémy se stavem

> [!NOTE]
> - Pokud žádný senzor je nainstalovaný na instanci služby Azure ATP během 60 dnů, můžou se odstranit instance a bude nutné ho znovu vytvořit.

## <a name="azure-atp-sensor"></a>Senzoru služby Azure ATP
Senzoru služby Azure ATP má následující základní funkce:
- Zachytávají a prošetřují síťový provoz na řadiči domény (místní provoz řadiče domény)
- Příjem událostí Windows přímo z řadičů domény 
- Zobrazí informace o monitorování účtů protokolu RADIUS od poskytovatele připojení VPN
- Získávají data o uživatelích a počítačích z domény Active Directory.
- Provádějí rozpoznání síťových entit (uživatelů, skupin a počítačů).
- Přenášejí relevantní data do cloudové služby Azure ATP

 
## <a name="azure-atp-sensor-features"></a>Funkce Azure ochrany ATP v programu senzor

Senzoru služby Azure ATP načte události místně bez nutnosti zakoupení a Udržovat další hardware ani konfigurace. Senzoru služby Azure ATP také podporuje trasování událostí pro Windows (ETW) poskytující informace o protokolu pro více detekcí. Tématu detekce na základě trasování událostí pro Windows zahrnují podezřelý DCShadow útoky pomocí žádosti o replikaci řadiče domény a povýšení řadiče domény.

### <a name="domain-synchronizer-candidate"></a>Kandidát na synchronizátora domény

Kandidát na synchronizátora domény zodpovídá za proaktivní synchronizaci všech entity z konkrétní domény služby Active Directory (podobně jako mechanismu, který používá sami řadiče domény pro replikaci). Jeden senzor se náhodně vybere ze seznamu kandidátů, která bude sloužit jako synchronizátor domény. 

Pokud je synchronizátor více než 30 minut offline, vybere se jiný kandidát. Pokud žádný synchronizátor domény není k dispozici pro konkrétní doménu, ochrana ATP v programu Azure aktivně synchronizuje entit a jejich změny, ale ochrany ATP v programu Azure načítat nové entity, když jste zjistili v monitorovaném provozu.
    
Pokud není dostupný žádný synchronizátor domény a hledáte entitu, která nemají žádný provoz s ní spojené, se nezobrazí žádné výsledky hledání.

Ve výchozím nastavení nejsou ochrany ATP v programu Azure senzorů kandidáti na synchronizátora. K ručnímu nastavení senzoru služby Azure ATP jako kandidát na synchronizátora domény, postupujte podle kroků v [pracovní postup instalace služby Azure ATP](install-atp-step5.md).

### <a name="resource-limitations"></a>Omezení prostředků

Senzoru služby Azure ATP zahrnuje monitorovací komponentu, která vyhodnotí dostupnou kapacitu výpočetní a paměťové prostředky na řadiči domény, na kterém je spuštěný. Proces monitorování spouští každých 10 sekund a dynamicky aktualizuje kvóty využití procesoru a paměti v procesu senzoru služby Azure ATP. Monitorování procesu je zajištěno, že řadič domény má vždy alespoň 15 % této bezplatné výpočetní a paměťové prostředky k dispozici.

Bez ohledu na to, co se stane v řadiči domény procesu monitorování průběžně uvolní prostředky, abyste měli jistotu, že nikdy je vliv na funkčnost základních řadič domény.

Pokud proces monitorování způsobí, že se senzoru služby Azure ATP dojdou prostředky, se monitoruje provoz jenom částečně a monitorování výstrahy "zrušenou provoz prostřednictvím zrcadlení portů sítě" se zobrazí stavové stránce portálu ochrany ATP v programu Azure.

### <a name="windows-events"></a>Události Windows

K vylepšení rozsahu zjišťování ochrany ATP v programu Azure na identity podezřelých krádež (pass-the-hash), podezřelá neúspěšná ověření, úpravy citlivých skupin, vytváření podezřelé služeb a typy aktivit Honeytokenu útoku, ochrana ATP v programu Azure potřebuje k analýze protokoly následující události Windows: 4776,4732,4733,4728,4729,4756,4757 a 7045. Tyto události jsou automaticky číst ochrany ATP v programu Azure snímačů správné [pokročilé zásady auditu](atp-advanced-audit-policy.md). 

## <a name="next-steps"></a>Další postup

- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/trisizingtool)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

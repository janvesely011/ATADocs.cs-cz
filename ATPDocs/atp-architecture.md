---
title: Architektura služby Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Popisuje architekturu z Azure Advanced Threat Analytics (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/27/2019
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6988b41b64dc3d8afef5f7af614f78b41501e2af
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085312"
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
Senzoru služby Azure ATP načte události místně bez nutnosti zakoupení a Udržovat další hardware ani konfigurace. Senzoru služby Azure ATP také podporuje trasování událostí pro Windows (ETW) poskytující informace o protokolu pro více detekcí. Trasování událostí pro Windows na základě detekce patří podezřelý DCShadow útoky pomocí žádosti o replikaci řadiče domény a povýšení řadiče domény.

### <a name="domain-synchronizer-candidate"></a>Kandidát na synchronizátora domény

    The domain synchronizer candidate is responsible for synchronizing all entities from a specific Active Directory domain proactively (similar to the mechanism used by the domain controllers themselves for replication). One sensor is chosen randomly, from the list of candidates, to serve as the domain synchronizer. 

    If the synchronizer is offline for more than 30 minutes, another candidate is chosen instead. If there is no domain synchronizer available for a specific domain, Azure ATP proactively synchronizes entities and their changes, however Azure ATP retrieves new entities as they are detected in the monitored traffic. 
    
    If there is no domain synchronizer available, and you search for an entity that did not have any traffic related to it, no search results are displayed.

    By default, Azure ATP sensors are not synchronizer candidates. To manually set an Azure ATP sensor as a domain synchronizer candidate, follow the steps in the [Azure ATP installation workflow](install-atp-step5.md#configure-azure-atp-sensor-settings).

### <a name="resource-limitations"></a>Omezení prostředků

    The Azure ATP sensor includes a monitoring component that evaluates the available compute and memory capacity on the domain controller on which it is running. The monitoring process runs every 10 seconds and dynamically updates the CPU and memory utilization quota on the Azure ATP sensor process. The monitoring process makes sure the domain controller always has at least 15% of free compute and memory resources available.

    No matter what occurs on the domain controller, the monitoring process continually frees up resources to make sure the domain controller's core functionality is never affected.

    If the monitoring process causes the Azure ATP sensor to run out of resources, only partial traffic is monitored and the monitoring alert "Dropped port mirrored network traffic" appears in the Azure ATP portal Health page.

### <a name="windows-events"></a>Události Windows

    To enhance Azure ATP detection coverage of suspected identity theft (pass-the-hash), suspicious authentication failures,modifications to sensitive groups, creation of suspicious services, and Honeytoken activity types of attack, Azure ATP needs to analyze the logs of the following Windows events: 4776,4732,4733,4728,4729,4756,4757, and 7045. These events are read automatically by Azure ATP sensors with correct [advanced audit policy settings](atp-advanced-audit-policy.md). 

## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/trisizingtool)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

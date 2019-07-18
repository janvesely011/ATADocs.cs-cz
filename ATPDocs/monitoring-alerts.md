---
title: Principy výstrah monitorování ATP Azure | Microsoft Docs
description: Popisuje, jak můžete pomocí protokolů ATP Azure řešit problémy.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 65279895689e230a3a28871a61f4cffe36d6042c
ms.sourcegitcommit: b7b3d4a401faaa3edb4bd669a1a003a6d21a4322
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2019
ms.locfileid: "68298760"
---
# <a name="understanding-azure-atp-sensor-and-standalone-sensor-monitoring-alerts"></a>Principy výstrah monitorování a samostatného senzoru ATP pro Azure ATP

Služba Azure ATP Health Center vám umožní zjistit, v případě problémů s vaší instancí služby Azure ATP, vyvoláním výstrahy monitorování. Tento článek popisuje všechna monitorovací upozornění jednotlivých komponent včetně příčiny a postupu vedoucího k vyřešení problému.

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Senzor nedosažitelný pro všechny řadiče domény

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Senzor ATP Azure je teď v režimu offline kvůli problémům s připojením ke všem nakonfigurovaným řadičům domény.|To má vliv na schopnost Azure ATP rozpoznat podezřelé aktivity související s řadiči domény, které monitoruje tento senzor Azure ATP.| Zajistěte, aby řadiče domény byly v provozu a aby se tento senzor ATP Azure mohl na ně připojit pomocí protokolu LDAP. Kromě toho v **Nastavení** nezapomeňte nakonfigurovat účet adresářové služby pro každou nasazenou doménovou strukturu.|Střední|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>Všechny/některé síťové adaptéry pro zachytávání na senzoru nejsou k dispozici.

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Všechny/některé vybrané síťové adaptéry pro zachytávání na senzoru ATP Azure jsou zakázané nebo odpojené.|Síťový provoz pro některé nebo všechny řadiče domény už není zachycený senzorem Azure ATP. To má vliv na schopnost detekovat podezřelé aktivity související s těmito řadiči domény.|Ujistěte se, že jsou vybrané síťové adaptéry pro zachytávání na senzoru ATP v Azure povolené a připojené.|Střední|

## <a name="no-traffic-received-from-domain-controller"></a>Z řadiče domény se nepřijímá žádný provoz

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Z řadiče domény se přes tento senzor Azure ATP nepřijal žádný provoz.|To může znamenat, že zrcadlení portů z řadičů domény do senzoru ATP Azure ještě není nakonfigurované nebo nefunguje.|Ověřte, že je na [síťových zařízeních správně nakonfigurované zrcadlení portů](configure-port-mirroring.md).<br></br>V síťovém adaptéru pro zachytávání senzorů Azure ATP zakažte tyto funkce v upřesňujících nastaveních:<br></br>Slučování příjmových segmentů (IPv4)<br></br>Slučování příjmových segmentů (IPv6)|Střední|

## <a name="read-only-user-password-to-expire-shortly"></a>Brzo vyprší platnost hesla uživatele jen pro čtení

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k rozpoznávání entit ve službě Active Directory, vyprší za méně než 30 dnů.|Pokud platnost hesla pro tohoto uživatele vyprší, všechny senzory Azure ATP přestanou běžet a nebudou shromažďována žádná nová data.|[Změňte heslo připojení k doméně](modifying-atp-config-dcpassword.md) a pak aktualizujte heslo na portálu Azure atp.|Střední|

## <a name="read-only-user-password-expired"></a>Vypršení platnosti hesla uživatele jen pro čtení

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k získání dat z adresáře, vypršela.|Všechny senzory Azure ATP přestanou běžet (nebo se brzy ukončí) a nebudou shromažďována žádná nová data.|[Změňte heslo připojení k doméně](modifying-atp-config-dcpassword.md) a pak aktualizujte heslo na portálu Azure atp.|Vysoká|

## <a name="sensor-outdated"></a>Senzor zastaralý

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Senzor ATP Azure je zastaralý.|Ve snímači ATP Azure je spuštěná verze, která je tři nebo víc verzí zastaralá.|Ručně aktualizujte senzor a zkontrolujte, proč se senzor neaktualizuje automaticky. Pokud to nepomůže, Stáhněte si nejnovější instalační balíček senzorů a odinstalujte a znovu nainstalujte senzor. Další informace najdete v tématu [Instalace senzoru ATP Azure](install-atp-step4.md).|Střední|

## <a name="sensor-reached-a-memory-resource-limit"></a>Senzor dosáhl limitu prostředků paměti.

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Senzor ATP Azure se sám zastavil a automaticky se restartuje, aby se chránil řadič domény před nedostatkem paměti.|Senzor ATP Azure vynutil na sebe omezení paměti, aby řadičům domény nedocházelo k omezením prostředků. To se stane, když má řadič domény velkou spotřebu paměti. Data z tohoto řadiče domény jsou monitorovaná jen částečně.|Zvětšete kapacitu paměti (RAM) řadiče domény nebo do této lokality přidejte další řadiče domény, aby zatížení tohoto řadiče domény bylo rovnoměrněji rozdělené.|Střední|

## <a name="sensor-service-failed-to-start"></a>Službu snímače se nepovedlo spustit.

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Službu Azure ATP snímače se nepovedlo spustit aspoň 30 minut.|To může mít vliv na schopnost detekovat podezřelé aktivity pocházející z řadičů domény monitorovaných tímto senzorem Azure ATP.|Sledujte protokoly senzorů Azure ATP, abyste porozuměli hlavní příčině selhání služby Azure ATP snímače.|Vysoká|

## <a name="sensor-stopped-communicating"></a>Senzor přestal komunikovat.

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Nedošlo k žádné komunikaci ze senzoru služby Azure ATP. Výchozí časové rozpětí tohoto upozornění je 5 minut.|Síťový adaptér na senzoru ATP Azure již nezachycuje síťový provoz. To má vliv na schopnost ATA detekovat podezřelé aktivity, protože síťový provoz nebude schopný získat přístup ke cloudové službě Azure ATP.|Ověřte, že port, který se používá pro komunikaci mezi senzorem ATP Azure a cloudovou službou Azure ATP, není blokovaný pro žádné směrovače ani brány firewall.|Střední|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Některé řadiče domény jsou nedosažitelné senzorem.

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Senzor ATP Azure má omezené funkce kvůli problémům s připojením k některým nakonfigurovaným řadičům domény.|Předání detekce hodnoty hash může být méně přesné, pokud se na některé řadiče domény nedokáže senzor ATP Azure dotazovat.|Zajistěte, aby řadiče domény byly v provozu a aby se tento senzor ATP Azure mohl na ně připojit pomocí protokolu LDAP.|Střední|

## <a name="some-forwarded-events-are-not-being-analyzed"></a>Některé předané události se neanalyzují

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Senzor ATP Azure získává více událostí, než dokáže zpracovat.|Některé předané události se neanalyzují, což může mít vliv na schopnost detekovat podezřelé aktivity pocházející z řadičů domény, které tento senzor Azure ATP monitoruje.|Ověřte, že se do snímače ATP Azure předávají jenom požadované události, nebo se zkuste některé z těchto událostí předejte jinému senzoru ATP Azure.|Střední|

## <a name="some-network-traffic-is-not-being-analyzed"></a>Některý síťový provoz se neanalyzuje

|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
|Senzor ATP Azure získává více síťových přenosů, než dokáže zpracovat.|Některý síťový provoz se neanalyzuje, což může mít vliv na schopnost detekovat podezřelé aktivity pocházející z řadičů domény monitorovaných tímto senzorem Azure ATP.|Podle potřeby zvažte [přidání dalších procesorů a paměti](atp-capacity-planning.md). Pokud se jedná o samostatný senzor Azure ATP, snižte počet monitorovaných řadičů domény.<br></br>K tomu může dojít také v případě, že používáte řadiče domény na virtuálních počítačích VMware. Pokud se chcete těmto upozorněním vyhnout, zkontrolujte, že následující nastavení mají hodnotu 0 nebo jsou na virtuálním počítači zakázaná:<br></br>– TsoEnable<br></br>-LargeSendOffload (IPv4)<br></br>– Snižování zátěže IPv4 TSO<br></br>Zvažte také zakázání procesu IPv4 Giant TSO Offload. Další informace najdete v dokumentaci k VMware.|Střední|

## <a name="windows-events-missing-from-domain-controller-audit-policy"></a>Chybí události Windows ze zásad auditu řadiče domény.
|Výstrahy|Popis|Řešení|severity|
|----|----|----|----|
| Chybí události Windows ze zásad auditu řadiče domény.|Chcete-li auditovat správné události a zahrnout je do protokolu událostí systému Windows, vyžadují řadiče domény přesné rozšířené nastavení zásad auditu. Nesprávná Pokročilá nastavení zásad auditu ponechají z vašich protokolů kritické události a výsledkem je nedokončené pokrytí ATP Azure.|Projděte si [zásady pokročilého auditu](atp-advanced-audit-policy.md) a podle potřeby je upravte. | Střední|



## <a name="see-also"></a>Viz také

- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

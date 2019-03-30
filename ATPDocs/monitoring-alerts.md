---
title: Principy Azure ochrany ATP v programu Sledování výstrah | Dokumentace Microsoftu
description: Popisuje, jak můžete k řešení potíží pomocí protokolů služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 12/02/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5a0d474eda8b7bbc75057f95ced58fdb7ae15ce5
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58675111"
---
# <a name="understanding-azure-atp-sensor-and-standalone-sensor-monitoring-alerts"></a>Principy senzoru služby Azure ATP a samostatný senzor výstrah monitorování

Health Center ochrany ATP v programu Azure vám umožňuje vědět, že dojde k nějakému problému s vaší instancí služby Azure ATP vyvoláním monitorovacího upozornění. Tento článek popisuje všechna monitorovací upozornění jednotlivých komponent včetně příčiny a postupu vedoucího k vyřešení problému.

## <a name="read-only-user-password-to-expire-shortly"></a>Brzy vyprší platnost hesla uživatele jen pro čtení

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k rozpoznávání entit ve službě Active Directory, vyprší za méně než 30 dnů.|Pokud heslo pro tohoto uživatele vyprší, zastaví všechny služby Azure ATP senzory a shromažďovat žádná nová data.|[Změna hesla připojení k doméně](modifying-atp-config-dcpassword.md) a pak aktualizujte heslo na portálu ochrany ATP v programu Azure.|Střední|

## <a name="read-only-user-password-expired"></a>Vypršení platnosti hesla uživatele jen pro čtení

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k získání dat z adresáře, vypršela.|Zastaví všechny senzory ochrany ATP v programu Azure (nebo se zastaví brzy) a shromažďovat žádná nová data.|[Změna hesla připojení k doméně](modifying-atp-config-dcpassword.md) a pak aktualizujte heslo na portálu ochrany ATP v programu Azure.|Vysoká|

## <a name="domain-synchronizer-not-assigned"></a>Nepřiřazený synchronizátor domény

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Žádný synchronizátor domény je přiřazený k žádnému senzoru služby Azure ATP. K tomu může dojít, pokud neexistuje žádný senzor ochrany ATP v programu Azure nakonfigurovaný jako kandidát na synchronizátora domény.|Když se doména nesynchronizuje, změny entit může způsobit informací o entitách v Azure ATP se zastaralé nebo chybí, ale nemá vliv na žádné zjišťování.|Ujistěte se, že tento aspoň jeden senzor ochrany ATP v programu Azure je nastaven jako [synchronizátor domény](install-atp-step5.md).|Nízká|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>Všechny nebo některé ze síťových adaptérů pro zachytávání na senzoru, která nejsou k dispozici

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Všechny nebo některé vybrané síťové adaptéry pro zachytávání na senzoru služby Azure ATP jsou zakázané nebo odpojené.|Senzoru služby Azure ATP je už nezachytává síťový provoz všech nebo některých řadičů domény. To má vliv na schopnost detekce podezřelých aktivit souvisejících s těmito řadiči domény.|Ujistěte se, že tyto vybrané síťové adaptéry pro zachytávání na senzoru služby Azure ATP povolené a připojené.|Střední|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Některé řadiče domény se nemůže připojit k žádnému senzoru

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Senzoru služby Azure ATP má omezenou funkčnost kvůli problémům s připojením k některým nakonfigurovaným řadičům domény.|Předání hodnoty Hash zjišťování může být méně přesné při nemůže dotazovat některé řadiče domény senzoru služby Azure ATP.|Ujistěte se, že řadiče domény jsou spuštěné a, že tento senzoru služby Azure ATP můžete otevřít připojení LDAP na ně.|Střední|

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Všechny řadiče domény se nemůže připojit k žádnému senzoru

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Snímač ochrany ATP v programu Azure je momentálně offline z důvodu problémů s připojením ke všem nakonfigurovaným řadičům domény.|To má vliv na služby Azure ATP schopnost detekce podezřelých aktivit souvisejících s řadiči domény sledováno tento senzoru služby Azure ATP.| Ujistěte se, že řadiče domény jsou spuštěné a, že tento senzoru služby Azure ATP můžete otevřít připojení LDAP na ně.|Střední|

## <a name="sensor-stopped-communicating"></a>Senzor přestal komunikovat

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Žádná komunikace pocházející od senzoru služby Azure ATP došlo. Výchozí časové rozpětí tohoto upozornění je 5 minut.|Síťový adaptér na senzoru služby Azure ATP je už nezachytává síťový provoz. To má vliv na schopnost detekce podezřelých aktivit, protože síťový provoz, nebudou moci kontaktovat cloudové službě ochrana ATP v programu Azure.|Zkontrolujte, že port používaný pro komunikaci mezi senzoru služby Azure ATP a cloudovou službou ochrany ATP v programu Azure neblokuje směrovači nebo firewally.|Střední|

## <a name="no-traffic-received-from-domain-controller"></a>Z řadiče domény se nepřijímá žádný provoz

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Z řadiče domény přes tento senzoru služby Azure ATP nebyl přijat žádný provoz.|To může znamenat, že zrcadlení portů z řadičů domény na senzor ochrany ATP v programu Azure ještě nemáte nakonfigurovaný nebo nepracuje.|Ověřte, že je na [síťových zařízeních správně nakonfigurované zrcadlení portů](configure-port-mirroring.md).<br></br>Na senzoru služby Azure ATP síťové karty pro zachytávání, zakázání těchto funkcí v upřesňujícím nastavení:<br></br>Slučování příjmových segmentů (IPv4)<br></br>Slučování příjmových segmentů (IPv6)|Střední|

## <a name="some-forwarded-events-are-not-being-analyzed"></a>Některé předané události se neanalyzují

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Senzoru služby Azure ATP přijímá více událostí, než dokáže zpracovat.|Některé předané události se neanalyzují, což může mít vliv na schopnost detekce podezřelých aktivit pocházejících od řadičů domény, které sleduje tato senzoru služby Azure ATP.|Ověřte, že jen požadované události se předávají do senzoru služby Azure ATP nebo zkuste některé události, které mají jiný senzoru služby Azure ATP předávat.|Střední|

## <a name="some-network-traffic-is-not-being-analyzed"></a>Některý síťový provoz se neanalyzuje

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Senzoru služby Azure ATP přijímá více síťového provozu, než dokáže zpracovat.|Některý síťový provoz se neanalyzuje, což může mít vliv na schopnost detekce podezřelých aktivit pocházejících od řadičů domény, které sleduje tato senzoru služby Azure ATP.|Podle potřeby zvažte [přidání dalších procesorů a paměti](atp-capacity-planning.md). Pokud je to ochrana ATP v programu Azure samostatný senzor, omezte počet monitorovaných řadičů domény.<br></br>To může také dojít, pokud používáte řadiče domény na virtuálních počítačích VMware. Pokud se chcete těmto upozorněním vyhnout, zkontrolujte, že následující nastavení mají hodnotu 0 nebo jsou na virtuálním počítači zakázaná:<br></br>-TsoEnable<br></br>-LargeSendOffload(IPv4)<br></br>– TSO Offload protokolu IPv4<br></br>Zvažte také zakázání procesu IPv4 Giant TSO Offload. Další informace najdete v dokumentaci k VMware.|Střední|

## <a name="sensor-service-failed-to-start"></a>Nepovedlo se spustit službu Sensor

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Službu sensor ochrany ATP v programu Azure se nepodařilo spustit aspoň 30 minut.|To může mít vliv na schopnost detekce podezřelých aktivit pocházejících od řadičů domény, které sleduje tato senzoru služby Azure ATP.|Monitorování ochrany ATP v programu Azure senzor protokoluje události do najdete hlavní příčinu, ochrana ATP v programu Azure služba sensor selhala.|Vysoká|

## <a name="sensor-reached-a-memory-resource-limit"></a>Senzor dosáhl limitu prostředků paměti

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Senzoru služby Azure ATP zastavil a automaticky restartuje, které řadič domény z ke stavu nedostatku paměti.|Senzoru služby Azure ATP vynucuje omezení paměti, aby řadič domény chránila před omezením prostředků. To se stane, když má řadič domény velkou spotřebu paměti. Data z tohoto řadiče domény jsou monitorovaná jen částečně.|Zvětšete kapacitu paměti (RAM) řadiče domény nebo do této lokality přidejte další řadiče domény, aby zatížení tohoto řadiče domény bylo rovnoměrněji rozdělené.|Střední|

## <a name="sensor-outdated"></a>senzor zastaralé

|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Senzoru služby Azure ATP je zastaralá.|Senzoru služby Azure ATP je spuštěna verze, která je zastaralá o tři nebo více verzí.|Ručně aktualizujte ze senzorů a zjistěte, proč senzor neaktualizují automaticky. Pokud to nepomůže, stáhněte si nejnovější instalační balíček ze senzorů a odinstalovat a senzoru. Další informace najdete v tématu [instalace senzoru služby Azure ATP](install-atp-step4.md).|Střední|

## <a name="see-also"></a>Viz také

- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

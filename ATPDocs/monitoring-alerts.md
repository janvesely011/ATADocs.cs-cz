---
title: "Principy Azure ATP výstrahy monitorování | Microsoft Docs"
description: "Popisuje, jak můžete použít protokol Azure ATP k řešení potíží"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cdb440e92aef0f9d09d3aa9411d0ce65435469d1
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*

# <a name="understanding-azure-atp-sensor-and-standalone-sensor-monitoring-alerts"></a>Princip senzor Azure ATP a senzor samostatné výstrahy monitorování

Azure ATP Health Center umožňuje vědět, když dojde k problému s žádným z vaší worksapces Azure ATP zobrazením upozornění na monitorování. Tento článek popisuje všechna monitorovací upozornění jednotlivých komponent včetně příčiny a postupu vedoucího k vyřešení problému.

## <a name="read-only-user-password-to-expire-shortly"></a>Jen pro čtení uživatelské heslo vyprší za chvíli

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k rozpoznávání entit ve službě Active Directory, vyprší za méně než 30 dnů.|Pokud vyprší platnost hesla pro tohoto uživatele, zastaví všechny snímače Azure ATP a žádná nová data se shromažďují.|[Změna hesla připojení k doméně](modifying-atp-config-dcpassword.md) a pak aktualizujte heslo v konzole Azure ATP.|Střední|

## <a name="read-only-user-password-expired"></a>Vypršení platnosti hesla uživatele jen pro čtení

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k získání dat z adresáře, vypršela.|Zastaví všechny snímače Azure ATP (nebo se zastaví brzy) a žádná nová data se shromažďují.|[Změna hesla připojení k doméně](modifying-atp-config-dcpassword.md) a pak aktualizujte heslo v konzole Azure ATP.|Vysoká|

## <a name="domain-synchronizer-not-assigned"></a>Nepřiřazený synchronizátor domény

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Žádný synchronizátor domény je přiřazený k žádné senzor Azure ATP. To může dojít, pokud neexistuje žádné senzor Azure ATP nakonfigurovaný jako kandidát na synchronizátora domény.|Pokud doména není synchronizován, změny entity může způsobit informace entity v Azure ATP se zastaralé nebo chybějící ale nemá vliv na všechny detekce.|Ujistěte se, že tento alespoň jeden senzor Azure ATP je nastaven jako [synchronizátor domény](install-atp-step5.md).|Nízká|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>Všechna nebo některá Zachytávání síťových adaptérů na senzoru, která nejsou k dispozici

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Všechny nebo některé vybrané Zachytávání síťových adaptérů v Azure ATP senzoru jsou zakázané nebo odpojené.|Senzor Azure ATP už zachycenou síťových přenosů pro některé nebo všechny z řadičů domény. To ovlivní schopnost rozpoznat podezřelé aktivity, týkající se těchto řadičů domény.|Ujistěte se, že jsou tyto síťové adaptéry vybrané zachycení na Azure ATP senzoru povolen a připojen.|Střední|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Některé řadiče domény nejsou dostupné snímače

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Azure ATP senzor má omezenou funkčnost kvůli potížím s připojením k některé z konfigurované řadiče domén.|Předejte hodnotu Hash detekce může být méně přesné Pokud některé řadiče domény nemůže být dotazována senzor Azure ATP.|Zajistěte, aby řadiče domény se uvedou do provozu a že tento senzor Azure ATP můžete otevřít připojení LDAP k nim.|Střední|

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Všechny řadiče domény nejsou dostupné snímače

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Senzor Azure ATP je nyní v režimu offline kvůli potížím s připojením k všechny konfigurované řadiče domén.|To ovlivní schopnost Azure ATP detekovat podezřelé aktivity související s řadičů domény sleduje tento senzor Azure ATP.| Zajistěte, aby řadiče domény se uvedou do provozu a že tento senzor Azure ATP můžete otevřít připojení LDAP k nim.|Střední|

## <a name="sensor-stopped-communicating"></a>senzor zastavena komunikaci

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Byl žádná komunikace z Azure ATP senzoru. Výchozí časové rozpětí tohoto upozornění je 5 minut.|Síťový adaptér na Azure ATP senzoru už zachycenou síťový provoz. To ovlivní schopnost ATA detekovat podezřelé aktivity, vzhledem k tomu, že síťový provoz, nebude možné k dosažení cloudové službě Azure ATP.|Zkontrolujte, zda port používaný pro komunikaci mezi senzor Azure ATP a Azure ATP cloudové služby není blokován nastavením všechny směrovače a brány firewall.|Střední|

## <a name="no-traffic-received-from-domain-controller"></a>Z řadiče domény se nepřijímá žádný provoz

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Žádný provoz byla přijata z řadiče domény přes tento senzor Azure ATP.|To může znamenat, že zrcadlení portů z řadičů domény do Azure ATP senzoru dosud nebyl nakonfigurován nebo nepracuje.|Ověřte, že je na [síťových zařízeních správně nakonfigurované zrcadlení portů](configure-port-mirroring.md).<br></br>Na Azure ATP senzoru zaznamenat síťový adaptér, zakázat tyto funkce v Upřesnit nastavení:<br></br>Slučování příjmových segmentů (IPv4)<br></br>Slučování příjmových segmentů (IPv6)|Střední|

## <a name="some-forwarded-events-are-not-being-analyzed"></a>Některé předané události se neanalyzují

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Senzor Azure ATP přijímá více událostí, než může zpracovat.|Některé předané události nejsou analyzované, což může ovlivnit detekovat podezřelé aktivity pocházející z řadičů domény, které sleduje tato senzor Azure ATP.|Ověřte, zda pouze požadované události se předávají do Azure ATP senzoru nebo pokusu o předání některé události do jiné senzor Azure ATP.|Střední|

## <a name="some-network-traffic-is-not-being-analyzed"></a>Některý síťový provoz se neanalyzuje

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Senzor Azure ATP přijímá další síťový provoz, než může zpracovat.|Není probíhá analýza některé síťový provoz, který může mít vliv na schopnost rozpoznat podezřelé aktivity pocházející z řadičů domény, které sleduje tato senzor Azure ATP.|Podle potřeby zvažte [přidání dalších procesorů a paměti](atp-capacity-planning.md). Pokud je to Azure ATP senzoru samostatné, snižte počet monitorovaných řadičů domény.<br></br>To také může dojít, pokud používáte řadiče domény na virtuální počítače VMware. Pokud se chcete těmto upozorněním vyhnout, zkontrolujte, že následující nastavení mají hodnotu 0 nebo jsou na virtuálním počítači zakázaná:<br></br>-TsoEnable<br></br>-LargeSendOffload(IPv4)<br></br>-IPv4 TSO snižování zátěže<br></br>Zvažte také zakázání procesu IPv4 Giant TSO Offload. Další informace najdete v dokumentaci VMware.|Střední|

## <a name="sensor-service-failed-to-start"></a>senzor služby se nezdařilo

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Služba Azure ATP senzor se nepodařilo spustit nejméně 30 minut.|To může mít vliv na schopnost rozpoznat podezřelé aktivity pocházející z řadičů domény, které sleduje tato senzor Azure ATP.|Monitorování Azure ATP senzor protokoly zjistit příčinu selhání služby senzor Azure ATP.|Vysoká|

## <a name="sensor-reached-a-memory-resource-limit"></a>senzor dosažení limitu prostředků paměti

|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Senzor Azure ATP samotné zastaví a restartuje automaticky chránit řadiče domény z nedostatku paměti.|Senzor Azure ATP vynucuje omezení paměti sám zabránit řadiče domény vyskytuje omezení prostředků. To se stane, když má řadič domény velkou spotřebu paměti. Data z tohoto řadiče domény jsou monitorovaná jen částečně.|Zvětšete kapacitu paměti (RAM) řadiče domény nebo do této lokality přidejte další řadiče domény, aby zatížení tohoto řadiče domény bylo rovnoměrněji rozdělené.|Střední|


## <a name="see-also"></a>Viz také

- [Požadavky Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
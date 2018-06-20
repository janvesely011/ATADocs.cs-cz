---
title: Vysvětlení monitorovacích upozornění | Dokumentace Microsoftu
description: Popisuje, jak můžete protokoly ATA použít k řešení potíží.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: b04fb8a4-b366-4b55-9d4c-6f054fa58a90
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6506ecf445641e9789cb1817916089f5463ba289
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009883"
---
*Platí pro: Advanced Threat Analytics verze 1.9*


# <a name="understanding-ata-monitoring-alerts"></a>Vysvětlení ATA monitorování výstrah
ATA Health Center vás vyvoláním monitorovacího upozornění informuje, pokud u nasazení ATA dojde k nějakému problému.
Tento článek popisuje všechna monitorovací upozornění jednotlivých komponent včetně příčiny a postupu vedoucího k vyřešení problému.
## <a name="ata-center-issues"></a>Problémy komponenty ATA Center
### <a name="center-running-out-of-disk-space"></a>Center volné místo na disku
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Na jednotce v počítači s komponentou ATA Center, která slouží k uložení databáze ATA, dochází volné místo.|To znamená, že na tomto pevném disku je méně než 200 GB nebo 20 % volného místa podle toho, která z těchto hodnot je menší. Když ATA zjistí, že na jednotce dochází místo, začne z databáze odstraňovat stará data. Pokud ho nelze odstranit stará data, protože je stále nutné data pro detekční modul, zobrazí se tato výstraha. Když obdržíte toto upozornění, přestane ATA sledovat nové aktivity.|Zvětšete velikost jednotky nebo na ní uvolněte místo.|Vysoká|
### <a name="failure-sending-mail"></a>Selhání odesílání e-mailu
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Řešení ATA se nedaří odeslat e-mailové oznámení na zadaný poštovní server.|Žádný e-mailové zprávy jsou odesílány z ATA.|Ověřte konfiguraci serveru SMTP.|Nízká|

### <a name="center-overloaded"></a>Center přetížených
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Komponenta ATA Center nedokáže zvládnout množství dat přenášených z komponent ATA Gateway. |ATA Center zastaví analýza nový síťový provoz a události. To znamená, že v době, kdy je toto monitorovací upozornění aktivní, je přesnost detekce a profilů snížená.|Zajistěte, aby komponenta ATA Center měla dostatek prostředků. Další podrobnosti o tom, jak správně plánování kapacity ATA Center najdete v tématu [plánování kapacity ATA](ata-capacity-planning.md). Prověřte výkon komponenty ATA Center pomocí článku [Řešení potíží s ATA pomocí čítačů výkonu](troubleshooting-ata-using-perf-counters.md).|Vysoká|

### <a name="failure-connecting-to-the-siem-server-using-syslog"></a>Neúspěšné připojení k serveru SIEM pomocí protokolu Syslog
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Řešení ATA se nedaří odesílat události zadanému serveru SIEM.|To znamená, že ATA Center nemůže serveru SIEM posílat podezřelé aktivity a monitorovací upozornění.|Ověřte, že je [nastavení serveru Syslog správně nakonfigurované](setting-syslog-email-server-settings.md).|Nízká|
### <a name="center-certificate-is-about-to-expire"></a>Certifikát Center platnost má vypršet
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Center vyprší za méně než 3 týdny.|Po vypršení platnosti certifikátu přestane fungovat připojení z komponent ATA Gateway na ATA Center. ATA Center, které proces dojde k chybě a všechny funkce ATA se zastaví.|[Vyměňte certifikát komponenty ATA Center](modifying-ata-center-configuration.md).|Střední|
### <a name="ata-center-certificate-expired"></a>Vypršení platnosti certifikátu komponenty ATA Center
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Center vypršela.|Po vypršení platnosti certifikátu: selhání připojení z ATA Gateway k ATA Center. K chybě v procesu ATA Center a zastaví všechny funkce ATA.|[Vyměňte certifikát komponenty ATA Center](modifying-ata-center-configuration.md).|Vysoká|
## <a name="ata-gateway-issues"></a>Problémy komponenty ATA Gateway
### <a name="read-only-user-password-to-expire-shortly"></a>Jen pro čtení uživatelské heslo vyprší za chvíli
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k rozpoznávání entit ve službě Active Directory, vyprší za méně než 30 dnů.|Pokud vyprší platnost hesla pro tohoto uživatele, všechny komponenty ATA Gateway se zastaví a žádná nová data se shromažďují.|[Změňte heslo pro připojení k doméně](modifying-ata-config-dcpassword.md) a aktualizujte heslo v konzole ATA.|Střední|
### <a name="read-only-user-password-expired"></a>Vypršení platnosti hesla uživatele jen pro čtení
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k získání dat z adresáře, vypršela.|Všechny komponenty ATA Gateway zastaví (nebo se zastaví brzy) a žádná nová data se shromažďují.|[Změňte heslo pro připojení k doméně](modifying-ata-config-dcpassword.md) a aktualizujte heslo v konzole ATA.|Vysoká|
### <a name="gateway-certificate-about-to-expire"></a>Certifikát brány vyprší
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Gateway vyprší za méně než 3 týdny.|Připojení z konkrétní ATA Gateway k ATA Center se nezdaří. Je odesílána žádná data z této komponenty ATA Gateway.|Certifikát komponenty ATA Gateway by se měl obnovit automaticky. Prohlédněte si protokoly komponent ATA Gateway a ATA Center a zjistěte, proč se tento certifikát automaticky neobnovil.|Střední|

### <a name="gateway-certificate-expired"></a>Platnost certifikátu brány
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Gateway vypršela.|Tato komponenta ATA Gateway nemá žádné připojení na ATA Center. Je odesílána žádná data z této komponenty ATA Gateway.|[Odinstalujte a znovu nainstalujte ATA Gateway](install-ata-step3.md).|Vysoká|
### <a name="domain-synchronizer-not-assigned"></a>Nepřiřazený synchronizátor domény
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|K žádné komponentě ATA Gateway není přiřazený synchronizátor domény. K tomu může dojít, pokud žádná komponenta ATA Gateway není nakonfigurovaná jako kandidát na synchronizátora domény.|Pokud doména není synchronizován, změny entity může způsobit informace entity v ATA se zastaralé nebo chybějící ale nemá vliv na všechny detekce.|Zajistěte, aby alespoň jedna komponenta ATA Gateway byla nastavená jako [synchronizátor domény](install-ata-step5.md).|Nízká|
### <a name="allsome-of-the-capture-network-adapters-on-a-gateway-are-not-available"></a>Všechna nebo některá Zachytávání síťových adaptérů na bránu, která nejsou k dispozici
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Všechny nebo některé vybrané síťové adaptéry pro zachytávání na ATA Gateway jsou zakázané nebo odpojené.|ATA Gateway už nezachytává síťový provoz všech nebo některých řadičů domény. To ovlivní schopnost rozpoznat podezřelé aktivity, týkající se těchto řadičů domény.|Zajistěte, aby vybrané síťové adaptéry pro zachytávání byly na ATA Gateway povolené a připojené.|Střední|
### <a name="some-domain-controllers-are-unreachable-by-a-gateway"></a>Některé řadiče domény nejsou dostupné prostřednictvím brány
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|ATA Gateway má omezenou funkčnost kvůli problémům s připojením k některým nakonfigurovaným řadičům domény.|Pokud ATA Gateway nemůže dotazovat některé řadiče domény, může být detekce předání hodnoty hash (Pass-the-Hash) méně přesná.|Zajistěte funkčnost řadičů domény a ověřte, že tato komponenta ATA Gateway může vůči nim otevřít připojení LDAP.|Střední|
### <a name="all-domain-controllers-are-unreachable-by-a-gateway"></a>Všechny řadiče domény nejsou dostupné prostřednictvím brány
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|ATA Gateway je momentálně offline kvůli problémům s připojením ke všem nakonfigurovaným řadičům domény.|To ovlivní schopnost ATA detekovat podezřelé aktivity související s řadičů domény sleduje tato komponenta ATA Gateway.| Zajistěte funkčnost řadičů domény a ověřte, že tato komponenta ATA Gateway může vůči nim otevřít připojení LDAP.|Střední|
### <a name="gateway-stopped-communicating"></a>Brána byla zastavena komunikaci
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Z komponenty ATA Gateway nepřichází žádná komunikace. Výchozí časové rozpětí tohoto upozornění je 5 minut.|Síťový adaptér na této komponentě ATA Gateway už nezachytává síťový provoz. To ovlivní schopnost ATA detekovat podezřelé aktivity, vzhledem k tomu, že síťový provoz, nebude možné vás zastihnout ATA Center.|Zkontrolujte, že port použitý ke komunikaci mezi komponentou ATA Gateway a službou ATA Center není blokovaný směrovači nebo firewally.|Střední|
### <a name="no-traffic-received-from-domain-controller"></a>Z řadiče domény se nepřijímá žádný provoz
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Přes tuto komponentu ATA Gateway nebyl z řadiče domény přijat žádný provoz.|To může značit, že zrcadlení portů z doménových řadičů na ATA Gateway ještě není nakonfigurované nebo nefunguje.|Ověřte, že je na [síťových zařízeních správně nakonfigurované zrcadlení portů](configure-port-mirroring.md).<br></br>Na ATA Gateway zaznamenat síťový adaptér, zakázat tyto funkce v Upřesnit nastavení:<br></br>Slučování příjmových segmentů (IPv4)<br></br>Slučování příjmových segmentů (IPv6)|Střední|
### <a name="some-forwarded-events-are-not-being-analyzed"></a>Některé předané události se neanalyzují
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|ATA Gateway přijímá více událostí, než dokáže zpracovat.|Některé předané události se neanalyzují, což může mít vliv na schopnost detekce podezřelých aktivit pocházejících od řadičů domény, které tato komponenta ATA Gateway monitoruje.|Ověřte, že se na ATA Gateway předávají jen požadované události, nebo zkuste některé z těchto událostí předávat na jinou komponentu ATA Gateway.|Střední|
### <a name="some-network-traffic-is-not-being-analyzed"></a>Některý síťový provoz se neanalyzuje
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|ATA Gateway přijímá více síťového provozu, než dokáže zpracovat.|Některý síťový provoz se neanalyzuje, což může mít vliv na schopnost detekce podezřelých aktivit pocházejících od řadičů domény, které tato komponenta ATA Gateway monitoruje.|Podle potřeby zvažte [přidání dalších procesorů a paměti](ata-capacity-planning.md). Pokud se jedná o samostatnou komponentu ATA Gateway, snižte počet monitorovaných řadičů domény.<br></br>To také může dojít, pokud používáte řadiče domény na virtuální počítače VMware. Pokud se chcete těmto upozorněním vyhnout, zkontrolujte, že následující nastavení mají hodnotu 0 nebo jsou na virtuálním počítači zakázaná:<br></br>-TsoEnable<br></br>-LargeSendOffload(IPv4)<br></br>-IPv4 TSO snižování zátěže<br></br>Zvažte také zakázání procesu IPv4 Giant TSO Offload. Další informace najdete v dokumentaci k VMware.|Střední|

### <a name="gateway-version-outdated"></a>Zastaralá verze brány
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|ATA Center je novější než verze nainstalovaná na komponentě ATA Gateway. ATA Gateway kvůli tomu přestane fungovat podle očekávání.|To může mít vliv na schopnost detekce podezřelých aktivit pocházejících z řadičů domény, které tato komponenta ATA Gateway monitoruje.|Aktualizujte ATA Gateway automaticky na nejnovější verzi povolením [automatických aktualizací](install-ata-step1.md) v konzole ATA nebo stažením nejnovějšího balíčku ATA Gateway v konzole ATA.|Vysoká|
### <a name="gateway-service-failed-to-start"></a>Služba brány se nepodařilo spustit
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Službu ATA Gateway se po nejméně 30 minut nepodařilo spustit.|To může mít vliv na schopnost detekce podezřelých aktivit pocházejících z řadičů domény, které tato komponenta ATA Gateway monitoruje.|Prohlédněte si protokoly komponenty ATA Gateway a [zjistěte původní příčinu chyby služby ATA Gateway](troubleshooting-ata-using-logs.md).|Vysoká|
## <a name="lightweight-gateway"></a>Lightweight Gateway
### <a name="lightweight--gateway-reached-a-memory-resource-limit"></a>Dosažení limitu prostředků paměti Lightweight Gateway
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Komponenta Lightweight ATA Gateway se zastavila a automaticky se restartuje, aby řadič domény chránila před stavem nedostatku paměti.|Lightweight ATA Gateway si vynucuje omezení paměti, aby řadič domény chránila před omezením prostředků. To se stane, když má řadič domény velkou spotřebu paměti. Data z tohoto řadiče domény jsou monitorovaná jen částečně.|Zvětšete kapacitu paměti (RAM) řadiče domény nebo do této lokality přidejte další řadiče domény, aby zatížení tohoto řadiče domény bylo rovnoměrněji rozdělené.|Střední|


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

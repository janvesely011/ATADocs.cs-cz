---
title: Vysvětlení monitorovacích upozornění | Dokumentace Microsoftu
description: Popisuje, jak můžete protokoly ATA použít k řešení potíží.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 02/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b04fb8a4-b366-4b55-9d4c-6f054fa58a90
ms.reviewer: elofek
ms.suite: ems
ms.openlocfilehash: abf42792620035e0427c3cc517094fa859aae5a5
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58675094"
---
# <a name="understanding-ata-monitoring-alerts"></a>Principy monitorování výstrah ATA

*Platí pro: Advanced Threat Analytics verze 1.9*

ATA Health Center vás vyvoláním monitorovacího upozornění informuje, pokud u nasazení ATA dojde k nějakému problému.
Tento článek popisuje všechna monitorovací upozornění jednotlivých komponent včetně příčiny a postupu vedoucího k vyřešení problému.
## <a name="ata-center-issues"></a>Problémy komponenty ATA Center
### <a name="center-running-out-of-disk-space"></a>System Center dochází místo na disku
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Na jednotce v počítači s komponentou ATA Center, která slouží k uložení databáze ATA, dochází volné místo.|To znamená, že na tomto pevném disku je méně než 200 GB nebo 20 % volného místa podle toho, která z těchto hodnot je menší. Když ATA zjistí, že na jednotce dochází místo, začne z databáze odstraňovat stará data. Pokud stará data ho nelze odstranit, protože je pořád tato data potřebuje pro detekční modul, zobrazí se tato výstraha. Když obdržíte toto upozornění, přestane ATA sledovat nové aktivity.|Zvětšete velikost jednotky nebo na ní uvolněte místo.|Vysoká|
### <a name="failure-sending-mail"></a>Chyba odeslání e-mailu
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Řešení ATA se nedaří odeslat e-mailové oznámení na zadaný poštovní server.|Z ATA nejsou odesílány žádné e-mailové zprávy.|Ověřte konfiguraci serveru SMTP.|Nízká|

### <a name="center-overloaded"></a>System Center přetížení
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Komponenta ATA Center nedokáže zvládnout množství dat přenášených z komponent ATA Gateway. |Komponenty ATA Center přestane analyzovat síťový provoz a události. To znamená, že v době, kdy je toto monitorovací upozornění aktivní, je přesnost detekce a profilů snížená.|Zajistěte, aby komponenta ATA Center měla dostatek prostředků. Další podrobnosti o tom, ke správnému naplánování kapacity pro ATA Center najdete v tématu [plánování kapacity ATA](ata-capacity-planning.md). Prověřte výkon komponenty ATA Center pomocí článku [Řešení potíží s ATA pomocí čítačů výkonu](troubleshooting-ata-using-perf-counters.md).|Vysoká|

### <a name="failure-connecting-to-the-siem-server-using-syslog"></a>Neúspěšné připojení k serveru SIEM pomocí protokolu Syslog
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Řešení ATA se nedaří odesílat události zadanému serveru SIEM.|To znamená, že ATA Center nemůže serveru SIEM posílat podezřelé aktivity a monitorovací upozornění.|Ověřte, že je [nastavení serveru Syslog správně nakonfigurované](setting-syslog-email-server-settings.md).|Nízká|
### <a name="center-certificate-is-about-to-expire"></a>Certifikát Center brzy vyprší platnost
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Center vyprší za méně než 3 týdny.|Po vypršení platnosti certifikátu: Přestane fungovat připojení z komponent ATA Gateway na ATA Center. Dojde k chybě procesu ATA Center a všechny funkce ATA se zastaví.|[Vyměňte certifikát komponenty ATA Center](modifying-ata-center-configuration.md).|Střední|
### <a name="ata-center-certificate-expired"></a>Vypršení platnosti certifikátu komponenty ATA Center
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Center vypršela.|Po vypršení platnosti certifikátu: Připojení z komponent ATA Gateway na ATA Center selže. Dojde k chybě procesu ATA Center a všechny funkce ATA se zastaví.|[Opětovné nasazení komponenty ATA Center](install-ata-step1.md)|Vysoká|
## <a name="ata-gateway-issues"></a>Problémy komponenty ATA Gateway
### <a name="read-only-user-password-to-expire-shortly"></a>Brzy vyprší platnost hesla uživatele jen pro čtení
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k rozpoznávání entit ve službě Active Directory, vyprší za méně než 30 dnů.|Pokud heslo pro tohoto uživatele vyprší, zastaví všechny komponenty ATA Gateway a shromažďovat žádná nová data.|[Změňte heslo pro připojení k doméně](modifying-ata-config-dcpassword.md) a aktualizujte heslo v konzole ATA.|Střední|
### <a name="read-only-user-password-expired"></a>Vypršení platnosti hesla uživatele jen pro čtení
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k získání dat z adresáře, vypršela.|Všechny komponenty ATA Gateway zastaví (nebo se zastaví brzy) a shromažďovat žádná nová data.|[Změňte heslo pro připojení k doméně](modifying-ata-config-dcpassword.md) a aktualizujte heslo v konzole ATA.|Vysoká|
### <a name="gateway-certificate-about-to-expire"></a>Brána brzké vypršení platnosti certifikátu
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Gateway vyprší za méně než 3 týdny.|Připojení z konkrétní komponenty ATA Gateway na ATA Center selže. Nejsou odesílána žádná data z této komponenty ATA Gateway.|Certifikát komponenty ATA Gateway by se měl obnovit automaticky. Prohlédněte si protokoly komponent ATA Gateway a ATA Center a zjistěte, proč se tento certifikát automaticky neobnovil.|Střední|

### <a name="gateway-certificate-expired"></a>Vypršela platnost certifikátu brány
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Gateway vypršela.|Tato komponenta ATA Gateway nemá žádné připojení na ATA Center. Nejsou odesílána žádná data z této komponenty ATA Gateway.|[Odinstalujte a znovu nainstalujte ATA Gateway](install-ata-step3.md).|Vysoká|
### <a name="domain-synchronizer-not-assigned"></a>Nepřiřazený synchronizátor domény
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|K žádné komponentě ATA Gateway není přiřazený synchronizátor domény. K tomu může dojít, pokud žádná komponenta ATA Gateway není nakonfigurovaná jako kandidát na synchronizátora domény.|Když se doména nesynchronizuje, změny entit může způsobit, že informace o entitách v ATA jsou zastaralé nebo chybí, ale nemá vliv na žádné zjišťování.|Zajistěte, aby alespoň jedna komponenta ATA Gateway byla nastavená jako [synchronizátor domény](install-ata-step5.md).|Nízká|
### <a name="allsome-of-the-capture-network-adapters-on-a-gateway-are-not-available"></a>Všechny nebo některé ze síťových adaptérů pro zachytávání na bránu, která nejsou k dispozici
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Všechny nebo některé vybrané síťové adaptéry pro zachytávání na ATA Gateway jsou zakázané nebo odpojené.|ATA Gateway už nezachytává síťový provoz všech nebo některých řadičů domény. To má vliv na schopnost detekce podezřelých aktivit souvisejících s těmito řadiči domény.|Zajistěte, aby vybrané síťové adaptéry pro zachytávání byly na ATA Gateway povolené a připojené.|Střední|
### <a name="some-domain-controllers-are-unreachable-by-a-gateway"></a>Některé řadiče domény nejsou dostupné prostřednictvím brány
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|ATA Gateway má omezenou funkčnost kvůli problémům s připojením k některým nakonfigurovaným řadičům domény.|Pokud ATA Gateway nemůže dotazovat některé řadiče domény, může být detekce předání hodnoty hash (Pass-the-Hash) méně přesná.|Zajistěte funkčnost řadičů domény a ověřte, že tato komponenta ATA Gateway může vůči nim otevřít připojení LDAP.|Střední|
### <a name="all-domain-controllers-are-unreachable-by-a-gateway"></a>Všechny řadiče domény nejsou dostupné prostřednictvím brány
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|ATA Gateway je momentálně offline kvůli problémům s připojením ke všem nakonfigurovaným řadičům domény.|To má vliv na schopnost detekce podezřelých aktivit souvisejících s řadiči domény, které tato komponenta ATA Gateway monitoruje.| Zajistěte funkčnost řadičů domény a ověřte, že tato komponenta ATA Gateway může vůči nim otevřít připojení LDAP.|Střední|
### <a name="gateway-stopped-communicating"></a>Gateway přestala komunikovat
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Z komponenty ATA Gateway nepřichází žádná komunikace. Výchozí časové rozpětí tohoto upozornění je 5 minut.|Síťový adaptér na této komponentě ATA Gateway už nezachytává síťový provoz. To má vliv na schopnost detekce podezřelých aktivit, protože síťový provoz, nebudou moct nedostane na ATA Center.|Zkontrolujte, že port použitý ke komunikaci mezi komponentou ATA Gateway a službou ATA Center není blokovaný směrovači nebo firewally.|Střední|
### <a name="no-traffic-received-from-domain-controller"></a>Z řadiče domény se nepřijímá žádný provoz
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Přes tuto komponentu ATA Gateway nebyl z řadiče domény přijat žádný provoz.|To může značit, že zrcadlení portů z doménových řadičů na ATA Gateway ještě není nakonfigurované nebo nefunguje.|Ověřte, že je na [síťových zařízeních správně nakonfigurované zrcadlení portů](configure-port-mirroring.md).<br></br>V komponentě ATA Gateway síťové karty pro zachytávání, zakázání těchto funkcí v upřesňujícím nastavení:<br></br>Slučování příjmových segmentů (IPv4)<br></br>Slučování příjmových segmentů (IPv6)|Střední|
### <a name="some-forwarded-events-are-not-being-analyzed"></a>Některé předané události se neanalyzují
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|ATA Gateway přijímá více událostí, než dokáže zpracovat.|Některé předané události se neanalyzují, což může mít vliv na schopnost detekce podezřelých aktivit pocházejících od řadičů domény, které tato komponenta ATA Gateway monitoruje.|Ověřte, že se na ATA Gateway předávají jen požadované události, nebo zkuste některé z těchto událostí předávat na jinou komponentu ATA Gateway.|Střední|
### <a name="some-network-traffic-is-not-being-analyzed"></a>Některý síťový provoz se neanalyzuje
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|ATA Gateway přijímá více síťového provozu, než dokáže zpracovat.|Některý síťový provoz se neanalyzuje, což může mít vliv na schopnost detekce podezřelých aktivit pocházejících od řadičů domény, které tato komponenta ATA Gateway monitoruje.|Podle potřeby zvažte [přidání dalších procesorů a paměti](ata-capacity-planning.md). Pokud se jedná o samostatnou komponentu ATA Gateway, snižte počet monitorovaných řadičů domény.<br></br>To může také dojít, pokud používáte řadiče domény na virtuálních počítačích VMware. Pokud se chcete těmto upozorněním vyhnout, zkontrolujte, že následující nastavení mají hodnotu 0 nebo jsou na virtuálním počítači zakázaná:<br></br>-TsoEnable<br></br>-LargeSendOffload(IPv4)<br></br>– TSO Offload protokolu IPv4<br></br>Zvažte také zakázání procesu IPv4 Giant TSO Offload. Další informace najdete v dokumentaci k VMware.|Střední|

### <a name="gateway-version-outdated"></a>Verze brány zastaralá
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|ATA Center je novější než verze nainstalovaná na komponentě ATA Gateway. ATA Gateway kvůli tomu přestane fungovat podle očekávání.|To může mít vliv na schopnost detekce podezřelých aktivit pocházejících z řadičů domény, které tato komponenta ATA Gateway monitoruje.|Aktualizujte ATA Gateway automaticky na nejnovější verzi povolením [automatických aktualizací](install-ata-step1.md) v konzole ATA nebo stažením nejnovějšího balíčku ATA Gateway v konzole ATA.|Vysoká|
### <a name="gateway-service-failed-to-start"></a>Nepovedlo se spustit službu brány
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Službu ATA Gateway se po nejméně 30 minut nepodařilo spustit.|To může mít vliv na schopnost detekce podezřelých aktivit pocházejících z řadičů domény, které tato komponenta ATA Gateway monitoruje.|Prohlédněte si protokoly komponenty ATA Gateway a [zjistěte původní příčinu chyby služby ATA Gateway](troubleshooting-ata-using-logs.md).|Vysoká|
## <a name="lightweight-gateway"></a>Lightweight Gateway
### <a name="lightweight--gateway-reached-a-memory-resource-limit"></a>Komponenta Lightweight Gateway dosáhla limitu prostředků paměti
|Výstrahy|Popis|Řešení|Severity|
|----|----|----|----|
|Komponenta Lightweight ATA Gateway se zastavila a automaticky se restartuje, aby řadič domény chránila před stavem nedostatku paměti.|Lightweight ATA Gateway si vynucuje omezení paměti, aby řadič domény chránila před omezením prostředků. To se stane, když má řadič domény velkou spotřebu paměti. Data z tohoto řadiče domény jsou monitorovaná jen částečně.|Zvětšete kapacitu paměti (RAM) řadiče domény nebo do této lokality přidejte další řadiče domény, aby zatížení tohoto řadiče domény bylo rovnoměrněji rozdělené.|Střední|


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

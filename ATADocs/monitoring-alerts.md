---
title: "Vysvětlení monitorovacích upozornění | Dokumentace Microsoftu"
description: "Popisuje, jak můžete protokoly ATA použít k řešení potíží."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/13/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b04fb8a4-b366-4b55-9d4c-6f054fa58a90
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4c232ea6bd25f1f13fe8e322719cda6388da9c0e
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/30/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



ATA Health Center vás vyvoláním monitorovacího upozornění informuje, pokud u nasazení ATA dojde k nějakému problému.
Tento článek popisuje všechna monitorovací upozornění jednotlivých komponent včetně příčiny a postupu vedoucího k vyřešení problému.
## Problémy komponenty ATA Center
<a id="ata-center-issues" class="xliff"></a>
### Komponentě ATA Center dochází místo na disku
<a id="ata-center-running-out-of-disk-space" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Na jednotce v počítači s komponentou ATA Center, která slouží k uložení databáze ATA, dochází volné místo.|To znamená, že na tomto pevném disku je méně než 200 GB nebo 20 % volného místa podle toho, která z těchto hodnot je menší. Když ATA zjistí, že na jednotce dochází místo, začne z databáze odstraňovat stará data. Pokud nemůže stará data odstranit, protože pořád tato data potřebuje pro detekční modul, zobrazí se toto upozornění. Když obdržíte toto upozornění, přestane ATA sledovat nové aktivity.|Zvětšete velikost jednotky nebo na ní uvolněte místo.|Vysoká|
### Neúspěšné odesílání e-mailů
<a id="failure-sending-mails" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Řešení ATA se nedaří odeslat e-mailové oznámení na zadaný poštovní server.|Z ATA nebudou odesílány žádné e-mailové zprávy.|Ověřte konfiguraci serveru SMTP.|Nízká|

### Přetížení komponenty ATA Center
<a id="ata-center-overloaded" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Komponenta ATA Center nedokáže zvládnout množství dat přenášených z komponent ATA Gateway. |ATA Center přestane analyzovat síťový provoz a události. To znamená, že v době, kdy je toto monitorovací upozornění aktivní, je přesnost detekce a profilů snížená.|Zajistěte, aby komponenta ATA Center měla dostatek prostředků. Další podrobnosti ke správnému naplánování kapacity pro ATA Center najdete v článku [Plánování kapacity ATA](ata-capacity-planning.md). Prověřte výkon komponenty ATA Center pomocí článku [Řešení potíží s ATA pomocí čítačů výkonu](troubleshooting-ata-using-perf-counters.md).|Vysoká|

### Neúspěšné připojení k serveru SIEM pomocí protokolu Syslog
<a id="failure-connecting-to-the-siem-server-using-syslog" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Řešení ATA se nedaří odesílat události zadanému serveru SIEM.|To znamená, že ATA Center nemůže serveru SIEM posílat podezřelé aktivity a monitorovací upozornění.|Ověřte, že je [nastavení serveru Syslog správně nakonfigurované](setting-syslog-email-server-settings.md).|Nízká|
### Brzké vypršení platnosti certifikátu komponenty ATA Center
<a id="ata-center-certificate-is-about-to-expire" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Center vyprší za méně než 3 týdny.|Po vypršení platnosti certifikátu přestane fungovat připojení z komponent ATA Gateway na ATA Center. Proces ATA Center se chybově ukončí a všechny funkce ATA se zastaví.|[Vyměňte certifikát komponenty ATA Center](modifying-ata-center-configuration.md).|Střední|
### Vypršení platnosti certifikátu komponenty ATA Center
<a id="ata-center-certificate-expired" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Center vypršela.|Po vypršení platnosti certifikátu přestane fungovat připojení z komponent ATA Gateway na ATA Center. Proces ATA Center se chybově ukončí a všechny funkce ATA se zastaví.|[Vyměňte certifikát komponenty ATA Center](modifying-ata-center-configuration.md).|Vysoká|
## Problémy komponenty ATA Gateway
<a id="ata-gateway-issues" class="xliff"></a>
### Brzké vypršení platnosti hesla uživatele jen pro čtení
<a id="read-only-user-password-is-about-to-expire" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k rozpoznávání entit ve službě Active Directory, vyprší za méně než 30 dnů.|Pokud platnost hesla tohoto uživatele vyprší, přestanou komponenty ATA Gateway fungovat a nebudou se shromažďovat žádná nová data.|[Změňte heslo pro připojení k doméně](modifying-ata-config-dcpassword.md) a aktualizujte heslo v konzole ATA.|Střední|
### Vypršení platnosti hesla uživatele jen pro čtení
<a id="read-only-user-password-expired" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost hesla uživatele jen pro čtení, který se používá k získání dat z adresáře, vypršela.|Všechny komponenty ATA Gateway přestanou fungovat a nebudou se shromažďovat žádná nová data.|[Změňte heslo pro připojení k doméně](modifying-ata-config-dcpassword.md) a aktualizujte heslo v konzole ATA.|Vysoká|
### Brzké vypršení platnosti certifikátu komponenty ATA Gateway
<a id="ata-gateway-certificate-about-to-expire" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Gateway vyprší za méně než 3 týdny.|Připojení z konkrétní komponenty ATA Gateway na ATA Center selže. Z této komponenty ATA Gateway se nebudou odesílat žádná data.|Certifikát komponenty ATA Gateway by se měl obnovit automaticky. Prohlédněte si protokoly komponent ATA Gateway a ATA Center a zjistěte, proč se tento certifikát automaticky neobnovil.|Střední|

### Vypršení platnosti certifikátu komponenty ATA Gateway
<a id="ata-gateway-certificate-expired" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Platnost certifikátu komponenty ATA Gateway vypršela.|Tato komponenta ATA Gateway nemá žádné připojení na ATA Center. Z této komponenty ATA Gateway se nebudou odesílat žádná data.|[Odinstalujte a znovu nainstalujte ATA Gateway](install-ata-step3.md).|Vysoká|
### Nepřiřazený synchronizátor domény
<a id="domain-synchronizer-not-assigned" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|K žádné komponentě ATA Gateway není přiřazený synchronizátor domény. K tomu může dojít, pokud žádná komponenta ATA Gateway není nakonfigurovaná jako kandidát na synchronizátora domény.|Pokud se doména nesynchronizuje, můžou změny entit způsobit, že informace o entitách v ATA jsou zastaralé nebo chybí, nijak to ale neovlivní detekci.|Zajistěte, aby alespoň jedna komponenta ATA Gateway byla nastavená jako [synchronizátor domény](install-ata-step5.md).|Nízká|
### Nedostupnost všech nebo některých síťových adaptérů pro zachytávání na ATA Gateway
<a id="allsome-of-the-capture-network-adapters-on-an-ata-gateway-are-not-available" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Všechny nebo některé vybrané síťové adaptéry pro zachytávání na ATA Gateway jsou zakázané nebo odpojené.|ATA Gateway už nezachytává síťový provoz všech nebo některých řadičů domény. To bude mít vliv na schopnost detekce podezřelých aktivit souvisejících s těmito řadiči domény.|Zajistěte, aby vybrané síťové adaptéry pro zachytávání byly na ATA Gateway povolené a připojené.|Střední|
### ATA Gateway se nemůže připojit k některým řadičům domény
<a id="some-domain-controllers-are-unreachable-by-a-ata-gateway" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|ATA Gateway má omezenou funkčnost kvůli problémům s připojením k některým nakonfigurovaným řadičům domény.|Pokud ATA Gateway nemůže dotazovat některé řadiče domény, může být detekce předání hodnoty hash (Pass-the-Hash) méně přesná.|Zajistěte funkčnost řadičů domény a ověřte, že tato komponenta ATA Gateway může vůči nim otevřít připojení LDAP.|Střední|
### ATA Gateway se nemůže připojit k žádnému řadiči domény
<a id="all-domain-controllers-are-unreachable-by-a-ata-gateway" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|ATA Gateway je momentálně offline kvůli problémům s připojením ke všem nakonfigurovaným řadičům domény.|To bude mít vliv na schopnost detekce podezřelých aktivit souvisejících s řadiči domény, které tato komponenta ATA Gateway monitoruje.| Zajistěte funkčnost řadičů domény a ověřte, že tato komponenta ATA Gateway může vůči nim otevřít připojení LDAP.|Střední|
### Komponenta ATA Gateway přestala komunikovat
<a id="ata-gateway-stopped-communicating" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Z komponenty ATA Gateway nepřichází žádná komunikace. Výchozí časové rozpětí tohoto upozornění je 5 minut.|Síťový adaptér na této komponentě ATA Gateway už nezachytává síťový provoz. To bude mít vliv na schopnost detekce podezřelých aktivit, protože síťový provoz se nedostane na ATA Center.|Zkontrolujte, že port použitý ke komunikaci mezi komponentou ATA Gateway a službou ATA Center není blokovaný směrovači nebo firewally.|Střední|
### Z řadiče domény se nepřijímá žádný provoz
<a id="no-traffic-received-from-domain-controller" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Přes tuto komponentu ATA Gateway nebyl z řadiče domény přijat žádný provoz.|To může značit, že zrcadlení portů z doménových řadičů na ATA Gateway ještě není nakonfigurované nebo nefunguje.|Ověřte, že je na [síťových zařízeních správně nakonfigurované zrcadlení portů](configure-port-mirroring.md).|Střední|
### Některé předané události se neanalyzují
<a id="some-forwarded-events-are-not-being-analyzed" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|ATA Gateway přijímá více událostí, než dokáže zpracovat.|Některé předané události se neanalyzují, což může mít vliv na schopnost detekce podezřelých aktivit pocházejících od řadičů domény, které tato komponenta ATA Gateway monitoruje.|Ověřte, že se na ATA Gateway předávají jen požadované události, nebo zkuste některé z těchto událostí předávat na jinou komponentu ATA Gateway.|Střední|
### Některý síťový provoz se neanalyzuje
<a id="some-network-traffic-is-not-being-analyzed" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|ATA Gateway přijímá více síťového provozu, než dokáže zpracovat.|Některý síťový provoz se neanalyzuje, což může mít vliv na schopnost detekce podezřelých aktivit pocházejících od řadičů domény, které tato komponenta ATA Gateway monitoruje.|Podle potřeby zvažte [přidání dalších procesorů a paměti](ata-capacity-planning.md). Pokud se jedná o samostatnou komponentu ATA Gateway, snižte počet monitorovaných řadičů domény.|Střední|

### Zastaralá verze ATA Gateway
<a id="ata-gateway-version-outdated" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|ATA Center je novější než verze nainstalovaná na komponentě ATA Gateway. ATA Gateway kvůli tomu přestane fungovat podle očekávání.|To může mít vliv na schopnost detekce podezřelých aktivit pocházejících z řadičů domény, které tato komponenta ATA Gateway monitoruje.|Aktualizujte ATA Gateway automaticky na nejnovější verzi povolením [automatických aktualizací](install-ata-step1.md) v konzole ATA nebo stažením nejnovějšího balíčku ATA Gateway v konzole ATA.|Vysoká|
### Službu ATA Gateway se nepodařilo spustit
<a id="ata-gateway-service-failed-to-start" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Službu ATA Gateway se po nejméně 30 minut nepodařilo spustit.|To může mít vliv na schopnost detekce podezřelých aktivit pocházejících z řadičů domény, které tato komponenta ATA Gateway monitoruje.|Prohlédněte si protokoly komponenty ATA Gateway a [zjistěte původní příčinu chyby služby ATA Gateway](troubleshooting-ata-using-logs.md).|Vysoká|
## Lightweight Gateway
<a id="lightweight-gateway" class="xliff"></a>
### Komponenta Lightweight ATA Gateway dosáhla limitu paměti
<a id="lightweight-ata-gateway-reached-a-memory-resource-limit" class="xliff"></a>
|Výstraha|Popis|Řešení|Závažnost|
|----|----|----|----|
|Komponenta Lightweight ATA Gateway se zastavila a automaticky se restartuje, aby řadič domény chránila před stavem nedostatku paměti.|Lightweight ATA Gateway si vynucuje omezení paměti, aby řadič domény chránila před omezením prostředků. To se stane, když má řadič domény velkou spotřebu paměti. Data z tohoto řadiče domény jsou monitorovaná jen částečně.|Zvětšete kapacitu paměti (RAM) řadiče domény nebo do této lokality přidejte další řadiče domény, aby zatížení tohoto řadiče domény bylo rovnoměrněji rozdělené.|Střední|


## Viz také
<a id="see-also" class="xliff"></a>
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

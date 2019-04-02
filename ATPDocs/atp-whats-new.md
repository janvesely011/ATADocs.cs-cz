---
title: Co je nového ve službě Azure Advanced Threat Protection (služby Azure ATP) | Dokumentace Microsoftu
description: Popisuje nejnovější verze ochrany ATP v programu Azure a poskytuje informace o novinkách v jednotlivých verzích.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/31/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ec0a64b0b4467ae27642dd59281b150fc6953f64
ms.sourcegitcommit: db60935a92fe43fe149f6a4d3114fe0edaa1d331
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/01/2019
ms.locfileid: "58764065"
---
# <a name="whats-new-in-azure-atp"></a>Co je nového v Azure ATP

## <a name="azure-atp-release-272"></a>Verze ochrany ATP v programu Azure 2.72
Vydáno 31. března 2019

- **Vylepšení funkce: Obor hloubka cesty laterální pohyb (LMP)**<br>
Cesty taktiky Lateral Movement (LMP) jsou klíče metodu zjišťování hrozeb a rizika v Azure ATP. Zajistit, aby byl aktivní na největší rizika nejcitlivější uživatelům, tato aktualizace umožňuje jednodušší a rychlejší analyzujte a náprava ohrožení citlivých uživatelů na jednotlivých LMP tím, že omezíte rozsah a hloubka každý graf zobrazí.   

    Zobrazit [cesty taktiky Lateral Movement](use-case-lateral-movement-path.md) Další informace o tom, jak ochrany ATP v programu Azure používá LMPs na povrchu přístup riziko pro každou entitu ve vašem prostředí.   

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-271"></a>Verze ochrany ATP v programu Azure 2.71
Vydáno 24. března 2019

- **Vylepšení funkce: Síť název řešení ÚTOKŮ výstrah monitorování**<br>
Monitorovací upozornění byly přidány pro přidružené výstrahy zabezpečení ochrany ATP v programu Azure, které jsou založeny na NNR úrovně spolehlivosti. Každé monitorování upozornění obsahuje praktické a podrobné doporučení, který vám pomůže vyřešit nízké úspěšnosti NNR. 

    Zobrazit [novinky překlad síťových názvů](atp-nnr-policy.md) získat další informace o používání služby Azure ATP ÚTOKŮ a proč je důležité pro přesnost výstrah. 

- **Podpora serveru: Podpora přidání pro 2019 serveru s využitím KB4487044**<br>
Byla přidána podpora pro použití systému Windows Server 2019, s úroveň opravy KB4487044. Použití serveru 2019 bez opravy není podporována a blokovaný od této aktualizace. 

- **Vylepšení funkce: Upozornění vyloučení založené na uživatelích**<br>
– Možnosti vyjmutí rozšířené výstrah nyní umožňují vyloučení konkrétních uživatelů z konkrétní výstrahy. Vyloučení může pomoci zabránit situacích, kde použití nebo konfigurace určitých typů interní opakovaně aktivuje Výstrahy neškodné zabezpečení.

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-270"></a>Verze ochrany ATP v programu Azure 2.70
Vydáno 17. březnu 2019

- **Vylepšení funkce: Úroveň spolehlivosti název řešení ÚTOKŮ sítě je přidán do více výstrah**<br> Překlad síťových názvů nebo (NNR) slouží ke snadnější identifikaci identity entity zdroje podezřelý útoků. Přidáním úrovně spolehlivosti NNR do služby Azure ATP výstrah důkazy seznamů můžete nyní okamžitě vyhodnotit a zjistili, jakou úroveň spolehlivosti NNR týkající se možných zdrojů identifikovat a opravit odpovídajícím způsobem. 

    Legitimace úrovně spolehlivosti NNR byl přidán do následující výstrahy:
  - [Mapování sondování sítě (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)
  - [Krádež identity podezřelého softwaru (pass-the-ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018) 
  - [Podezření na útok relay NTLM (účet Exchange) – preview](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview)
  - [Podezřelý útok DCSync (replikace adresářových služeb)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)

- **Další stav výstrahy scénář: Azure službu sensor ochrany ATP v programu se nepodařilo spustit**<br>V případech, kdy se nespustila kvůli sítě zachytávání ovladačem senzoru služby Azure ATP se teď aktivuje upozornění na stav senzoru. [Řešení potíží senzoru služby Azure ATP s protokoly ochrany ATP v programu Azure](troubleshooting-atp-using-logs.md) Další informace o protokolech ochrany ATP v programu Azure a způsob jejich použití. 
  
- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-269"></a>Verze ochrany ATP v programu Azure 2.69
Vydáno 10. března 2019

- **Vylepšení funkce: Upozornění (pass-the-ticket) krádeží podezřelý identity**<br> Toto upozornění se teď nabízí nové poznatky s podrobnostmi o připojení pomocí protokolu vzdálené plochy (RDP). Přidání důkazy usnadňuje napravit známý problém (B-TP) Benign True pozitivní výstrahy způsobené použití vzdáleného Credential Guard přes připojení RDP. 

- **Vylepšení funkce: Vzdálené spuštění kódu přes upozornění DNS**<br> Toto upozornění se teď nabízí nové poznatky ukazující stav aktualizace zabezpečení informací, kdy mají být aktualizace požadované řadiče domény.   

- **Funkce nové dokumentace: Azure MITRE at upozornění zabezpečení ochrany ATP v programu & CK Matrix™**<br>

    Vysvětlují a zjednodušíme proces mapování vztah mezi výstrah zabezpečení služby Azure ATP a zkušenosti MITRE AT & gentní Zámek matice, přidali jsme relevantní MITRE techniky pro výpisy výstrah zabezpečení služby Azure ATP. Tento odkaz na další usnadňuje pochopit techniku podezřelý útok potenciálně používán, když se aktivuje upozornění zabezpečení služby Azure ATP. Další informace o [Průvodce výstrah zabezpečení služby Azure ATP](suspicious-activity-guide.md).  

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-268"></a>Verze ochrany ATP v programu Azure 2.68
3. března 2019 všeobecně dostupné

- **Vylepšení funkce: Podezření na útok hrubou silou upozornění útoku (LDAP)**<br>
Vylepšení použitelnosti významné provedly se tato výstraha zabezpečení, včetně revidované popis, zřídit další zdroje informací a podrobnosti pokusů o uhádnutí pro rychlejší opravy. Další informace o [vzbuzovat podezření na útok hrubou silou (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004) výstrahy zabezpečení. 

- **Funkce nové dokumentace: Oznámení testovacího prostředí zabezpečení**<br>

    Výkon služby Azure ATP vysvětlují zjistit skutečné hrozby pro vaše pracovní prostředí, přidali jsme novou **lab výstrah zabezpečení** do této dokumentace. **Lab výstrah zabezpečení** vám pomůže rychle nastavit testovací prostředí nebo testovací prostředí a vysvětluje, nejlepší obranné posturing proti common, skutečná hrozeb a útoků.  

    [Podrobné lab](atp-playbook-lab-overview.md) je navržený tak, aby strávíte minimální čas při vytváření a další čas získání informací o světě hrozeb a k dispozici oznámení služby Azure ATP a ochrany. Jsme rádi bychom znali váš názor.

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-267"></a>Verze ochrany ATP v programu Azure 2.67
Vydáno 24. února 2019

- **Nová výstraha zabezpečení: Rekognoskace instančního objektu zabezpečení (LDAP) – (preview)**<br>

    Azure ATP [rekognoskace instančního objektu zabezpečení (LDAP) – ve verzi preview](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038---preview) výstraha zabezpečení je teď ve verzi public preview. <br> V této detekce se aktivuje upozornění zabezpečení služby Azure ATP při použití instančního objektu zabezpečení rekognoskace útočníci získat důležité informace o prostředí domény. Tyto informace pomáhají útočníci namapovat na doménovou strukturu, stejně jako identifikovat privilegovaných účtů pro použití v dalších krocích v jejich řetězu událostí útoku. 

    Adresář přístup protokolu LDAP (Lightweight) je nejoblíbenější metody používá pro účely legitimní a škodlivý dotaz službě Active Directory. LDAP, zaměřuje zabezpečení, rekognoskace instančního objektu se často používá jako první fáze Kerberoasting útoku. Útoky Kerberoasting slouží k získání seznamu cílové názvy objektu zabezpečení (SPN), což útočníci se pak pokusí získat lístky Server udělování lístků (TGS) pro.

- **Vylepšení funkce: Výstraha rekognoskace (NTLM) výčtu účtů** <br> 
    Vylepšené **účet rekognoskace výčet (NTLM)** výstrah pomocí další analýzy a vylepšenou detekční logiku ke snížení **B-TP** a **FP** jejich výsledky. 
 
- **Vylepšení funkce: Výstraha rekognoskace (DNS) mapování sítě** <br>
    Nové typy detekcí přidán do výstrahy rekognoskace (DNS) mapování sítě. Kromě zjišťování podezřelých žádosti AXFR ochrany ATP v programu Azure teď detekuje podezřelé typy požadavků pocházejících z jiné servery než DNS pomocí odesílá nadměrný počet požadavků.

 - Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-266"></a>Verze ochrany ATP v programu Azure 2,66
Vydáno 17. února 2019

- **Vylepšení funkce: Podezřelý upozornění DCSync útoku (replikace adresářových služeb)**<br>
Vylepšení použitelnosti byly provedeny na tuto výstrahu zabezpečení, včetně revidované popis zřídit další zdroje informací, nové infografika a další fakta. Další informace o [DCSync vzbuzovat podezření na útok (replikace adresářových služeb)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006) výstrahy zabezpečení. 

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-265"></a>Verze ochrany ATP v programu Azure 2.65
Vydáno 10. února 2019

- **Nová výstraha zabezpečení: Podezření na útok přenosového protokolu NTLM (účet Exchange) – (preview)**<br>
Azure ATP [útoku relay vzbuzovat podezření na NTLM (účet Exchange) – ve verzi preview](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview) výstraha zabezpečení je teď ve verzi public preview. <br> V této detekce se aktivuje upozornění zabezpečení služby Azure ATP při zjištění použijte přihlašovací údaje účtu Exchange z podezřelých zdroje. Tyto typy útoků pokusí využít techniky NTLM relay k získání oprávnění exchange řadič domény a jsou označovány jako **ExchangePriv**. Další informace o **ExchangePriv** techniku z [ADV190007 poradce](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV190007) publikován do 31. ledna 2019 a [odpovědi upozornění služby Azure ATP](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/How-to-win-the-latest-security-race-over-NTLM-relay/ba-p/334511).  

- **Obecná dostupnost: Vzdálené spuštění kódu v DNS**<br>
Tato výstraha je teď ve verzi GA (obecná dostupnost). Další informace a výstrah funkce, najdete v článku [vzdálené spuštění kódu v popisu výstrahy na stránce DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036). 

- **Obecná dostupnost: Průsak dat ven přes protokol SMB**<br>
Tato výstraha je teď ve verzi GA (obecná dostupnost). Další informace a výstrah funkce, najdete v článku [průsak dat ven přes SMB popis výstrahy stránky](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030).


- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-264"></a>Verze ochrany ATP v programu Azure 2.64
vydáno 4. února 2019

- **Obecná dostupnost: Podezřelé použití Golden Ticket (ticket anomálií)**<br>
Tato výstraha je teď ve verzi GA (obecná dostupnost). Další informace a výstrah funkce, najdete v článku [podezřelý Golden Ticket využití (ticket anomálií) popis výstrahy stránky](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032). 

- **Vylepšení funkce: Mapování sondování sítě (DNS)**<br>
Vylepšená logika upozornění detekce nasazení pro tuto výstrahu, chcete-li minimalizovat false pozitivní a rušivé výstrahy. Tato výstraha teď má období učení z osm dní, než se upozornění aktivují pravděpodobně poprvé. Další informace o této výstraze najdete v části [síťové mapování rekognoskace (DNS) popis výstrahy stránky](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007). 

    **Z důvodu vylepšení této výstrahy musí metoda nslookup už nebude používat k testování připojení služby Azure ATP během počáteční konfigurace.** 

- **Vylepšení funkce:**<br>
Tato verze zahrnuje přepracovaný stránek výstrah a nové poznatky, poskytuje lepší výstrahy vyšetřování. 
    - [Podezřelý útok hrubou silou (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)
    - [Podezření na stránce Golden Ticket využití (čas anomálií) popis výstrahy](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)
    - [Podezření na útok overpass-the-hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)
    - [Podezřelé použití Metasploit hacking framework](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)
    - [Podezření na útok WannaCry ransomwaru](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.


## <a name="azure-atp-release-263"></a>Verze ochrany ATP v programu Azure 2.63
Vydáno 27. ledna 2019

- **Nová funkce: Nedůvěryhodné doménové struktuře podpora – (preview)**<br>
Podpora Azure ATP senzorů v nedůvěryhodných doménových strukturách je teď ve verzi public preview. Z portálu služby Azure ATP **adresářové služby** proveďte další sadu pověření k povolení ochrany ATP v programu Azure senzorů k připojení do různých doménových strukturách služby Active Directory a nahlásit službě ochrana ATP v programu Azure. Zobrazit [více doménovými strukturami služby Azure ATP](atp-multi-forest.md) Další informace. 

- **Nová funkce: Pokrytí řadiče domény**<br>
Ochrana ATP v programu Azure nyní poskytuje informace o pokrytí pro služby Azure ATP monitoruje řadiče domény.  
Z portálu služby Azure ATP **senzorů** stránce, zobrazí se počet řadičů domény monitorovaných a nemonitorované detekoval ochrany ATP v programu Azure ve vašem prostředí. Stažení seznamu řadič domény monitorovaných k další analýze a k vytváření akční plán. Najdete v článku [monitorování řadiče domény](atp-sensor-monitoring.md) příručce s postupy pro další informace. 

- **Vylepšení funkce: Rekognoskace výčtu účtů**<br>
Detekce rekognoskace výčet účtů služby Azure ATP teď detekuje a vydá upozornění pro pokusy o výčet pomocí protokolů Kerberos a NTLM. Dříve zjišťování pouze pracoval pro pokusy o s použitím protokolu Kerberos. Zobrazit [ochrany ATP v programu Azure rekognoskace výstrahy](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003) Další informace. 

- **Vylepšení funkce: Výstraha Pokus o spuštění vzdáleného kódu**<br>
    - Všechny vzdálené spuštění aktivity, jako je například vytvoření služby, spuštění WMI a nové **Powershellu** provádění, byly přidány na časovou osu profil cílového počítače. Cílový počítač je že řadič domény příkazu se provedl u. 
    - **Prostředí PowerShell** spuštění byl přidán do seznamu uvedená v upozornění ose profil entity aktivity spuštění vzdáleného kódu.
    - Zobrazit [pokus o spuštění vzdáleného kódu](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019) Další informace.  

- **Problém LSASS 2019 Windows serveru a služby Azure ATP**<br>
V reakci na zpětnou vazbu od zákazníků týkající se používání služby Azure ATP s řadiče domény se systémem Windows Server 2019 tato aktualizace zahrnuje další logiku ke neměl spouštět ohlášené chování na počítačích systému Windows Server 2019. Plnou podporu pro senzoru služby Azure ATP 2019 systému Windows Server je plánovaná pro budoucí aktualizace ochrany ATP v programu Azure, ale instalaci a používání služby Azure ATP 2019 servery Windows **není** v tuto chvíli nepodporuje. Zobrazit [požadavky senzoru služby Azure ATP](atp-prerequisites.md#azure-atp-sensor-requirements) Další informace. 

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.


## <a name="azure-atp-release-262"></a>Verze ochrany ATP v programu Azure 2.62
Vydáno 20. ledna 2019

- **Nová výstraha zabezpečení: Vzdálené spuštění kódu nad DNS – (preview)**<br>
Azure ATP [vzdálené spuštění kódu nad DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036) výstraha zabezpečení je teď ve verzi public preview. <br> V této detekce se aktivuje upozornění zabezpečení služby Azure ATP při dotazy DNS vzbuzovat podezření na zneužití ohrožení zabezpečení [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) se provádí na řadiči domény v síti.

- **Vylepšení funkce: 72 hodin zpožděné aktualizace senzorů** <br> Změněné možnost zpoždění senzor aktualizací na vybrané senzory až 72 hodin (místo předchozích 24 hodin zpožděním) po každé aktualizaci verze služby Azure ATP. Zobrazit [aktualizace senzoru služby Azure ATP](sensor-update.md) pokyny ke konfiguraci. 


- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-261"></a>Verze ochrany ATP v programu Azure 2.61
Vydáno 13. ledna 2019

- **Nová výstraha zabezpečení: Průsak dat ven přes protokol SMB - (preview)**<br>
Azure ATP [průsak dat ven přes protokol SMB](atp-exfiltration-alerts.md) výstraha zabezpečení je teď ve verzi public preview. <br> Útočníci s právy správce domény může ohrozit účet KRBTGT. Pomocí účtu KRBTGT, útočníci můžete vytvořit lístek Kerberos udělující lístek (TGT), který poskytuje autorizaci k jakémukoli prostředku. 


- **Vylepšení funkce: Pokus o spuštění vzdáleného kódu** výstraha zabezpečení <br> Nový popis výstrahy a další důkazy byly přidány do srozumitelnější výstrahy a poskytovat lepší šetření pracovních postupů. 


- **Vylepšení funkce: Logické aktivity dotaz DNS** <br>Další dotaz typy byly přidány do [ochrany ATP v programu Azure monitorovat aktivity](monitored-activities.md) včetně: **TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**. 

- **Vylepšení funkce: Podezřelý Golden Ticket využití (ticket anomálií) a podezřelý Golden Ticket (neexistující účet)** <br>
Vylepšenou detekční logiku použil se pro obě výstrahy pro snížení počtu výstrah FP a poskytovat přesnější výsledky.

- **Vylepšení funkce: Dokumentace k Azure ATP výstraha zabezpečení** <br>
Byl rozšířené ochrany ATP v programu zabezpečení výstrah dokumentace ke službě Azure a i na lepší popisech výstrah, přesnější upozornění klasifikace a vysvětlení, opravy, a ochrany před únikem informací. Seznamte se s nové výstrahy dokumentaci návrhu zabezpečení pomocí následujících odkazů: 
    - [Výstrahy zabezpečení služby Azure ATP](suspicious-activity-guide.md)
    - [Porozumění výstrahám zabezpečení](understanding-security-alerts.md)
        - [Upozornění fáze rekognoskace](atp-reconnaissance-alerts.md)
        - [Ohrožení zabezpečení přihlašovacích údajů Fáze oznámení](atp-compromised-credentials-alerts.md)
        - [Laterální pohyb fáze oznámení](atp-lateral-movement-alerts.md)
        - [Upozornění fáze dominance v doméně](atp-domain-dominance-alerts.md)
        - [Fáze oznámení průsak ven](atp-exfiltration-alerts.md)
    - [Prošetřování počítačů](investigate-a-computer.md)
    - [Prošetřování uživatelů](investigate-a-user.md)

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.


## <a name="azure-atp-release-260"></a>Verze ochrany ATP v programu Azure 2,60
Vydáno 6. ledna 2019

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-259"></a>Verze ochrany ATP v programu Azure 2.59
Vydáno 16 dne 2018

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.


## <a name="azure-atp-release-258"></a>Verze ochrany ATP v programu Azure 2.58

Vydáno 9. prosince 2018

- **Vylepšení upozornění zabezpečení: Neobvyklá implementace protokolu upozornění rozdělení**<br>
Azure ATP řadu výstrah zabezpečení neobvyklé implementace protokolu, které dříve sdíleli, 1 externalId (2002), jsou teď rozdělit do čtyř rozlišovací výstrahy, s odpovídající jedinečného externího ID. 

### <a name="new-alert-externalids"></a>Nové výstrahy externalIds

> [!div class="mx-tableFixed"] 

|Nový název výstrahy zabezpečení|Předchozí název výstrahy zabezpečení|Jedinečné ID externí|
|---------|----------|---------|
|Podezřelý útok hrubou silou (SMB)|Neobvyklá implementace protokolu (potenciální použití škodlivých nástrojů, jako je Hydra)|2033
|Podezření na útok overpass-the-hash (Kerberos)|Neobvyklá implementace protokolu Kerberos (možný útok overpass-the-hash)|2002|
|Podezřelé použití Metasploit hacking framework|Neobvyklá implementace protokolu (potenciální použijte Metasploit hacking nástroje)|2034
|Podezření na útok WannaCry ransomwaru|Neobvyklá implementace protokolu (možný útok ransomwarem WannaCry)|2035
|

- **Nové monitorované aktivity: Kopírování souborů přes protokol SMB**<br>
Kopírování souborů přes protokol SMB je nyní monitorované a filtrovat aktivity. Další informace o tom, které [aktivity ochrany ATP v programu Azure monitoruje](monitored-activities.md)a jak [filtru a vyhledávání monitorování aktivity](atp-activities-search.md) na portálu. 

- **Velký obrázek rozšíření cesty laterální pohyb**<br>
Při zobrazení cesty taktiky Lateral Movement velké, ochrana ATP v programu Azure nyní zvýrazňuje pouze uzly, které jsou připojené k vybrané entity, namísto rozostření do dalších uzlů. Tato změna přináší přináší značné vylepšení v velké LMP rychlost vykreslování. 

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-257"></a>Verze ochrany ATP v programu Azure 2.57
Vydáno 2. prosince 2018

- **Nová výstraha zabezpečení: Podezřelý anomálií použití lístku Golden ticket (preview)**<br>
Azure ATP [podezřelý Golden Ticket použití – lístek anomálií](suspicious-activity-guide.md) výstraha zabezpečení je teď ve verzi public preview. <br> Útočníci s právy správce domény může ohrozit účet KRBTGT. Pomocí účtu KRBTGT, útočníci můžete vytvořit lístek Kerberos udělující lístek (TGT), který poskytuje autorizaci k jakémukoli prostředku. 
<br>Tato falešných lístků TGT se nazývá "Zlatých lístků", protože to útočníkům umožňuje dosáhnout trvalého trvalost sítě. Falešných Zlatých lístků tohoto typu mají jedinečné charakteristiky, které tato nové detekce slouží k identifikaci. 


- **Vylepšení funkce: Automatické vytvoření instance (pracovní prostor) služby Azure ATP** <br>
Od dnešního dne, ochrana ATP v programu Azure *pracovní prostory* se přejmenovat ochrany ATP v programu Azure *instance*. Ochrana ATP v programu Azure teď podporuje jednu instanci služby Azure ATP jeden účet služby Azure ATP. Instance pro nové zákazníky jsou vytvořené pomocí Průvodce vytvořením instance v [ochrany ATP v programu Azure portal](https://portal.atp.azure.com). Existujícím pracovním prostorům ochrany ATP v programu Azure se automaticky převedou na instance služby Azure ATP s touto aktualizací.  

  - Zjednodušené vytváření instance pro rychlejší nasazení a ochranu pomocí [vytvořit instanci služby Azure ATP](install-atp-step1.md). 
  - Všechny [ochrany osobních údajů a dodržování předpisů](atp-privacy-compliance.md) zůstává stejná. 

  Další informace o instancích ochrany ATP v programu Azure najdete v tématu [vytvořit instanci služby Azure ATP](install-atp-step1.md). 

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-256"></a>Verze ochrany ATP v programu Azure 2.56
Vydáno 25. listopadu 2018


- **Vylepšení funkce: Cesty taktiky Lateral Movement (LMPs)** <br>
K rozšíření možností Azure ochrany ATP v programu laterální pohyb cestu (LMP) jsou přidány dvě další funkce:

  - Historie LMP jsou nyní uloženy a dostupnější za entity a pomocí LMP sestavy. 
  - Postupujte podle entity v LMP prostřednictvím časové osy aktivity a prozkoumat pomocí dalších důkazu zjišťování potenciální útok cesty. 

  Zobrazit [cesty taktiky Lateral Movement ochrany ATP v programu Azure](use-case-lateral-movement-path.md) Další informace o tom, jak používat a prozkoumat pomocí rozšířené LMPs. 

- **Dokumentace k vylepšení: Cesty taktiky Lateral Movement, názvy výstraha zabezpečení**<br> Přidání a aktualizace byly provedeny na služby Azure ATP články s popisem cesty laterální pohyb popisy a funkce, název se přidá mapování pro všechny instance starých názvy výstrah zabezpečení nové názvy a externalIds. 
  - V tématu [cesty taktiky Lateral Movement ochrany ATP v programu Azure](use-case-lateral-movement-path.md), [prozkoumat cesty taktiky Lateral Movement](investigate-lateral-movement-path.md), a [Průvodce výstrah zabezpečení](suspicious-activity-guide.md) Další informace.   

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-255"></a>Verze ochrany ATP v programu Azure 2.55
Vydáno 18. listopadu 2018

- **Výstraha zabezpečení: Podezřelá komunikace prostřednictvím DNS – obecné dostupnosti**<br>
Azure ATP [podezřelá komunikace prostřednictvím DNS](suspicious-activity-guide.md) výstrahy zabezpečení jsou teď obecně dostupné. <br> Protokol DNS ve většině organizací není obvykle, monitorovat a zřídka blokované před škodlivými aktivitami. To umožňuje útočníkovi na napadeném počítači zneužívání protokolu DNS. Škodlivý komunikace prostřednictvím DNS je možné pro průsak dat ven, příkazu a řízení a/nebo omezení úmyslem vyhnout podnikové sítě.

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-254"></a>Verze ochrany ATP v programu Azure 2,54
Vydáno 11. listopadu 2018

- **Vylepšení funkce: Výchozí vyloučení domény přidá do podezřelá komunikace přes upozornění DNS**<br>   Novým rozšířením tři Oblíbené domény do seznamu vyloučení výchozí domény. Seznam vyloučení zůstává plně přizpůsobitelné. Zobrazit [vyloučení entit z detekce](excluding-entities-from-detections.md), další informace. 

- **Dokumentace k vylepšení: Aktualizace protokolu SIEM, pokyny známé problémy**<br>    externalId mapování a další vysvětlení byly přidány do systému SIEM protokolu popisy. Zobrazit [referenční informace k protokolům SIEM](cef-format-sa.md), další informace. <br>Byla přidána další článek pokyny aktuálně nevyřešené známé problémy. Zobrazit, [známé problémy ochrany ATP v programu Azure](known-issues.md), další informace.  

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-253"></a>Verze ochrany ATP v programu Azure 2,53
Vydáno 4. listopadu 2018

- **Vylepšení upozornění zabezpečení: Podezřelé ověřování se nezdařilo**<br>
Azure ATP [podezřelé chyby ověřování zabezpečení upozornění](suspicious-activity-guide.md) teď obsahuje monitorování pro detekci hesla hrubou zařízení vynutit útoky.
V typické **heslo zařízení** útoku, útočníci po úspěšně výčet seznamu platní uživatelé z řadiče domény, zkuste jedno heslo pečlivě vytvořené pro všechny známé uživatelské účty (jedno heslo na více účtů) . Při počáteční heslo zařízení neproběhne úspěšně, bude snaží znovu, využívají jiné heslo pečlivě vytvořený, obvykle po uplynutí 30 minut mezi pokusy. Doba čekání útočníkům umožňuje, aby neměl spouštět nejčastěji podle času účet uzamčení prahové hodnoty. Heslo zařízení se rychle stal oblíbenou technikou útočník a testery pera. Heslo zařízení útoky ukázaly na zajistit efektivitu při získávání počáteční základnu v organizaci a pro následné laterální přesuny pokouší o zvýšení oprávnění. 

- **Vylepšení funkce: Odeslat zprávu Syslog**<br>   Nová možnost odeslat testovací zpráva Syslogu během procesu instalace systému SIEM. Zobrazit [integrace se Syslogem](setting-syslog.md), další informace. 

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-252"></a>Verze ochrany ATP v programu Azure 2.52
Vydáno 28. října 2018


- **Vylepšení upozornění zabezpečení: Pokus o spuštění vzdáleného kódu**<br>
Azure ATP [upozornění na zabezpečení. pokus o vzdálené spuštění kódu](suspicious-activity-guide.md) nyní zahrnuje monitorování podezřelých pokusy o spuštění vzdáleného kódu Powershellu v řadičích domény. Je běžné metody pro provádění platné příkazy pro správu vzdáleného prostředí PowerShell, ale se často používá speciálně při pokusu o spuštění skriptů na vzdálené koncové body. 

- **Vylepšení funkce: Nastavit plánování sestav**
<br>Teď můžete nastavit jenom konkrétní hodiny naplánování sestav pomocí služby Azure ATP [sestavy](reports.md#) funkce. 

- **Přidání konfigurace: Tenant řízení přístupu na základě role (RBAC)**
<br>Konfigurování rolí zabezpečení vašeho tenanta v Centru pro správu Azure Active Directory (AAD) přímo z nové propojení správce portálu ochrany ATP v programu Azure. 

- **Dokumentace k revidované struktuře a obsahu**
<br>Nedávné změny obsahu dokumentace ke službě ochrana ATP v programu Azure zahrnují nových článků, za předpokladu, že úplný seznam všech ochrany ATP v programu Azure monitoruje aktivity, filtrování pokyny pro činnost, jakož i verzí struktury webu Dokumentace pro lepší použitelnost:
  - [Ochrana ATP v programu Sledování aktivitách v Azure](monitored-activities.md) 
  - [Azure ATP aktivity filtrování](atp-activities-search.md) 
  - [Dokumentace ke službě Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/)  

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-251"></a>Verze ochrany ATP v programu Azure 2.51
Vydáno 21. října 2018

- Můžete teď povolit nebo zakázat **ATP v programu WD integrace** z portálu služby Azure ATP [konfigurace](integrate-wd-atp.md#how-to-integrate-azure-atp-with-windows-defender-atp) obrazovky. (Pro přístup k této funkci, musí být uživatel ochrany ATP v programu Azure globální nebo správce zabezpečení v AAD tenanta).

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-250"></a>Verze ochrany ATP v programu Azure 2,50
Vydáno 14. října 2018
- Tato verze obsahuje opravy a vylepšení pro několik problémů.


## <a name="azure-atp-release-249"></a>Verze ochrany ATP v programu Azure 2.49
Vydáno 7. října 2018
-   **Nové detekce: Podezřelá komunikace DNS** (preview)<br>Nové detekce přidána k chrání před útoky komunikace podezřelé DNS:

    -   Tato detekce pomáhá odhalit útoky na protokolu DNS. Protokol DNS není ve většině organizací, monitorovat a zřídka blokované před škodlivými aktivitami. Povoluje se útočník na napadeném počítači zneužívají protokolu DNS. Škodlivý komunikace prostřednictvím DNS je možné pro průsak dat ven, příkaz a ovládací prvek a/nebo omezení úmyslem vyhnout podnikové sítě.

- **Nové funkce** <br>Ochrana ATP v programu Azure **role uživatele** vylepšen o následující funkce:
  - Změna stavu výstrah zabezpečení (znovu otevřete, zavřete, vyloučení, potlačení)
  - Nastavit plánované sestavy
  - Nastavit značky entit (citlivé a honey token)
  - Vyloučení detekce
  - Změnit jazyk
  - Nastavení oznámení prostřednictvím e-mailu nebo protokolu syslog


- Bude častěji docházet **Rekognoskace adresáře pomocí dotazů služby** výstrahy zabezpečení, ke kterým došlo na 16. září 2018 se identifikovat a vyřešit. 

- Tato verze rovněž obsahuje opravy a vylepšení pro několik problémů.


## <a name="azure-atp-release-248"></a>Verze ochrany ATP v programu Azure 2.48
Vydáno 16. září 2018
- **Výstraha zabezpečení:** Rekognoskace pomocí dotazů na adresářové služby

  Tato výstraha zabezpečení teď vylepšili infografiky a doklady. 

- **Vyloučení entit z detekce** 

  Pokud chcete snížit počet falešně pozitivních výsledků, teď můžete vyloučit entity z následujících detekcí: 
  - Podezřelé připojení k síti VPN (vyloučení uživatele)
  - Povýšení řadiče domény podezřelé (možný útok DcShadow)
  - Podezřelá replikace požadavku (možný útok DcShadow)

- Tato verze rovněž obsahuje opravy a vylepšení pro několik problémů.


## <a name="azure-atp-release-247"></a>Verze ochrany ATP v programu Azure 2.47
Vydáno 2. září 2018

- **Rozšířená Kontrola zásad auditu Azure ATP**
 
Azure Advanced Threat Protection teď zkontroluje řadič domény existujících pokročilé zásady auditu a doporučuje změny zásad zajistit maximální pokrytí služeb ochrany ATP v programu Azure pro vaši organizaci. 

**Tato nová kontrola vám umožní:**
  -  Určení události z protokolů událostí Windows, které jsou aktuálně vyloučené z pokrytí ochrany ATP v programu Azure chybí.
  -  Ověřte ideální nastavení a proveďte změny na základě stavu výstrah doporučení, které jsou k dispozici.
  -  Upozornění stavu jednoho agregované něhož budou vydány pro všechny řadiče domény včetně nápravy návrhy (if /, je potřeba).

Kontrola jak [nakonfigurovat pokročilé zásady auditu](atp-advanced-audit-policy.md) pro váš systém správně nakonfigurovaná. 
- Tato verze rovněž obsahuje opravy a vylepšení pro několik problémů.

## <a name="azure-atp-release-246"></a>Verze ochrany ATP v programu Azure 2.46

Vydáno 26. srpna 2018

- Tato verze obsahuje opravy a vylepšení pro několik problémů.

## <a name="azure-atp-release-245"></a>Verze ochrany ATP v programu Azure 2.45

Vydáno 19. srpna 2018

- **Ochrana ATP v programu Azure přidá jako zdroj dalších dat trasování událostí pro Windows (ETW)**  <br> Trasování událostí pro Windows (ETW) přidat jako zdroj dalších dat kromě existující síťový provoz a události Windows. Trasování událostí pro Windows poskytuje detekci další podezřelé aktivity, včetně: povýšení řadiče domény podezřelé a pro replikaci řadiče domény podezřelé žádosti (obojí jsou napadení DCShadow). <br>
Pouze ochrany ATP v programu senzorů nainstalovaná na řadičích domény podpory trasování událostí pro Windows na základě detekce. Detekce trasování událostí pro Windows nepodporuje senzorů samostatné ochrany ATP v programu. <br>  

- **Čtyři nové detekce, nyní ve všeobecné dostupnosti** <br>
  - Podezřelé připojení k síti VPN
  - Protokol Kerberos Golden Ticket – neexistující účet 
  - Povýšení řadiče domény podezřelé (možný útok DcShadow) – zjišťování, k dispozici pouze s senzorů ochrany ATP v programu na základě trasování událostí pro Windows 
  - Žádost o replikaci řadiče domény podezřelé (možný útok DcShadow) – zjišťování, k dispozici pouze s senzorů ochrany ATP v programu na základě trasování událostí pro Windows

- Tato verze rovněž obsahuje opravy a vylepšení pro několik problémů.


## <a name="azure-atp-release-244"></a>Verze ochrany ATP v programu Azure 2.44

Vydáno 12. srpna 2018

- Tato verze obsahuje opravy a vylepšení pro několik problémů.
- Soubory protokolu na počítači senzoru už vytvořili protokol "Statistiky výjimky".


## <a name="azure-atp-release-243"></a>Verze ochrany ATP v programu Azure 2.43

Vydané 5. srpna 2018

- Tato verze obsahuje opravy a vylepšení pro několik problémů.



## <a name="azure-atp-release-242"></a>Verze ochrany ATP v programu Azure 2,42

Vydáno 29. července 2018

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 


## <a name="azure-atp-release-241"></a>Verze ochrany ATP v programu Azure 2.41

Vydáno 22. července 2018

- **Podpora více doménovými strukturami Azure ochrany ATP v programu je postupně zavádí (preview)** <br> Ochrana ATP v programu Azure teď můžete podpořit organizace s více doménovými strukturami, které poskytují možnost monitorování aktivity a profily uživatelů napříč doménovými strukturami. Tato nová funkce umožňuje:

  - Zobrazení a prošetřování aktivity prováděné uživateli napříč více doménovými strukturami z podokně ze skla.
  - Zlepšuje detekci a omezuje počet falešně pozitivních výsledků tím, že poskytuje pokročilé integrace služby Active Directory a účet řešení.
  - Získejte lepší výstrah monitorování a vytváření sestav pro pokrytí napříč organizací.


-   **Nové detekce: DCShadow**<br>Dvě nové detekce byly přidány k ochraně před útoky stínové (DCShadow) řadiče domény:

    -   Povýšení řadiče domény podezřelé (možný útok DCShadow) – tato detekce pomáhá detekovat útoky, ve kterých zosobnit počítače s řadičem domény a pak se pokusí použít replikační změny do ostatních řadičů domény ve vaší doméně.

    -   Podezřelá žádost o replikaci (možný útok DCShadow) – tato detekce, které pomáhá chránit proti útokům, které se pokusil o provedení povýšení řadiče domény z počítačů, které nejsou řadiče domény chcete-li změnit adresářových objektů.

-   **Vylepšené informace oslabení šifrování**<br>Šifrování downgrade detekce nyní poskytuje další informace týkající se konkrétního typu útoku zjistil: overpass-the-hash, zlatý lístek a typu skeleton key. Tyto výstrahy navíc mají byl agregován umožňující snadnější šetření.
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 


## <a name="azure-atp-release-240"></a>Verze ochrany ATP v programu Azure 2,40

Vydáno 15. července 2018

- Detekce pass-the-ticket nyní obsahuje oddíl důkazy na stránce podrobností výstrahy. To poskytuje další informace k prošetření upozornění.

- Příznaky ovládacích prvků přístup uživatele, které najdete v profilu uživatele v adresáři data, nyní obsahují legendu, takže můžete líp pochopit, které atributy jsou a které jsou vypnuté.  

## <a name="azure-atp-release-239"></a>Verze ochrany ATP v programu Azure 2.39

Vydané 5. července 2018
-   **Přidat nové detekce: Kerberos golden ticket - neexistující účet** (preview)<br>Toto nové zjišťování pomáhá chránit vaši organizaci před útoky, ve kterých je vytvořen zlatý lístek Kerberos účtu, který neexistuje ve vaší doméně. Další informace najdete v tématu [Průvodce prošetřováním podezřelých aktivit rozšířené ochrany před internetovými útoky pro Azure](suspicious-activity-guide.md)

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 


## <a name="azure-atp-release-238"></a>Verze ochrany ATP v programu Azure 2,38

Vydáno 1. července 2018

- Tato verze obsahuje opravy a vylepšení pro více problémů a také vylepšení ochrany ATP v programu Azure portal.

## <a name="azure-atp-release-237"></a>Verze ochrany ATP v programu Azure 2.37

Vydáno 24. června 2018

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 

## <a name="azure-atp-release-236"></a>Verze ochrany ATP v programu Azure hodnotu 2,36

Vydáno 17. června 2018

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 


## <a name="azure-atp-release-235"></a>Verze ochrany ATP v programu Azure 2.35

Vydáno 10. června 2018
 
- **Nové ve verzi preview detekce**<br></br>Z nichž lze dodat nové funkce v nyní, bude ochrana ATP v programu Azure využít výhod skutečnost, že je Cloudová služba – rychlá cykly – a poskytneme vám nové detekce nejkratší možné době. Tyto nové detekce byla označená jako "preview" při prvním vydání. Obvykle nové detekce se přesune z verze preview pro obecnou dostupnost během pár týdnů. Ve výchozím nastavení se zobrazí náhled detekcí. Informace o vyjádří svůj nesouhlas najdete v tématu [ve verzi preview detekce](working-with-suspicious-activities.md#preview-detections).
 
- **Podezřelé zjišťování sítě VPN**<br></br>Tato verze přináší předběžnou verzi detekce podezřelých VPN. Ochrana ATP v programu Azure učí chování uživatele sítě VPN, včetně počítačů, uživatelů přihlášených k a umístění, které uživatelé připojit z a vás upozorní, když je odchylky od očekávané chování. Další informace najdete v tématu [detekce podezřelých VPN](suspicious-activity-guide.md).

- **Zpožděné aktualizace**<br></br>Teď máte možnost nastavit ochrana ATP v programu Azure snímačů a aktualizovat později pokaždé, když aktualizace ochrany ATP v programu Azure. Teď můžete nastavit každou senzoru služby Azure ATP **zpožděné aktualizace** tak, aby se aktualizuje po 24 hodinách od aktualizace ochrany ATP v programu Azure cloud service. Tato funkce umožňuje otestovat aktualizaci na konkrétní testovací senzorů a aktualizovat vaše produkční senzorů pouze později. Pokud během první cyklu aktualizací zjistíte problém, otevřete lístek podpory. Další informace najdete v části [ochrany ATP v programu Azure aktualizace senzorů](sensor-update.md).

- **Implementace zjišťování aktualizované neobvyklý protokol**<br></br>Neobvyklý protokol implementace detekce nyní poskytuje další informace. Můžete teď najdete v tématu, které potenciál útoku podezření nástroj ochrany ATP v programu Azure je v práci v síti. Další informace najdete v tématu [Průvodce prošetřováním podezřelých aktivit](suspicious-activity-guide.md).
 
- **Výstraha zastaralé senzor**<br></br>Ochrana ATP v programu Azure zahrnuje nové monitorování výstrahy dali vám vědět, pokud je senzoru více než tři verze zastaralé. Pokud se zobrazí toto upozornění, by měl aktualizovat senzoru nebo prozkoumat, proč se senzor neaktualizují automaticky. Pokud výstrahy se opakuje, odinstalujte a znovu nainstalujte senzoru.

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 

## <a name="azure-atp-release-234"></a>Verze ochrany ATP v programu Azure 2.34

Vydáno 3. června 2018
 
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 

 
## <a name="azure-atp-release-233"></a>Verze ochrany ATP v programu Azure 2,33

Vydáno 27. května 2018

- Funkce ve verzi Preview: Ochrana ATP v programu Azure teď podporuje nové jazyky a 13 nové národní prostředí:
    - Čeština
    - Maďarština
    - italština
    - Korejština
    - Holandština
    - polština
    - Portugalština (Brazílie)
    - Portugalština (Portugalsko)
    - Rusko
    - švédština
    - turečtina
    - Čínština (Čína)
    - Čínština (Tchaj-wan)


## <a name="azure-atp-release-232"></a>Verze ochrany ATP v programu Azure 2.32

Vydáno 13. května 2018
 
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 

## <a name="azure-atp-release-231"></a>Verze ochrany ATP v programu Azure 2.31

Vydáno 6. května 2018
 
- Byly vylepšeny překlad názvů. V rámci tohoto úsilí, kromě aktivního řešení RPC a NetBIOS senzor vydat paket TLS klienta Hello na koncový bod protokolu RDP (3389) portu. 
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 

## <a name="azure-atp-release-230"></a>Verze ochrany ATP v programu Azure 2,30

Vydáno 29. dubna 2018
 
- Podezřelé aktivity oslabení šifrování teď obsahují důkazy oddílu, který popisuje příznaky detekovaných službou ochrany ATP v programu Azure, které ji podezření, že, k čemu aktivita oslabení šifrování. 
-   Ochrana ATP v programu Azure nyní používá Azure Email Orchestrator pro všechny e-mailů z ochrany ATP v programu Azure, včetně podezřelých aktivit monitorování výstrah a sestav. Uvidíte, že tato e-mailová oznámení teď řídí konzistentní formát pro snadné použití a Excelové soubory se propojí s e-mailu ke stažení z konzoly.
 
 
## <a name="azure-atp-release-229"></a>Verze ochrany ATP v programu Azure 2.29

Vydáno 22. dubna 2018
 
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 
 
 
## <a name="azure-atp-release-228"></a>Verze ochrany ATP v programu Azure 2.28

Vydáno 15. dubna 2018
 
-   Uživatelé, kteří jsou členy skupin rolí uživatelů ochrany ATP v programu Azure a prohlížeče ochrany ATP v programu Azure teď mají oprávnění k zobrazení výstrah monitorování.
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 


## <a name="azure-atp-release-227"></a>Verze ochrany ATP v programu Azure 2,27

Vydáno 8. dubna 2018

- Nyní máte možnost k poskytnutí zpětné vazby uživatelů v horním navigačním panelu. Kliknutím na ikonu veselého obličeje v panelu nabídky vám umožní odesílat e-mailu týmu rozšířené ochrany před internetovými útoky pro Azure s vaším názorem.

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 
 

## <a name="azure-atp-release-226"></a>Verze ochrany ATP v programu Azure 2.26

Vydáno 25. března 2018

- Když ochrany ATP v programu Azure upozorňuje vás na podezřelé aktivity, které identifikují jako neškodné pozitivní (legitimní akci, která není podezřelé aktivity) máte možnost vyloučit počítače a IP adresy pro další způsoby detekce, včetně: Oslabení šifrování, útok hrubou silou v protokolu LDAP, podobě zfalšovaných certifikátů PAC, útoky hrubou silou a Pass-the-hash.
-   Byl vylepšen výkon senzoru služby Azure ATP.
-   Nové oblasti pro nasazení pracovního prostoru, přidala se teď můžete nasadit pracovní prostor v Asii. 


## <a name="azure-atp-release-225"></a>Verze ochrany ATP v programu Azure 2.25

Vydáno 18. března 2018

- Vícefaktorové ověřování (MFA) je nyní podporována v ochrany ATP v programu Azure. Tenanty používající MFA nyní můžete zadat na portálu ochrany ATP v programu Azure.
- Ochrana ATP v programu Azure teď má [ **stav systému** ](https://health.atp.azure.com/) stránku, kde přinášejí informace o tom, zda na portálu pro správu pracovního prostoru je aplikace bude aktivní, pokud dojde k problémům s detekcí a senzor je možné odeslat přenosy dat do cloudu. Můžete přistupovat **stav systému** z řádku nabídek služby Azure ATP.


## <a name="azure-atp-release-224"></a>Verze ochrany ATP v programu Azure 2,24

Vydáno 11. března 2018

**Nové a aktualizované detekce**
  - Podezřelé vytvoření služby – útočníci se pokusí spustit podezřelé služby ve vaší síti. Ochrana ATP v programu Azure nyní vydá výstrahu, když zjistí, že někdo v určitém počítači běží novou službu, která se zdá podezřelá. Tato detekce se zakládá na událostech (ne přenosy v síti) a je na všech řadičích domény v síti, které je předávání událostí 7045 do služby Azure ATP. Další informace najdete v článku [Průvodce prošetřováním podezřelých aktivit](suspicious-activity-guide.md).

**Vylepšené šetření**
  - Ochrana ATP v programu Azure zahrnuje bohatších možností [profil entity](entity-profiles.md). Profil entity poskytuje platformu, která je navržená pro podrobné informace o zkoumání aktivity uživatelů, jedná se o prostředky, které k nim přistupovat, počítače, které jsou přihlášeni a mnoho dalších. Profil entity také poskytuje data adresáře a umožní vám identifikovat potenciální cesty taktiky Lateral Movement do nebo z entity, můžete získat další informace o potenciálním porušením ve vaší organizaci.

  - Ochrana ATP v programu můžete ručně značka entity jako *citlivé* k vylepšení detekce a sledování. Toto značení ovlivňuje mnoho detekce ochrany ATP v programu Azure, jako je například detekci úprav citlivých skupin a [cesty laterální pohyb](use-case-lateral-movement-path.md), které využívají entity, které se považují za citlivé.

**Nové sestavy, které pomáhají s prošetřením**
  - [Hesla přístupný ve formátu prostého textu sestavy](reports.md) umožňuje rozpoznat, kdy se služby odeslat přihlašovací údaje k účtu se odesílají v prostém textu. To umožňuje prozkoumat služby a zvýšit úroveň zabezpečení sítě. Tato sestava nahradí výstrahy podezřelá aktivita ve formě prostého textu.
  - [Laterální cesty Lateral Movement k citlivým účtům sestavě](reports.md) obsahuje citlivé účty, které jsou zveřejňovány prostřednictvím cesty taktiky Lateral Movement. To umožňuje zmírnit tyto cesty a posilovat jejich zabezpečení sítě s cílem minimalizovat riziko útoku povrchu. To vám umožňuje zabránit taktiky Lateral Movement tak, aby útočníci nelze přesouvat mezi vaší sítě mezi uživatelé a počítače služby, dokud se přístupů v loterii zabezpečení virtuálních: přihlašovací údaje účtu správce citlivé.

- Můžete teď snadno poskytnout přístup k dokumentaci z odkazu v rámci upozornění na podezřelou aktivitu Chcete-li zobrazit [šetření kroky, které můžete provést](suspicious-activity-guide.md). 

**Vylepšení výkonu**
 -  Senzor infrastruktury služby Azure ATP byla vylepšena z hlediska výkonu: agregovaná zobrazení provozu povolí optimalizaci CPU a paketů kanálu a opětovně používá sockets k řadičům domény, chcete-li minimalizovat relace protokolu SSL řadiči domény.

## <a name="see-also"></a>Viz také
- [Co je Azure Advanced Threat Protection?](what-is-atp.md)
- [Nejčastější dotazy](atp-technical-faq.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

---
title: Co je nového v Azure Advanced Threat Protection (Azure ATP) | Microsoft Docs
description: Tento článek se často aktualizuje, aby vám věděl, co je nového v nejnovější verzi Azure Advanced Threat Protection (Azure ATP).
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 08/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 851aead0a82167a5f7d0f4afb43376e2f343255c
ms.sourcegitcommit: 033ac9277effa00c4423caf6f2a3febd796ca3db
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2019
ms.locfileid: "70052452"
---
# <a name="whats-new-in-azure-advanced-threat-protection-azure-atp"></a>Co je nového v Azure Advanced Threat Protection (ATP Azure)

Tento článek se často aktualizuje, aby vám věděl, co je nového v nejnovější verzi služby Azure ATP.

Informační kanál RSS: Po aktualizaci této stránky se zobrazí oznámení zkopírováním a vložením následující adresy URL do čtečky informačních kanálů:`https://docs.microsoft.com/api/search/rss?search=%22This+article+is+updated+frequently+to+let+you+know+what%27s+new+in+the+latest+release+of+Azure+ATP%22&locale=en-us`

Vydáno 25. srpna 2019

## <a name="azure-atp-release-292"></a>Azure ATP verze 2,92
- Verze zahrnuje vylepšení a opravy chyb pro infrastrukturu interního senzoru.

Vydáno 18. srpna 2019

## <a name="azure-atp-release-291"></a>Azure ATP verze 2,91

- Verze zahrnuje vylepšení a opravy chyb pro infrastrukturu interního senzoru.

Vydáno 11. srpna 2019

## <a name="azure-atp-release-290"></a>Azure ATP verze 2,90

- Verze zahrnuje vylepšení a opravy chyb pro infrastrukturu interního senzoru.

Vydáno 4. srpna 2019

## <a name="azure-atp-release-289"></a>Azure ATP verze 2,89

- **Vylepšení metod senzorů**<br>Aby se zabránilo nadměrnému generování provozu protokolu NTLM při tvorbě přesného přenosu cest LMP (), byly vylepšení pro metody senzoru ATP v Azure, která využívají méně využívání protokolu NTLM a významně využívají protokol Kerberos.  

- **Vylepšení výstrahy: Podezřelé používání lístku (neexistující účet)**<br>Do podporovaných typů legitimace uvedených v tomto typu výstrahy byly přidány změny názvu SAM. Další informace o výstraze, včetně toho, jak zabránit tomuto typu aktivity a opravit, najdete v tématu [podezřelé použití lístku (neexistující účet)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027).

- **Obecná dostupnost: Podezření na manipulaci s ověřováním NTLM**<br> Podezřelá výstraha na [manipulaci s ověřováním NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) už není v režimu náhledu a je teď všeobecně dostupná. 

- Verze zahrnuje vylepšení a opravy chyb pro infrastrukturu interního senzoru.


Vydáno 28. července 2019

## <a name="azure-atp-release-288"></a>Azure ATP verze 2,88 

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

Vydáno 21. července 2019

## <a name="azure-atp-release-287"></a>Azure ATP verze 2,87 

- **Vylepšení funkcí: Automatizovaná kolekce událostí syslog pro samostatné senzory Azure ATP**<br> Příchozí připojení syslog pro samostatné senzory Azure ATP jsou teď plně automatizovaná a při odebrání možnosti přepínacího tlačítka z obrazovky konfigurace. Tyto změny nemají žádný vliv na odchozí připojení syslog. 

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-286"></a>Azure ATP verze 2,86 

Vydáno 14. července 2019

- **Nové upozornění zabezpečení: Podezření na manipulaci s ověřováním NTLM (externí ID 2039)**<br>
Nově podezřelá výstraha zabezpečení [ověřování NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) v Azure ATP je teď ve verzi Public Preview. <br> V tomto detekci se aktivuje výstraha zabezpečení Azure ATP, pokud použití útoku "man-in-the-middle" vychází z úspěšného obejít kontrolu integrity zprávy NTLM (MIC), což je zabezpečení popsané v Microsoft [CVE-2019-040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040). Tyto typy útoků se snaží o downgrade funkcí zabezpečení NTLM a jejich úspěšné ověření s konečným cílem provést úspěšné navýšení pohybů. 

- **Vylepšení funkcí: Identifikace operačního systému obohaceného zařízení**<br> Dokud teď služba Azure ATP poskytla informace o operačním systému zařízení entity na základě dostupného atributu ve službě Active Directory. Pokud se dřív ve službě Active Directory nepoužily informace o operačním systému, tyto informace byly na stránkách entit ATP Azure také nedostupné. Od této verze poskytuje Azure ATP tyto informace pro zařízení, ve kterých služba Active Directory nemá informace, nebo nejsou zaregistrovaná ve službě Active Directory pomocí metod identifikace operačního systému obohaceného zařízení. 
 
    Přidání identifikačních dat operačního systému obohaceného zařízení pomáhá identifikovat neregistrovaná zařízení, která nejsou registrovaná, a současně se zasílat do procesu šetření. Další informace o překladu síťových názvů v Azure ATP najdete v tématu [Principy překladu názvu sítě (útoků)](atp-nnr-policy.md).  

- **Nová funkce: Ověřený proxy server – Preview**<br> Azure ATP teď podporuje ověřený proxy server. Zadejte adresu URL proxy serveru pomocí příkazového řádku senzoru a zadejte uživatelské jméno/heslo pro používání proxy serverů, které vyžadují ověření. Další informace o použití ověřeného proxy serveru najdete v tématu [konfigurace proxy serveru](https://docs.microsoft.com/azure-advanced-threat-protection/configure-proxy#configure-the-proxy).

- **Vylepšení funkcí: Automatizovaný proces synchronizace domén**<br> Proces označení a označení řadičů domény jako kandidátů na synchronizátora domény během instalace a průběžná konfigurace je teď plně automatizovaná. Možnost přepínání k ručnímu výběru řadičů domény jako kandidátů na synchronizátory domény se odebere. 

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-285"></a>Azure ATP verze 2,85

Vydáno 7. července 2019

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-284"></a>Azure ATP verze 2,84

Vydáno od 1. července 2019

- **Podpora nového umístění: Datové centrum Azure UK**<br>
    Instance Azure ATP se teď podporují v datovém centru Azure UK. Další informace o vytváření instancí ATP Azure a odpovídajících umístění datových center najdete v tématu [Krok 1 instalace ATP Azure](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step10).

- **Vylepšení funkcí: Upozornění na nové jméno a funkce pro podezřelé přídavky na důvěrné skupiny (externí ID 2024)**<br> 
    Upozornění na **podezřelé doplňky citlivých skupin** se dřív jmenovalo jako **podezřelé úpravy výstrahy citlivých skupin** . Externí ID výstrahy (ID 2024) zůstane stejné. Změna popisného názvu je přesnější a odráží účel upozornění na přidání do vašich **citlivých** skupin. Vylepšená výstraha také nabízí nové legitimace a vylepšené popisy. Další informace najdete v tématu [podezřelé přídavky citlivých skupin](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-additions-to-sensitive-groups-external-id-2024).  

- **Nová funkce dokumentace: Průvodce přechodem z Advanced Threat Analytics na Azure ATP**<br>
    Tento nový článek zahrnuje požadavky, pokyny k plánování a také kroky konfigurace a ověření pro přechod z ATA na službu Azure ATP. Další informace najdete v tématu [Přesun z ATA do služby Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/ata-atp-move-overview).   

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-283"></a>Azure ATP verze 2,83

Vydáno 23. června 2019

- **Vylepšení funkcí: Podezřelá výstraha při vytváření služby (externí ID 2026)**<br> 
    Tato výstraha teď obsahuje vylepšenou stránku s upozorněním a další legitimace a nový popis. Další informace najdete v tématu [Výstraha zabezpečení pro vytvoření podezřelé služby](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-service-creation-external-id-2026).

-  **Podpora pojmenovávání instancí: Přidání podpory pro předponu domény pouze číslicemi**<br>
    Byla přidána podpora pro vytváření instancí Azure ATP pomocí počátečních předpon domény, které obsahují jenom číslice. Například použití číslic počáteční předpony domény, jako je například 123456.contoso.com, je nyní podporováno. 

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.


## <a name="azure-atp-release-282"></a>Azure ATP verze 2,82

Vydáno 18. června 2019

- **Nová verze Public Preview**<br>
Prostředí pro šetření identity v Azure ATP je teď v **Public Preview**a dostupné pro všechny klienty chráněné Azure atp. Další informace najdete v tématu věnovaném [prostředí Azure ATP Microsoft Cloud App Security šetření](atp-mcas-integration.md) . 

- **Obecná dostupnost**<br>
Podpora Azure ATP pro nedůvěryhodné doménové struktury je teď obecně dostupná. Další informace najdete v tématu více [doménových struktur Azure ATP](atp-multi-forest.md) . 

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-281"></a>Azure ATP verze 2,81

Vydáno 10. června 2019

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-280"></a>Azure ATP verze 2,80

Vydáno 2. června 2019

- **Vylepšení funkcí: Upozornění na podezřelé připojení VPN**<br>
   Tato výstraha teď obsahuje rozšířené legitimace a texty pro lepší použitelnost. Další informace o funkcích výstrah a navrhovaných krocích a prevence při nápravě najdete v [popisu výstrahy na podezřelé připojení VPN](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025).

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-279"></a>Azure ATP verze 2,79
Vydáno 26. května 2019

- **Obecná dostupnost: Security Principal rekognoskace (LDAP) (externí ID 2038)**

    Tato výstraha je teď v GA (obecně dostupná). Další informace o výstrahách, funkcích výstrah a navrhované nápravě a prevenci najdete v [popisu výstrahy zabezpečení rekognoskace (LDAP Security)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038) .

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-278"></a>Azure ATP verze 2,78

Vydáno 19. května 2019

- **Vylepšení funkcí: Citlivé entity**<br> Ruční označování označení pro servery Exchange

    Nyní můžete ručně označit entity jako servery Exchange během konfigurace.

    Ruční označení entity jako serveru Exchange:
    1. Na portálu Azure ATP přejděte do nabídky **Konfigurace** .
    2. V části **detekce**vyberte **značky entit**a pak vyberte **citlivé**.
    3. Vyberte **servery Exchange** a pak přidejte entitu, kterou chcete označit.

    Po označení počítače jako serveru Exchange bude označen jako citlivý a zobrazí, že byl označen jako Exchange Server.  V profilu entity počítače se zobrazí citlivá značka a počítač se bude považovat za všechna zjišťování založená na citlivých účtech a cestách přesunu.

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-277"></a>Azure ATP verze 2,77

Vydáno 12. května 2019

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-276"></a>Azure ATP verze 2,76

Vydáno 6. května 2019

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-275"></a>Azure ATP verze 2,75

Vydáno 28. dubna 2019

- **Vylepšení funkcí: Citlivé entity**<br> Od této verze (2,75) jsou počítače identifikované jako servery Exchange ATP Azure ATP nyní automaticky označeny jako **citlivé**.  

    Entity, které jsou automaticky označeny jako **citlivé** , protože fungují jako servery Exchange seznam této klasifikace jako důvody, proč jsou označeny. 

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-274"></a>Azure ATP verze 2,74

Vydání 14. dubna 2019

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-273"></a>Azure ATP verze 2,73

Vydání 10. dubna 2019

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-272"></a>Azure ATP verze 2,72

Vydáno 31. března 2019

- **Vylepšení funkcí: LMP (cesta k okraji) – Hloubka rozsahu**<br>
Cesty na boku (LMPs) jsou klíčovou metodou pro zjišťování hrozeb a rizik ve službě Azure ATP. Aby bylo možné se soustředit na kritická rizika pro uživatele s nejcitlivější, tato aktualizace usnadňuje a urychluje analýzu a nápravu rizik u citlivých uživatelů na jednotlivých LMP, a to tak, že omezuje rozsah a hloubku každého zobrazeného grafu.   

    Další [](use-case-lateral-movement-path.md) informace o tom, jak Azure ATP používá LMPs k přístupu ke všem entitám ve vašem prostředí, najdete v části dráhy přesunu.   

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-271"></a>Azure ATP verze 2,71

Vydáno 24. března 2019

- **Vylepšení funkcí: Výstrahy monitorování překladu síťových názvů (útoků)**<br>
Výstrahy monitorování se přidaly pro úrovně spolehlivosti spojené s výstrahami zabezpečení ATP Azure, které jsou založené na útoků. Každé monitorování výstrah zahrnuje užitečná a podrobná doporučení, která vám pomůžou vyřešit útoků míry úspěšnosti. 

    Další informace o tom, jak Azure ATP používá útoků a proč je důležité pro přesnost výstrah, najdete v tématu [co je překlad síťových názvů](atp-nnr-policy.md) . 

- **Podpora serveru: Přidala se podpora pro server 2019 s použitím KB4487044.**<br>
Byla přidána podpora pro použití systému Windows Server 2019 s úrovní opravy KB4487044. Použití serveru 2019 bez opravy není podporované a od této aktualizace se zablokuje. 

- **Vylepšení funkcí: Vyloučení výstrah založené na uživateli**<br>
Rozšířené možnosti vyloučení výstrah teď umožňují vyloučit konkrétní uživatele z konkrétních výstrah. Vyloučení můžou zabránit situacím, kdy použití nebo konfigurace určitých typů interního softwaru opakovaně aktivované výstrahy zabezpečení neškodí.

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-270"></a>Azure ATP verze 2,70
Vydáno 17. března 2019

- **Vylepšení funkcí: Úroveň spolehlivosti útoků (Network Name Resolution) přidaná do více výstrah**<br> Překlad názvu sítě nebo (útoků) se používá k identifikaci identifikace zdrojové entity u podezřelých útoků. Tím, že přidáte útoků úrovně spolehlivosti do seznamů legitimace výstrah Azure ATP, teď můžete okamžitě posoudit a pochopit úroveň důvěry útoků související se zjištěnými zdroji a patřičně ji opravit. 

    ÚTOKŮ legitimace úrovně spolehlivosti se přidala k těmto výstrahám:
  - [Mapování sítě rekognoskace (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)
  - [Podezření na krádež identity (pass-the-Ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018) 
  - [Podezření na útok pomocí protokolu NTLM (účet Exchange) – Preview](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)
  - [Podezřelý útok DCSync (replikace adresářových služeb)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)

- **Další scénář upozornění na stav: Službu Azure ATP snímače se nepovedlo spustit.**<br>V případech, kdy se senzor Azure ATP nepovedlo spustit kvůli problému se zachytáváním síťového ovladače, se teď aktivuje výstraha o stavu senzoru. [Řešení potíží se senzorem Azure ATP pomocí protokolů ATP Azure](troubleshooting-atp-using-logs.md) , kde najdete další informace o protokolech ATP Azure a jejich použití. 
  
- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-269"></a>Azure ATP verze 2,69
Vydáno 10. března 2019

- **Vylepšení funkcí: Podezřelá výstraha krádeže identity (pass-the-Ticket)**<br> Tato výstraha teď nabízí nové legitimace s podrobnostmi o připojeních, která provedla pomocí protokolu RDP (Remote Desktop Protocol). Přidané legitimace usnadňuje nápravu známého problému pozitivních výstrah z neškodné hodnoty (B-TP) způsobených používáním připojení Remote Credential Guard přes připojení RDP. 

- **Vylepšení funkcí: Vzdálené spuštění kódu prostřednictvím výstrahy DNS**<br> Tato výstraha teď nabízí nové legitimace ukazující stav aktualizace zabezpečení řadiče domény, který vás informuje o tom, kdy se vyžadují aktualizace.   

- **Nová funkce dokumentace: Výstraha zabezpečení Azure ATP MITRE ATT & CK – matice™**<br>

    K tomu, abyste usnadnili mapování vztahů mezi výstrahami zabezpečení Azure ATP a známou MITREovou maticí CK & ATT, Přidali jsme příslušné techniky MITRE do seznamů výstrah zabezpečení Azure ATP. Tento další odkaz usnadňuje pochopení podezřelé techniky útoku, která se může použít, když se aktivuje výstraha zabezpečení ATP Azure. Přečtěte si další informace o [Průvodci výstrahou zabezpečení Azure ATP](suspicious-activity-guide.md).  

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-268"></a>Azure ATP verze 2,68
Vydáno 3. března 2019

- **Vylepšení funkcí: Výstraha s podezřelým útokem hrubou silou (LDAP)**<br>
V této výstraze zabezpečení byla provedena významná vylepšení použitelnosti, včetně revidovaného popisu, zřízení dalších zdrojových informací a podrobností o pokusůch o rychlejší nápravu. Přečtěte si další informace o výstrahách zabezpečení pro podezřelé útoky hrubou silou [(LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004) . 

- **Nová funkce dokumentace: Testovací prostředí pro výstrahy zabezpečení**<br>

    Abychom vám pomohli vysvětlit výkon služby Azure ATP při zjišťování skutečných hrozeb pro vaše pracovní prostředí, Přidali jsme do této dokumentace nové **prostředí pro upozornění zabezpečení** . **Testovací prostředí výstrah zabezpečení** vám pomůže rychle nastavit testovací prostředí nebo testovací prostředí a vysvětluje nejlepší obrannou linií posturing proti běžným skutečným hrozbám a útokům.  

    [Podrobné vývojové prostředí](atp-playbook-lab-overview.md) je navrženo tak, aby bylo zajištěno, že strávíte minimální dobu vytváření a Zajímáte se o hrozbách a máte k dispozici výstrahy a ochranu ATP Azure. Rádi uslyšíme váš názor.

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-267"></a>Azure ATP verze 2,67
Vydáno 24. února 2019

- **Nové upozornění zabezpečení: Security Principal rekognoskace (LDAP) – (Preview)**<br>

    Výstraha zabezpečení [rekognoskace (Security Principal Security) ve verzi Preview (LDAP)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038) Azure ATP je teď ve verzi Public Preview. <br> V tomto zjišťování se aktivuje výstraha zabezpečení ATP Azure, když útočníci rekognoskace používají k získání důležitých informací o prostředí domény. Tyto informace pomáhají útočníkům namapovat strukturu domény a identifikovat privilegované účty pro použití v pozdějších krocích v řetězu jejich útoků. 

    Protokol LDAP (Lightweight Directory Access Protocol) je jednou z nejoblíbenějších metod používaných pro legitimní i škodlivé účely dotazování služby Active Directory. Rekognoskace zabezpečení LDAP zaměřené na zabezpečení se běžně používá jako první fáze útoku Kerberoasting. Útoky Kerberoasting slouží k získání cílového seznamu hlavních názvů zabezpečení (SPN), které se následně pokusí získat lístky TGT (Ticket Granting Server) pro.

- **Vylepšení funkcí: Výstraha rekognoskace výčtu účtů (NTLM)** <br> 
    Vylepšená výstraha **rekognoskace výčtu účtů (NTLM)** pomocí dalších analýz a vylepšená logika zjišťování pro snížení výsledků výstrah **B-TP** a **FP** . 
 
- **Vylepšení funkcí: Výstraha rekognoskace (DNS) mapování sítě** <br>
    Nové typy detekce přidaných do výstrah síťového mapování rekognoskace (DNS). Služba Azure ATP kromě detekce podezřelých požadavků na nenáročné instance teď detekuje podezřelé typy požadavků pocházejících z jiných serverů než DNS s využitím nadměrného počtu požadavků.

 - Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-266"></a>Azure ATP verze 2,66
Vydáno 17. února 2019

- **Vylepšení funkcí: Podezřelý útok DCSync (replikace adresářových služeb) – výstraha**<br>
V této výstraze zabezpečení se provedla vylepšení použitelnosti, včetně revidovaného popisu, zřízení dalších zdrojů informací, nových infografika a dalších důkazů. Přečtěte si další informace o [podezřelém útoku DCSync (replikaci adresářových služeb)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006) výstrah zabezpečení. 

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-265"></a>Azure ATP verze 2,65
Vydáno 10. února 2019

- **Nové upozornění zabezpečení: Podezření na útok pomocí protokolu NTLM (účet Exchange) – (Preview)**<br>
[Podezřelý útok protokolu NTLM pro útoky Azure ATP (účet Exchange) –](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037) výstraha zabezpečení ve verzi Preview je teď ve verzi Public Preview. <br> V tomto zjišťování se aktivuje výstraha zabezpečení ATP Azure ATP, když se identifikuje použití přihlašovacích údajů účtu Exchange z podezřelého zdroje. Tyto typy útoků se pokoušejí využít techniky předávání protokolu NTLM k získání oprávnění pro výměnu řadičů domény a jsou známy jako **ExchangePriv**. Přečtěte si další informace o technikě **ExchangePriv** od Poradce pro [ADV190007](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV190007) , který je nejdřív publikovaný 31. ledna 2019 a odpověď na [výstrahu Azure ATP](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/How-to-win-the-latest-security-race-over-NTLM-relay/ba-p/334511).  

- **Obecná dostupnost: Vzdálené spuštění kódu přes DNS**<br>
Tato výstraha je teď v GA (obecně dostupná). Další informace a funkce výstrah najdete na stránce s [popisem výstrahy vzdálené spuštění kódu přes DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036). 

- **Obecná dostupnost: Data exfiltrace přes SMB**<br>
Tato výstraha je teď v GA (obecně dostupná). Další informace a funkce výstrah najdete na stránce s [popisem výstrahy pro data exfiltrace over SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030).


- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-264"></a>Azure ATP verze 2,64
Vydáno 4. února 2019

- **Obecná dostupnost: Podezřelé použití zlatého lístku (anomálie lístků)**<br>
Tato výstraha je teď v GA (obecně dostupná). Další informace a funkce výstrah najdete na stránce s [popisem výstrahy na podezřelé použití lístku (anomálie lístku)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032). 

- **Vylepšení funkcí: Mapování sítě rekognoskace (DNS)**<br>
Vylepšená logika detekce výstrah nasazená pro tuto výstrahu pro minimalizaci falešně pozitivních hodnot a hluku výstrah. Tato výstraha teď má období učení osm dní, než se výstraha může aktivovat poprvé. Další informace o této výstraze najdete na [stránce s popisem výstrahy pro mapování sítě rekognoskace (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007). 

    **Z důvodu vylepšení této výstrahy by se metoda nslookup neměla už používat k testování připojení Azure ATP během počáteční konfigurace.** 

- **Vylepšení funkcí:**<br>
Tato verze zahrnuje přepracované stránky výstrah a nové legitimace, které poskytují lepší šetření výstrah. 
    - [Podezřelý útok hrubou silou (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)
    - [Podezřelé zlaté použití lístku (časová anomálie) Stránka s popisem výstrahy](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)
    - [Podezřelá Overpass-the-hash – útok (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)
    - [Podezření na použití rozhraní Metasploit pro hackery](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)
    - [Podezřelý útok WannaCry ransomwarem](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.


## <a name="azure-atp-release-263"></a>Azure ATP verze 2,63
Vydáno 27. ledna 2019

- **Nová funkce: Podpora nedůvěryhodných doménových struktur – (Preview)**<br>
Podpora Azure ATP pro senzory v nedůvěryhodných doménových strukturách je teď ve verzi Public Preview. Na stránce **adresářové služby** portálu Azure ATP nakonfigurujte další sady přihlašovacích údajů, aby se senzory Azure ATP mohly připojovat k různým doménovým strukturám služby Active Directory, a nahlaste se zpátky do služby Azure atp. Další informace najdete v tématu více [doménových struktur Azure ATP](atp-multi-forest.md) . 

- **Nová funkce: Pokrytí řadiče domény**<br>
Azure ATP teď poskytuje informace o pokrytí pro řadiče domény monitorovaných v Azure ATP.  
Na stránce senzory na portálu Azure ATP Zobrazte Počet monitorovaných a nemonitorovaných řadičů domény zjištěných ATP Azure ve vašem prostředí. Stáhněte si seznam monitorovaných řadičů domény pro další analýzu a sestavte plán akcí. Další informace najdete v průvodci [monitorováním řadičů domény](atp-sensor-monitoring.md) . 

- **Vylepšení funkcí: Rekognoskace výčtu účtů**<br>
Detekce výčtu účtů Azure ATP rekognoskace nyní detekuje a vydává výstrahy pro pokusy o výčet pomocí protokolu Kerberos a NTLM. Dříve byla detekce pracovala pouze pro pokusy pomocí protokolu Kerberos. Další informace najdete v tématu [výstrahy Azure ATP rekognoskace](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003) . 

- **Vylepšení funkcí: Výstraha vzdáleného pokusu o spuštění kódu**<br>
    - Do časové osy profilu cílového počítače se přidaly všechny aktivity vzdáleného spuštění, jako je třeba vytvoření služby, spuštění služby WMI a nové spuštění **prostředí PowerShell** . Cílový počítač je řadič domény, na kterém byl příkaz spuštěn. 
    - Do seznamu aktivit vzdáleného spuštění kódu uvedených na časové ose upozornění profilu entity se přidalo spuštění **prostředí PowerShell** .
    - Další informace najdete v tématu [o spuštění vzdáleného kódu](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019) .  

- **Problémy s Windows serverem 2019 LSASS a Azure ATP**<br>
V reakci na zpětnou vazbu od zákazníků týkající se využití ATP Azure s řadiči domény s Windows serverem 2019 obsahuje tato aktualizace další logiku, která neumožňuje aktivovat nahlášené chování na počítačích s Windows serverem 2019. Na Windows serveru 2019 se plánuje plná podpora snímače ATP pro Azure ATP, ale instalace a provozování Azure ATP na Windows serverech 2019 se momentálně nepodporuje. Další informace najdete v tématu [požadavky na senzor ATP Azure](atp-prerequisites.md#azure-atp-sensor-requirements) . 

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.


## <a name="azure-atp-release-262"></a>Azure ATP verze 2,62
Vydáno 20. ledna 2019

- **Nové upozornění zabezpečení: Vzdálené spuštění kódu přes DNS – (Preview)**<br>
[Vzdálené spuštění kódu](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036) v Azure ATP prostřednictvím výstrahy zabezpečení DNS je teď ve verzi Public Preview. <br> V tomto zjišťování se aktivuje výstraha zabezpečení ATP Azure ATP, když dotazy DNS s podezřením na zneužití ohrožení zabezpečení [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) probíhají na řadiči domény v síti.

- **Vylepšení funkcí: Zpožděná aktualizace senzoru pro 72 hodin** <br> Změna možnosti pro zpoždění aktualizací senzorů u vybraných senzorů na 72 hodin (místo předchozí 24 hodinové prodlevy) po každé aktualizaci verze Azure ATP. Pokyny ke konfiguraci najdete v tématu [aktualizace pro senzory Azure ATP](sensor-update.md) . 


- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-261"></a>Azure ATP verze 2,61
Vydáno 13. ledna 2019

- **Nové upozornění zabezpečení: Data exfiltrace přes SMB – (Preview)**<br>
Výstraha zabezpečení služby Azure ATP ( [data exfiltrace over SMB](atp-exfiltration-alerts.md) ) je teď ve verzi Public Preview. <br> Útočníci s právy správce domény může ohrozit účet KRBTGT. Pomocí účtu KRBTGT můžou útočníci vytvořit lístek protokolu Kerberos pro udělování lístků (TGT), který poskytuje autorizaci k jakémukoli prostředku. 


- **Vylepšení funkcí: Výstraha zabezpečení při** pokusu o vzdálené spuštění kódu <br> Byl přidán nový popis výstrahy a další legitimace, které vám pomůžou usnadnit pochopení výstrahy a poskytovat lepší vyšetřovací pracovní postupy. 


- **Vylepšení funkcí: Logické aktivity dotazů DNS** <br>K [monitorovaným aktivitám Azure ATP](monitored-activities.md) byly přidány další typy dotazů, včetně: **TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**. 

- **Vylepšení funkcí: Podezřelé používání lístku (anomálie lístku) a podezřelé zlaté použití lístku (neexistující účet)** <br>
Vylepšená logika detekce byla aplikována na obě výstrahy, aby se snížil počet výstrah FP a poskytovaly přesnější výsledky.

- **Vylepšení funkcí: Dokumentace k výstraze zabezpečení Azure ATP** <br>
Dokumentace k výstraze zabezpečení Azure ATP se rozšířila a rozšířila tak, aby obsahovala lepší popisy výstrah, přesnější klasifikace výstrah a vysvětlení legitimace, nápravy a prevence. Seznamte se s novým návrhem dokumentace k bezpečnostním výstrahám pomocí následujících odkazů: 
    - [Výstrahy zabezpečení Azure ATP](suspicious-activity-guide.md)
    - [Porozumění výstrahám zabezpečení](understanding-security-alerts.md)
        - [Výstrahy fáze rekognoskace](atp-reconnaissance-alerts.md)
        - [Výstrahy fáze zneužití přihlašovacích údajů](atp-compromised-credentials-alerts.md)
        - [Výstrahy fáze pohybu na okraji](atp-lateral-movement-alerts.md)
        - [Výstrahy fáze dominantního postavení domény](atp-domain-dominance-alerts.md)
        - [Výstrahy fáze exfiltrace](atp-exfiltration-alerts.md)
    - [Prošetřování počítačů](investigate-a-computer.md)
    - [Prošetřování uživatelů](investigate-a-user.md)

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.


## <a name="azure-atp-release-260"></a>Azure ATP verze 2,60
Vydáno 6. ledna 2019

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-259"></a>Azure ATP verze 2,59
Vydáno 16. prosince 2018

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.


## <a name="azure-atp-release-258"></a>Verze ochrany ATP v programu Azure 2.58

Vydáno 9. prosince 2018

- **Vylepšení výstrahy zabezpečení: Neobvyklé rozdělení výstrah implementace protokolu**<br>
Řada neobvyklých výstrah zabezpečení implementace protokolu pro Azure ATP, které dříve sdílely 1 externalId (2002), jsou teď rozdělené na čtyři rozlišující výstrahy s odpovídajícím jedinečným externím ID. 

### <a name="new-alert-externalids"></a>Nové výstrahy externalIds

> [!div class="mx-tableFixed"] 

|Nový název výstrahy zabezpečení|Předchozí název výstrahy zabezpečení|Jedinečné externí ID|
|---------|----------|---------|
|Podezřelý útok hrubou silou (SMB)|Neobvyklá implementace protokolu (potenciální použití škodlivých nástrojů, jako je Hydra)|2033
|Podezření na útok overpass-the-hash (Kerberos)|Neobvyklá implementace protokolu Kerberos (možný útok overpass-the-hash)|2002|
|Podezřelé použití Metasploit hacking framework|Neobvyklá implementace protokolu (potenciální použijte Metasploit hacking nástroje)|2034
|Podezření na útok WannaCry ransomwaru|Neobvyklá implementace protokolu (možný útok ransomwarem WannaCry)|2035
|

- **Nová monitorovaná aktivita: Kopírování souborů prostřednictvím protokolu SMB**<br>
Kopírování souborů přes protokol SMB je nyní monitorované a filtrovat aktivity. Další informace o tom, které [aktivity ochrany ATP v programu Azure monitoruje](monitored-activities.md)a jak [filtru a vyhledávání monitorování aktivity](atp-activities-search.md) na portálu. 

- **Velký obrázek rozšíření cesty laterální pohyb**<br>
Při zobrazení cesty taktiky Lateral Movement velké, ochrana ATP v programu Azure nyní zvýrazňuje pouze uzly, které jsou připojené k vybrané entity, namísto rozostření do dalších uzlů. Tato změna přináší přináší značné vylepšení v velké LMP rychlost vykreslování. 

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-257"></a>Verze ochrany ATP v programu Azure 2.57
Vydáno 2. prosince 2018

- **Nové upozornění zabezpečení: Podezřelé použití lístku – anomálie lístku (Preview)**<br>
Azure ATP [podezřelý Golden Ticket použití – lístek anomálií](suspicious-activity-guide.md) výstraha zabezpečení je teď ve verzi public preview. <br> Útočníci s právy správce domény může ohrozit účet KRBTGT. Pomocí účtu KRBTGT, útočníci můžete vytvořit lístek Kerberos udělující lístek (TGT), který poskytuje autorizaci k jakémukoli prostředku. 
<br>Tato falešných lístků TGT se nazývá "Zlatých lístků", protože to útočníkům umožňuje dosáhnout trvalého trvalost sítě. Falšování Zlatých lístků tohoto typu mají jedinečné charakteristiky. Tato nová detekce je navržena k identifikaci. 


- **Vylepšení funkcí: Automatizované vytváření instancí Azure ATP (pracovní prostor)** <br>
Od dnešního dne, ochrana ATP v programu Azure *pracovní prostory* se přejmenovat ochrany ATP v programu Azure *instance*. Ochrana ATP v programu Azure teď podporuje jednu instanci služby Azure ATP jeden účet služby Azure ATP. Instance pro nové zákazníky jsou vytvořené pomocí Průvodce vytvořením instance v [ochrany ATP v programu Azure portal](https://portal.atp.azure.com). Existujícím pracovním prostorům ochrany ATP v programu Azure se automaticky převedou na instance služby Azure ATP s touto aktualizací.  

  - Zjednodušené vytváření instance pro rychlejší nasazení a ochranu pomocí [vytvořit instanci služby Azure ATP](install-atp-step1.md). 
  - Všechny [ochrany osobních údajů a dodržování předpisů](atp-privacy-compliance.md) zůstává stejná. 

  Další informace o instancích ATP Azure najdete v tématu [vytvoření instance ATP Azure](install-atp-step1.md). 

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-256"></a>Verze ochrany ATP v programu Azure 2.56
Vydáno 25. listopadu 2018


- **Vylepšení funkcí: Cesty bočního pohybu (LMPs)** <br>
K rozšíření možností Azure ochrany ATP v programu laterální pohyb cestu (LMP) jsou přidány dvě další funkce:

  - Historie LMP jsou nyní uloženy a dostupnější za entity a pomocí LMP sestavy. 
  - Postupujte podle entity v LMP prostřednictvím časové osy aktivity a prozkoumat pomocí dalších důkazu zjišťování potenciální útok cesty. 

  Zobrazit [cesty taktiky Lateral Movement ochrany ATP v programu Azure](use-case-lateral-movement-path.md) Další informace o tom, jak používat a prozkoumat pomocí rozšířené LMPs. 

- **Vylepšení dokumentace: Cesty bočního pohybu, názvy výstrah zabezpečení**<br> Přidání a aktualizace byly provedeny na služby Azure ATP články s popisem cesty laterální pohyb popisy a funkce, název se přidá mapování pro všechny instance starých názvy výstrah zabezpečení nové názvy a externalIds. 
  - V tématu [cesty taktiky Lateral Movement ochrany ATP v programu Azure](use-case-lateral-movement-path.md), [prozkoumat cesty taktiky Lateral Movement](investigate-lateral-movement-path.md), a [Průvodce výstrah zabezpečení](suspicious-activity-guide.md) Další informace.   

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-255"></a>Verze ochrany ATP v programu Azure 2.55
Vydáno 18. listopadu 2018

- **Výstraha zabezpečení: Podezřelá komunikace přes DNS – Obecná dostupnost**<br>
Azure ATP [podezřelá komunikace prostřednictvím DNS](suspicious-activity-guide.md) výstrahy zabezpečení jsou teď obecně dostupné. <br> Protokol DNS ve většině organizací není obvykle, monitorovat a zřídka blokované před škodlivými aktivitami. To umožňuje útočníkovi na napadeném počítači zneužívání protokolu DNS. Škodlivý komunikace prostřednictvím DNS je možné pro průsak dat ven, příkazu a řízení a/nebo omezení úmyslem vyhnout podnikové sítě.

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-254"></a>Verze ochrany ATP v programu Azure 2,54
Vydáno 11. listopadu 2018

- **Vylepšení funkcí: Výchozí vyloučení domén přidaná do podezřelé komunikace prostřednictvím výstrahy DNS**<br>   Novým rozšířením tři Oblíbené domény do seznamu vyloučení výchozí domény. Seznam vyloučení zůstává plně přizpůsobitelné. Zobrazit [vyloučení entit z detekce](excluding-entities-from-detections.md), další informace. 

- **Vylepšení dokumentace: Aktualizace protokolu SIEM, pokyny ke známým problémům**<br>    externalId mapování a další vysvětlení byly přidány do systému SIEM protokolu popisy. Zobrazit [referenční informace k protokolům SIEM](cef-format-sa.md), další informace. <br>Byla přidána další článek pokyny aktuálně nevyřešené známé problémy. Zobrazit, [známé problémy ochrany ATP v programu Azure](known-issues.md), další informace.  

- Tato verze obsahuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-253"></a>Verze ochrany ATP v programu Azure 2,53
Vydáno 4. listopadu 2018

- **Vylepšení výstrahy zabezpečení: Podezřelé selhání ověřování**<br>
Azure ATP [podezřelé chyby ověřování zabezpečení upozornění](suspicious-activity-guide.md) teď obsahuje monitorování pro detekci hesla hrubou zařízení vynutit útoky.
V typické **heslo zařízení** útoku, útočníci po úspěšně výčet seznamu platní uživatelé z řadiče domény, zkuste jedno heslo pečlivě vytvořené pro všechny známé uživatelské účty (jedno heslo na více účtů) . Při počáteční heslo zařízení neproběhne úspěšně, bude snaží znovu, využívají jiné heslo pečlivě vytvořený, obvykle po uplynutí 30 minut mezi pokusy. Doba čekání útočníkům umožňuje, aby neměl spouštět nejčastěji podle času účet uzamčení prahové hodnoty. Heslo zařízení se rychle stal oblíbenou technikou útočník a testery pera. Heslo zařízení útoky ukázaly na zajistit efektivitu při získávání počáteční základnu v organizaci a pro následné laterální přesuny pokouší o zvýšení oprávnění. 

- **Vylepšení funkcí: Odeslat testovací zprávu syslog**<br>   Nová možnost odeslat testovací zpráva Syslogu během procesu instalace systému SIEM. Zobrazit [integrace se Syslogem](setting-syslog.md), další informace. 

- Tato verze také zahrnuje vylepšení a opravy chyb pro interní senzor infrastruktury.

## <a name="azure-atp-release-252"></a>Verze ochrany ATP v programu Azure 2.52
Vydáno 28. října 2018


- **Vylepšení výstrahy zabezpečení: Pokus o vzdálené spuštění kódu**<br>
Azure ATP [upozornění na zabezpečení. pokus o vzdálené spuštění kódu](suspicious-activity-guide.md) nyní zahrnuje monitorování podezřelých pokusy o spuštění vzdáleného kódu Powershellu v řadičích domény. Je běžné metody pro provádění platné příkazy pro správu vzdáleného prostředí PowerShell, ale se často používá speciálně při pokusu o spuštění skriptů na vzdálené koncové body. 

- **Vylepšení funkcí: Nastavení plánování sestav**
<br>Teď můžete nastavit jenom konkrétní hodiny naplánování sestav pomocí služby Azure ATP [sestavy](reports.md#) funkce. 

- **Přidání konfigurace: Řízení přístupu na základě role klienta (RBAC)**
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
-   **Nové detekce: Podezřelá komunikace** DNS (Preview)<br>Nové detekce přidána k chrání před útoky komunikace podezřelé DNS:

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

  Toto upozornění zabezpečení teď má vylepšenou informační grafiku a legitimaci. 

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

- **Podpora více doménovými strukturami Azure ochrany ATP v programu je postupně zavádí (preview)** <br> Azure ATP teď může podporovat organizace s více doménovými strukturami, které vám umožní sledovat aktivity a profily uživatelů napříč doménovými strukturami. Tato nová funkce umožňuje:

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
-   **Nově přidaná detekce: Kerberos zlatý lístek-neexistující účet** (Preview)<br>Toto nové zjišťování pomáhá chránit vaši organizaci před útoky, ve kterých je vytvořen zlatý lístek Kerberos účtu, který neexistuje ve vaší doméně. Další informace najdete v tématu [Průvodce prošetřováním podezřelých aktivit rozšířené ochrany před internetovými útoky pro Azure](suspicious-activity-guide.md)

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

- Funkce ve verzi Preview: Azure ATP teď podporuje nové jazyky a 13 nových národních prostředí:
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

- Když Azure ATP upozorní na podezřelou aktivitu, kterou zjistíte jako neškodný pozitivní (legitimní akce, která není podezřelá aktivita), máte možnost vyloučit počítače a IP adresy pro další detekce, včetně těchto: Downgrade šifrování, LDAP hrubá síla, falešný PAC, hrubá síla a pass-the-hash.
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

---
title: Upozornění zabezpečení fáze rekognoskace v Azure ochrany ATP v programu | Dokumentace Microsoftu
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of reconnaissance phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 02/04/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 09649f57041ca53ae7cdd183e60584ff37be9c9f
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2019
ms.locfileid: "56264028"
---
# <a name="tutorial-reconnaissance-alerts"></a>Kurz: Rekognoskace výstrahy  

Obvykle kybernetických útoků jsou spouštěny proti jakémukoli subjektu přístupné, jako je například uživatel s nízkým oprávněním a potom rychle následně k laterálnímu pohybu dokud útočník získá přístup k cenný majetek, který. Cenný majetek, který může být citlivých účtů, správci domény nebo vysoce citlivá data. Ochrana ATP v programu Azure identifikuje tyto důmyslných hrozeb ve zdrojovém kódu v celém řetězu událostí útoku a klasifikuje do následujících fází:

1. **Rekognoskace**
2. [Zneužití přihlašovacích údajů](atp-compromised-credentials-alerts.md)
3. [Taktiky Lateral Movement](atp-lateral-movement-alerts.md)
4. [Dominance v doméně](atp-domain-dominance-alerts.md)
5. [Průsak ven](atp-exfiltration-alerts.md) 

Další informace o tom, jak pochopit strukturu a běžné součásti všech výstrah zabezpečení ochrany ATP v programu Azure najdete v tématu [Principy výstrah zabezpečení](understanding-security-alerts.md).

Výstrahy pomáhají identifikovat a napravit následující zabezpečení **Rekognoskace** fáze podezřelých aktivitách zjištěných ochrany ATP v programu Azure ve vaší síti.

V tomto kurzu se dozvíte, jak porozumět, klasifikovat, opravit a brání následující typy útoků:

> [!div class="checklist"]
> * Rekognoskace výčet účtu (externí ID 2003)
> * Mapování sondování sítě (DNS) (externí ID 2007)
> * Uživatele a IP adres pro rekognoskaci (SMB) (externí ID 2012)
> * Rekognoskace členství uživatelů a skupin (SAMR) (externí ID 2021)

## <a name="account-enumeration-reconnaissance-external-id-2003"></a>Rekognoskace výčet účtu (externí ID 2003) 


*Předchozí název:* Rekognoskace pomocí výčtu účtů

**Popis**

V rekognoskace výčet účtu útočník používá slovník s tisíci uživatelská jména nebo nástrojů, jako je KrbGuess ve snaze uhodnout uživatelská jména v doméně.

**Protokol Kerberos**: Útočník se vytvářejí požadavky protokolu Kerberos pomocí tyto názvy se pokouší vyhledat platné uživatelské jméno v doméně. Při odhad úspěšně Určuje uživatelské jméno, útočník získá **požadované předběžné ověření** místo **neznámý objekt zabezpečení** Chyba protokolu Kerberos.

**NTLM**: Útočník bude žádosti o ověření NTLM pomocí slovník názvů, které chcete najít platné uživatelské jméno v doméně. Pokud odhad úspěšně Určuje uživatelské jméno, útočník získá **WrongPassword (0xc000006a)** místo **NoSuchUser (0xc0000064)** chyba NTLM.

V této výstrahy detekce ochrany ATP v programu Azure detekuje útok zaměřený na výčet účet, odkud, celkový počet pokusů uhádnout a kolik pokusů se shoda našla. Pokud existuje příliš mnoho uživatelů neznámý, ochrana ATP v programu Azure rozpozná jako podezřelou aktivitu.

**TP, B-TP nebo FP**

Některé servery a aplikace dotazovat řadiče domény k určení, zda neexistují účty ve scénářích oprávněné použití.

Chcete-li zjistit, zda tento dotaz **TP**, **BTP** nebo **FP**, klikněte na výstrahu zobrazíte stránku s jeho podrobnostmi:

1. Zaškrtněte, pokud byl zdrojový počítač má provádět tento typ dotazu. Příklady **B-TP** v tomto případě může být serverech Microsoft Exchange nebo systémech lidských zdrojů.

2. Zkontrolujte účet domény.
   - Zobrazit další uživatele, kteří patří do jiné domény? 
     <br>Chybná konfigurace serveru jako je například Exchange a Skypu nebo ADSF může způsobit další uživatele, které patří do jiných domén.
   - Podívejte se na konfiguraci služby problematické opravit chybným nastavením.

     Pokud vaše odpověď **Ano** na otázky uvedené výše, je **B-TP** aktivity. *Zavřít* dané výstraze zabezpečení.<br>

Jako další krok podívejte se na zdrojovém počítači: 

1. Je skript nebo aplikace spuštěné na zdrojovém počítači, který může generovat toto chování?  
   - Je skript skriptu staré staré přihlašovacích údajů ke spuštění? <br>Pokud ano, zastavte a upravit nebo odstranit skript. 
   - Je aplikace pro správu nebo zabezpečení skriptu nebo aplikace, která se má spustit v prostředí?
 
     Pokud vaše odpověď **Ano** k předchozí otázce *Zavřít* zabezpečení výstrahy a vyloučit tento počítač. Pravděpodobně se jedná **B-TP** aktivity.

Nyní podívejte se na účty:<br>
<br>Útočníci se označuje použití slovník náhodnými názvy k vyhledání názvů existujících účtů v organizaci.

1. Neexistujících účtů vám to povědomé?  
   - Zda povědomé neexistujících účtů, může se zakázanými účty nebo patří zaměstnancům, kteří opustil společnost.
   - Zkontrolujte aplikaci nebo skript, který ověří a určí, které účty jsou stále existují ve službě Active Directory.

     Pokud vaše odpověď **Ano** k jednomu z předchozí dotazy, *Zavřít* výstrahy zabezpečení, je pravděpodobně **B-TP** aktivity.

2. Pokud některý z odhad pokusí shodovat s existujícími názvy účtů, jak útočník ví o existenci účty ve vašem prostředí a může pokusit použít útok hrubou silou pro přístup k vlastní domény s využitím zjištěných uživatelská jména. 
    - Zkontrolujte názvy účtů uhádnuté další podezřelých aktivit. 
    - Zkontrolujte, jestli některý z odpovídající účty jsou citlivé účty.

### <a name="understand-the-scope-of-the-breach"></a>Vysvětlení rozsahu porušení

1. Prozkoumejte zdrojový počítač
2. Pokud některý z tento počet pokusů uhádnout odpovídá existujícími názvy účtů, jak útočník ví o existenci účty ve vašem prostředí a můžete použít útok hrubou silou na pokus o přístup k vlastní domény s využitím zjištěných uživatelská jména. Prozkoumat existující účty pomocí [uživatelská příručka k vyšetřování](investigate-a-user.md). 

### <a name="suggested-remediation-and-steps-for-prevention"></a>Navrhované nápravné kroky a pro ochrany před únikem informací

1. Zdroj obsahovat [počítače](investigate-a-computer.md). 
    1. Najít nástroj, který provádí útoku a jeho odebrání.
    2. Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu aktivity došlo k chybě, protože tyto uživatele může také dojít k ohrožení. 
    3. Resetování hesel a povolení vícefaktorového ověřování.
2. Vynutit [komplexní a dlouho hesla](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) v organizaci. Složitá a dlouhá hesla zadejte nezbytnou první úroveň zabezpečení před útoky hrubou silou. Dalším krokem v řetězu událostí internetového útoku po výčtu jsou obvykle útoky hrubou silou. 

## <a name="network-mapping-reconnaissance-dns-external-id-2007"></a>Mapování sondování sítě (DNS) (externí ID 2007) 


*Předchozí název:* Rekognoskace pomocí DNS

**Popis**

DNS server obsahuje mapu všech počítačů, IP adresy a služby ve vaší síti. Tyto údaje používají útočníci ke zmapování struktury vaší sítě a zacílení zajímavých počítačů v pozdějších krocích útoku. 
 
Protokol DNS obsahuje několik typů dotazů. Tato výstraha zabezpečení služby Azure ATP detekuje podezřelé žádosti AXFR (přenos) pocházející z jiné servery než DNS.

**Období učení**

Toto upozornění nemá období učení z 8 dní od samého začátku monitorování řadiče domény. 

**TP, B-TP nebo FP**

1. Zkontrolujte, jestli zdrojový počítač je DNS server.

    - Pokud zdrojový počítač **je** DNS server, zavřete výstrahu zabezpečení jako **FP**. 
    - Aby se zabránilo budoucnost **snímků za sekundu**, ověřte, zda je UDP port 53 **otevřete** mezi senzorem Azure ATP a zdrojový počítač.

Dotazy DNS můžete vygenerovat bezpečnostní skenery a oprávněné aplikace. 

1. Zaškrtněte, pokud se tento zdrojový počítač by měl generovat tento typ aktivity?

    - Pokud se tento zdrojový počítač by měl generovat tento typ aktivity, **Zavřít** zabezpečení výstrahy a vyloučit počítače jako **B-TP** aktivity.

**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový počítač](investigate-a-computer.md). 

**Navrhované nápravné kroky a pro ochrany před únikem informací**

**Náprava:**
1. Obsahují zdrojový počítač. 
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu aktivity došlo k chybě, protože tyto uživatele může také dojít k ohrožení. Resetování hesel a povolení vícefaktorového ověřování.

**Ochrany před únikem informací:** Je důležité zabránit budoucím útokům pomocí dotazů AXFR díky zabezpečení interní server DNS.

1. Zabezpečení interní server DNS pro rekognoskaci pomocí DNS tím, že zakážete přenosů zóny nebo podle [omezení přenosů zóny](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)) pouze na zadané IP adresy. Úprava přenosů zóny je jedním z úkolů na kontrolním seznamu, která by měla být určena pro [zabezpečení před útoky interních i externích serverů DNS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)).

## <a name="user-and-ip-address-reconnaissance-smb-external-id-2012"></a>Uživatele a IP adres pro rekognoskaci (SMB) (externí ID 2012) 


*Předchozí název:* Rekognoskace pomocí výčtu relací SMB

### <a name="description"></a>Popis

Výčet pomocí protokolu bloku SMB (Server Message) umožňuje útočníkům získat informace, kde uživatelé nedávno přihlašovali. Jakmile útočník tyto informace, se můžete přesunout následně k laterálnímu v síti k určité citlivých účtů.

V této detekce se aktivuje upozornění, když se provádí výčet relací SMB proti řadiči domény. 

**TP, B-TP nebo FP**

Bezpečnostní skenery a aplikace může oprávněně dotazovat řadiče domény na otevřenými relacemi SMB.

1. Tento zdrojový počítač by měl generovat aktivity tohoto typu?
2. Existuje nějaký druh kontrolu zabezpečení, které běží na zdrojovém počítači?  
    Pokud odpovíte Ano, je pravděpodobně B-TP aktivity. *Zavřít* zabezpečení výstrahy a vyloučit tento počítač.
3. Zaškrtněte uživatele, které provádí operaci.
   Mají tito uživatelé provádět tyto akce?  
    Pokud odpovíte Ano, *Zavřít* dané výstraze zabezpečení jako aktivita B-TP.

**Vysvětlení rozsahu porušení**

1. Prozkoumejte zdrojový počítač.  
2. Na stránce výstrah zkontrolujte, jestli jsou všechny odhalených uživatelů. Aby to prověřili jednotlivých ohrožených uživatelů, zkontrolujte svůj profil. Doporučujeme že začít šetření s uživateli šetření citlivé a vysokou prioritou.

**Navrhované nápravné kroky a pro ochrany před únikem informací**

Použití [Net ukončí nástroj](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) Posilte zabezpečení vašeho prostředí vůči útoku.

## <a name="user-and-group-membership-reconnaissance-samr-external-id-2021"></a>Rekognoskace členství uživatelů a skupin (SAMR) (externí ID 2021) 


*Předchozí název:* Rekognoskace pomocí dotazů na adresářové služby 

**Popis** uživatele a skupiny členství rekognoskace se útočníci používají ke zmapování struktury adresáře a zacílení privilegovaných účtů pro pozdější kroky útoku. Protokol vzdáleného správce zabezpečení účtů (SAM-R) je jedna z metod používaných k dotazování adresáře k provedení tohoto typu mapování.  
Při zjišťování žádné výstrahy týkající se aktivují první měsíc po nasazení služby Azure ATP (období učení). Během učení období, ochrana ATP v programu Azure profily které dotazy SAM-R se sestavují z které počítače výčet a jednotlivé dotazy citlivých účtů. 

**Období učení**

Čtyři týdny každý řadič domény od první aktivitu sítě SAMR, proti konkrétní řadič domény.

**TP, B-TP nebo FP** 

1. Klikněte na zdrojový počítač, přejděte na stránku jeho profil.        
   - Zdrojový počítač by měl generovat aktivity tohoto typu?
     - Pokud ano, *Zavřít* zabezpečení výstrahy a vyloučit tento počítač jako **B-TP** aktivity. 
   - Zkontrolujte uživatele/s, který provedl operaci.
     - Tito uživatelé běžně protokolovat do zdrojového počítače, nebo jsou správci, kteří by měl provádět tyto konkrétní akce?   
     - Zkontrolujte profil uživatele a jejich souvisejícími uživatelskými aktivity. Pochopení jejich chování v režimu normálního uživatele a hledat další podezřelých aktivit pomocí [uživatelská příručka k vyšetřování](investigate-a-user.md). 
    
     Pokud vaše odpověď **Ano** na předchozí výše, *Zavřít* výstrahu jako **B-TP** aktivity. 
  
**Vysvětlení rozsahu porušení**

1. Zkontrolujte dotazy, které byly provedeny, například Enterprise admins nebo správce a určit, pokud byli úspěšní.
2. Prozkoumání jednotlivých vystavené uživatele s využitím v uživatelské příručce šetření.
3. Prozkoumejte zdrojový počítač.  
  
**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Obsahují zdrojový počítač.
2. Vyhledat a odstranit nástroj, který provádí útoku.
3. Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu jako aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.
4. Resetovat heslo uživatele zdroje a povolit vícefaktorové ověřování.
5. Použít přístup k síti a omezovat klienty moct vzdáleně volat SAM zásad skupiny.

> [!NOTE]
> Zakázat všechny výstrahy zabezpečení služby Azure ATP, obraťte se na podporu.

> [!div class="nextstepaction"]
> [Upozornění kurzu ohrožení zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)

## <a name="see-also"></a>Viz také

- [Prošetřování počítačů](investigate-a-computer.md)
- [Prošetřování uživatelů](investigate-a-user.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před taktikou lateral movement](atp-lateral-movement-alerts.md)
- [Výstrahy před dominancí v doméně](atp-domain-dominance-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)
- [Referenční informace k protokolům Azure ATP SIEM](cef-format-sa.md)
- [Práce s cesty taktiky Lateral Movement](use-case-lateral-movement-path.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

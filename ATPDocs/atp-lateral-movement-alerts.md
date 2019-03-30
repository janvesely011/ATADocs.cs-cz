---
title: Ochrana ATP v programu Azure laterální pohyb výstrahy zabezpečení | Dokumentace Microsoftu
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of lateral movement phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/18/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2257eb00-8614-4577-b6a1-5c65085371f2
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7d6ace87ba8f27b70ecb81de2ac8f07ab5bc214a
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674788"
---
# <a name="tutorial-lateral-movement-alerts"></a>Kurz: Upozornění taktiky Lateral Movement  

Obvykle kybernetických útoků jsou spouštěny proti jakémukoli subjektu přístupné, jako je například uživatel s nízkým oprávněním a potom rychle následně k laterálnímu pohybu dokud útočník získá přístup k cenný majetek, který. Cenný majetek, který může být citlivých účtů, správci domény nebo vysoce citlivá data. Ochrana ATP v programu Azure identifikuje tyto důmyslných hrozeb ve zdrojovém kódu v celém řetězu událostí útoku a klasifikuje do následujících fází:

1. [Rekognoskace](atp-reconnaissance-alerts.md)
2. [Zneužití přihlašovacích údajů](atp-compromised-credentials-alerts.md)
3. **Taktiky Lateral Movement**
4. [Dominance v doméně](atp-domain-dominance-alerts.md)
5. [Průsak ven](atp-exfiltration-alerts.md)

Další informace o tom, jak pochopit strukturu a běžné součásti všech výstrah zabezpečení ochrany ATP v programu Azure najdete v tématu [Principy výstrah zabezpečení](understanding-security-alerts.md).

Výstrahy pomáhají identifikovat a napravit následující zabezpečení **taktiky Lateral Movement** fáze podezřelých aktivitách zjištěných ochrany ATP v programu Azure ve vaší síti. V tomto kurzu se dozvíte, jak pochopit, klasifikovat, opravit a brání následující typy útoků:

> [!div class="checklist"]
> * Vzdálené spuštění kódu nad DNS (externí ID 2036)
> * Krádež identity podezřelého softwaru (pass-the-hash) (externí ID 2017)
> * Krádež identity podezřelého softwaru (pass-the-ticket) (externí ID 2018)
> * Podezření na útok přenosového protokolu NTLM (účet Exchange) (externí ID 2037) – preview
> * Podezření na útok overpass-the-hash (oslabení šifrování) (externí ID 2008)
> * Podezření na útok overpass-the-hash (Kerberos) (externí ID 2002)

## <a name="remote-code-execution-over-dns-external-id-2036"></a>Vzdálené spuštění kódu nad DNS (externí ID 2036)

**Popis**

Publikované 12/11/2018 Microsoft [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626), oznamujeme, že existuje nově zjištěných vzdálené spuštění kódu na serverech Windows systému DNS (Domain Name). V toto ohrožení zabezpečení servery nepodaří správně zpracovávat požadavky. Útočník, který tuto chybu zabezpečení úspěšně zneužije, může spustit libovolný kód v kontextu místního systémového účtu. Servery Windows aktuálně nakonfigurované jako servery DNS vystavují se riziku toto ohrožení zabezpečení.

V této detekce se aktivuje upozornění zabezpečení služby Azure ATP při podezření na zneužití ohrožení zabezpečení CVE-2018-8626 dotazy DNS se provádí na řadiči domény v síti.

**TP, B-TP nebo FP**

1. Cílové počítače jsou aktuální a patched proti CVE-2018-8626? 
    - Pokud jsou počítače v aktuálním stavu a opravou, **Zavřít** dané výstraze zabezpečení jako **FP**.
2. Byla služba vytvořena nebo neznámého proces spuštěn v době výskytu útoku
    - Pokud se nenajde žádné nové služby nebo neznámého procesu, **Zavřít** dané výstraze zabezpečení jako **FP**. 
3. Tento typ útoku může dojít k selhání služby DNS před recyklováním úspěšně provádění kódu.
    - Zaškrtněte, pokud několikrát v době výskytu útoku se restartoval službu DNS.
    - Pokud DNS byl restartován, byl pravděpodobně pokus o zneužití CVE-2018-8626. Vezměte v úvahu tuto výstrahu **TP** a postupujte podle pokynů v **pochopit tak rozsah porušení**. 

**Vysvětlení rozsahu porušení**

- Prozkoumat [zdrojový a cílový počítač](investigate-a-computer.md).

**Navrhované nápravné kroky a pro ochrany před únikem informací**

**Náprava**

1. Obsahovat řadiče domény. 
    1. Opravte pokus o spuštění vzdáleného kódu.
    2. Vyhledejte uživatelé také přihlášení přibližně ve stejnou dobu jako podezřelou aktivitu, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování. 
2. Obsahují zdrojový počítač.
    1. Najít nástroj, který provádí útoku a jeho odebrání.
    2. Vyhledejte uživatelé také přihlášení přibližně ve stejnou dobu jako podezřelou aktivitu, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.

**Ochrany před únikem informací**

- Ujistěte se, že všechny servery DNS v prostředí jsou aktuální a patched proti [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626). 

## <a name="suspected-identity-theft-pass-the-hash-external-id-2017"></a>Krádež identity podezřelého softwaru (pass-the-hash) (externí ID 2017)

*Předchozí název:* Krádež identity pomocí útoku Pass-the-Hash

**Popis**

Pass-the-Hash je technika laterálního pohybu, kdy útočník získá NTLM hash uživatele z jednoho počítače a použije ho k získání přístupu k jinému počítači.

**TP, B-TP nebo FP?**
1. Určit, pokud byl použit-the-hash z počítače, které uživatel používá pravidelně? 
    - Pokud byl použit algoritmus hash z počítačů používat pravidelně, **Zavřít** výstrahu jako **FP**.  
 
**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový a cílový počítač](investigate-a-computer.md) dále.  
2. Prozkoumat [dojde k ohrožení bezpečnosti uživatelského](investigate-a-computer.md).
 
**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Resetovat heslo uživatele, zdroje a povolit vícefaktorové ověřování.
2. Obsahují zdrojový a cílový počítač.
3. Najít nástroj, který provádí útoku a jeho odebrání.
4. Hledejte uživatele přihlášené přibližně ve stejnou dobu aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.

## <a name="suspected-identity-theft-pass-the-ticket-external-id-2018"></a>Krádež identity podezřelého softwaru (pass-the-ticket) (externí ID 2018)

*Předchozí název:* Krádež identity pomocí útoku Pass-the-Ticket

**Popis**

Pass-the-Ticket je technika laterálního pohybu, kdy útočník získá lístek Kerberos z jednoho počítače a použije ho k získání přístupu k jinému počítači opětovným použitím odcizených lístků. Při zjišťování je zobrazena lístek protokolu Kerberos používá na dvou (nebo více) různých počítačích.

**TP, B-TP nebo FP?**

Úspěšně překladu IP adres počítačům v organizaci je důležitá pro identifikaci útoků pass-the-ticket z jednoho počítače do jiného. 

1. Zaškrtněte, pokud jeden nebo oba počítače IP adresa patří k podsíti, která je přidělena z nedostatečné velikosti fondu adres DHCP, například VPN, Wi-Fi nebo VDI? 
2. IP adresa sdílí (například zařízení NAT)?  
3. Řešení není senzor nejméně jeden z cílové IP adresy? Pokud cílová IP adresa není vyřešen, může to znamenat, že správné porty mezi ze senzorů a zařízení nejsou otevřené správně. 

    Pokud je odpověď na všechny předchozí otázky **Ano**, zkontrolujte, jestli počítače zdroje a cíle jsou stejné. Pokud se shodují, je **FP** nebyly žádné skutečné pokusy o **pass-the-ticket**. 

[Vzdálené Credential Guard](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard) funkce připojení RDP, když použít spolu s Windows 10 na Windows serveru 2016 a novější, může způsobit **B-TP** výstrahy. Používání výstrah důkazy, zkontrolujte, pokud uživatel provést připojení ke vzdálené ploše ze zdrojového počítače do cílového počítače.

1. Kontrola pro korelaci důkaz.
2. Pokud je existuje korelace důkazy, podívejte se, pokud bylo navázáno připojení RDP pomocí vzdáleného Credential Guard. 
3. Pokud odpovíte Ano, **Zavřít** dané výstraze zabezpečení jako **T BP** aktivity. 

Existují vlastní aplikace, které dál lístky jménem uživatelů. Tyto aplikace mají oprávnění pro delegování do uživatelských lístků.

1. Je typ vlastní aplikace jako ten výše popsaný, aktuálně na cílových počítačích? Služby, které je aplikace spuštěna? Jsou služby jednají jménem uživatelů, například přístupu do databází?
    - Pokud odpovíte Ano, **Zavřít** dané výstraze zabezpečení jako **T BP** aktivity.
2. Je cílový počítač delegování server?
    - Pokud odpovíte Ano, **Zavřít** zabezpečení výstrahy a vyloučit tento počítač jako **T BP** aktivity.
 
**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový a cílový počítač](investigate-a-computer.md).  
2. Prozkoumat [dojde k ohrožení bezpečnosti uživatelského](investigate-a-computer.md). 

**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Resetovat heslo uživatele, zdroje a povolit vícefaktorové ověřování.
2. Obsahují zdrojový a cílový počítač.
3. Najít nástroj, který provádí útoku a jeho odebrání.
4. Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu jako aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.
5. Pokud máte nainstalovaný – programu Windows Defender ATP použít **vyprázdnit klist.exe** odstranit všechny lístky zadané přihlašovací relace a zabránit dalším využívání lístky.

## <a name="suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview"></a>Podezření na útok přenosového protokolu NTLM (účet Exchange) (externí ID 2037) – preview

**Popis**

Exchange Server lze nastavit k aktivaci ověřování protokolem NTLM účtem systému Exchange Server vzdálené http serveru spustit ze strany útočníka. Tento server čeká na serveru Exchange Server komunikace předat vlastní citlivé ověřování na libovolný server nebo dokonce i další zajímavé ke službě Active Directory přes LDAP a získá informace o ověřování.

Jakmile obdrží server předávací ověřování protokolem NTLM, poskytuje výzvu, který byl původně vytvořen na cílový server. Klient odpoví na výzvu, zabraňuje útočníkovi trvá odpověď a použít ho k pokračovat vyjednávání protokolu NTLM se cílového řadiče domény. 

V této detekce se aktivuje upozornění při identifikaci ochrany ATP v programu Azure použijte přihlašovací údaje účtu Exchange z podezřelých zdroje.

**TP, B-TP nebo FP?**

1. Kontrola zdrojového počítače za bránou IP adresy. 
    1. Pokud zdrojový počítač je Exchange Server, **Zavřít** dané výstraze zabezpečení jako **FP** aktivity.
    2. Určuje, pokud zdrojový účet by měl ověřit pomocí protokolu NTLM z těchto počítačů? Pokud se musí ověřit, **Zavřít** zabezpečení výstrahy a vylučte tyto počítače jako **B-TP** aktivity.

**Vysvětlení rozsahu porušení**

1. Pokračovat [zkoumání zdrojových počítačích](investigate-a-computer.md) za používané IP adresy.  
2. Prozkoumat [účet zdrojové](investigate-a-user.md).

**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Obsahují zdrojových počítačích
    1. Najít nástroj, který provádí útoku a jeho odebrání.
    2. Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu aktivity došlo k chybě, protože může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.
2. Vynutit používání zapečetěné NTLMv2 v doméně pomocí **zabezpečení sítě: Úroveň ověřování pro systém LAN Manager** zásady skupiny. Další informace najdete v tématu [úrovně pokyny programu LAN Manager ověřování](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) pro nastavení zásad skupiny pro řadiče domény. 

## <a name="suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008"></a>Podezření na útok overpass-the-hash (oslabení šifrování) (externí ID 2008) 

*Předchozí název:* Aktivita snížení úrovně šifrování

**Popis**

Oslabení šifrování je metoda oslabení oslabení šifrování různých polí protokolu, obvykle šifrována pomocí nejvyšší úrovně šifrování pomocí protokolu Kerberos. Oslabeným šifrované pole může být snazší target na offline útoky hrubou silou při pokusech. Různých metod útoku zvýšit využití slabé šifrování doklad protokolu Kerberos. V tomto zjišťování služby Azure ATP učí typy šifrování pomocí protokolu Kerberos, počítačů a uživatelů a upozornění, že vás, když je slabší šifrovací používá server, který neobvyklé, že u zdrojového počítače nebo uživatele a odpovídá techniky známých útoků. 

V over-pass-the-hash útok útočník využije k vytvoření lístku silné žádost Kerberos AS slabé odcizené hodnoty hash. Při zjišťování jsou zjištěny instance, kde je downgradovat typ šifrování zprávy AS_REQ ze zdrojového počítače, ve srovnání s dřív zjištěné chování (počítač používá AES).

**TP, B-TP nebo FP?**
1. Určete, jestli nedávno změnit konfiguraci čipové karty. 
   - Účty používané nedávno mají změny konfigurace pomocí čipové karty?  
    
     Pokud odpovíte Ano, **Zavřít** dané výstraze zabezpečení jako **T BP** aktivity. 

Některé legitimní materiálů nepodporují silné šifrování šifry a toto upozornění mohou aktivovat. 

2. Všechny zdroje uživatelé sdílet něco? 
   1. Například všechny marketingové pracovníky ve vaší organizaci přistupují konkrétní prostředek, který by mohl způsobit aktivovat upozornění?
   2. Podívejte se na zdroje přistupuje těchto lístků. 
       - Zaškrtnutím tohoto políčka ve službě Active Directory tak, že zkontrolujete atribut *msDS-SupportedEncryptionTypes*, prostředků účtu služby.
   3. Pokud existuje pouze jeden prostředek používaná, zkontrolujte, zda není platný prostředek pro tyto uživatele bude možné získat přístup.   

      Pokud je odpověď na jednu z předchozí otázky **Ano**, je pravděpodobné, že **T BP** aktivity. Zkontrolujte prostředku může podporovat silné šifrování šifer s nižší sílou,-li implementovat šifer s nižší sílou silnější šifrování, kde je to možné, a **Zavřít** dané výstraze zabezpečení.

**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový počítač](investigate-a-computer.md).  
2. Prozkoumat [dojde k ohrožení bezpečnosti uživatelského](investigate-a-computer.md). 

**Navrhované nápravné kroky a pro ochrany před únikem informací** 

**Náprava**
1. Resetovat heslo uživatele, zdroje a povolit vícefaktorové ověřování. 
2. Obsahují zdrojový počítač. 
3. Najít nástroj, který provádí útoku a jeho odebrání. 
4. Vyhledejte uživatelé přihlášení v době aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování  

**Ochrany před únikem informací**
 
1. Konfigurace vaší domény pro podporu silného šifrování doklad a odebrat *šifrování pomocí protokolu Kerberos DES*. Další informace o [typy šifrování a protokolu Kerberos](https://blogs.msdn.microsoft.com/openspecification/2011/05/30/windows-configurations-for-kerberos-supported-encryption-type/). 
2. Ujistěte se, že je úroveň funkčnosti domény nastavená pro podporu silného šifrování doklad.  
3. Dávat přednost použití aplikace, které podporují doklad silné šifrování.

## <a name="suspected-overpass-the-hash-attack-kerberos-external-id-2002"></a>Podezření na útok overpass-the-hash (Kerberos) (externí ID 2002) 

*Předchozí název:* Neobvyklá implementace protokolu Kerberos (možný útok overpass-the-hash)

**Popis**

Útočníci používají nástroje, které implementují nestandardním způsobem různé protokoly, například pomocí protokolů Kerberos a protokolu SMB. Microsoft Windows přijímá tento typ síťového provozu bez upozornění, je ochrana ATP v programu Azure rozpoznat potenciální škodlivým činnostem. Chování je indikátorem techniky, jako je například over-pass-the-hash, útoky hrubou silou a zneužití pokročilé ransomwaru například WannaCry, se používají.

**TP, B-TP nebo FP?**

Někdy aplikace implementovat vlastní zásobník protokolu Kerberos, není v souladu s RFC protokolu Kerberos. 

1. Zaškrtněte, pokud zdrojovém počítači běží aplikace s vlastní zásobník protokolu Kerberos, není v souladu s RFC protokolu Kerberos.  
2. Pokud zdrojovém počítači běží takové aplikace, a měla by **není** to udělat, opravte konfiguraci aplikace. **Zavřít** dané výstraze zabezpečení jako **T BP** aktivity.  
3. Pokud zdrojovém počítači běží takovou aplikaci a mělo by to uděláte tak, **Zavřít** dané výstraze zabezpečení jako **T BP** aktivity a vyloučit počítače. 

**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový počítač](investigate-a-computer.md).  
2. Pokud je [zdrojový uživatel](investigate-a-user.md), prozkoumat. 

**Navrhované nápravné kroky a pro ochrany před únikem informací** 

1. Resetovat hesla ohrožených uživatelů a povolte vícefaktorové ověřování.
2. Obsahují zdrojový počítač.
3. Najít nástroj, který provádí útoku a jeho odebrání.
4. Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu jako podezřelou aktivitu, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.  
5. Resetování hesel uživateli zdroje a povolit vícefaktorové ověřování.

> [!div class="nextstepaction"]
> [Upozornění kurzu dominance v doméně](atp-domain-dominance-alerts.md)

## <a name="see-also"></a>Viz také

- [Prošetřování počítačů](investigate-a-computer.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Práce s cesty taktiky Lateral Movement](use-case-lateral-movement-path.md)
- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před dominancí v doméně](atp-domain-dominance-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

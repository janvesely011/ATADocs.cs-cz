---
title: Výstrahy zabezpečení na bočním místě Azure ATP | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of lateral movement phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 08/05/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2257eb00-8614-4577-b6a1-5c65085371f2
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: dd78f2d18010b043dc58bfb6fac24429a36ba2f1
ms.sourcegitcommit: 8df26fb312472b8df1da70e581517223d26de8c2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/05/2019
ms.locfileid: "68781841"
---
# <a name="tutorial-lateral-movement-alerts"></a>Návodu Výstrahy před taktikou lateral movement  

Obvykle se internetoví útoky spouští na jakékoli přístupné entitě, jako je uživatel s nízkým oprávněním, a pak se rychle přesune později, dokud útočník nezíská přístup k cenným assetům. Cenné prostředky můžou být citlivé účty, správci domény nebo citlivá data. Azure ATP identifikuje tyto rozšířené hrozby ve zdroji v celém rámci celého řetězce dezaktivačního útoku a klasifikuje je v následujících fázích:

1. [Rekognoskace](atp-reconnaissance-alerts.md)
2. [Napadené přihlašovací údaje](atp-compromised-credentials-alerts.md)
3. **Boční pohyb**
4. [Dominantní doména](atp-domain-dominance-alerts.md)
5. [Exfiltrace](atp-exfiltration-alerts.md)

Další informace o tom, jak pochopit strukturu a společné komponenty všech výstrah zabezpečení Azure ATP, najdete v tématu [Vysvětlení výstrah zabezpečení](understanding-security-alerts.md).

Následující výstrahy zabezpečení vám pomůžou identifikovat a opravit podezřelé aktivity fáze **přesunu** zjištěné službou Azure ATP ve vaší síti. V tomto kurzu se dozvíte, jak pochopit, klasifikovat, opravit a zabránit těmto typům útoků:

> [!div class="checklist"]
> * Vzdálené spuštění kódu přes DNS (externí ID 2036)
> * Podezření na krádež identity (pass-the-hash) (externí ID 2017)
> * Podezření na krádež identity (pass-the-Ticket) (externí ID 2018)
> * Podezření na manipulaci s ověřováním NTLM (externí ID 2039) 
> * Podezřelý útok útoku NTLM (účet Exchange) (externí ID 2037)
> * Podezřelý útok Overpass-the-hash (v downgradu šifrování) (externí ID 2008)
> * Podezřelá Overpass-the-hash – útok (Kerberos) (externí ID 2002)

## <a name="remote-code-execution-over-dns-external-id-2036"></a>Vzdálené spuštění kódu přes DNS (externí ID 2036)

**Popis**

12/11/2018 společnost Microsoft zveřejnila [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626)a oznamuje, že nově zjištěná zranitelnost vzdáleného spuštění kódu existuje v serverech DNS (Domain Name System) systému Windows. V této chybě zabezpečení nejsou servery správně zpracovávat požadavky. Útočník, který úspěšně zneužije chybu zabezpečení, může spustit libovolný kód v kontextu místního systémového účtu. Pro tuto chybu zabezpečení jsou ohroženy servery Windows aktuálně nakonfigurované jako servery DNS.

V tomto zjišťování se aktivuje výstraha zabezpečení Azure ATP, když se dotazy DNS, které jsou podezřelé z zneužití chyby zabezpečení CVE-2018-8626, provedou na řadiči domény v síti.

**TP, B-TP nebo FP**

1. Jsou cílové počítače aktuální a jsou opravené oproti CVE-2018-8626? 
    - Pokud jsou počítače v aktuálním stavu a opraveny, **zavřete** výstrahu zabezpečení jako **FP**.
2. Byla vytvořena služba nebo nebyl spuštěn neznámý proces kolem doby útoku.
    - Pokud se nenajde žádná nová služba ani neznámý proces, **zavřete** výstrahu zabezpečení jako **FP**. 
3. Tento typ útoku může způsobit chybu služby DNS před tím, než úspěšně vykonávání kódu.
    - Ověřte, zda se služba DNS několikrát restartovala okolo doby útoku.
    - Pokud byl server DNS restartován, byl nejspíš pokus o zneužití CVE-2018-8626. Zvažte toto upozornění v **transakčním** programu a postupujte podle pokynů v tématu **pochopení rozsahu porušení**. 

**Pochopení rozsahu porušení**

- Prozkoumejte [zdrojový a cílový počítač](investigate-a-computer.md).

**Navrhovaná náprava a kroky pro prevenci**

**Náprava**

1. Obsahuje řadiče domény. 
    1. Opravte pokus o vzdálené spuštění kódu.
    2. Hledání uživatelů se také může přihlásilo přibližně ve stejnou dobu jako podezřelá aktivita, jak mohou být ohroženy také. Resetujte hesla a povolte MFA. 
2. Obsahují zdrojový počítač.
    1. Najít nástroj, který provádí útoku a jeho odebrání.
    2. Hledání uživatelů se také může přihlásilo přibližně ve stejnou dobu jako podezřelá aktivita, jak mohou být ohroženy také. Resetujte hesla a povolte MFA.

**Únikem**

- Zajistěte, aby všechny servery DNS v prostředí byly aktuální a byly opraveny v porovnání [s CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626). 

## <a name="suspected-identity-theft-pass-the-hash-external-id-2017"></a>Podezření na krádež identity (pass-the-hash) (externí ID 2017)

*Předchozí název:* Krádež identity pomocí útoku Pass-the-Hash

**Popis**

Pass-the-Hash je technika laterálního pohybu, kdy útočník získá NTLM hash uživatele z jednoho počítače a použije ho k získání přístupu k jinému počítači.

**TRANSAKČNÍ program, B-TP nebo FP?**
1. Určete, jestli se hodnota hash použila z počítačů, které uživatel pravidelně používá? 
    - Pokud byl algoritmus hash použit z pravidelně používaných počítačů, **zavřete** výstrahu jako **FP**.  
 
**Pochopení rozsahu porušení**

1. Podrobněji Prozkoumejte [zdrojové a cílové počítače](investigate-a-computer.md) .  
2. Prozkoumejte [ohroženého uživatele](investigate-a-computer.md).
 
**Navrhovaná náprava a kroky pro prevenci**

1. Resetujte heslo ke zdrojovému uživateli a povolte MFA.
2. Obsahují zdrojové a cílové počítače.
3. Najít nástroj, který provádí útoku a jeho odebrání.
4. Vyhledat uživatele přihlášené kolem stejné doby aktivity, jak mohou být ohroženy také. Resetujte hesla a povolte MFA.

## <a name="suspected-identity-theft-pass-the-ticket-external-id-2018"></a>Podezření na krádež identity (pass-the-Ticket) (externí ID 2018)

*Předchozí název:* Krádež identity pomocí útoku Pass-the-Ticket

**Popis**

Pass-the-Ticket je technika laterálního pohybu, kdy útočník získá lístek Kerberos z jednoho počítače a použije ho k získání přístupu k jinému počítači opětovným použitím odcizených lístků. Při zjišťování je zobrazena lístek protokolu Kerberos používá na dvou (nebo více) různých počítačích.

**TRANSAKČNÍ program, B-TP nebo FP?**

Úspěšné překladu IP adres na počítače v organizaci je důležité k identifikaci útoků typu Pass-The-Ticket z jednoho počítače do druhého. 

1. Ověřte, jestli IP adresa jednoho nebo obou počítačů patří do podsítě, která je přidělená z nedostatečného fondu DHCP, například VPN, VDI nebo Wi-Fi? 
2. Sdílí se IP adresa (například zařízením NAT)?  
3. Neřeší tento senzor jednu nebo více cílových IP adres? Pokud cílová IP adresa není vyřešená, může to znamenat, že se správně neotevřou správné porty mezi senzorem a zařízeními. 

    Pokud je odpověď na některou z předchozích otázek **Ano**, ověřte, zda jsou zdrojové a cílové počítače stejné. Pokud jsou stejné, jedná se o **FP** a při **průchodu Pass-The-Ticket**se neobjevily žádné reálné pokusy. 

Funkce [Remote Credential Guard](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard) připojení RDP, pokud se používá s Windows 10 na windows serveru 2016 a novějším, může způsobovat výstrahy **B-TP** . Pomocí legitimace výstrahy ověřte, zda uživatel provedl připojení ke vzdálené ploše ze zdrojového počítače do cílového počítače.

1. Podívejte se na korelační legitimace.
2. Pokud existuje korelace, ověřte, zda bylo připojení RDP provedeno pomocí vzdálené ochrany přihlašovacích údajů. 
3. Pokud je odpověď ano, **zavřete** výstrahu zabezpečení jako aktivitu **T-BP** . 

K dispozici jsou vlastní aplikace, které předávají lístky jménem uživatelů. Tyto aplikace mají pro lístky uživatele práva pro delegování.

1. Je vlastní typ aplikace, například dříve popsaná, aktuálně na cílových počítačích? Které služby aplikace spouští? Mají služby, které jednají jménem uživatelů, například přístup k databázím?
    - Pokud je odpověď ano, **zavřete** výstrahu zabezpečení jako aktivitu **T-BP** .
2. Je cílový počítač serverem delegování?
    - Pokud je odpověď ano, **zavřete** výstrahu zabezpečení a vylučte tento počítač jako aktivitu **T-BP** .
 
**Pochopení rozsahu porušení**

1. Prozkoumejte [zdrojový a cílový počítač](investigate-a-computer.md).  
2. Prozkoumejte [ohroženého uživatele](investigate-a-computer.md). 

**Navrhovaná náprava a kroky pro prevenci**

1. Resetujte heslo ke zdrojovému uživateli a povolte MFA.
2. Obsahují zdrojové a cílové počítače.
3. Najít nástroj, který provádí útoku a jeho odebrání.
4. Vyhledejte uživatele přihlášené přibližně ve stejnou dobu jako aktivita, jak mohou být ohroženy také. Resetujte hesla a povolte MFA.
5. Pokud máte nainstalované ochrany ATP v programu Windows Defender – pomocí **příkaz Klist (. exe** odstraňte všechny lístky zadané přihlašovací relace a zabraňte budoucímu používání lístků.

## <a name="suspected-ntlm-authentication-tampering-external-id-2039"></a>Podezření na manipulaci s ověřováním NTLM (externí ID 2039)

V červnu 2019 mohla společnost Microsoft zveřejnila [bezpečnostní ohrožení zabezpečení CVE-2019-1040](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1040)a oznamuje zjišťování nové chyby zabezpečení v systému Microsoft Windows, když útok "man-in-the-middle" dokáže úspěšně obejít mikrofon protokolu NTLM (kontrola integrity zpráv). antivirový.

Škodlivé objekty actor, které úspěšně využívají tuto chybu zabezpečení, mají možnost downgradovat funkce zabezpečení NTLM a můžou úspěšně vytvářet ověřené relace jménem jiných účtů. Neopravované servery Windows jsou ohrožené touto chybou zabezpečení.
 
V tomto zjišťování se aktivuje výstraha zabezpečení ATP Azure ATP, když žádosti o ověření NTLM podezřelé z zneužití chyby zabezpečení zjištěné v [CVE-2019-1040](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1040) probíhají na řadiči domény v síti.

**TRANSAKČNÍ program, B-TP nebo FP?**

1.  Jsou zahrnuté počítače, včetně řadičů domény, aktualizované a opravené oproti [CVE-2019-1040](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1040)? v případě, že jsou počítače v aktuálním stavu a opraveny, očekáváme, že ověřování selže. Pokud se ailed ověřování, **zavřete** výstrahu zabezpečení jako neúspěšný pokus.
 
**Pochopení rozsahu porušení**
1.  Prozkoumejte [zdrojové počítače](investigate-a-computer.md).
2.  Prozkoumejte [zdrojový účet](investigate-a-user.md).

**Navrhovaná náprava a kroky pro prevenci**

**Náprava**
1.  Obsahuje zdrojové počítače.
2.  Najít nástroj, který provádí útoku a jeho odebrání.
3.  Vyhledejte uživatele přihlášené přibližně ve stejnou dobu, jako by došlo k aktivitě, protože mohou být ohroženy také. Resetujte hesla a povolte MFA.
4.  Vynutit použití zapečetěných NTLMv2 v doméně pomocí **zabezpečení sítě: Zásady** skupiny pro ověřování LAN Manager. Další informace najdete v tématu [pokyny pro ověřování v programu LAN Manager](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) pro nastavení zásad skupiny pro řadiče domény.
 
**Prevence** • zajistěte, aby všechna zařízení v prostředí byla aktuální, a byla opravena s chybou [CVE-2019-1040](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1040).

## <a name="suspected-ntlm-relay-attack-exchange-account-external-id-2037"></a>Podezřelý útok útoku NTLM (účet Exchange) (externí ID 2037)

**Popis**

Systém Exchange Server je možné nakonfigurovat tak, aby aktivoval ověřování NTLM s účtem Exchange serveru na vzdálený server http spuštěný útočníkem. Tento server počká, než komunikace s Exchange serverem přenáší své vlastní citlivé ověřování na jakýkoli jiný server nebo ještě více zájmů služby Active Directory přes protokol LDAP, a připraví ověřovací údaje.

Jakmile Server Relay obdrží ověřování NTLM, poskytne mu výzvu, která byla původně vytvořena cílovým serverem. Klient odpoví na výzvu, zabrání útočníkovi v přijetí odpovědi a použije ho k pokračování vyjednávání protokolu NTLM s cílovým řadičem domény. 

V tomto zjišťování se aktivuje výstraha, když Azure ATP identifikuje přihlašovací údaje účtu Exchange z podezřelého zdroje.

**TRANSAKČNÍ program, B-TP nebo FP?**

1. Kontrolovat zdrojové počítače za IP adresami. 
    1. Pokud je zdrojový počítač Exchange Server, **zavřete** výstrahu zabezpečení jako aktivitu **FP** .
    2. Určete, jestli se má zdrojový účet ověřit pomocí protokolu NTLM z těchto počítačů? Pokud by se měly ověřit, **zavřete** výstrahu zabezpečení a Vylučte tyto počítače jako aktivitu **B-TP** .

**Pochopení rozsahu porušení**

1. Pokračujte [ve zkoumání zdrojových počítačů](investigate-a-computer.md) za IP adresami, které jsou v něm zapojené.  
2. Prozkoumejte [zdrojový účet](investigate-a-user.md).

**Navrhovaná náprava a kroky pro prevenci**

1. Obsahuje zdrojové počítače.
    1. Najděte nástroj, který předá útok, a odeberte ho.
    2. Vyhledejte uživatele přihlášené přibližně ve stejnou dobu, jako by došlo k aktivitě, protože mohou být ohroženy také. Resetujte hesla a povolte MFA.
2. Vynutit použití zapečetěných NTLMv2 v doméně pomocí **zabezpečení sítě: Zásady** skupiny pro ověřování LAN Manager. Další informace najdete v tématu [pokyny pro ověřování v programu LAN Manager](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) pro nastavení zásad skupiny pro řadiče domény. 

## <a name="suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008"></a>Podezřelý útok Overpass-the-hash (v downgradu šifrování) (externí ID 2008) 

*Předchozí název:* Aktivita v downgradu šifrování

**Popis**

Downgrade šifrování je metoda oslabení protokolu Kerberos pomocí šifrování. downgrade různých polí protokolu se obvykle šifrují pomocí nejvyšší úrovně šifrování. Oslabeným šifrované pole může být snazší target na offline útoky hrubou silou při pokusech. Různých metod útoku zvýšit využití slabé šifrování doklad protokolu Kerberos. V této detekci zjistí Azure ATP typy šifrování Kerberos používané počítači a uživateli a upozorní vás, když se použije slabší šifrováním, který je pro zdrojový počítač neobvyklý, a/nebo uživatel a odpovídá známým technikům útoku. 

V případě útoku over-pass-the-hash může útočník použít slabý autentizační algoritmus hash k vytvoření silného lístku s protokolem Kerberos jako žádosti. V takovém případě se instance zjišťují, kde se v porovnání s dříve zjištěným chováním (počítač používal AES) downgrade typ šifrování zprávy AS_REQ ze zdrojového počítače.

**TRANSAKČNÍ program, B-TP nebo FP?**
1. Zjistěte, jestli se nedávno změnila konfigurace čipové karty. 
   - Zahrnovaly tyto účty nedávno změny konfigurace čipové karty?  
    
     Pokud je odpověď ano, **zavřete** výstrahu zabezpečení jako aktivitu **T-BP** . 

Některé legitimní prostředky nepodporují silné šifrovací šifry a mohou aktivovat tuto výstrahu. 

2. Sdílí všichni zdrojový uživatel něco? 
   1. Například všichni vaši pracovníci marketingu přistupují k určitému prostředku, který by mohl způsobit aktivaci výstrahy?
   2. Podívejte se na zdroje přistupuje těchto lístků. 
       - Zaškrtnutím tohoto políčka ve službě Active Directory tak, že zkontrolujete atribut *msDS-SupportedEncryptionTypes*, prostředků účtu služby.
   3. Pokud je k dispozici pouze jeden prostředek, ověřte, zda se jedná o platný prostředek pro přístup k těmto uživatelům.   

      Pokud je odpověď na jednu z předchozích otázek **Ano**, může to být aktivita **T-BP** . Ověřte, zda prostředek může podporovat silné šifrovací šifrování, pokud je to možné, implementujte silnější šifrovací šifru a **zavřete** výstrahu zabezpečení.

**Pochopení rozsahu porušení**

1. Prozkoumejte [zdrojový počítač](investigate-a-computer.md).  
2. Prozkoumejte [ohroženého uživatele](investigate-a-computer.md). 

**Navrhovaná náprava a kroky pro prevenci** 

**Náprava**
1. Resetujte heslo ke zdrojovému uživateli a povolte MFA. 
2. Obsahují zdrojový počítač. 
3. Najít nástroj, který provádí útoku a jeho odebrání. 
4. Vyhledejte uživatele přihlášené kolem doby aktivity, jak mohou být ohroženy také. Resetování hesel a povolení vícefaktorového ověřování  

**Únikem**
 
1. Nakonfigurujte doménu tak, aby podporovala silné šifrování cyphers, a odeberte *použití typů šifrování Kerberos DES*. Přečtěte si další informace o [typech šifrování a protokolu Kerberos](https://blogs.msdn.microsoft.com/openspecification/2011/05/30/windows-configurations-for-kerberos-supported-encryption-type/). 
2. Ujistěte se, že je úroveň funkčnosti domény nastavená tak, aby podporovala silné šifrování cyphers.  
3. Poskytněte přednost používání aplikací, které podporují silné šifrování cyphers.

## <a name="suspected-overpass-the-hash-attack-kerberos-external-id-2002"></a>Podezřelá Overpass-the-hash – útok (Kerberos) (externí ID 2002) 

*Předchozí název:* Neobvyklá implementace protokolu Kerberos (možný útok overpass-the-hash)

**Popis**

Útočníci používají nástroje, které implementují nestandardním způsobem různé protokoly, například pomocí protokolů Kerberos a protokolu SMB. I když Microsoft Windows akceptuje tento typ síťového provozu bez upozornění, může Azure ATP rozpoznat potenciální škodlivý záměr. Chování je popsána v části techniky, jako je například metoda over-Pass-hash, hrubá síla a rozšířená ransomwarem zneužití, jako je například WannaCry, se používají.

**TRANSAKČNÍ program, B-TP nebo FP?**

Někdy aplikace implementovat vlastní zásobník protokolu Kerberos, není v souladu s RFC protokolu Kerberos. 

1. Ověřte, zda na zdrojovém počítači běží aplikace s vlastním zásobníkem protokolu Kerberos, nikoli v souladu se specifikací RFC protokolu Kerberos.  
2. Pokud na zdrojovém počítači běží taková aplikace a nemělo by to udělat , opravte konfiguraci aplikace. **Zavřete** výstrahu zabezpečení jako aktivitu **T-BP** .  
3. Pokud na zdrojovém počítači běží taková aplikace a mělo by to pokračovat, **zavřete** výstrahu zabezpečení jako aktivitu **T-BP** a vylučte počítač. 

**Pochopení rozsahu porušení**

1. Prozkoumejte [zdrojový počítač](investigate-a-computer.md).  
2. Pokud existuje [zdrojový uživatel](investigate-a-user.md), prozkoumejte. 

**Navrhovaná náprava a kroky pro prevenci** 

1. Resetujte hesla ohrožených uživatelů a povolte MFA.
2. Obsahují zdrojový počítač.
3. Najít nástroj, který provádí útoku a jeho odebrání.
4. Hledání uživatelů přihlášených přibližně ve stejnou dobu jako podezřelá aktivita, jak mohou být ohroženy také. Resetujte hesla a povolte MFA.  
5. Resetujte hesla zdrojového uživatele a povolte MFA.

> [!div class="nextstepaction"]
> [Kurz pro upozornění na dominantní doménu](atp-domain-dominance-alerts.md)

## <a name="see-also"></a>Viz také

- [Prošetřování počítačů](investigate-a-computer.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Práce s cestami k příčnému přesunu](use-case-lateral-movement-path.md)
- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před dominancí v doméně](atp-domain-dominance-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

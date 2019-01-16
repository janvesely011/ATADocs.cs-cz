---
title: Ochrana ATP v programu Azure laterální pohyb výstrahy zabezpečení | Dokumentace Microsoftu
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of lateral movement phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/15/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2257eb00-8614-4577-b6a1-5c65085371f2
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7816dba02c2fea07afc080c7aed5ede073c88fac
ms.sourcegitcommit: e2daa0f93d97d552cfbf1577fbd05a547b63e95b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/15/2019
ms.locfileid: "54314308"
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
> * Krádež identity podezřelého softwaru (pass-the-hash) (externí ID 2017)
> * Krádež identity podezřelého softwaru (pass-the-ticket) (externí ID 2018)
> * Podezření na útok overpass-the-hash (oslabení šifrování) (externí ID 2008)
> * Podezření na útok overpass-the-hash (Kerberos) (externí ID 2002)

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

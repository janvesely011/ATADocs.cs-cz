---
title: Upozornění kurz služby Azure ATP průsak ven | Dokumentace Microsoftu
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of exfiltration phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 02/11/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 452d951c-5f49-4a21-ae10-9fb38c3de302
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 704e372952d1b02fdcf6564bad26ebc4c7d184f2
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196877"
---
# <a name="tutorial-exfiltration-alerts"></a>Kurz: Upozornění průsak ven  

Obvykle kybernetických útoků jsou spouštěny proti jakémukoli subjektu přístupné, jako je například uživatel s nízkým oprávněním a potom rychle následně k laterálnímu pohybu dokud útočník získá přístup k cenný majetek, který. Cenný majetek, který může být citlivých účtů, správci domény nebo vysoce citlivá data. Ochrana ATP v programu Azure identifikuje tyto důmyslných hrozeb ve zdrojovém kódu v celém řetězu událostí útoku a klasifikuje do následujících fází:

1. [Rekognoskace](atp-reconnaissance-alerts.md)
2. [Zneužití přihlašovacích údajů](atp-compromised-credentials-alerts.md)
3. [Taktiky Lateral Movement](atp-lateral-movement-alerts.md)
4. [Dominance v doméně](atp-domain-dominance-alerts.md)
5. **Průsak ven**

Další informace o tom, jak pochopit strukturu a běžné součásti všech výstrah zabezpečení ochrany ATP v programu Azure najdete v tématu [Principy výstrah zabezpečení](understanding-security-alerts.md)

Výstrahy pomáhají identifikovat a napravit následující zabezpečení **průsak ven** fáze podezřelých aktivitách zjištěných ochrany ATP v programu Azure ve vaší síti. V tomto kurzu zjistěte, jak pochopit, klasifikovat, zabránit a opravit následující útoků:

> [!div class="checklist"]
> * Podezřelá komunikace prostřednictvím DNS (externí ID 2031)
> * Průsak dat ven přes protokol SMB (externí ID 2030)

## <a name="suspicious-communication-over-dns-external-id-2031"></a>Podezřelá komunikace prostřednictvím DNS (externí ID 2031) 

*Předchozí název*: Podezřelá komunikace prostřednictvím DNS

**Popis**

Protokol DNS ve většině organizací je obvykle není monitorovat a zřídka blokované před škodlivými aktivitami. Povoluje se útočník na napadeném počítači zneužívají protokolu DNS. Škodlivý komunikace prostřednictvím DNS je možné pro průsak dat ven, příkazu a řízení a/nebo omezení úmyslem vyhnout podnikové sítě.

**TP, B-TP nebo FP?**
 
Některé společnosti oprávněně použití serveru DNS pro pravidelné komunikace. Chcete-li zjistit stav výstrahy zabezpečení:

1. Zkontrolujte, pokud patří doména registrovaný dotaz pro důvěryhodného zdroje, jako je například poskytovatele antivirového softwaru.  
    - Považujte jej **B-TP** aktivitu, pokud je známé a důvěryhodné domény a nejsou povoleny pro dotazy DNS. *Zavřít* výstrahy zabezpečení a vyloučit domény z budoucích oznámení.  
    - Pokud domény registrovaný dotaz není důvěryhodný, identifikujte proces vytváření žádosti na zdrojovém počítači. Použití [monitorování procesu](https://docs.microsoft.com/sysinternals/downloads/procmon) jako pomoc s touto úlohou.

**Vysvětlení rozsahu porušení**

1. V cílovém počítači, který by měl být DNS server, zkontrolujte záznamy v doméně.
    - Jaké IP jsou to korelována?
    - Kdo je vlastníkem domény?
    - Pokud je IP adresa?
1. Prozkoumat [zdrojový a cílový počítač](investigate-a-computer.md).

**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu jako aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.
2. Pokud po šetření, zůstane domény registrovaný dotaz není důvěryhodný, doporučujeme blokování na cílovou doménu, aby všechny budoucí komunikaci.

> [!NOTE]
> *Podezřelá komunikace prostřednictvím DNS* výstrahy zabezpečení seznamu podezřelých domény. Nové domény nebo domény nedávno přidali, které nejsou dosud známé nebo rozpoznávaných ochrany ATP v programu Azure, ale jsou známé nebo součástí vaší organizaci se dá zavřít.

## <a name="data-exfiltration-over-smb-external-id-2030"></a>Průsak dat ven přes protokol SMB (externí ID 2030)

**Popis** řadičích domény se nachází nejcitlivější data organizace. Pro většinu útočníky jedním z nejdůležitějších úkolů jejich je k získání přístupu k řadiči domény, aby ukrást vaše nejcitlivější data. Cílem Ntds.dit soubor, uložený na řadiči domény, například umožňuje útočníkovi forge poskytující registraci tickets(TGT) prostředek lístek protokolu Kerberos. Falešných lístků TGT protokolu Kerberos povolit umožní nastavit dobu platnosti lístku do libovolného kdykoli. Azure ATP **průsak dat ven přes protokol SMB** aktivuje upozornění při podezřelých přenosy dat jsou dodržovány z monitorovaných řadičů domény.

**TP, B-TP nebo FP**
1. Tito uživatelé mají zkopírujte tyto soubory do tohoto počítače?  
    - Pokud je odpověď na otázku předchozí **Ano**, **Zavřít** zabezpečení výstrahy a vyloučit počítače jako **B-TP** aktivity.

**Vysvětlení rozsahu porušení**
1. Prozkoumat [zdroje uživatelé](investigate-a-user.md).  
2. Prozkoumat [zdrojový a cílový počítač](investigate-a-computer.md) kopie. 

**Navrhované nápravné kroky a pro ochrany před únikem informací**
1. Resetovat heslo uživatele zdroje a povolit vícefaktorové ověřování.
2. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Najít soubory, které byly zkopírovány a neodeberete. 
    <br>Zaškrtněte, pokud byly na tyto soubory jiné aktivity. Kde přesunou na jiné místo? Zaškrtněte, pokud byly převedeny mimo síť organizace? 
    - Vyhledejte uživatelé přihlášení přibližně ve stejnou dobu jako aktivity, jak může být ohrožena. Resetování hesel a povolení vícefaktorového ověřování.
3. Pokud jeden ze souborů se **ntds.dit** souboru:
    - Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
    - Obnovení účtu KRBTGT dvojím zruší platnost všechny lístky protokolu Kerberos v této doméně. Zrušení platnosti všechny lístky protokolu Kerberos v doméně znamená **všechny** služby nebude fungovat a nebudou fungovat znovu, dokud se obnovit nebo v některých případech se službu restartovat.

    - **Pečlivě naplánujte před provedením obnovení double KRBTGT. Resetování double KRBTGT má vliv na všechny počítače, servery a uživatelů v rámci prostředí.**

   - Zavřete všechny existující relace položky celkem řadiče domény. 

## <a name="see-also"></a>Viz také

- [Prošetřování počítačů](investigate-a-computer.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Práce s cesty taktiky Lateral Movement](use-case-lateral-movement-path.md)
- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před taktikou lateral movement](atp-lateral-movement-alerts.md)
- [Výstrahy před dominancí v doméně](atp-domain-dominance-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

---
title: Ochrana ATP v programu Azure dojde k ohrožení bezpečnosti výstrahy zabezpečení přihlašovacích údajů Fáze | Dokumentace Microsoftu
d|Description: This article explains the Azure ATP alerts issued when attacks typical of the compromised credentials phase are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c92ca6cb208d2a23de38ad39b9ce39dffbca0710
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58675213"
---
# <a name="tutorial-compromised-credential-alerts"></a>Kurz: Upozornění ohrožení zabezpečení přihlašovacích údajů  

Obvykle kybernetických útoků jsou spouštěny proti jakémukoli subjektu přístupné, jako je například uživatel s nízkým oprávněním a potom rychle následně k laterálnímu pohybu dokud útočník získá přístup k cenným prostředků – například citlivých účtů, správci domény a vysoce citlivá data . Ochrana ATP v programu Azure identifikuje tyto důmyslných hrozeb ve zdrojovém kódu v celém řetězu událostí útoku a klasifikuje do následujících fází:

1. [Rekognoskace](atp-reconnaissance-alerts.md)
2. **Ohrožení zabezpečení přihlašovacích údajů**
3. [Taktiky Lateral Movement](atp-lateral-movement-alerts.md)
4. [Dominance v doméně](atp-domain-dominance-alerts.md)
5. [Průsak ven](atp-exfiltration-alerts.md) 

Další informace o tom, jak pochopit strukturu a běžné součásti všech výstrah zabezpečení ochrany ATP v programu Azure najdete v tématu [Principy výstrah zabezpečení](understanding-security-alerts.md).

Výstrahy pomáhají identifikovat a napravit následující zabezpečení **přihlašovací údaje** fáze podezřelých aktivitách zjištěných ochrany ATP v programu Azure ve vaší síti. V tomto kurzu se dozvíte, jak pochopit, klasifikovat, opravit a brání následující typy útoků:

> [!div class="checklist"]
> * Aktivita Honeytokenu (externí ID 2014)
> * Podezřelý útok hrubou silou (pomocí protokolu Kerberos, NTLM) (externí ID 2023)
> * Podezřelý útok hrubou silou (LDAP) (externí ID 2004)
> * Podezřelý útok hrubou silou (SMB) (roku 2033 externí ID)
> * Podezřelý útok ransomwarem WannaCry (externí ID 2035)
> * Podezřelé použití Metasploit hacking framework (. 2034 externí ID)
> * Podezřelé připojení k síti VPN (externí ID 2025)

## <a name="honeytoken-activity-external-id-2014"></a>Aktivita Honeytokenu (externí ID 2014) 

*Předchozí název:* Aktivita Honeytokenu

**Popis**

Návnada účty nastavené tak identifikovat a sledovat škodlivou aktivitu, která zahrnuje tyto účty jsou účty Honeytokenu. Honeytokenové účty by měla zůstat nevyužité, přitom má atraktivní název k navést útočníci (například SQL-Admin). Všechny aktivity z nich může znamenat škodlivého chování.

Další informace o honeytokenové účty, najdete v části [konfigurovat vyloučení detekcí a účty honeytoken](install-atp-step7.md).

**TP, B-TP nebo FP**

1. Zaškrtněte, pokud vlastník zdrojový počítač používá účet Honeytokenu k ověření, pomocí metody popsané na stránce podezřelých aktivit (například Kerberos, LDAP, NTLM).

    Pokud vlastník zdrojového počítače použili účet honeytokenu k ověření, pomocí přesné metody popsané ve výstraze *Zavřít* zabezpečení výstrahy jako **B-TP** aktivity.

**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový uživatel](investigate-a-user.md).
2. Prozkoumat [zdrojový počítač](investigate-a-computer.md).

**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu aktivity došlo k chybě, protože tyto uživatele může také dojít k ohrožení. Resetování hesel a povolení vícefaktorového ověřování.

## <a name="suspected-brute-force-attack-kerberos-ntlm-external-id-2023"></a>Podezřelý útok hrubou silou (pomocí protokolu Kerberos, NTLM) (externí ID 2023)

*Předchozí název:* Podezřelé chyby ověřování

**Popis**

V rámci útoku hrubou silou se útočník pokusí ověřování pomocí více hesla na různé účty, dokud nebude nalezen správné heslo, nebo pomocí jednoho hesla ve velkém měřítku heslo zařízení, která funguje pro alespoň jeden účet. Jednou najde, útočník přihlásí pomocí ověření účtu.

V této detekce se aktivuje upozornění při dojít mnoho chyb ověřování pomocí protokolu Kerberos, NTLM, nebo zjištění použijte heslo zařízení. Použití protokolu Kerberos nebo NTLM, tento typ útoku je obvykle potvrzeny buď *vodorovné*, pomocí malé sady hesel v mnoha uživateli *svislé* s rozsáhlou sadou hesla na několik uživatelů, nebo žádný kombinaci obojího.

Heslo zařízení po úspěšně výčet seznamu platní uživatelé z řadiče domény, útočníci zkuste jedno heslo pečlivě vytvořené pro všechny známé uživatelské účty (jedno heslo na více účtů). Pokud selže počáteční heslo zařízení, zkuste to znovu, využívají jiné heslo pečlivě vytvořený, obvykle po uplynutí 30 minut mezi pokusy. Doba čekání útočníkům umožňuje, aby neměl spouštět nejčastěji podle času účet uzamčení prahové hodnoty. Heslo zařízení se rychle stal oblíbenou technikou útočník a testery pera. Heslo zařízení útoky ukázaly na zajistit efektivitu při získávání počáteční základnu v organizaci a pro následné laterální přesuny pokouší o zvýšení oprávnění. Minimální dobu, než může být výstraha je jeden týden.

**Období učení**
 <br>1 týden

**TP, B-TP nebo FP**

Je důležité zkontrolovat, pokud ukončení všech pokusů o přihlášení pomocí ověřování úspěšné.

1. Pokud všech pokusů o přihlášení skončila úspěšně, zkontrolujte, zda má některý **odhadnuté účty** se obvykle používají z tohoto zdrojového počítače.
   - Je pravděpodobné, že tyto účty se nezdařila, protože byl použit chybného hesla?  
   - Obraťte se na uživatele, pokud se vygeneruje aktivity (fe doby přihlášení se nezdařilo a pak bylo úspěšné). 

     Pokud je odpověď na výše uvedené otázky **Ano**, **Zavřít** dané výstraze zabezpečení jako aktivita B-TP.

2. Pokud neexistují žádné **odhadnuté účty**, zkontrolujte, jestli některý z **napadených účtů** se obvykle používají ze zdrojového počítače.
    - Zkontrolujte, jestli je skript spuštěn na zdrojovém počítači pomocí přihlašovacích údajů k chybě/old?
    - Pokud je odpověď na otázku předchozí **Ano**, zastavte a upravit nebo odstranit skript. **Zavřít** dané výstraze zabezpečení jako aktivita B-TP.

**Vysvětlení rozsahu porušení**

1. Prozkoumejte zdrojový počítač.  
2. Na stránce výstrahy zkontrolujte, které, pokud existuje, uživatelé úspěšně uhádl.
    - Každý uživatel, který byl úspěšně, uhodnout [zkontrolujte svůj profil](investigate-a-user.md) dále prozkoumat.
3. Pokud se provádí ověřování pomocí protokolu NTLM, někdy zobrazení výstrahy v mnoha případech, nebude existovat dostatek informací o serveru, které na zdrojovém počítači se pokusili získat přístup k dispozici.
    1. Získat tyto informace, ujistěte se, že chcete povolit auditování na řadičích domény používané protokolu NTLM.  
    2. Pokud chcete povolit auditování protokolu NTLM, zapněte události 8004 (NTLM authentication událost, která obsahuje informace o zdrojovém počítači, uživatelský účet a serveru, na kterém se pokusili získat přístup na zdrojovém počítači).
    3. Když zjistíte, které server odeslal ověření ověřování, prozkoumejte serveru tak, že zkontrolujete události, například události 4624, aby lépe porozumět procesu ověřování.

**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Resetovat hesla uhádnuté uživatelů a povolte vícefaktorové ověřování.
2. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu aktivity došlo k chybě, protože tyto uživatele může také dojít k ohrožení. Resetování hesel a povolení vícefaktorového ověřování.
3. Resetování hesel uživateli zdroje a povolit vícefaktorové ověřování.
4. Vynutit [složitá a dlouhá hesla](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) v organizaci, bude poskytovat nezbytnou první úroveň zabezpečení proti budoucím útokům hrubou silou.

## <a name="suspected-brute-force-attack-ldap-external-id-2004"></a>Podezřelý útok hrubou silou (LDAP) (externí ID 2004) 

*Předchozí název:* Útok hrubou silou pomocí jednoduché vazby LDAP.

**Popis**

V rámci útoku hrubou silou se útočník pokusí ověření pomocí mnoha různých hesel pro různé účty, dokud nebude nalezen správné heslo pro alespoň jeden účet. Jednou najde, útočník může přihlásit pomocí tohoto účtu.  
V této detekce se aktivuje upozornění, když zjistí velké množství jednoduché vazby ověřování ochrana ATP v programu Azure. Tato výstraha detekuje útok hrubou silou provést buď *vodorovně* s menší skupinou hesel mezi mnoha uživateli *svisle* s rozsáhlou sadou hesla u několika uživatelů či libovolnou kombinaci Tyto dvě možnosti.

**TP, B-TP nebo FP**

Je důležité zkontrolovat, pokud ukončení všech pokusů o přihlášení pomocí ověřování úspěšné.

1. Pokud všechny pokusy o přihlášení skončila úspěšně, jsou všechny **odhadnuté účty** běžně používaný z tohoto zdrojového počítače?
   - Je pravděpodobné, že tyto účty se nezdařila, protože byl použit chybného hesla?  
   - Obraťte se na uživatele, pokud se vygeneruje aktivity (přihlášení několikrát se nezdařilo a pak bylo úspěšné).

     Pokud je odpověď na předchozí otázky **Ano**, **Zavřít** dané výstraze zabezpečení jako aktivita B-TP.

2. Pokud neexistují žádné **odhadnuté účty**, zkontrolujte, jestli některý z **napadených účtů** se obvykle používají ze zdrojového počítače.
   - Zkontrolujte, jestli je skript spuštěn na zdrojovém počítači pomocí přihlašovacích údajů k chybě/old?

     Pokud je odpověď na otázku předchozí **Ano**, zastavte a upravit nebo odstranit skript. **Zavřít** dané výstraze zabezpečení jako aktivita B-TP.

**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový počítač](investigate-a-computer.md).  
2. Na stránce výstrah zjistěte, kteří uživatelé, pokud existuje, úspěšně uhádl. Každý uživatel, který byl úspěšně, uhodnout [zkontrolujte svůj profil](investigate-a-user.md) dále prozkoumat.

**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Resetovat hesla uhádnuté uživatelů a povolte vícefaktorové ověřování.
2. Obsahují zdrojový počítač.
    - Najít nástroj, který provádí útoku a jeho odebrání.
    - Vyhledejte uživatele, kteří byli přihlášeni přibližně ve stejnou dobu aktivity došlo k chybě, protože tyto uživatele může také dojít k ohrožení. Resetování hesel a povolení vícefaktorového ověřování.
3. Resetování hesel uživateli zdroje a povolit vícefaktorové ověřování.
4. Vynutit [složitá a dlouhá hesla](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) v organizaci, bude poskytovat nezbytnou první úroveň zabezpečení proti budoucím útokům hrubou silou.
5. Zabraňte dalším využívání protokolu nešifrovaný text LDAP ve vaší organizaci.

## <a name="suspected-brute-force-attack-smb-external-id-2033"></a>Podezřelý útok hrubou silou (SMB) (roku 2033 externí ID) 

*Předchozí název:* Neobvyklá implementace protokolu (potenciální použití škodlivých nástrojů, jako je Hydra)

**Popis**

Útočníci používají nástroje, které implementují nestandardním způsobem různé protokoly, jako jsou SMB, protokolu Kerberos a NTLM. Tento typ síťového provozu je přijat ve Windows bez upozornění, je ochrana ATP v programu Azure rozpoznat potenciální škodlivým činnostem. Chování je indikátorem technik útoku hrubou silou.

**TP, B-TP nebo FP**

1. Zkontrolujte, jestli zdrojovém počítači běží nástroj útoku, jako je například Hydra.
   1. Pokud zdrojovém počítači běží nástroj útoku, je tato výstraha **TP**. Postupujte podle pokynů v [pochopit tak rozsah porušení](#understand-the-scope-of-the-breach).

V některých případech aplikace implementovat vlastní ověřování protokolem NTLM nebo SMB zásobníku.

1. Zkontrolujte, jestli zdrojovém počítači běží vlastní ověřování protokolem NTLM nebo SMB zásobníku typu aplikace.
    1. Pokud zdrojový počítač se nachází spuštění tohoto typu aplikace a by neměl dál běžet, opravte konfiguraci aplikace podle potřeby. **Zavřít** dané výstraze zabezpečení jako **T BP** aktivity.
    2. Pokud zdrojový počítač se nachází spuštění tohoto typu aplikace, a mělo by to dokončíte, **Zavřít** dané výstraze zabezpečení jako **T BP** aktivitu a vyloučit tento počítač.

**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový počítač](investigate-a-computer.md).
2. Prozkoumat [zdrojový uživatel](investigate-a-user.md)) (Pokud je zdrojový uživatel).

**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Resetovat hesla uživatelů uhádnuté a povolení služby Multi-Factor authentication.
2. Obsahují zdrojový počítač
   1. Najít nástroj, který provádí útoku a jeho odebrání.
   2. Hledat uživatele přihlášení v době aktivity, jak může být ohrožena.
   3. Resetování hesel a povolení služby Multi-Factor authentication.
3. Vynutit [komplexní a dlouho hesla](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-policy) v organizaci. Složitá a dlouhá hesla zadejte nezbytnou první úroveň zabezpečení proti budoucím útokům hrubou silou.
4. [Zakázat SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

## <a name="suspected-wannacry-ransomware-attack-external-id-2035"></a>Podezřelý útok ransomwarem WannaCry (externí ID 2035)

*Předchozí název:* Neobvyklá implementace protokolu (možný útok ransomwarem WannaCry)

**Popis**

Útočníci používají nástroje, které různé protokoly implementují nestandardním způsobem. Tento typ síťového provozu je přijat ve Windows bez upozornění, je ochrana ATP v programu Azure rozpoznat potenciální škodlivým činnostem. Chování je indikátorem technik používaných pokročilé ransomwaru, jako je například WannaCry.

**TP, B-TP nebo FP**

1. Kontrola, zda je na zdrojovém počítači spuštěná WannaCry. 

    - Pokud WannaCry běží, je tato výstraha **TP**. Postupujte podle pokynů v [pochopit tak rozsah porušení](#understand-the-scope-of-the-breach).

V některých případech aplikace implementovat vlastní ověřování protokolem NTLM nebo SMB zásobníku.

1. Zkontrolujte, jestli zdrojovém počítači běží vlastní ověřování protokolem NTLM nebo SMB zásobníku typu aplikace. 
    1. Pokud zdrojový počítač se nachází spuštění tohoto typu aplikace a by neměl dál běžet, opravte konfiguraci aplikace podle potřeby. **Zavřít** dané výstraze zabezpečení jako **T BP** aktivity.
    2. Pokud zdrojový počítač se nachází spuštění tohoto typu aplikace, a mělo by to dokončíte, **Zavřít** dané výstraze zabezpečení jako **T BP** aktivitu a vyloučit tento počítač.

**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový počítač](investigate-a-computer.md).
2. Prozkoumat [dojde k ohrožení bezpečnosti uživatelského](investigate-a-user.md).

**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Obsahují zdrojový počítač.
      - [Odebrat WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)
      - WanaKiwi může dešifrovat data v rámci ransom softwaru, ale jen pokud uživatel nebyl restartovat nebo vypnout počítač. Další informace najdete v tématu [WannaCry Ransomwaru](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)
      - Vyhledejte uživatelé přihlášení v době aktivity, jak může být ohrožené. Resetování hesel a povolení vícefaktorového ověřování.
2. Oprava všech počítačů, a ujistěte se, aby aktualizace zabezpečení. 
      - [Zakázat SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

## <a name="suspected-use-of-metasploit-hacking-framework-external-id-2034"></a>Podezřelé použití Metasploit hacking framework (. 2034 externí ID)

*Předchozí název:* Neobvyklá implementace protokolu (potenciální použijte Metasploit hacking nástroje)

**Popis**

Útočníci použít nástroje, které implementují různé protokoly (SMB, Kerberos, NTLM) nestandardním způsobem. Tento typ síťového provozu je přijat ve Windows bez upozornění, je ochrana ATP v programu Azure rozpoznat potenciální škodlivým činnostem. Chování je indikátorem techniky, jako je například používání hackerským metasploitu. 

**TP, B-TP nebo FP**

1. Zkontrolujte, jestli zdrojovém počítači běží nástroj útoku, třeba Metasploit nebo Medusa.

2. Pokud ano, jde o pravdivě pozitivní upozornění. Postupujte podle pokynů v [pochopit tak rozsah porušení](#understand-the-scope-of-the-breach).

V některých případech aplikace implementovat vlastní ověřování protokolem NTLM nebo SMB zásobníku.

 1. Zkontrolujte, jestli zdrojovém počítači běží vlastní ověřování protokolem NTLM nebo SMB zásobníku typu aplikace. 
    1. Pokud zdrojový počítač se nachází spuštění tohoto typu aplikace a by neměl dál běžet, opravte konfiguraci aplikace podle potřeby. **Zavřít** dané výstraze zabezpečení jako **T BP** aktivity.
    2. Pokud zdrojový počítač se nachází spuštění tohoto typu aplikace, a mělo by to dokončíte, **Zavřít** dané výstraze zabezpečení jako **T BP** aktivitu a vyloučit tento počítač.

**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový počítač](investigate-a-computer.md).
2. Pokud není zdrojový uživatel [prozkoumat uživatel](investigate-a-user.md).

**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Resetovat hesla uhádnuté uživatelů a povolte vícefaktorové ověřování.
2. Obsahují zdrojový počítač.
   1. Najít nástroj, který provádí útoku a jeho odebrání.
   2. Hledat uživatele přihlášení v době aktivity, jak může být ohrožena. Resetování hesel a povolení služby Multi-Factor authentication.
3. Resetování hesel uživateli zdroje a povolit vícefaktorové ověřování. 
4. [Zakázat SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/) 

## <a name="suspicious-vpn-connection-external-id-2025"></a>Podezřelé připojení k síti VPN (externí ID 2025) 

*Předchozí název:* Podezřelé připojení k síti VPN 

**Popis**

Ochrana ATP v programu Azure se učí chování entit pro uživatele sítě VPN klouzavou dobu jednoho měsíce. 

Model chování VPN je založen na počítače, které se uživatelé přihlašují k a umístění, které se uživatelé připojovat z. 

Oznámení se otevře po odchylky od chování uživatele podle algoritmu strojového učení.

**Období učení**

30 dní od první připojení k síti VPN a nejméně 5 připojení k síti VPN v posledních 30 dní, za uživatele.

**TP, B-TP nebo FP**

1. Podezřelé uživatel by měl být provádění těchto operací?
    1. Uživatel naposledy změnit jejich umístění?
    2. Je uživatel cestují a připojení z nového zařízení?

Pokud jsou odpovědi na otázky uvedené výše, **Zavřít** dané výstraze zabezpečení jako **B-TP** aktivity.

**Vysvětlení rozsahu porušení**

1. Prozkoumat [zdrojový počítač](investigate-a-computer.md).
2. Pokud není zdrojový uživatel [prozkoumat uživatel](investigate-a-user.md).

**Navrhované nápravné kroky a pro ochrany před únikem informací**

1. Resetovat heslo uživatele a povolit vícefaktorové ověřování.
2. Vezměte v úvahu blokování tento uživatel v připojení pomocí sítě VPN.
3. Vezměte v úvahu blokování tomuto počítači ze připojení pomocí sítě VPN.
4. Zkontrolujte, jestli existují další uživatelé připojené prostřednictvím sítě VPN z těchto umístění a zkontrolujte jejich bezpečnosti.

> [!div class="nextstepaction"]
> [Laterální pohyb výstrah kurz](atp-lateral-movement-alerts.md)

## <a name="see-also"></a>Viz také

- [Prošetřování počítačů](investigate-a-computer.md)
- [Prošetřování uživatelů](investigate-a-user.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Práce s cesty taktiky Lateral Movement](use-case-lateral-movement-path.md)
- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před taktikou lateral movement](atp-lateral-movement-alerts.md)
- [Výstrahy před dominancí v doméně](atp-domain-dominance-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

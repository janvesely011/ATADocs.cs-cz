---
title: Azure Průvodce výstrah zabezpečení ochrany ATP v programu | Dokumentace Microsoftu
d|Description: This article provides a list of the security alerts issued by Azure ATP and steps for remediation.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/26/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4fe68a3f11a1191035fbbcfadbc497929cf5e80a
ms.sourcegitcommit: eac0aa855270b550dfb4b8c61b9cf0953f1e5204
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/26/2018
ms.locfileid: "52298166"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="azure-advanced-threat-protection-security-alert-guide"></a>Azure Advanced Threat Protection výstrah Příručka zabezpečení

Po správném šetření můžete všechny výstrahy zabezpečení služby Azure ATP klasifikováno jako:

-   **Pravdivě pozitivní upozornění**: škodlivá akce zjištěná službou ochrany ATP v programu Azure.

-   **Neškodné pravdivě pozitivní upozornění**: akce zjištěná službou ochrany ATP v Azure, která je skutečná, ale není škodlivá, třeba test průniku.

-   **Falešně pozitivní**: alarm hodnotu false, to znamená aktivity neměli stát.

Další informace o tom, jak pracovat s výstrahami zabezpečení služby Azure ATP najdete v tématu [práce s výstrahami zabezpečení](working-with-suspicious-activities.md).

## <a name="security-alert-name-mapping-and-unique-externalid"></a>Mapování názvu upozornění zabezpečení a jedinečný externalId

Ve verzi 2.56 všechny existující výstrahy zabezpečení služby Azure ATP byly přejmenovány s snáze pochopit názvy. Mapování mezi staré i nové názvy a jejich odpovídající jedinečný externalIds jsou uvedené v následující tabulce. Společnost Microsoft doporučuje použití výstrahy externalIds místo upozornění názvů pro skripty nebo automatizace jsou trvalé pouze výstrahy externalIds zabezpečení a nelze změnit. 

> [!div class="mx-tableFixed"] 
|Nový název výstrahy zabezpečení|Název výstrahy zabezpečení pro starší verze|ExternalId jedinečný|
|---------|----------|---------|
|Podezřelý útok hrubou silou (LDAP)|Útok hrubou silou pomocí jednoduché vazby LDAP.|2004|
|Podezřelý útoku typu Skeleton Key (oslabení šifrování)|Šifrování downgrade aktivity Skeleton key|2011|
|Podezření na útok over-pass-the-hash (oslabení šifrování)|Aktivita snížení úrovně šifrování (možný útok overpass-the-hash)|2008|
|Podezřelé použití lístku golden (oslabení šifrování)|Aktivita snížení úrovně šifrování (potenciální útok metodou golden ticket)|2009|
|Útoku typu skeleton key podezřelého softwaru (oslabení šifrování)|Aktivita snížení úrovně šifrování (potenciální útoku typu skeleton key)|2010|
|Aktivita Honeytokenu|Aktivita Honeytokenu|2014|
|Krádež identity podezřelého softwaru (pass-the-hash)|Krádež identity pomocí útoku Pass-the-Hash|2017|
|Krádež identity podezřelého softwaru (pass-the-ticket)|Krádež identity pomocí útoku Pass-the-Ticket|2018|
|Podezřelé použití golden ticket (čas anomálií) |Lístek protokolu Kerberos golden – čas anomálií|2022|
|Podezřelé využití lístku golden (neexistující účet)|Protokol Kerberos Golden Ticket - neexistující účet|2027|
|Škodlivá žádost Data Protection API hlavní klíč|Škodlivá žádost o soukromé informace přes Data Protection|2020|
|Podezřelý útok DCSync (replikace adresářových služeb)|Škodlivá replikace adresářových služeb|2006|
|Podezřelé použití lístku Golden (falešných dat autorizace) |Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace|2013|
|Rekognoskace výčtu účtů|Rekognoskace pomocí výčtu účtů|2003|
|Rekognoskace mapování sítě (DNS)|Rekognoskace pomocí DNS|2007|
|Uživatele a IP adres pro rekognoskaci (SMB) |Rekognoskace pomocí výčtu relací SMB|2012|
|Rekognoskace členství uživatelů a skupin (SAMR)|Rekognoskace pomocí dotazů na adresářové služby|2021|
|Pokus o spuštění vzdáleného kódu|Pokus o spuštění vzdáleného kódu|2019|
|Podezření na útok DCShadow (žádost o replikaci řadiče domény)|Žádost o replikaci řadiče domény podezřelé (možný útok DCShadow)|2029|
|Podezřelý útok DCShadow (povýšení řadiče domény)|Povýšení řadiče domény podezřelé (možný útok DCShadow)|2028|
|Podezřelá komunikace prostřednictvím DNS|Podezřelá komunikace prostřednictvím DNS|2031|
|Podezřelé úprava citlivých skupin|Podezřelé úprava citlivých skupin|2024|
|Podezřelé vytvoření služby|Podezřelé vytvoření služby|2026|
|Podezřelé připojení k síti VPN|Podezřelé připojení k síti VPN|2025|
|Podezření na útok WannaCry ransomwaru|Neobvyklá implementace protokolu (možný útok ransomwarem WannaCry) *|2002|
|Podezřelý útok hrubou silou (SMB)|Neobvyklá implementace protokolu (potenciální použití škodlivých nástrojů, jako je Hydra) *|2002|
|Podezřelé použití Metasploit hacking framework|Neobvyklá implementace protokolu (potenciální použijte Metasploit hacking nástroje) *|2002|
|Podezření na útok overpass-the-hash (Kerberos)|Neobvyklý protokol Kerberos protokol implementace (možný útok overpass-the-hash) *|2002|
|*Neobvyklá implementace protokolu* výstrahy aktuálně sdílet externalId. ExternalId pro každý typ tyto výstrahy se změní v budoucích vydáních na jedinečné externalId||****|

## <a name="suspected-brute-force-attack-ldap"></a>Podezřelý útok hrubou silou (LDAP) 
<a name="brute-force-attack-using-ldap-simple-bind"></a>
*Předchozí název:* pomocí jednoduché vazby LDAP útoku hrubou silou

**Popis**

>[!NOTE]
> Hlavní rozdíl mezi **podezřelá neúspěšná ověření** a toto zjišťování je, že v této detekce ochrany ATP v programu Azure můžete určit, zda byly použity odlišná hesla.

V rámci útoku hrubou silou se útočník pokusí ověření pomocí mnoha různých hesel pro různé účty, dokud nebude nalezen správné heslo pro alespoň jeden účet. Jednou najde, útočník může přihlásit pomocí tohoto účtu.

V této detekce se aktivuje upozornění, když zjistí velké množství jednoduché vazby ověřování ochrana ATP v programu Azure. Může to být buď *vodorovně* s menší skupinou hesel mezi mnoha uživateli; nebo *svisle "* s rozsáhlou sadou hesla u několika uživatelů; či libovolnou kombinaci těchto dvou možností.

**Šetření**

1. Pokud se využívá řada řadu účtů, klikněte na tlačítko **stáhnout podrobnosti o** pro zobrazení seznamu v Excelové tabulce.

2. Klikněte na výstrahu, kterou chcete přejít na jeho vyhrazenou stránku. Zkontrolujte, zda pokusů o přihlášení jakékoli skončilo s po provedení úspěšného ověření. Pokusy se zobrazí jako **odhadnuté účty** na pravé straně infografiku. Pokud ano, jsou všechny **odhadnuté účty** běžně používaný ze zdrojového počítače? Pokud ano, **potlačit** podezřelou aktivitu.

3. Pokud neexistují žádné **odhadnuté účty**, jsou všechny **napadených účtů** běžně používaný ze zdrojového počítače? Pokud ano, **potlačit** podezřelou aktivitu.

**Náprava**

[Složitá a dlouhá hesla](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) poskytují nezbytnou první úroveň zabezpečení před útoky hrubou silou.

## <a name="suspected-skeleton-key-attack-encryption-downgrade"></a>Podezřelý útoku typu Skeleton Key (oslabení šifrování)
<a name="encryption-downgrade-activity-potential-skeleton-key-attack"></a>

*Předchozí název:* aktivita snížení úrovně šifrování

**Popis** oslabení šifrování je metoda oslabení podle downgradu úrovně šifrování protokolu různých polí, které jsou šifrované pomocí nejvyšší úrovně šifrování pomocí protokolu Kerberos. Oslabeným šifrované pole může být snazší target na offline útoky hrubou silou při pokusech. Různých metod útoku zvýšit využití slabé šifrování doklad protokolu Kerberos. V tomto zjišťování ochrany ATP v programu Azure učí typy šifrování pomocí protokolu Kerberos, počítačů a uživatelů a upozorní vás, když je slabší šifrovací, který používá: (1) neobvyklé, že u zdrojového počítače nebo uživatele. a (2) shod označuje technik útoku. 

Skeleton Key je malware, který běží na řadičích domény a umožňuje ověření vůči doméně pomocí libovolného účtu bez znalosti jeho hesla. Tento malware často používá slabší šifrovací algoritmy k vytvoření hodnoty hash hesel uživatelů na řadiči domény. Tato detekce byla metoda šifrování zprávy KRB_ERR z řadiče domény k účtu s žádostí o lístek downgradovat ve srovnání s dřív zjištěné chování.


**Šetření**
1. Klikněte na zdrojový počítač nebo účet, přejděte na stránku jeho profil. <br>Zkontrolujte, co se stalo v době replikace, hledání neobvyklých aktivit, jako je například kdo byl přihlášen a které prostředky jsou-li získat přístup. <br>Pokud jste nepovolili integraci ochrany ATP v programu Windows Defender, klikněte na možnost ochrana ATP v programu Windows Defender odznáčku ![Oznámení "BADGE" ochrany ATP v programu Windows Defender](./media/wd-badge.png) aby to prověřili počítače. V programu Windows Defender ATP zobrazí se výstrahy a procesů došlo k přibližně v době výstrahy. 
2. Zaškrtněte, pokud Skeleton Key ovlivnila řadičů domény s použitím [kontroly vytvořené týmem služby Azure ATP](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73).


**Náprava**
1. Odstraňte malware. Další informace o odebrání malwaru, naleznete v tématu [analýzy Malware Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).


## <a name="suspected-golden-ticket-attack-encryption-downgrade"></a>Podezření na útok typu Golden Ticket (oslabení šifrování)
<a name="Encryption-downgrade-activity-potential-golden-ticket-attack"></a>

*Předchozí název:* aktivita snížení úrovně šifrování

**Popis** oslabení šifrování je metoda oslabení podle downgradu úrovně šifrování protokolu různých polí, které jsou šifrované pomocí nejvyšší úrovně šifrování pomocí protokolu Kerberos. Oslabeným šifrované pole může být snazší target na offline útoky hrubou silou při pokusech. Různých metod útoku zvýšit využití slabé šifrování doklad protokolu Kerberos. V tomto zjišťování ochrany ATP v programu Azure učí typy šifrování pomocí protokolu Kerberos, počítačů a uživatelů a upozorní vás, když je slabší šifrovací, který používá: (1) neobvyklé, že u zdrojového počítače nebo uživatele. a (2) shod označuje technik útoku. 

Ve výstraze Golden Ticket metoda šifrování pole TGT v TGS_REQ (žádost o službu) zprávy ze zdrojového počítače downgradovat ve srovnání s dřív zjištěné chování. To není založené na čase anomálií (stejně jako v jiných detekce Golden Ticket). Kromě toho se žádný požadavek na ověření Kerberos související s předchozí žádosti o službu detekovaných službou ochrany ATP v programu.

**Šetření**
1. Některé prostředky nepodporují silné šifrování metody a může aktivovat tuto výstrahu.
   1. Podívejte se na zdroje přistupuje těchto lístků. Zaškrtnutím tohoto políčka ve službě Active Directory tak, že zkontrolujete atribut *msDS-SupportedEncryptionTypes*, prostředků účtu služby.
   2. Pokud jeden prostředek, který je přistupováno ho ověří. Ujistěte se, že je platný prostředek, který už má přístup. 
2. Vlastní aplikace může ověřit pomocí nižší šifry šifrování.
   1. Zkontrolujte, jestli jsou všechny vlastní aplikace ověřování pomocí nižší šifry šifrování ve zdrojovém počítači.
   2. Pokud existuje více uživatelů, zkontrolujte, jestli mají něco společné. <br>Například všechny pracovníky marketingu pomocí konkrétní aplikaci, která může být aktivaci výstrahy.
3. Klikněte na zdrojový počítač nebo účet, přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době replikace. Ujistěte se, že až po hledání neobvyklých aktivit, jako je například kdo byl přihlášen a které prostředky jsou-li získat přístup. 

4. Pokud jste nepovolili integraci ochrany ATP v programu Windows Defender, klikněte na možnost ochrana ATP v programu Windows Defender odznáčku ![Oznámení "BADGE" ochrany ATP v programu Windows Defender](./media/wd-badge.png) aby to prověřili počítače. V programu Windows Defender ATP zobrazí se výstrahy a procesů došlo k přibližně v době výstrahy.

**Náprava**

1. Resetování hesla pro uživatele ohrožení zabezpečení.
2. Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Obnovení účtu KRBTGT dvojím zruší platnost všechny lístky protokolu Kerberos v této doméně, takže pečlivě naplánujte před provedením obnovení.

## <a name="suspected-over-pass-the-hash-attack-encryption-downgrade"></a>Podezření na útok over-pass-the-Hash (oslabení šifrování) 
<a name="Encryption-downgrade-activity-potential-over-pass-the-hash"></a>

*Předchozí název:* aktivita snížení úrovně šifrování

**Popis**

Oslabení šifrování je metoda oslabení podle downgradu úrovně šifrování protokolu různých polí, které jsou šifrované pomocí nejvyšší úrovně šifrování pomocí protokolu Kerberos. Oslabeným šifrované pole může být snazší target na offline útoky hrubou silou při pokusech. Různých metod útoku zvýšit využití slabé šifrování doklad protokolu Kerberos. V tomto zjišťování ochrany ATP v programu Azure učí typy šifrování pomocí protokolu Kerberos, počítačů a uživatelů a upozorní vás, když je slabší šifrovací, který používá: (1) neobvyklé, že u zdrojového počítače nebo uživatele. a (2) shod označuje technik útoku. 

V over-pass-the-hash útok útočník využije k vytvoření lístku silné žádost Kerberos AS slabé odcizené hodnoty hash. Při tomto zjišťování byla downgradovat typ šifrování zprávy AS_REQ ze zdrojového počítače, ve srovnání s dřív zjištěné chování (to znamená, počítač se pomocí standardu AES).

**Šetření**

1. Čipová karta konfigurace v poslední době změnilo? <br>Zaškrtněte, pokud došlo ke změně tímto způsobem pro účty používané. Pokud ano, to je pravděpodobně o neškodné pravdivě pozitivní upozornění a lze potlačit.
2. Některé prostředky nepodporují metody silné šifrování. Metody slabé šifrování můžete aktivovat tuto výstrahu.<br>Podívejte se na zdroje přistupuje těchto lístků. Zaškrtnutím tohoto políčka ve službě Active Directory tak, že zkontrolujete atribut *msDS-SupportedEncryptionTypes*, prostředků účtu služby.<br>Pokud jeden prostředek, který je přistupováno ho ověří. Ujistěte se, že je platný prostředek, který už má přístup. 
3. Klikněte na zdrojový počítač nebo účet, přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době replikace, hledání neobvyklých aktivit, jako je například kdo byl přihlášen a které prostředky jsou-li získat přístup. <br> Pokud jste nepovolili integraci ochrany ATP v programu Windows Defender, klikněte na možnost ochrana ATP v programu Windows Defender odznáčku ![Oznámení "BADGE" ochrany ATP v programu Windows Defender](./media/wd-badge.png) aby to prověřili počítače. V programu Windows Defender ATP zobrazí se výstrahy a procesů došlo k přibližně v době výstrahy.


**Náprava**
1. Pokud je ohrožené uživatele *není citlivé* -resetovat heslo daného účtu. To zabrání útočník vytváření nových lístky protokolu Kerberos z hodnoty hash hesla, i když existující lístky je stále možné až do vypršení jejich platnosti. 
2. Pokud je ohrožené uživatele *citlivé* – zvažte obnovení účtu KRBTGT dvakrát. Obnovení účtu KRBTGT dvojím zruší platnost všechny lístky protokolu Kerberos v této doméně, takže pečlivě naplánujte před provedením obnovení. Přečtěte si pokyny v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Viz také pomocí [resetování nástroj hesla/klíčů účtu KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).


## <a name="honeytoken-activity"></a>Aktivita Honeytokenu
<a name="honeytoken-activity"></a>

*Předchozí název:* aktivita Honeytokenu

**Popis**

Návnada účty nastavené tak identifikovat a sledovat škodlivou aktivitu, která zahrnuje tyto účty jsou účty Honeytokenu. Honeytokenové účty by měla zůstat nevyužité, přitom má atraktivní název k navést útočníci (například SQL-Admin). Všechny aktivity z nich může znamenat škodlivého chování.

Další informace o honey token účty, najdete v části [instalace služby Azure ATP – krok 7](install-atp-step7.md).

**Šetření**

1.  Zkontrolujte, zda Vlastník zdrojového počítače používá účet Honeytokenu k ověření, pomocí metody popsané na stránce podezřelých aktivit (například Kerberos, LDAP, NTLM).

2.  Přejděte na stránku nebo stránky zdrojového počítače profilu a zkontrolujte ostatní účty, které se ověřil z nich. Obraťte se na vlastníky účtů, pokud použity účtů Honeytokenu.

3.  To může být neinteraktivního přihlášení, proto nezapomeňte zaškrtnout pro aplikace nebo skripty, které běží na zdrojovém počítači.

Pokud po provedení kroků 1 až 3, pokud neexistuje žádný doklad o neškodné použití, se předpokládá, že jde o škodlivé.

**Náprava**

Ujistěte se, že Honeytokenu účtů se používají pouze pro jejich zamýšlený účel, jinak může generovat více výstrah.

## <a name="suspected-identity-theft-pass-the-hash"></a>Krádež identity podezřelého softwaru (pass-the-hash) 
<a name="identity-theft-using-pass-the-hash-attack"></a>

*Předchozí název:* krádež Identity pomocí útoku Pass-the-Hash

**Popis**

Pass-the-Hash je technika laterálního pohybu, kdy útočník získá NTLM hash uživatele z jednoho počítače a použije ho k získání přístupu k jinému počítači. 

**Šetření**

Zjistěte, jestli hodnota hash byla použita na počítači, který cílový uživatel vlastní, nebo pravidelně používá? Pokud ano, jde o falešně pozitivní upozornění a pokud ne, pravděpodobně se jedná o pravdivě pozitivní upozornění.

**Náprava**

1. Pokud není potřebný účet citlivé, resetujte heslo daného účtu. To zabrání útočník vytváření nových lístky protokolu Kerberos z hodnoty hash hesla, i když existující lístky je stále možné až do vypršení jejich platnosti. 

2. Pokud je citlivý účet, měli byste zvážit, obnovení účtu KRBTGT dvakrát jako podezřelá aktivita zlatého lístku. Obnovení účtu KRBTGT dvakrát zruší platnost všech protokolu Kerberos, takže Plánujte lístky v této doméně než to uděláte. Přečtěte si pokyny v [KRBTGT účet skriptů pro resetování hesla nyní dostupný pro zákazníky se](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), také naleznete pomocí [resetování nástroj hesla/klíčů účtu KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Protože to je technika laterálního pohybu, postupujte podle osvědčené postupy z [předání hodnoty hash doporučení](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="suspected-identity-theft-pass-the-ticket"></a>Krádež identity podezřelého softwaru (pass-the-ticket) 
<a name="identity-theft-using-pass-the-ticket-attack"></a>

*Předchozí název:* krádež Identity pomocí útoku Pass-the-Ticket

**Popis**

Pass-the-Ticket je technika laterálního pohybu, kdy útočník získá lístek Kerberos z jednoho počítače a použije ho k získání přístupu k jinému počítači opětovným použitím odcizených lístků. Při zjišťování je zobrazena lístek protokolu Kerberos používá na dvou (nebo více) různých počítačích.

**Šetření**

1. Klikněte na tlačítko **stáhnout podrobnosti o** tlačítko zobrazit úplný seznam IP adres zahrnuté. Nemá IP adresu jedné nebo obou počítačích patřit do podsítě, která je přidělena z nedostatečné velikosti fondu adres DHCP, například síť VPN nebo Wi-Fi? Sdílet adresu IP Například tím, že zařízení NAT? Jsou jedna nebo více zdrojových IP adres nebyl rozeznán senzor? (to může znamenat, že nejsou správně otevřené správné porty z senzor do zařízení.) Pokud je odpověď na kteroukoli z těchto otázek Ano, je falešně pozitivní.

2. Existuje vlastní aplikaci, která předává lístky jménem uživatelů? Pokud ano, jedná se o neškodnou pravdivě pozitivní.

**Náprava**

1. Pokud není potřebný účet citlivé, resetujte heslo daného účtu. To zabrání útočník vytváření nových lístky protokolu Kerberos z hodnoty hash hesla, i když existující lístky je stále možné až do vypršení jejich platnosti.  

2. Pokud je citlivý účet, měli byste zvážit, obnovení účtu KRBTGT dvakrát jako podezřelá aktivita zlatého lístku. Obnovení účtu KRBTGT dvakrát zruší platnost všech protokolu Kerberos, takže Plánujte lístky v této doméně než to uděláte. Přečtěte si pokyny v [KRBTGT účet skriptů pro resetování hesla nyní dostupný pro zákazníky se](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), také naleznete pomocí [resetování nástroj hesla/klíčů účtu KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Protože to je technika laterálního pohybu, postupujte podle osvědčených postupů v [předání hodnoty hash doporučení](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="suspected-golden-ticket-usage-forged-authorization-data"></a>Podezřelé použití lístku Golden (falešných dat autorizace)
<a name="golden-ticket"></a>

Předchozí název: Kerberos golden ticket

**Popis**

Útočníci s právy správce domény může ohrozit [účtu KRBTGT](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). Pomocí účtu KRBTGT, můžete vytvořit lístek Kerberos udělující lístek (TGT), který poskytuje autorizaci k jakémukoli prostředku a nastavit dobu platnosti lístku do libovolného kdykoli. Tato falešných lístků TGT se nazývá "goldentTicket" a útočníkům umožňuje dosáhnout trvalého průniku do sítě.

V této detekce se aktivuje upozornění, pokud je lístek Kerberos udělující lístek se používá pro více než povolená doba uvedená v [maximální doba života lístku uživatele](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx), jde **čas anomálií**útok typu golden Ticket, nebo neexistující účet jde **neexistující účet** útok metodou golden ticket.


**Šetření**

- **Čas anomálií**
   1.   Byl poslední (během posledních několik hodin) změny do maximální doba života lístku nastavení hlavního názvu uživatele v zásadách skupiny? Vyhledat konkrétní hodnotu a zjistěte, jestli je nižší než čas, kdy-the-ticket se použil pro. Pokud ano, pak zavřete výstrahu (bylo falešně pozitivní).
   2.   Je senzoru služby Azure ATP zahrnutých v této výstraze virtuálního počítače? Pokud ano, ji nedávno pokračovat od uloženého stavu? Pokud ano, tuto výstrahu zavřete.
   3.   Pokud je odpověď na otázky uvedené výše předpokládají Ne, to se zlými úmysly.

- **Neexistující účet – nové** 
   1.   Odpovědět na tyto otázky:
         - Uživatel je známé a platná doména uživatel? Pokud ano, pak zavřete výstrahu (bylo falešně pozitivní).
         - Uživatel byl nedávno přidán? Pokud ano, pak zavřete výstrahu, změna nemusí mít nebyly synchronizovány.
         - Uživatel byl nedávno odstraněn z AD? Pokud ano, pak zavřete výstrahu.
   2.   Pokud je odpověď na otázky uvedené výše předpokládají Ne, to se zlými úmysly.

1. Pro oba typy útoků pomocí zlatého lístku, klikněte na tlačítko na zdrojovém počítači přejděte do jeho **profilu** stránky. Zkontrolujte, co se stalo v době aktivity a podívejte se na neobvyklé aktivity, včetně, který byl přihlášen, získal přístup k jakým prostředkům? 

2.  Jsou všichni uživatelé, které se připojily k počítači, by měl být přihlášení? Jaké jsou jejich oprávnění? 

3.  Uživatelé, kteří jsou přihlášení mají mít přístup k těmto prostředkům?<br>
Pokud jste nepovolili integraci ochrany ATP v programu Windows Defender, klikněte na oznámení ochrany ATP v programu Windows Defender.
 
 4. K hlubšímu prošetření je počítač, zkontrolujte, které procesy a výstrahy došlo k chybě v době výskytu výstrahy v ochrany ATP v programu Windows Defender.

**Náprava**


Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Obnovení účtu KRBTGT dvakrát zruší platnost všech protokolu Kerberos, takže Plánujte lístky v této doméně než to uděláte. Navíc vzhledem k tomu, že vytvoření Golden Ticket vyžaduje práva správce domény, implementovat [předání hodnoty hash doporučení](https://www.microsoft.com/download/details.aspx?id=36036).


## <a name="malicious-request-of-data-protection-api-master-key"></a>Škodlivá žádost Data Protection API hlavní klíč
<a name="malicious-data-protection-private-information-request"></a>

*Předchozí název:* škodlivých dat soukromých ochrany informace žádosti

**Popis**

Data Protection API (DPAPI) používá Windows bezpečné ochrany hesel uložil prohlížeče, šifrované soubory a další citlivá data. Řadičích domény se nachází záložní hlavní klíč, který slouží k dešifrování všech tajných kódů zašifrovaných pomocí rozhraní DPAPI na počítačích připojených k doméně Windows. Útočníci můžou používat tohoto hlavního klíče k dešifrování všech tajných kódů chráněn DPAPI na všech počítačích připojených k doméně.
V této detekce se aktivuje upozornění při použití neúspěšně pokusil načíst záložní hlavní klíč rozhraní DPAPI.

**Šetření**

1. Zdrojový počítač, s organizaci schválení je pokročilý kontrolu zabezpečení Active Directory?

2. Pokud ano a ji by měl vždy být tím, **zavřít a vyloučit** podezřelou aktivitu.

3. Pokud ano a je to dělat neměli, **Zavřít** podezřelou aktivitu.

**Náprava**

Použití rozhraní DPAPI, potřebuje útočník práva správce domény. Implementace [předání hodnoty hash doporučení](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="suspected-dcsync-attack-replication-of-directory-services"></a>Podezřelý útok DCSync (replikace adresářových služeb)
<a name="malicious-replication-of-directory-services"></a>

*Předchozí název:* škodlivá replikace adresářových služeb


**Popis**

Replikace služby Active Directory je proces, podle kterého se změny provedené na jednom řadiči domény synchronizují s jinými řadiči domény. Udělili nezbytná oprávnění, útočníci mohou zahájit žádost o replikaci, což jim umožní načíst dat uložená ve službě Active Directory, včetně hodnot hash hesel.

V této detekce se aktivuje upozornění, když se spustí požadavek replikace na počítači, který není řadičem domény.

**Šetření**

> [!NOTE]
> Pokud máte řadiče domény, ve kterých nejsou nainstalované senzory ochrany ATP v programu Azure, tyto řadiče domény nejsou pokryty ochrany ATP v programu Azure. V takovém případě Pokud nasazujete nový řadič domény na řadič domény zrušit nebo nechráněné, ho nejsou označené pomocí služby Azure ATP jako řadič domény v první. Důrazně doporučujeme nainstalovat na každý řadič domény zajistěte tak kompletní senzoru služby Azure ATP.

1. Je počítač v otázce řadiče domény? Například připojovaly řadiče domény, které měly potíže s replikací. Pokud ano, **Zavřít** podezřelou aktivitu. 
2.  Dotyčný počítač by měl být replikaci dat ze služby Active Directory? Například Azure AD Connect nebo v síti monitorování výkonu zařízení. Pokud ano, **zavřít a vyloučit** podezřelou aktivitu.
3. Je IP adresa, ze které byl odeslán požadavek na replikaci NAT nebo proxy server? Pokud ano, zkontrolujte, jestli je nový řadič domény za zařízení, nebo pokud z něj došlo k jiné podezřelých aktivit. 

4. Klikněte na zdrojový počítač nebo účet, přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době replikace, hledání neobvyklých aktivit, jako například: kdo byl přihlášen, které prostředky tam, kde získat přístup. Pokud jste nepovolili integraci ochrany ATP v programu Windows Defender, klikněte na možnost ochrana ATP v programu Windows Defender odznáčku ![Oznámení "BADGE" ochrany ATP v programu Windows Defender](./media/wd-badge.png) aby to prověřili počítače. V programu Windows Defender ATP zobrazí se výstrahy a procesů došlo k přibližně v době výstrahy. 


**Náprava**

Ověřte následující oprávnění: 

- Replikace změn adresáře   

- Replikovat všechny změny v adresáři  

Další informace najdete v tématu [udělení Active Directory Domain Services oprávnění k synchronizaci profilu v SharePoint serveru 2013](https://technet.microsoft.com/library/hh296982.aspx).
Můžete využít [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit skript prostředí Windows PowerShell k určení, kdo v doméně tato oprávnění má.


## <a name="suspected-golden-ticket-usage-forged-authorization-data"></a>Podezřelé použití lístku golden (falešných dat autorizace)
<a name="privilege-escalation-using-forged-authorization-data"></a>

*Předchozí název:* eskalace oprávnění prostřednictvím zfalšovaných dat autorizace

**Popis**

Známé chyby zabezpečení ve starších verzích Windows serveru umožňují útočníkům manipulovat s certifikát PAC (Privileged Attribute). Certifikát PAC je pole v lístku protokolu Kerberos, která obsahuje data autorizace uživatelů (ve službě Active Directory je to členství ve skupině), poskytování útočníci další oprávnění.

**Šetření**

1. Klikněte na výstrahu, kterou chcete získat jeho stránku podrobností.

2. Je cílovém počítači (v části **ACCESSED** sloupce) opravit zneužití MS14-068 (řadič domény) nebo zneužití MS11-013 (server)? Pokud ano, **Zavřít** podezřelé aktivity (je falešně pozitivní).

3. Pokud ne, běží zdrojovém počítači (v části **FROM** sloupce) označuje upravuje PAC operačního systému nebo aplikace? Pokud ano, **potlačit** podezřelé aktivity (jedná se o neškodnou pravdivě pozitivní).

4. Pokud byla odpověď již na výše uvedené dva dotazy, předpokládá to se zlými úmysly.

**Náprava**

Ujistěte se, že všechny řadiče domény s operačním systémem až do systému Windows Server 2012 R2 se instalují s [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) a všech členských serverech a řadičích domény až 2012 R2 jsou aktuální s KB2496930. Další informace najdete v tématu [stříbrný certifikát PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) a [podobě zfalšovaných certifikátů PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="account-enumeration-reconnaissance"></a>Rekognoskace výčtu účtů
<a name="reconnaissance-using-account-enumeration"></a>
*Předchozí název:* Rekognoskace pomocí výčtu účtů

**Popis**

V účtu výčet rekognoskace útočník využívá slovník s tisíci uživatelská jména nebo nástrojů, jako je KrbGuess pokusu odhadnout uživatelská jména ve vaší doméně. Útočník vytvářejí požadavky protokolu Kerberos pomocí tyto názvy, abyste mohli zkusit najít platné uživatelské jméno ve vaší doméně. Pokud odhad úspěšně Určuje uživatelské jméno, útočník získá Chyba protokolu Kerberos **požadované předběžné ověření** místo **neznámý objekt zabezpečení**. 

Při zjišťování dokáže ochrana ATP v programu Azure útoku, odkud, celkový počet pokusů uhádnout a kolik se shoda našla. Pokud existuje příliš mnoho uživatelů neznámý, ochrana ATP v programu Azure rozpozná jako podezřelou aktivitu. 

**Šetření**

1. Klikněte na výstrahu, kterou chcete získat jeho stránku podrobností. 

2. Tento hostitelský počítač by měl dotaz řadičem domény. jde o tom, jestli existují účty (například servery Exchange)? <br></br>
Je skript nebo aplikace spuštěná v hostiteli, který může generovat toto chování? <br></br>
Pokud ano, je odpověď na některý z těchto otázek **Zavřít** podezřelé aktivity (jedná se o neškodnou pravdivě pozitivní) a vyloučení, který hostovat v rámci podezřelé aktivity.

3. Stáhněte podrobnosti výstrahy v Excelové tabulce pohodlně zobrazí seznam pokusů o účet, rozdělit do existující a neexistujících účtů. Pokud se podíváte na kartě neexistující účty v tabulce a účty nic neříká, mohou být zakázané účty nebo zaměstnanců, kteří opustil společnost. V takovém případě je pravděpodobné, že tento pokus pochází ze slovníku. Největší pravděpodobností je aplikace nebo skript, který kontroluje se, které účty jsou stále existují ve službě Active Directory, což znamená, že se jedná o neškodnou pravdivě pozitivní.

3. Pokud jsou do značné míry neznámé názvy, odpovídat kterákoli tento počet pokusů uhádnout existujícími názvy účtů ve službě Active Directory? Pokud neexistují žádné odpovídající položky, pokus byl zbytečné, ale byste měli věnovat pozornost výstrahu, kterou chcete zobrazit, pokud se aktualizuje v čase.

4. Pokud některý z odhad pokusí shodovat s existujícími názvy účtů, jak útočník ví o existenci účty ve vašem prostředí a může pokusit použít útok hrubou silou pro přístup k vlastní domény s využitím zjištěných uživatelská jména. Zkontrolujte názvy účtů uhádnuté další podezřelých aktivit. Zkontrolujte, jestli některý z odpovídající účty jsou citlivé účty.


**Náprava**

[Složitá a dlouhá hesla](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) poskytují nezbytnou první úroveň zabezpečení před útoky hrubou silou.


## <a name="user-and-group-membership-reconnaissance-samr"></a>Rekognoskace členství uživatelů a skupin (SAMR)
<a name="reconnaissance-using-directory-services-queries"></a>

Rekognoskace pomocí dotazů na adresářové služby

**Popis**

Rekognoskace adresářových služeb je útočníci ke zmapování struktury adresáře a zacílení privilegovaných účtů v pozdějších krocích útoku. Protokol vzdáleného správce zabezpečení účtů (SAM-R) je jedna z metod používaných k dotazování adresáře k provedení těchto mapování.

Při zjišťování by žádné výstrahy aktivovat první měsíc po nasazení služby Azure ATP. Během učení období, ochrana ATP v programu Azure profily které dotazy SAM-R se sestavují z které počítače výčet a jednotlivé dotazy citlivých účtů.

**Šetření**

1. Klikněte na výstrahu, kterou chcete získat jeho stránku podrobností. Zkontrolujte, které dotazy se prováděly (pro příklad, Enterprise admins nebo správce) a jestli byli úspěšní.

2. Takové dotazy mají být provedeny ze zdrojového počítače dotyčný?

3. Pokud ano a výstraha aktualizována, **potlačit** podezřelou aktivitu.

4. Pokud ano a to už nepotřebujeme, by neměla provést **Zavřít** podezřelou aktivitu.

5. Pokud nejsou k dispozici informace na zahrnutých účtu: k tomuto účtu mají takové dotazy nebo nemá tento účet normálně přihlásit ke zdrojovému počítači?

 - Pokud ano a výstraha aktualizována, **potlačit** podezřelou aktivitu.

 - Pokud ano a to už nepotřebujeme, by neměla provést **Zavřít** podezřelou aktivitu.

 - Pokud byla odpověď Ne všechny výše uvedené, se předpokládá to se zlými úmysly.

6. Pokud není k dispozici žádné informace o účet, který je obsažená, můžete přejít ke koncovému bodu a zkontrolovat účtu, který byl přihlášen v době výstrahy.

**Náprava**

Posilte zabezpečení svého prostředí proti tuto techniku provedením následujících kroků:
1. Je počítač se službou zjišťování nástroj ohrožení zabezpečení?  
2. Zjistěte, jestli konkrétní dotazované uživatele a skupiny v útoku jsou privilegovaných nebo vysoce hodnotných účtů (to znamená, generální ředitel, Ředitelka, správy IT, atd.).  Pokud ano, podívejte se na další aktivitu v koncovém bodě také a monitorovat počítače, které jsou dotazované účty přihlášení, protože jde pravděpodobně o cíle taktiky Lateral Movement.

## <a name="network-mapping-reconnaissance-dns"></a>Rekognoskace mapování sítě (DNS)
<a name="reconnaissance-using-dns"></a>

Rekognoskace pomocí DNS

**Popis**

DNS server obsahuje mapu všech počítačů, IP adresy a služby ve vaší síti. Tyto údaje používají útočníci ke zmapování struktury vaší sítě a zacílení zajímavých počítačů v pozdějších krocích útoku.

Protokol DNS obsahuje několik typů dotazů. Ochrana ATP v programu Azure detekuje žádosti AXFR (přenos) pocházející z jiné servery než DNS.

**Šetření**

1. Je na zdrojovém počítači (**pocházející z...** ) DNS server? Pokud ano, pak jde pravděpodobně o falešně pozitivní upozornění. Pokud chcete ověřit, klikněte na výstrahu, kterou chcete získat jeho stránku podrobností. V tabulce v části **dotazu**, zkontrolujte, které domény se poslal dotaz. Jsou tyto existující domény? Pokud ano, pak **Zavřít** podezřelé aktivity (je falešně pozitivní). Kromě toho Ujistěte se, že je UDP port 53 otevřený mezi samostatnou senzoru služby Azure ATP a zdrojový počítač, aby se zabránilo budoucí počet falešně pozitivních výsledků.

2. Zdrojový počítač je spuštěný kontrolu zabezpečení? Pokud ano, **vyloučit entity** v ochrany ATP v programu, buď přímo pomocí **zavřít a vyloučit** nebo prostřednictvím **vyloučení** stránky (v části **konfigurace** – k dispozici pro správce služby Azure ATP).

3. Pokud odpověď je pro všechny předchozí otázky Ne, ponechat zkoumání zaměření na zdrojovém počítači. Klikněte na zdrojovém počítači přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době požadavku hledání neobvyklých aktivit, jako například: kdo byl přihlášen, které prostředky tam, kde získat přístup. Pokud jste nepovolili integraci ochrany ATP v programu Windows Defender, klikněte na možnost ochrana ATP v programu Windows Defender odznáčku ![Oznámení "BADGE" ochrany ATP v programu Windows Defender](./media/wd-badge.png) aby to prověřili počítače. V programu Windows Defender ATP zobrazí se výstrahy a procesů došlo k přibližně v době výstrahy. 

**Náprava**

Interní server DNS lze proti rekognoskaci pomocí DNS zabezpečit zakázáním nebo omezením přenosů zóny jen na konkrétní IP adresy. Další informace o omezení přenosů zóny najdete v tématu [omezení přenosů zóny](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
Úprava přenosů zóny je jedním z úkolů na kontrolním seznamu, která by měla být určena pro [zabezpečení před útoky interních i externích serverů DNS](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).

## <a name="user-and-ip-address-reconnaissance-smb"></a>Uživatele a IP adres pro rekognoskaci (SMB)
<a name="reconnaissance-using-smb-session-enumeration"></a> Rekognoskace pomocí výčtu relací SMB


**Popis**

Výčet Message Block (SMB) serveru umožňuje útočníkům získat informace, kde uživatelé nedávno přihlašovali. Jakmile útočník tyto informace, se můžete přesunout následně k laterálnímu v síti k určité citlivých účtů.

V této detekce se aktivuje upozornění při provádění výčet relací SMB proti řadiči domény, protože to nemělo stát.

**Šetření**

1. Klikněte na výstrahu, kterou chcete získat jeho stránku podrobností. Zkontrolujte operaci provést, které účtu/s a které účty byly vystaveny, pokud existuje.

 - Existuje nějaký druh kontrolu zabezpečení, které běží na zdrojovém počítači? Pokud ano, **zavřít a vyloučit** podezřelou aktivitu.

2. Zkontrolujte operaci provést, které zahrnutých uživatelů/s. Obvykle protokolují do zdrojového počítače nebo jsou správci, kteří by měl provádět tyto akce?  

3. Pokud ano a výstraha aktualizována, **potlačit** podezřelou aktivitu.  

4. Pokud ano a to už nepotřebujeme, by neměla provést **Zavřít** podezřelou aktivitu.

5. Pokud odpovědi na všechny výše uvedené je Ne, Předpokládejme, že to je škodlivý.

**Náprava**

Použití [Net ukončí nástroj](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) Posilte zabezpečení vašeho prostředí vůči útoku.

## <a name="remote-code-execution-attempt"></a>Pokus o spuštění vzdáleného kódu
<a name="remote-code-execution-attempt"></a>
*Předchozí název:* pokus o spuštění vzdáleného kódu

**Popis**

Útočníci, kteří ohrozit přihlašovacími údaji správce, nebo použijte před zneužitím nultého dne může na vašem řadiči domény spouštět vzdálené příkazy. Toho mohou využít k trvalému průniku do sítě, shromažďování informací, útokům DoS (Denial of Service) nebo z jakéhokoli jiného důvodu. Ochrana ATP v programu Azure zjistí připojení PSexec, vzdáleného rozhraní WMI a Powershellu.

**Šetření**

1. To je běžné, že pracovní stanice pro správu a členové týmu IT a účty služeb, které provádět úlohy správy na řadiče domény. Pokud je to tento případ a výstraha aktualizována od stejné správce a/nebo počítače provádění úkolů, pak **potlačit** výstrahu.

2. Je **počítače** dotyčný povoleno vzdálené spuštění vůči vašemu řadiči domény?

 - Je **účet** dotyčný povoleno vzdálené spuštění vůči vašemu řadiči domény?

 - Pokud na obě otázky odpovíte *Ano*, pak **Zavřít** výstrahu.

3. Pokud je odpověď na obě otázky Ne, pak toto by měl být pravdivě pozitivní upozornění. Pokuste se najít zdrojový na pokus o kontrolou počítače a účtu profily. Klikněte na zdrojový počítač nebo účet, přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době těchto pokusů o přihlášení, hledání neobvyklých aktivit, jako například: kdo byl přihlášen, které prostředky tam, kde získat přístup. Pokud jste povolili Windows Defender ATPintegration, klikněte na oznámení ochrany ATP v programu Windows Defender ![Oznámení "BADGE" ochrany ATP v programu Windows Defender](./media/wd-badge.png) aby to prověřili počítače. V systému Windows Defender ATPyou můžete zobrazit výstrahy a procesů došlo k přibližně v době výstrahy. 

**Náprava**

1. Zakažte vzdálený přístup k řadičům domény z počítačů, které nejsou ve vrstvě 0.

2. Implementace [privilegovaný přístup](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) povolit jen počítačům s posíleným zabezpečením pro připojení k řadiči domény pro správce.

> [!NOTE]
> Upozornění pokus o spuštění vzdáleného kódu jsou podporovány pouze senzorů ochrany ATP v programu. 

## <a name="suspected-brute-force-attack-kerberos-ntlm"></a>Podezřelý útok hrubou silou pomocí protokolu Kerberos protokol NTLM)
<a name="suspicious-authentication-failures"></a>

*Předchozí název:* podezřelá neúspěšná ověření

**Popis**

V rámci útoku hrubou silou se útočník pokusí ověřit více hesel na různé účty, dokud nebude nalezen správné heslo nebo pomocí jednoho hesla v rozsáhlých heslo zařízení, který funguje pro alespoň jeden účet. Jednou najde, útočník přihlásí pomocí ověření účtu.

V této detekce se aktivuje upozornění, když dojít mnoho chyb ověřování pomocí protokolu Kerberos nebo NTLM nebo využívání ve formě heslo se detekuje. Pomocí protokolu Kerberos nebo NTLM, tento útok je obvykle buď vodorovně, pomocí malé sady hesel v mnoha uživateli; nebo svislé s rozsáhlou sadou hesla na několik uživatelů. nebo libovolné kombinaci obou. Heslo zařízení po úspěšně výčet seznamu platní uživatelé z řadiče domény, útočníci zkuste jedno heslo pečlivě vytvořené pro všechny známé uživatelské účty (jedno heslo na více účtů). Pokud selže počáteční heslo zařízení, zkuste to znovu, využívají jiné heslo pečlivě vytvořený, obvykle po uplynutí 30 minut mezi pokusy. Doba čekání útočníkům umožňuje, aby neměl spouštět nejčastěji podle času účet uzamčení prahové hodnoty. Heslo zařízení se rychle stal oblíbenou technikou útočník a testery pera. Heslo zařízení útoky ukázaly na zajistit efektivitu při získávání počáteční základnu v organizaci a pro následné laterální přesuny pokouší o zvýšení oprávnění. 

**Období učení** minimální dobu, než tento typ upozornění se dá spouštět je jeden týden.

**Šetření**

1.  Klikněte na tlačítko **stáhnout podrobnosti o** zobrazíte úplné informace v Excelové tabulce. Je k dispozici následující informace: 
   -    Seznam napadené účty
   -    Seznam odhadnuté účty v které pokusů o přihlášení, bylo dokončeno s úspěšné ověření
   -    Pokud byly provedeny pokusy o ověření, pomocí protokolu NTLM, zobrazí se vám relevantní události aktivit 
   -    Pokud byly provedeny pokusy o ověření, pomocí protokolu Kerberos, zobrazí se příslušné síťové aktivity
   -  Pokud pokusy o ověření použít heslo zařízení, zobrazí se příslušné síťové aktivity

2.  Klikněte na zdrojovém počítači přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době těchto pokusů o přihlášení, hledání neobvyklých aktivit, jako například: kdo byl přihlášen, které prostředky tam, kde získat přístup. Pokud jste nepovolili integraci ochrany ATP v programu Windows Defender, klikněte na možnost ochrana ATP v programu Windows Defender odznáčku ![Oznámení "BADGE" ochrany ATP v programu Windows Defender](./media/wd-badge.png) aby to prověřili počítače. V programu Windows Defender ATP zobrazí se výstrahy a procesů došlo k přibližně v době výstrahy. 

3.  Pokud se provádí ověřování pomocí protokolu NTLM a uvidíte, že výstraha vyskytuje v mnoha případech a není dostatek informací o serveru, který zdrojový počítač se pokusil získat přístup, povolte **auditování protokolu NTLM** na součástí řadiče domény. K tomuto účelu zapněte události 8004. Toto je událost ověřování NTLM, která obsahuje informace o zdrojovém počítači, uživatelský účet a ** serveru, které na zdrojovém počítači se pokusili získat přístup. Až budete vědět, které server odeslal ověření ověřování, prozkoumejte serveru tak, že zkontrolujete jeho události, jako je 4624 pro lepší pochopení procesu ověřování. 

**Náprava**

[Složitá a dlouhá hesla](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) poskytují nezbytnou první úroveň zabezpečení před útoky hrubou silou.

## <a name="suspicious-communication-over-dns"></a>Podezřelá komunikace prostřednictvím DNS
<a name="suspicious-communication-over-dns"></a>

*Předchozí název:* podezřelá komunikace prostřednictvím DNS 

**Popis**

Protokol DNS ve většině organizací je obvykle není monitorovat a zřídka blokované před škodlivými aktivitami. To umožňuje útočníkovi na napadeném počítači zneužívání protokolu DNS. Škodlivý komunikace prostřednictvím DNS je možné pro průsak dat ven, příkaz a ovládací prvek a/nebo omezení úmyslem vyhnout podnikové sítě.

**Šetření**
> [!NOTE]
> *Podezřelá komunikace prostřednictvím DNS* výstrahy zabezpečení seznamu podezřelých domény. Nové domény nebo domény nedávno přidali, které nejsou dosud známé nebo rozpoznávaných ochrany ATP v programu Azure, ale jsou známé nebo součástí vaší organizaci se dá zavřít. 


1.  Některé legitimní společnosti používají službu DNS pro pravidelné komunikace. Zkontrolujte, pokud patří doména registrovaný dotaz pro důvěryhodného zdroje, jako je například poskytovatele antivirového softwaru. Pokud je známé a důvěryhodné domény a dotazy DNS jsou povolené, upozornění se dá zavřít a doména může být [vyloučené](excluding-entities-from-detections.md) odběr budoucích upozornění. 
2.   Pokud domény registrovaný dotaz není důvěryhodný, identifikujte proces vytváření žádosti na zdrojovém počítači. Použití [monitorování procesu](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon) jako pomoc s touto úlohou.
3.  Určuje, kdy podezřelá aktivita spuštěna? Programy byly některé nové nasazení nebo nainstalovaná (AV?) v organizaci? Existují další výstrahy z současně?
4.  Klikněte na zdrojový počítač pro přístup k jeho stránku profilu. Zkontrolujte, co se stalo v době dotazu DNS hledání neobvyklých aktivit, jako je například kdo byl přihlášen, a které prostředky byly použity. Pokud jste nepovolili integraci ochrany ATP v programu Windows Defender, klikněte na možnost ochrana ATP v programu Windows Defender odznáčku ![Oznámení "BADGE" ochrany ATP v programu Windows Defender](./media/wd-badge.png) aby to prověřili počítače. Pomocí ochrany ATP v programu Windows Defender můžete zobrazit výstrahy a procesů došlo k přibližně v době výstrahy.

**Náprava**

Pokud po šetření není důvěryhodné domény registrovaný dotaz, doporučujeme blokování na cílovou doménu, aby všechny budoucí komunikaci. 

## <a name="suspected-dcshadow-attack-dc-promotion"></a>Podezřelý útok DCShadow (povýšení řadiče domény)
<a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>

*Předchozí název:* povýšení řadiče domény podezřelé (možný útok DCShadow)

**Popis**

Útok stínové (DCShadow) řadiče domény je útok navržené tak, aby změnit pomocí škodlivou replikaci objektů adresáře. Tento útok lze provést z libovolného počítače tak, že vytvoříte řadič domény neautorizovaných serverů pomocí procesu replikace.
 
DCShadow používá vzdálené volání Procedur a protokolu LDAP:
1. Zaregistrovat účet počítače jako řadič domény (pomocí oprávnění správce domény), a
2. Provádění replikace (s použitím udělena práva replikace) za drsuapi s žádostí o a odeslat změny objektů adresáře.
 
V této detekce se aktivuje upozornění, když počítače v síti se pokouší zaregistrovat jako řadič domény neautorizovaných serverů. 

**Šetření**
 
1. Je počítač v otázce řadiče domény? Například připojovaly řadiče domény, které měly potíže s replikací. Pokud ano, **Zavřít** podezřelou aktivitu.
2. Dotyčný počítač by měl být replikaci dat ze služby Active Directory? Například Azure AD Connect. Pokud ano, **zavřít a vyloučit** podezřelou aktivitu.
3. Klikněte na zdrojový počítač nebo účet, přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době replikace, hledání neobvyklých aktivit, jako například: kdo byl přihlášen, k jakým prostředkům a co je počítač, operační systém?
   1. Jsou všichni uživatelé, které se připojily k počítači, by měl být přihlášení? Jaké jsou jejich oprávnění? Mají oprávnění ke zvýšení úrovně serveru na řadič domény? (jsou domain admins)?
   2. Mají uživatelé k těmto prostředkům přístup?
   3. Běží počítači operační systém Windows Server (nebo Windows/Linux)? Počítač jiného typu než server by nemělo replikovat data.
Pokud jste nepovolili integraci ochrany ATP v programu Windows Defender, klikněte na možnost ochrana ATP v programu Windows Defender Odznáček ![ochrany ATP v programu Windows Defender oznámení "BADGE"](./media/wd-badge.png) k hlubšímu prošetření je počítač. V programu Windows Defender ATP zobrazí se výstrahy a procesů došlo k přibližně v době výstrahy.

4. Podívejte se na Prohlížeč událostí zobrazíte [události služby Active Directory, které zaznamenává v adresáři protokolu služeb](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/). V protokolu můžete použít ke sledování změn ve službě Active Directory. Ve výchozím nastavení služby Active Directory zaznamená pouze kritické chybové události, ale pokud se tato výstraha se opakuje, povolte tento audit na řadiči domény relevantní pro další zkoumání.

**Opravit**

Kontrola, kdo ve vaší organizaci tato oprávnění: 
- Replikace změn adresáře 
- Replikovat všechny změny v adresáři 
 
 
Další informace najdete v tématu [udělení Active Directory Domain Services oprávnění k synchronizaci profilu v SharePoint serveru 2013](https://technet.microsoft.com/library/hh296982.aspx). 

Můžete využít [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit skript prostředí Windows PowerShell k určení, kdo v doméně tato oprávnění má.
 
> [!NOTE]
> Výstrahy povýšení (možný útok DCShadow) řadiče domény podezřelé jsou podporovány pouze senzorů ochrany ATP v programu. 

## <a name="suspicious-modification-of-sensitive-groups"></a>Podezřelé úprava citlivých skupin
<a name="suspicious-midification-of-sensitive-groups"></a>

*Předchozí název:* podezřelé úprava citlivých skupin

**Popis**

Útočníci přidání uživatelů do skupiny s vysokou úrovní oprávnění. Učiní tak získat přístup k více prostředkům a k získání průniku do sítě. Tato detekce spoléhá na profilaci aktivity Změna skupiny uživatelů a upozorní při viděli doplněk neobvyklé citlivých skupin. Profilace se neustále provádí pomocí služby Azure ATP. Minimální dobu, než může být výstraha je jeden měsíc na každém řadiči domény.

Definice citlivých skupin v Azure ATP, naleznete v tématu [práce s citlivými účty](sensitive-accounts.md).


Tato detekce spoléhá na [události se auditují na řadiče domény](configure-event-collection.md).
Abyste měli jistotu, vaše doména auditu řadiče potřebné události.

**Šetření**

1. Úpravy skupiny je legitimní? </br>Úpravy legitimní skupiny zřídka dojít a nebyly zjistili, jako je "normální", může dojít k upozornění, která může být považovaná za neškodné pravdivě pozitivní upozornění.

2. Pokud byl přidaný objekt uživatelský účet, zkontrolujte akce, které trvalo uživatelský účet po přidání do skupiny správců. Přejděte na stránku uživatele v Azure ATP, chcete-li získat podrobnější přehled. Tam byli jakýkoli jiný podezřelé aktivity, které jsou přidružené k účtu před nebo po přidání konal úplně? Stáhnout **úpravy citlivých skupin** sestavu, abyste viděli, jaké další změny byly provedeny a kým stejného časového období.

**Náprava**

Minimalizujte počet uživatelů, kteří mají oprávnění upravit citlivých skupin.

Nastavit [Privileged Access Management pro službu Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) Pokud je k dispozici.



## <a name="suspected-dcshadow-attack-dc-replication-request"></a>Podezření na útok DCShadow (žádost o replikaci řadiče domény)
<a name="suspicious-replication-request-potential-dcshadow-attack"></a>

*Předchozí název:* podezřelá replikace požadavku (možný útok DCShadow) 

**Popis** 

Replikace služby Active Directory je proces, podle kterého se změny provedené na jednom řadiči domény synchronizují s jinými řadiči domény. Udělili nezbytná oprávnění, útočníci mohou neuděluje práva k jejich účet počítače, což jim umožní zosobnit řadiče domény. Útočníci se snažit inicializujte žádost o škodlivou replikaci, což jim umožní změnit objekty služby Active Directory na řadič domény pravosti, která může přidělit útočníci přetrvávání v doméně.
V této detekce se aktivuje upozornění při generování podezřelá replikace požadavek proti řadiči domény originální chráněné službou ochrany ATP v programu Azure. Chování je indikátorem techniky využívají útocích stínové řadič domény.

**Šetření** 
 
1. Je počítač v otázce řadiče domény? Například připojovaly řadiče domény, které měly potíže s replikací. Pokud ano, **Zavřít** podezřelou aktivitu.
2. Dotyčný počítač by měl být replikaci dat ze služby Active Directory? Například Azure AD Connect. Pokud ano, **zavřít a vyloučit** podezřelou aktivitu.
3. Klikněte na zdrojovém počítači přejděte na stránku jeho profil. Zkontrolujte, co se stalo **v době** replikace, hledání neobvyklých aktivit, jako například: kdo byl přihlášen, které prostředky byly použity a co je počítač, operační systém?

   1.  Jsou všichni uživatelé, které se připojily k počítači, by měl být přihlášení? Jaké jsou jejich oprávnění? Mají oprávnění k provedení akce replikace (jsou domain admins)?
   2.  Mají uživatelé k těmto prostředkům přístup?
   3. Běží počítači operační systém Windows Server (nebo Windows/Linux)? Počítač jiného typu než server by nemělo replikovat data.
Pokud jste nepovolili integraci ochrany ATP v programu Windows Defender, klikněte na možnost ochrana ATP v programu Windows Defender Odznáček ![ochrany ATP v programu Windows Defender oznámení "BADGE"](./media/wd-badge.png) k hlubšímu prošetření je počítač. V programu Windows Defender ATP zobrazí se výstrahy a procesů došlo k přibližně v době výstrahy.
1. Podívejte se na Prohlížeč událostí zobrazíte [události služby Active Directory, které zaznamenává v adresáři protokolu služeb](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/). V protokolu můžete použít ke sledování změn ve službě Active Directory. Ve výchozím nastavení služby Active Directory zaznamená pouze kritické chybové události, ale pokud se tato výstraha se opakuje, povolte tento audit na řadiči domény relevantní pro další zkoumání.

**Náprava**

Kontrola, kdo ve vaší organizaci tato oprávnění: 
- Replikace změn adresáře 
- Replikovat všechny změny v adresáři 

K tomuto účelu můžete využít [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit skript prostředí Windows PowerShell k určení, kdo v doméně tato oprávnění má.

> [!NOTE]
> Upozornění na podezřelé replikace žádosti (možný útok DCShadow) jsou podporovány pouze senzorů ochrany ATP v programu. 


## <a name="suspicious-service-creation"></a>Podezřelé vytvoření služby
<a name="suspicious-service-creation"></a>

*Předchozí název:* podezřelé vytvoření služby

**Popis**

Podezřelé služba je vytvořená na řadiči domény ve vaší organizaci. Tato výstraha se spoléhá na událost 7045 za účelem zjištění této podezřelé aktivity. 

**Šetření**

1. Pokud v daném počítači je k pracovní stanici správce, nebo počítače, na které členové týmu IT a služba účty provádět úlohy správy, může jít o falešně pozitivní upozornění a možná budete muset **potlačit** upozornění a přidejte ho do Seznam vyloučení v případě potřeby.

2. Je služba něco, co rozpoznat v tomto počítači?

 - Je **účet** dotyčný můžou nainstalovat tuto službu?

 - Pokud na obě otázky odpovíte *Ano*, pak **Zavřít** výstrahu nebo ho přidejte do seznamu vyloučení.

3. Pokud na obě otázky odpovíte *žádné*, a to by se měly zvažovat pravdivě pozitivní upozornění.

**Náprava**

- Implementace méně privilegovaný přístup v doméně počítače povolit jenom konkrétní uživatelé práva k vytvoření nové služby.


## <a name="suspicious-vpn-connection"></a>Podezřelé připojení k síti VPN
<a name="suspicious-vpn-detection"></a>

*Předchozí název:* podezřelé sítě VPN 

**Popis**

Ochrana ATP v programu Azure se učí chování entit pro uživatele sítě VPN klouzavou dobu jednoho měsíce. 

Model chování VPN je založen na následující činnosti: počítače přihlášení uživatele k a umístění se uživatelé připojovat z. 

Oznámení se otevře po odchylky od chování uživatele podle algoritmu strojového učení.

**Šetření**

1.  Dotyčný uživatel by měl být provádění těchto operací?
2.  Vezměte v úvahu následující případů jako potenciální falešně pozitivní: uživatel změnil jeho umístění, jako uživatel, který je na cestách a připojit se z nového zařízení.

**Náprava**

1.  Zvažte, resetuje se heslo tohoto uživatele. Útočník zabrání vytvoření nových připojení sítě VPN pomocí staré přihlašovacích údajů.
2.  Vezměte v úvahu blokování tento uživatel v připojení prostřednictvím sítě VPN.

## <a name="unusual-protocol-implementation"></a>Neobvyklá implementace protokolu
<a name="unusual-protocol-implementation"></a>

*Předchozí název:* neobvyklá implementace protokolu 

**Popis**

Útočníci použít nástroje, které implementují různé protokoly (SMB, Kerberos, NTLM) nestandardním způsobem. Tento typ síťového provozu je přijat ve Windows bez upozornění, je ochrana ATP v programu Azure rozpoznat potenciální škodlivým činnostem. Chování je indikátorem techniky, jako je například over-pass-the-Hash a útoky hrubou silou, jakož i zneužití používané Upřesnit ransomwaru, například WannaCry.

**Šetření**

Identifikace protokol, který neobvyklé – z časové osy podezřelých aktivit, klikněte na výstrahu zabezpečení zobrazíte na stránku jeho podrobnosti. protokol se zobrazí nad šipku: protokolu Kerberos nebo NTLM.

- **Protokol Kerberos**: to se často aktivuje, pokud hackerům nástroj, jako je nástroj Mimikatz se použil, potenciálně provedení útoku Overpass-the-Hash. Zaškrtněte, pokud zdrojovém počítači běží aplikace, která implementuje vlastní zásobník protokolu Kerberos, není v souladu s RFC protokolu Kerberos. Pokud je to tento případ, se jedná o neškodné pravdivě pozitivní upozornění a můžete **Zavřít** výstrahu. Pokud výstrahu pokračuje k aktivaci a je stále splněny, můžete předchozí kontrola **potlačit** výstrahu.

- **NTLM**: pravděpodobně WannaCry nebo nástrojů, jako je Metasploit Medusa a Hydra.  

Pokud chcete zjistit, zda se jedná o útok WannaCry, proveďte následující kroky:

1. Zkontrolujte, jestli zdrojovém počítači běží nástroj útoku například Metasploit, Medusa nebo Hydra.

2. Pokud se nenajdou žádné nástroje útoku, zkontrolujte, zda zdrojovém počítači běží aplikace, která implementuje vlastní zásobník protokolu NTLM nebo podepisování SMB.

3. Klikněte na zdrojovém počítači přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době výskytu výstrahy, hledání neobvyklých aktivit, jako například: kdo byl přihlášen, které prostředky tam, kde získat přístup. Pokud jste nepovolili integraci ochrany ATP v programu Windows Defender, klikněte na možnost ochrana ATP v programu Windows Defender odznáčku ![oznámení "BADGE" WD](./media/wd-badge.png) aby to prověřili počítače. V programu Windows Defender ATP zobrazí se výstrahy a procesů došlo k přibližně v době výstrahy.


**Náprava**

Oprava všech počítačů, zejména použití aktualizací zabezpečení.

1. [Zakázat SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Odebrat WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3. WanaKiwi může dešifrovat data v rámci ransom softwaru, ale jen pokud uživatel nebyl restartovat nebo vypnout počítač. Další informace najdete v tématu [chcete pokřik Ransomwaru](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)



> [!NOTE]
> Pokud chcete zakázat výstrahu zabezpečení, obraťte se na podporu.


## <a name="see-also"></a>Viz také
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

---
title: Průvodce podezřelými aktivitami ATA | Dokumentace Microsoftu
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: be1a699ffd1ab0925df43910aec7f8166d4e423d
ms.sourcegitcommit: 58c75026e5ec4dcab3b0852a41f9f0a0ad6f22eb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2018
ms.locfileid: "49315842"
---
*Platí pro: Advanced Threat Analytics verze 1.9*


# <a name="advanced-threat-analytics-suspicious-activity-guide"></a>Průvodce prošetřováním podezřelých aktivit rozšířené analýzy hrozeb

Po správném šetření dají považovat za podezřelé aktivity:

-   **Pravdivě pozitivní upozornění**: škodlivá akce zjištěná službou ATA.

-   **Neškodné pravdivě pozitivní upozornění**: akce zjištěná službou ATA, která je skutečná, ale není škodlivá, třeba test průniku.

-   **Falešně pozitivní**: alarm hodnotu false, to znamená aktivity neměli stát.

Další informace o tom, jak pracovat s výstrahami ATA najdete v tématu [práce s podezřelými aktivitami](working-with-suspicious-activities.md).

Pro dotazy nebo připomínky, obraťte se na tým ATA v [ ATAEval@microsoft.com ](mailto:ATAEval@microsoft.com).

## <a name="abnormal-sensitive-group-modification"></a>Neobvyklá úprava citlivých skupin


**Popis**

Útočníci přidání uživatelů do skupiny s vysokou úrovní oprávnění. Udělají to k získání přístupu k více prostředkům a k získání průniku do sítě. Detekce spoléhají na profilaci aktivity Změna skupiny uživatelů a upozorní při viděli doplněk neobvyklé citlivých skupin. Profilace se provádí nepřetržitě pomocí ATA. Minimální dobu, než může být výstraha je jeden měsíc na řadiči domény.

Definice citlivých skupin v ATA najdete v části [práce s konzolou ATA](working-with-ata-console.md#sensitive-groups).


Tato detekce spoléhá na [události se auditují na řadiče domény](https://docs.microsoft.com/advanced-threat-analytics/configure-event-collection).
Pokud chcete mít jistotu, potřebné události auditu řadičů domény, použijte nástroj odkazuje [ATA auditování (AuditPol, rozšířeného auditu vynucení nastavení zjišťování služeb Lightweight Gateway)](https://aka.ms/ataauditingblog).

**Šetření**

1. Úpravy skupiny je legitimní? </br>Úpravy legitimní skupiny zřídka dojít a nebyly zjistili, jako je "normální", může dojít k upozornění, která může být považovaná za neškodné pravdivě pozitivní upozornění.

2. Pokud byl přidaný objekt uživatelský účet, zkontrolujte akce, které trvalo uživatelský účet po přidání do skupiny správců. Přejděte na stránku uživatele v ATA získali podrobnější přehled. Tam byli jakýkoli jiný podezřelé aktivity, které jsou přidružené k účtu před nebo po přidání konal úplně? Stáhnout **úpravy citlivých skupin** sestavu, abyste viděli, jaké další změny byly provedeny a kým stejného časového období.

**Náprava**

Minimalizujte počet uživatelů, kteří mají oprávnění upravit citlivých skupin.

Nastavit [Privileged Access Management pro službu Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) Pokud je k dispozici.

## <a name="broken-trust-between-computers-and-domain"></a>Porušený vztah důvěryhodnosti mezi počítači a domény

> [!NOTE]
> Porušený vztah důvěryhodnosti mezi počítači a domény výstraha byla zrušena a zobrazí pouze v ATA verze starší než 1.9.

**Popis**

Porušený vztah důvěryhodnosti znamená, že požadavky na zabezpečení služby Active Directory nemusí platit pro tyto počítače. Je to standardních hodnot zabezpečení a dodržování předpisů a za snadný cíl pro útočníky. V této detekce se aktivuje upozornění, pokud více než pět chybám ověření protokolem Kerberos nějakého účtu počítače do 24 hodin.

**Šetření**

Je počítač Zkoumáme, umožnit uživatelům domény pro přihlášení? 
- Pokud ano, můžete ignorovat tento počítač nápravných kroků.

**Náprava**

V případě potřeby znovu připojit počítač znovu k doméně nebo resetovat jeho heslo.


## <a name="brute-force-attack-using-ldap-simple-bind"></a>Útok hrubou silou pomocí jednoduché vazby LDAP.

**Popis**

>[!NOTE]
> Hlavní rozdíl mezi **podezřelá neúspěšná ověření** a toto zjišťování je, že v této detekce ATA můžete určit, zda byly použity odlišná hesla.

V rámci útoku hrubou silou se útočník pokusí ověření pomocí mnoha různých hesel pro různé účty, dokud nebude nalezen správné heslo pro alespoň jeden účet. Jednou najde, útočník může přihlásit pomocí tohoto účtu.

V této detekce se aktivuje upozornění, když ATA zjistí masivní počet ověření jednoduché vazby. Může to být buď *vodorovně* s menší skupinou hesel mezi mnoha uživateli; nebo *svisle "* s rozsáhlou sadou hesla u několika uživatelů; či libovolnou kombinaci těchto dvou možností.

**Šetření**

1. Pokud se využívá řada řadu účtů, klikněte na tlačítko **stáhnout podrobnosti o** pro zobrazení seznamu v Excelové tabulce.

2. Klikněte na výstrahu, kterou chcete přejít na jeho vyhrazenou stránku. Zkontrolujte, zda pokusů o přihlášení jakékoli skončilo s po provedení úspěšného ověření. Pokusy se zobrazí jako **odhadnuté účty** na pravé straně infografiku. Pokud ano, jsou všechny **odhadnuté účty** běžně používaný ze zdrojového počítače? Pokud ano, **potlačit** podezřelou aktivitu.

3. Pokud neexistují žádné **odhadnuté účty**, jsou všechny **napadených účtů** běžně používaný ze zdrojového počítače? Pokud ano, **potlačit** podezřelou aktivitu.

**Náprava**

[Složitá a dlouhá hesla](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) poskytují nezbytnou první úroveň zabezpečení před útoky hrubou silou.

## <a name="encryption-downgrade-activity"></a>Aktivita snížení úrovně šifrování

**Popis**

Oslabení šifrování je metoda oslabení podle downgradu úrovně šifrování protokolu různých polí, které jsou obvykle šifrována pomocí nejvyšší úrovně šifrování pomocí protokolu Kerberos. Oslabeným šifrované pole může být snazší target na offline útoky hrubou silou při pokusech. Různých metod útoku zvýšit využití slabé šifrování doklad protokolu Kerberos. V této detekce ATA učí typy šifrování pomocí protokolu Kerberos, počítačů a uživatelů a upozorní vás, když je slabší šifrovací, který používá: (1) neobvyklé, že u zdrojového počítače nebo uživatele. a (2) shod označuje technik útoku.

Existují tři typy detekce:

1.  Skeleton Key – je malware, který běží na řadičích domény a umožňuje ověření vůči doméně pomocí libovolného účtu bez znalosti jeho hesla. Tento malware často používá slabší šifrovací algoritmy k vytvoření hodnoty hash hesel uživatelů na řadiči domény. Tato detekce byla metoda šifrování zprávy KRB_ERR z řadiče domény k účtu s žádostí o lístek downgradovat ve srovnání s dřív zjištěné chování.

2.  Lístku Golden – [Golden Ticket](#golden-ticket) výstrah, metoda šifrování pole TGT v TGS_REQ (žádost o službu) zprávy ze zdrojového počítače byl downgradovat ve srovnání s dřív zjištěné chování. To není založené na čase anomálií (stejně jako v jiných detekce Golden Ticket). Kromě toho se žádný požadavek na ověření Kerberos související s předchozí žádosti o službu ATA detekuje.

3.  Overpass-the-Hash – může útočník zneužít k vytvoření lístku silné žádost Kerberos AS slabé odcizené hodnoty hash. Při tomto zjišťování byla downgradovat typ šifrování zprávy AS_REQ ze zdrojového počítače, ve srovnání s dřív zjištěné chování (to znamená, počítač se pomocí standardu AES).

**Šetření**

Nejprve zkontrolujte Popis upozornění a uvidíte, které z výše uvedených tří typů detekce, že pracujete s. Další informace stáhněte si Excelové tabulky.
1.  Skeleton Key – můžete zkontrolovat, pokud řadiče domény s použitím ovlivnila Skeleton Key [kontroly vytvořené týmem ATA](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). Skener najde malware na 1 nebo více řadičů domény, jde o pravdivě pozitivní upozornění.
2.  Zlatý lístek – v Excelové tabulce, přejděte **síťové aktivity** kartu. Uvidíte, že je pole relevantní sníženou příbuzností **typ šifrování lístku žádosti**, a **typy šifrování podporované zdrojové počítače** uvádí silnější metody šifrování.
  a.    Zkontrolujte zdrojový počítač a účet, nebo pokud existuje více zdrojových počítačů a účtů kontrolovat, jestli se mají něco společné (například všechny marketingové pracovníky pomocí konkrétní aplikace, které by mohly způsobovat aktivovat upozornění). Existují případy, ve kterých je vlastní aplikaci, která se zřídka se používá ověřování pomocí nižší šifry šifrování. Zkontrolujte, jestli jsou na zdrojovém počítači těchto vlastních aplikací. Pokud ano, je pravděpodobně o neškodné pravdivě pozitivní upozornění a **potlačit** ho.
  b.    Zkontrolujte prostředek přistupuje tyto lístky, pokud je jeden prostředek, ke kterým všechny přistupují, ověřte ho, ujistěte se, že je platný prostředek, který se má přístup. Dále ověřte, jestli cílový prostředek podporuje metody silné šifrování. Můžete zkontrolovat ve službě Active Directory tak, že zkontrolujete atribut `msDS-SupportedEncryptionTypes`, prostředků účtu služby.
3.  Overpass-the-Hash – v Excelové tabulce, přejděte **síťové aktivity** kartu. Uvidíte, že je pole relevantní sníženou příbuzností **šifrované typ šifrování časové razítko** a **typy šifrování podporované zdrojové počítače** obsahuje silnější metody šifrování.
  a.    Existují případy, ve kterých může aktivuje toto upozornění, když uživatel přihlásí pomocí čipové karty, pokud byla nedávno změnila konfigurace čipové karty. Zaškrtněte, pokud došlo ke změně tímto způsobem pro účty používané. Pokud ano, je pravděpodobně o neškodné pravdivě pozitivní upozornění a **potlačit** ho.
  b.    Zkontrolujte prostředek přistupuje tyto lístky, pokud je jeden prostředek, ke kterým všechny přistupují, ověřte ho, ujistěte se, že je platný prostředek, který se má přístup. Dále ověřte, jestli cílový prostředek podporuje metody silné šifrování. Můžete zkontrolovat ve službě Active Directory tak, že zkontrolujete atribut `msDS-SupportedEncryptionTypes`, prostředků účtu služby.

**Náprava**

1.  Kostru klíče – odebere malware. Další informace najdete v tématu [analýzy Malware Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).

2.  Zlatý lístek – postupujte podle pokynů [Golden Ticket](#golden-ticket) podezřelých aktivit.   
    Navíc vzhledem k tomu, že vytvoření Golden Ticket vyžaduje práva správce domény, implementovat [předání hodnoty hash doporučení](https://www.microsoft.com/download/details.aspx?id=36036).

3.  Overpass-the-Hash – Pokud je potřebný účet není citlivé, poté resetujte heslo daného účtu. To zabrání útočník vytváření nových lístky protokolu Kerberos z hodnoty hash hesla, i když existující lístky je stále možné až do vypršení jejich platnosti. Pokud je citlivý účet, měli byste zvážit, obnovení účtu KRBTGT dvakrát jako podezřelá aktivita zlatého lístku. Obnovení účtu KRBTGT dvakrát zruší platnost všech protokolu Kerberos, takže Plánujte lístky v této doméně než to uděláte. Přečtěte si pokyny v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Viz také pomocí [resetování nástroj hesla/klíčů účtu KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Protože to je technika laterálního pohybu, postupujte podle osvědčené postupy z [předání hodnoty hash doporučení](https://www.microsoft.com/download/details.aspx?id=36036).


## <a name="honeytoken-activity"></a>Aktivita Honeytokenu


**Popis**

Návnada účty nastavené tak identifikovat a sledovat škodlivou aktivitu, která zahrnuje tyto účty jsou účty Honeytokenu. Honeytokenové účty by měla zůstat nevyužité, přitom má atraktivní název k navést útočníci (například SQL-Admin). Všechny aktivity z nich může znamenat škodlivého chování.

Další informace o honey token účty, najdete v části [instalace ATA – krok 7](install-ata-step7.md).

**Šetření**

1.  Zkontrolujte, zda Vlastník zdrojového počítače používá účet Honeytokenu k ověření, pomocí metody popsané na stránce podezřelých aktivit (například Kerberos, LDAP, NTLM).

2.  Přejděte na stránku nebo stránky zdrojového počítače profilu a zkontrolujte ostatní účty, které se ověřil z nich. Obraťte se na vlastníky účtů, pokud použity účtů Honeytokenu.

3.  To může být neinteraktivního přihlášení, proto nezapomeňte zaškrtnout pro aplikace nebo skripty, které běží na zdrojovém počítači.

Pokud po provedení kroků 1 až 3, pokud neexistuje žádný doklad o neškodné použití, se předpokládá, že jde o škodlivé.

**Náprava**

Ujistěte se, že Honeytokenu účtů se používají pouze pro jejich zamýšlený účel, jinak může generovat více výstrah.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Krádež identity pomocí útoku Pass-the-Hash

**Popis**

Pass-the-Hash je technika laterálního pohybu, kdy útočník získá NTLM hash uživatele z jednoho počítače a použije ho k získání přístupu k jinému počítači. 

**Šetření**

Zkontrolujte, jestli-the-hash používá z počítače vůči cílové uživatele nebo pravidelně používá? Pokud ano, je falešně pozitivní výstrahu, pokud nejsou, pravděpodobně se jedná o pravdivě pozitivní upozornění.

**Náprava**

1. Pokud není potřebný účet citlivé, resetovat heslo daného účtu. Resetuje se heslo zabraňuje útočníkovi vytváření nových lístky protokolu Kerberos z hodnoty hash hesla. Existující lístky jsou stále možné použít, dokud nevyprší jejich platnost. 

2. Pokud je potřebný účet citlivý, zvažte obnovení účtu KRBTGT dvakrát, stejně jako v podezřelá aktivita zlatého lístku. Obnovení účtu KRBTGT dvojím zruší platnost všechny lístky protokolu Kerberos domény, než to uděláte, takže Plánujte kolem dopad. Přečtěte si pokyny v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), platí také pro použití [nástroj hesla/klíčů účtu KRBTGT pro resetování](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Toto je obvykle technika laterálního pohybu, postupujte podle osvědčené postupy z [předání hodnoty hash doporučení](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Krádež identity pomocí útoku Pass-the-Ticket

**Popis**

Pass-the-Ticket je technika laterálního pohybu, kdy útočník získá lístek Kerberos z jednoho počítače a použije ho k získání přístupu k jinému počítači opětovným použitím odcizených lístků. Při zjišťování je zobrazena lístek protokolu Kerberos používá na dvou (nebo více) různých počítačích.

**Šetření**

1. Klikněte na tlačítko **stáhnout podrobnosti o** tlačítko zobrazit úplný seznam IP adres zahrnuté. Je IP adresa jeden nebo oba počítače jsou součástí podsítě přidělené z nedostatečné velikosti fondu adres DHCP, například síť VPN nebo Wi-Fi? Sdílet adresu IP Například tím, že zařízení NAT? Pokud je odpověď na kteroukoli z těchto otázek Ano, je oznámení falešně pozitivní.

2. Existuje vlastní aplikaci, která předává lístky jménem uživatelů? Pokud ano, jedná se o neškodnou pravdivě pozitivní.

**Náprava**

1. Pokud není potřebný účet citlivé, resetujte heslo daného účtu. Heslo zopakuje útočník zabrání vytváření nových lístky protokolu Kerberos z hodnoty hash hesla. Všechny existující lístky zůstávají použitelné, dokud platnost vypršela.  

2. Pokud je citlivý účet, měli byste zvážit, obnovení účtu KRBTGT dvakrát jako podezřelá aktivita zlatého lístku. Obnovení účtu KRBTGT dvakrát zruší platnost všech protokolu Kerberos, takže Plánujte lístky v této doméně než to uděláte. Přečtěte si pokyny v [KRBTGT účet skriptů pro resetování hesla nyní dostupný pro zákazníky se](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), také naleznete pomocí [resetování nástroj hesla/klíčů účtu KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Protože to je technika laterálního pohybu, postupujte podle osvědčených postupů v [předání hodnoty hash doporučení](https://www.microsoft.com/download/details.aspx?id=36036).

## Protokol Kerberos Golden Ticket<a name="golden-ticket"></a>

**Popis**

Útočníci s právy správce domény může ohrozit vaši [účtu KRBTGT](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). Útočníci můžete použít účet KRBTGT domény vytvořit lístek Kerberos udělující lístek (TGT) poskytuje autorizaci k jakémukoli prostředku. Vypršení platnosti lístku můžete nastavit na libovolný kdykoli. Tato falešných lístků TGT se nazývá "Zlatých lístků" a útočníkům umožňuje dosáhnout a zachovávat průniku do sítě ve vaší síti.

V této detekce se aktivuje upozornění, pokud je Kerberos lístku pro přidělování lístků (TGT) se používá pro více než povolená doba uvedená v [maximální doba života lístku uživatele](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx) zásady zabezpečení.

**Šetření**

1. Pokusil se poslední (během posledních několik hodin) změny provedené **maximální doba života lístku uživatele** nastavení v zásadách skupiny? Pokud ano, pak **Zavřít** upozornění (bylo falešně pozitivní).

2. ATA Gateway je zahrnuté v této výstraze virtuálního počítače? Pokud ano, ji nedávno pokračovat od uloženého stavu? Pokud ano, pak **Zavřít** této výstrahy.

3. Pokud je odpověď na otázky uvedené výše předpokládají Ne, to se zlými úmysly.

**Náprava**

Změnit heslo protokolu Kerberos KRBTGT Ticket Granting Ticket () dvakrát podle pokynů v [KRBTGT účet skriptů pro resetování hesla nyní k dispozici pro zákazníky, kteří](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), použije [resetování hesla/klíčů účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Obnovení účtu KRBTGT dvakrát zruší platnost všech protokolu Kerberos, takže Plánujte lístky v této doméně než to uděláte.  
Navíc vzhledem k tomu, že vytvoření Golden Ticket vyžaduje práva správce domény, implementovat [předání hodnoty hash doporučení](https://www.microsoft.com/download/details.aspx?id=36036).


## <a name="malicious-data-protection-private-information-request"></a>Škodlivá žádost o soukromé informace přes Data Protection

**Popis**

Data Protection API (DPAPI) používá Windows bezpečné ochrany hesel uložil prohlížeče, šifrované soubory a další citlivá data. Řadičích domény se nachází záložní hlavní klíč, který slouží k dešifrování všech tajných kódů zašifrovaných pomocí rozhraní DPAPI na počítačích připojených k doméně Windows. Útočníci můžou používat tohoto hlavního klíče k dešifrování všech tajných kódů chráněn DPAPI na všech počítačích připojených k doméně.
V této detekce se aktivuje upozornění při použití neúspěšně pokusil načíst záložní hlavní klíč rozhraní DPAPI.

**Šetření**

1. Zdrojový počítač, s organizaci schválení je pokročilý kontrolu zabezpečení Active Directory?

2. Pokud ano a ji by měl vždy být tím,**zavřít a vyloučit** podezřelou aktivitu.

3. Pokud ano a je to dělat neměli, ** zavřete podezřelou aktivitu.

**Náprava**

Použití rozhraní DPAPI, potřebuje útočník práva správce domény. Implementace [předání hodnoty hash doporučení](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="malicious-replication-of-directory-services"></a>Škodlivá replikace adresářových služeb


**Popis**

Replikace služby Active Directory je proces, podle kterého se změny provedené na jednom řadiči domény synchronizují s jinými řadiči domény. Udělili nezbytná oprávnění, útočníci mohou zahájit žádost o replikaci, což jim umožní načíst dat uložená ve službě Active Directory, včetně hodnot hash hesel.

V této detekce se aktivuje upozornění, když se spustí požadavek replikace na počítači, který není řadičem domény.

**Šetření**

1.  Je počítač v otázce řadiče domény? Například připojovaly řadiče domény, které měly potíže s replikací. Pokud ano, **Zavřít** podezřelou aktivitu. 
2.  Dotyčný počítač by měl být replikaci dat ze služby Active Directory? Například Azure AD Connect. Pokud ano, **zavřít a vyloučit** podezřelou aktivitu.
3.  Klikněte na zdrojový počítač nebo účet, přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době replikace, hledání neobvyklých aktivit, jako například: kdo byl přihlášen, které prostředky tam, kde získat přístup. 


**Náprava**

Ověřte následující oprávnění: 

- Replikace změn adresáře   

- Replikovat všechny změny v adresáři  

Další informace najdete v tématu [udělení Active Directory Domain Services oprávnění k synchronizaci profilu v SharePoint serveru 2013](https://technet.microsoft.com/library/hh296982.aspx).
Můžete využít [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit skript prostředí Windows PowerShell k určení, kdo v doméně tato oprávnění má.

## <a name="massive-object-deletion"></a>Hromadné odstranění objektů

**Popis**

V některých scénářích útočníci provádět útok na dostupnost služby (DoS) a ne pouze zcizování informace. Odstranění velkého počtu účtů je jedna z metod pokus o útok DoS. 

V této detekce se aktivuje upozornění, kdykoli více než 5 % všech účtů se odstraní. Zjišťování vyžaduje oprávnění čtení ke kontejneru odstraněných objektů.  
Informace o konfiguraci oprávnění jen pro čtení pro kontejner odstraněných objektů najdete v tématu **Změna oprávnění pro kontejner odstraněných objektů** v [zobrazení nebo nastavení oprávnění u objektu adresáře](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

**Šetření**

Projděte si seznam odstraněné účty a určení, zda je vzor nebo obchodní důvod, který opravňuje ve velkém měřítku odstranění.

**Náprava**

Odeberte oprávnění uživatelům, kteří mohou odstraňovat účty ve službě Active Directory. Další informace najdete v tématu [zobrazení nebo nastavení oprávnění u objektu adresáře](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

## <a name="privilege-escalation-using-forged-authorization-data"></a>Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace

**Popis**

Známé chyby zabezpečení ve starších verzích Windows serveru umožňují útočníkům manipulovat s certifikát PAC (Privileged Attribute). Pole v lístku protokolu Kerberos, který obsahuje data autorizace uživatele je PAC (ve službě Active Directory je to členství ve skupině) a udělí útočníci další oprávnění.

**Šetření**

1. Klikněte na výstrahu, kterou chcete získat přístup na stránku podrobností.

2. Je cílovém počítači (v části **ACCESSED** sloupce) opravit zneužití MS14-068 (řadič domény) nebo zneužití MS11-013 (server)? Pokud ano, **Zavřít** podezřelé aktivity (je falešně pozitivní).

3. Pokud není nainstalované opravy do cílového počítače, zdrojovém počítači běží (v části **FROM** sloupce) označuje upravuje PAC operačního systému nebo aplikace? Pokud ano, **potlačit** podezřelé aktivity (jedná se o neškodnou pravdivě pozitivní).

4. Pokud byla odpověď na dvě předchozí otázky Ne, předpokládají tato aktivita se zlými úmysly.

**Náprava**

Zajistěte, aby na všech řadičích domény s operačním systémem až do verze Windows Server 2012 R2 byla nainstalovaná aktualizace [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) a na všech členských serverech a řadičích domény až do verze 2012 R2 byla nainstalovaná aktualizace KB2496930. Další informace najdete v článku [Stříbrný certifikát PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) a [Zfalšovaný certifikát PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-account-enumeration"></a>Rekognoskace pomocí výčtu účtů

**Popis**

V účtu výčet rekognoskace útočník využívá slovník s tisíci uživatelská jména nebo nástrojů, jako je KrbGuess pokusu odhadnout uživatelská jména ve vaší doméně. Útočník vytvářejí požadavky protokolu Kerberos pomocí tyto názvy, abyste mohli zkusit najít platné uživatelské jméno ve vaší doméně. Pokud odhad úspěšně Určuje uživatelské jméno, útočník zobrazí chybová zpráva protokolu Kerberos **požadované předběžné ověření** místo **neznámý objekt zabezpečení**. 

Při zjišťování dokáže ATA útok, odkud, celkový počet pokusů uhádnout a kolik se shoda našla. Pokud existuje příliš mnoho uživatelů neznámý, detekuje to ATA jako podezřelou aktivitu. 

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


## <a name="reconnaissance-using-directory-services-queries"></a>Rekognoskace pomocí dotazů na adresářové služby

**Popis**

Rekognoskace adresářových služeb je útočníci ke zmapování struktury adresáře a zacílení privilegovaných účtů v pozdějších krocích útoku. Protokol vzdáleného správce zabezpečení účtů (SAM-R) je jedna z metod používaných k dotazování adresáře k provedení těchto mapování.

V tomto zjišťování by první měsíc po nasazení ATA aktivovat žádné výstrahy. Během učení období, ATA profily které dotazy SAM-R se sestavují z které počítače výčet a jednotlivé dotazy citlivých účtů.

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

Použití [nástroj SAMRi10](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b) Posilte zabezpečení svého prostředí pro tento postup.
Pokud nástroj se nevztahuje na vašem řadiči domény:
1. Je počítač se službou zjišťování nástroj ohrožení zabezpečení?  
2. Zjistěte, jestli konkrétní dotazované uživatele a skupiny v útoku jsou privilegovaných nebo vysoce hodnotných účtů (to znamená, generální ředitel, Ředitelka, správy IT, atd.).  Pokud ano, podívejte se na další aktivitu v koncovém bodě také a monitorovat počítače, které jsou dotazované účty přihlášení, protože jde pravděpodobně o cíle taktiky Lateral Movement.

## <a name="reconnaissance-using-dns"></a>Rekognoskace pomocí DNS

**Popis**

DNS server obsahuje mapu všech počítačů, IP adresy a služby ve vaší síti. Tyto údaje používají útočníci ke zmapování struktury vaší sítě a zacílení zajímavých počítačů v pozdějších krocích útoku.

Protokol DNS obsahuje několik typů dotazů. ATA detekuje žádosti AXFR (přenos) pocházející z jiné servery než DNS.

**Šetření**

1. Je na zdrojovém počítači (**pocházející z...** ) DNS server? Pokud ano, pak jde pravděpodobně o falešně pozitivní upozornění. Pokud chcete ověřit, klikněte na výstrahu, kterou chcete získat jeho stránku podrobností. V tabulce v části **dotazu**, zkontrolujte, které domény se poslal dotaz. Jsou tyto existující domény? Pokud ano, pak **Zavřít** podezřelé aktivity (je falešně pozitivní). Kromě toho Ujistěte se, že je mezi komponentou ATA Gateway a zdrojovém počítači zabránit budoucím počet falešně pozitivních výsledků otevřený UDP port 53.
2.  Zdrojový počítač je spuštěný kontrolu zabezpečení? Pokud ano, **vyloučit** entitách v ATA, buď přímo pomocí **zavřít a vyloučit** nebo prostřednictvím **vyloučení** stránky (v části **konfigurace** – k dispozici pro správce ATA).
3.  Pokud odpověď je pro všechny předchozí otázky Ne, ponechat zkoumání zaměření na zdrojovém počítači. Klikněte na zdrojovém počítači přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době požadavku hledání neobvyklých aktivit, jako například: kdo byl přihlášen, které prostředky tam, kde získat přístup.


**Náprava**

Interní server DNS lze proti rekognoskaci pomocí DNS zabezpečit zakázáním nebo omezením přenosů zóny jen na konkrétní IP adresy. Další informace o omezení přenosů zóny najdete v tématu [omezení přenosů zóny](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
Úprava přenosů zóny je jedním z úkolů na kontrolním seznamu, která by měla být určena pro [zabezpečení před útoky interních i externích serverů DNS](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).

## <a name="reconnaissance-using-smb-session-enumeration"></a>Rekognoskace pomocí výčtu relací SMB


**Popis**

Výčet Message Block (SMB) serveru umožňuje útočníkům získat informace, kde uživatelé nedávno přihlašovali. Jakmile útočník tyto informace, se můžete přesunout následně k laterálnímu v síti k určité citlivých účtů.

V této detekce se aktivuje upozornění, když se provádí výčet relací SMB proti řadiči domény.

**Šetření**

1. Klikněte na výstrahu, kterou chcete získat jeho stránku podrobností. Zkontrolujte účtu/s, který provedl operaci a které účty byly vystaveny, pokud existuje.

 - Existuje nějaký druh kontrolu zabezpečení, které běží na zdrojovém počítači? Pokud ano, **zavřít a vyloučit** podezřelou aktivitu.

2. Zkontrolujte operaci provést, které zahrnutých uživatelů/s. Obvykle protokolují do zdrojového počítače nebo jsou správci, kteří by měl provádět tyto akce?  

3. Pokud ano a výstraha aktualizována, **potlačit** podezřelou aktivitu.  

4. Pokud ano a nesmí získat aktualizaci **Zavřít** podezřelou aktivitu.

5. Pokud ne, aktivity odpovědí ke všemu, co je výše se zlými úmysly.

**Náprava**

Použití [Net ukončí nástroj](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) Posilte zabezpečení svého prostředí pro tento typ útoku.

## <a name="remote-execution-attempt-detected"></a>Zjištěn pokus o vzdálené spuštění

**Popis**

Útočníci, kteří ohrozit přihlašovacími údaji správce, nebo použijte před zneužitím nultého dne může na vašem řadiči domény spouštět vzdálené příkazy. Tímto lze pro získání trvalého shromažďují se informace, útoky na dostupnost služby (DOS) nebo jakéhokoli jiného důvodu. ATA detekuje PSexec a WMI vzdáleného připojení.

**Šetření**

1. To je běžné pro pracovní stanice pro správu také členové týmu IT a účty služeb, které provádět úlohy správy řadiče domény. Pokud je to tento případ, a výstrahu získá aktualizovat, protože je správce nebo počítač provádí úlohu, **potlačit** výstrahu.
2.  Je povolené vzdálené spuštění vůči vašemu řadiči domény v daném počítači?
  - Je dotyčného účtu povolené vzdálené spuštění vůči vašemu řadiči domény?
  - Pokud na obě otázky odpovíte Ano, pak **Zavřít** výstrahu.
3.  Pokud je odpověď na obě otázky Ne, tato aktivita by se měly zvažovat pravdivě pozitivní upozornění. Pokuste se najít zdrojový na pokus o kontrolou počítače a účtu profily. Klikněte na zdrojový počítač nebo účet, přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době těchto pokusů o přihlášení, hledání neobvyklých aktivit, jako například: kdo byl přihlášen, které prostředky tam, kde získat přístup.


**Náprava**

1. Zakažte vzdálený přístup k řadičům domény z počítačů, které nejsou ve vrstvě 0.

2. Implementace [privilegovaný přístup](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) povolit jen počítačům s posíleným zabezpečením pro připojení k řadiči domény pro správce.

## <a name="sensitive-account-credentials-exposed--services-exposing-account-credentials"></a>Vystaveny přihlašovací údaje k účtu a služby, které odhalují přihlašovací údaje k účtu

> [!NOTE]
> Toto podezřelé aktivity se přestala nabízet a zobrazí pouze v ATA verze starší než 1.9. Pro ATA 1.9 nebo novější, najdete v článku [sestavy](reports.md).

**Popis**

Některé služby posílají přihlašovací údaje účtu v prostém textu. To může nastat i pro citlivé účty. Útočníci monitorování síťového provozu můžete zachytit a pak znovu použít tyto přihlašovací údaje ke škodlivým účelům. Všechny textové heslo pro citlivých účtů aktivuje výstrahu, zatímco u tohoto počtu účtů, se aktivuje výstraha, pokud pět nebo více různých účtů z jednomu zdrojovému počítači odesílat hesla v nešifrovaném textu. 

**Šetření**

Klikněte na výstrahu, kterou chcete získat jeho stránku podrobností. Podívejte se, které účty byly vystaveny. Pokud existují mnoho takové účty, klikněte na **stáhnout podrobnosti o** pro zobrazení seznamu v Excelové tabulce.

Obvykle je skript nebo starší verze aplikace na zdrojových počítačích, který používá jednoduché vazby LDAP.

**Náprava**

Ověřte konfiguraci na zdrojových počítačích a zajistěte, aby nepoužívaly jednoduchou vazbu protokolu LDAP. Namísto použití jednoduché vazby protokolu LDAP můžete použít LDAP SALS nebo LDAPS.

## <a name="suspicious-authentication-failures"></a>Podezřelé chyby ověřování

**Popis**

V rámci útoku hrubou silou se útočník pokusí ověření pomocí mnoha různých hesel pro různé účty, dokud nebude nalezen správné heslo pro alespoň jeden účet. Jednou najde, útočník může přihlásit pomocí tohoto účtu.

Tato detekce se aktivuje upozornění, když došlo k mnoha chyb ověřování pomocí protokolu Kerberos nebo NTLM, napříč mnoha uživatelů; to může být buď vodorovně s menší skupinou hesel nebo svisle s velkým nastavte hesel pouze několik uživatelů. nebo libovolnou kombinaci těchto dvou možností. Minimální dobu, než může být výstraha je jeden týden.

**Šetření**

1.  Klikněte na tlačítko **stáhnout podrobnosti o** zobrazíte úplné informace v Excelové tabulce. Můžete získat následující informace: 
  - Seznam napadené účty
  - Seznam odhadnuté účty v které pokusů o přihlášení, bylo dokončeno s úspěšné ověření
  - Pokud byly provedeny pokusy o ověření, pomocí protokolu NTLM, zobrazí se příslušné události aktivit 
  - Pokud byly provedeny pokusy o ověření, pomocí protokolu Kerberos, zobrazí se příslušné síťové aktivity
2.  Klikněte na zdrojovém počítači přejděte na stránku jeho profil. Zkontrolujte, co se stalo v době těchto pokusů o přihlášení, hledání neobvyklých aktivit, jako například: kdo byl přihlášen, které prostředky tam, kde získat přístup. 
3.  Pokud se provádí ověřování pomocí protokolu NTLM a objeví se, že výstrahy v mnoha případech a není dostatek informací o serveru, který je na zdrojovém počítači se pokusili získat přístup, měli byste povolit **auditování protokolu NTLM** na součástí řadiče domény. K tomuto účelu zapněte události 8004. Toto je událost ověřování NTLM, která obsahuje informace o zdrojovém počítači, uživatelský účet a **server** , které na zdrojovém počítači se pokusili získat přístup. Až budete vědět, které server odeslal ověření ověřování, které byste měli prozkoumat serveru tak, že zkontrolujete jeho události, jako je 4624 pro lepší pochopení procesu ověřování. 


**Náprava**

[Složitá a dlouhá hesla](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) poskytují nezbytnou první úroveň zabezpečení před útoky hrubou silou.

## Podezřelé vytvoření služby <a name="suspicious-service-creation"></a>

**Popis**

Útočníci se pokusí spustit podezřelé služby ve vaší síti. Po vytvoření nové služby, který se zdá podezřelá na řadiči domény, ATA vydá výstrahu. Tato výstraha spoléhá na událost 7045 a je zjištěn z každého řadiče domény, který se bude vztahovat ATA Gateway a Lightweight Gateway.

**Šetření**

1. Pokud v daném počítači je k pracovní stanici správce, nebo počítače, na které členové týmu IT a služba účty provádět úlohy správy, může jít o falešně pozitivní upozornění a možná budete muset **potlačit** upozornění a přidejte ho do Seznam vyloučení v případě potřeby.

2. Je služba něco, co rozpoznat v tomto počítači?

 - Je **účet** dotyčný můžou nainstalovat tuto službu?

 - Pokud na obě otázky odpovíte *Ano*, pak **Zavřít** výstrahu nebo ho přidejte do seznamu vyloučení.

3. Pokud na obě otázky odpovíte *žádné*, a to by se měly zvažovat pravdivě pozitivní upozornění.

**Náprava**

- Implementace méně privilegovaným přístupem na doménu počítačů Povolit jenom konkrétní uživatelé práva k vytvoření nové služby.


## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Podezření na krádež identity na základě neobvyklého chování

**Popis**

ATA učí chování entit pro uživatele, počítače a zdroje, posuvného tří týdnů. Model chování je založen na následující činnosti: počítače entity přihlášení k, požadované entity zdroje získat přístup a doby konal úplně těchto operací. Služba ATA odesílá oznámení po odchylky od chování entit podle algoritmů strojového učení. 

**Šetření**

1. Dotyčný uživatel by měl být provádění těchto operací?

2. Vezměte v úvahu následující případů jako potenciální falešně pozitivní: uživatel, který vrátil z dovolené, IT pracovníky, kteří provádějí nadbytečné přístup jako součást svého provozu (třeba nárůst podpory oddělení technické podpory v daného dne nebo týdne), vzdálené desktopových aplikací. a pokud jste **Zavřít a vyloučit** upozornění, bude uživatel již být součástí detekce


**Náprava**

 Různé akce je třeba provést v závislosti na tom, co způsobilo tento neobvyklé chování na výskyt. Například pokud síť byla provedena, zdrojový počítač by měl být blokovaný síť (Pokud bude po schválení).

## <a name="unusual-protocol-implementation"></a>Neobvyklá implementace protokolu


**Popis**

Útočníci použít nástroje, které implementují různé protokoly (SMB, Kerberos, NTLM) nestandardním způsobem. Přestože tento typ síťového provozu je přijat ve Windows bez upozornění, ATA je schopen rozpoznat potenciální škodlivým činnostem. Chování je indikátorem techniky, jako je například over-pass-the-Hash, jakož i zneužití používané Upřesnit ransomwaru, jako je například WannaCry.

**Šetření**

Identifikujte na protokol, který neobvyklá – z časové osy podezřelých aktivit, klikněte na podezřelé aktivity a přístup ke stránce Podrobnosti; protokol se zobrazí nad šipku: protokolu Kerberos nebo NTLM.

- **Kerberos**: často aktivovat v případě, že hackerům nástroj, jako je nástroj Mimikatz potenciálně se používá k útoku Overpass-the-Hash. Zaškrtněte, pokud zdrojovém počítači běží aplikace, která implementuje vlastní zásobníku protokolu Kerberos, který není v souladu s RFC protokolu Kerberos. V takovém případě se jedná o neškodné pravdivě pozitivní upozornění a výstrahy může být **uzavřeno**. Pokud udržuje se výstraha a se stále o případ, můžete si **potlačit** výstrahu.

- **NTLM**: může být WannaCry nebo nástrojů, jako je Metasploit Medusa a Hydra.  

Pokud chcete zjistit, zda je aktivita o útok WannaCry, proveďte následující kroky:

1. Zkontrolujte, jestli zdrojovém počítači běží nástroj útoku například Metasploit, Medusa nebo Hydra.

2. Pokud se nenajdou žádné nástroje útoku, zkontrolujte, zda zdrojovém počítači běží aplikace, která implementuje vlastní zásobník protokolu NTLM nebo podepisování SMB.

3. Pokud ne, zkontrolujte, zda způsobené WannaCry spuštěním skriptu skener WannaCry, například [Tento skener](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner) proti účastnící se podezřelá aktivita zdrojového počítače. Pokud skener zjistí, že tento počítač jako nakažené nebo zranitelné, práce na opravy chyb počítač a odebrat malware a blokování ze sítě.

4. Pokud skript nenašli, že daný počítač hostuje nakažené nebo ohrožená a pak může pořád nakažené, ale SMBv1 můžou byly zakázané nebo na počítači, byla opravena, které by ovlivnily skenovací nástroj.

**Náprava**

Platí pro všechny počítače nejnovějších oprav a zkontrolovat, se použijí všechny aktualizace zabezpečení.

1. [Zakázat SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Odebrat WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3.  Data v ovládacím prvku ransom softwaru může někdy dešifrovat. Dešifrování je možné, pouze pokud si uživatel ještě restartovat nebo vypnout počítač. Další informace najdete v tématu [chcete pokřik Ransomwaru](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)


>[!NOTE]
> Pokud chcete zakázat upozornění na podezřelou aktivitu, obraťte se na podporu.

## <a name="related-videos"></a>Související videa
- [Připojení k zabezpečení komunitě](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Viz také
- [Playbook podezřelé aktivity ATA](http://aka.ms/ataplaybook)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)

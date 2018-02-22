---
title: "Průvodce podezřelou aktivitu Azure ATP | Microsoft Docs"
d|Description: This article provides a list of the suspicious activities Azure ATP can detect and steps for remediation.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ee8e45b6ef2da2d8866a1795bdab3987180acefe
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="azure-advanced-threat-protection-suspicious-activity-guide"></a>Průvodce podezřelou aktivitu Azure Advanced Threat Protection

Následující správné šetření můžou být klasifikované podezřelé aktivity, jako:

-   **Hodnota TRUE, kladnou**: škodlivou akci detekovaných službou Azure ATP.

-   **Neškodné true kladnou**: akce detekovaných službou Azure ATP skutečné, ale není škodlivý, jako je například průnikům testu.

-   **Falešně pozitivní**: znamená aktivity nebylo dojít alarmů hodnotu false.

Další informace o tom, jak pracovat s výstrahami Azure ATP najdete v tématu [práce s podezřelými aktivitami](working-with-suspicious-activities.md).


## <a name="abnormal-sensitive-group-modification"></a>Neobvyklá úprava citlivých skupin


**Popis**

Útočníci přidání uživatelů do vysoce privilegovaných skupin. Učiní tak k získání přístupu k více prostředkům a k získání persistency. Detekce spoléhá na profilace činnosti Změna skupiny uživatelů a výstrahy, když je vidět neobvyklé doplněk ke skupině citlivé. Profilace nepřetržitě provádí ATP. Minimální dobu, než může být výstraha je jeden měsíc na každém řadiči domény.

Definice citlivých skupin v Azure ATP, najdete v části [práce s citlivé účty](sensitive-accounts.md).


Detekce spoléhá na [události auditovat na řadičích domény](configure-event-collection.md).
Abyste měli jistotu, vaše doména je potřebné události auditu řadiče.

**Šetření**

1. Oprávněný úpravy skupiny? </br>Úpravy legitimní skupiny, které dochází zřídka a nebyly naučili jako "normální", může způsobit výstrahu, která lze považovat za neškodné skutečně pozitivní.

2. Pokud objekt přidaný uživatelský účet, zkontrolujte, které akce trvala uživatelský účet po přidávané ke skupině pro správu. Přejděte na stránku uživatele v Azure ATP získat další kontext. Byly existuje jakékoliv podezřelé aktivity, které jsou přidružené k účtu před nebo po přidání byla provedena? Stažení **citlivou skupinu úpravy** sestav zobrazit, jaké další úpravy byly učiněna a kým stejné časovém období.

**Nápravy**

Minimalizujte počet uživatelů, kteří mají oprávnění k úpravě citlivých skupin.

Nastavit [Privileged Access Management pro službu Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) Pokud jsou k dispozici.


## <a name="brute-force-attack-using-ldap-simple-bind"></a>Útoku hrubou silou použití jednoduché vazby protokolu LDAP

**Popis**

>[!NOTE]
> Hlavní rozdíl mezi **selhání podezřelé ověřování** a toto zjišťování je, že v této detekce Azure ATP můžete určit, zda různá hesla používán.

V rámci útoku hrubou silou útočník pokusí ověřování pomocí mnoho různých hesla pro různé účty, dokud nebude nalezen správné heslo pro alespoň jeden účet. Jednou najde, útočník může přihlásit pomocí tohoto účtu.

V této detekce výstrahy při Azure ATP zjistí masivní počet ověření jednoduchých vazeb. To může být buď *vodorovně* s malou sadu hesla mezi mnoha uživateli; nebo *svisle "* s velké sady hesla na několika uživatelů; nebo libovolnou kombinaci těchto dvou možností.

**Šetření**

1. Pokud existuje mnoho účtů související se situací, klikněte na tlačítko **stáhnout podrobnosti o** pro zobrazení seznamu v tabulce aplikace Excel.

2. Klikněte na výstrahu, kterou chcete přejít na stránku s jeho vyhrazené. Zkontrolujte, zda pokusy o žádné přihlášení bylo dokončeno s úspěšné ověření. Pokusy se zobrazí jako **uhádnout účty** na pravé straně infografice. Pokud ano, jsou některé z **uhádnout účty** běžně používaný ze zdrojového počítače? Pokud ano, **potlačit** podezřelou aktivitu.

3. Pokud neexistují žádné **uhádnout účty**, jsou některé z **napadení účty** běžně používaný ze zdrojového počítače? Pokud ano, **potlačit** podezřelou aktivitu.

**Nápravy**

[Komplexní a dlouhá hesla](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) poskytovat potřebné první úrovně zabezpečení před útoky hrubou silou.

## <a name="encryption-downgrade-activity"></a>Přechod na starší verzi aktivity šifrování

**Popis**

Přechod na starší verzi šifrování je metoda oslabení protokolu Kerberos podle Downgrade úrovně šifrování různých polí protokolu, které jsou obvykle šifrována pomocí nejvyšší úroveň šifrování. Oslabeným šifrované pole může být snazší cíl pokusů offline hrubou silou. Různé metody útoku využívat slabé šifrování doklad protokolu Kerberos. V této detekce Azure ATP zjišťuje typy šifrování pomocí protokolu Kerberos, počítačů a uživatelů a upozorní, že jste po slabší šifrováním použije: (1) neobvyklé pro zdrojový počítač nebo uživatele. a (2) odpovídá známé útoky techniky.

Existují tři typy detekce:

1.  Typu Skeleton Key – je malware, který běží na řadičích domény a povoluje ověřování k doméně pomocí libovolného účtu bez znalosti jeho heslo. Tímto malwarem často používá slabší algoritmy šifrování hodnoty hash hesla uživatele na řadiči domény. V této detekce metodu šifrování zprávy KRB_ERR z řadiče domény k účtu s žádostí o lístek snížit ve srovnání s dřív zjištěné chování.

2.  Lístek Golden – [zlatý lístek](#golden-ticket) výstrah, metodu šifrování pole lístku TGT zprávy TGS_REQ (žádost o službu) ze zdrojového počítače byl snížit ve srovnání s dřív zjištěné chování. Toto není založena na čas anomálií (stejně jako ostatní zlatý lístek detekce). Kromě toho se žádný požadavek ověřování protokolu Kerberos přidružené předchozí žádost o služby rozpozná ATP.

3.  Overpass-the-Hash – útočník může použít slabé odcizené hodnoty hash chcete-li vytvořit lístek silné s žádostí ověřovací služby protokolu Kerberos. V této detekce AS_REQ typ šifrování zprávy ze zdrojového počítače byl snížit ve srovnání s dřív zjištěné chování (to znamená, počítač se pomocí standardu AES).

**Šetření**

Nejprve zkontrolujte popis výstrahy, abyste zjistili, která výše tři typy detekce, že pracujete s.

1.  Typu Skeleton Key – můžete zkontrolovat, pokud typu Skeleton Key ovlivnil řadičů domény pomocí [skeneru zapsána tým Azure ATP](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73).
    Pokud skeneru najde malware v 1 nebo více řadičů domény, je skutečně pozitivní.

2.  Zlatý lístek – existují případy, ve kterých je vlastní aplikaci, která je používána zřídka, ověřování pomocí nižší úroveň šifrování. Zkontrolujte, zda jsou na zdrojovém počítači všechny vlastní aplikace. Pokud ano, je pravděpodobně neškodné skutečně pozitivní a lze potlačit.

3.  Overpass-the-Hash – existují případy, ve kterých může být tato výstraha aktivuje, když uživatelé nakonfigurovaní s čipovými kartami jsou požadovány pro interaktivní přihlášení a toto nastavení je zakázané a poté povoleny. Zkontrolujte, pokud byly související se situací změny takto pro účty. Pokud ano, to je pravděpodobně neškodné skutečně pozitivní a lze potlačit.

**Nápravy**

1.  Kostru klíče – odebere malware. Další informace najdete v tématu [Malware Analysis typu Skeleton Key](https://www.secureworks.com/research/skeleton-key-malware-analysis) podle SecureWorks.

2.  Zlatý lístek – postupujte podle pokynů [zlatý lístek](#golden-ticket) podezřelé aktivity.   
    Navíc vzhledem k tomu, že vytváření zlatý lístek vyžaduje oprávnění správce domény, implementovat [předat doporučení hash](http://aka.ms/PtH).

3.  Overpass-the-Hash – Pokud související se situací účet nerozlišuje malá písmena, pak resetovat heslo tohoto účtu. To brání útočník vytváření nové lístky protokolu Kerberos z hodnoty hash hesla, i když existujících lístků je můžete dále používat, dokud nevyprší jejich platnost. Pokud se jedná o citlivých účet, měli byste zvážit resetovat účet KRBTGT dvakrát jako podezřelou aktivitu zlatý lístek. Resetování KRBTGT dvakrát zruší platnost všech Kerberos lístků v této doméně, takže Plánujte než tak učiníte. Viz pokyny v [KRBTGT účtu heslo resetovat skripty nyní dostupné pro zákazníky](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Viz také pomocí [resetování hesla nebo klíče nástroj účet KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Protože se jedná o laterální pohyb techniku, držte se osvědčených postupů z [předat doporučení hash](http://aka.ms/PtH).

## Zlatý lístek<a name="golden-ticket"></a>

**Popis**

Útočníci s právy správce domény může ohrozit [účet KRBTGT](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). Pomocí účtu KRBTGT, můžete vytvořit lístku TGT, která poskytuje autorizace k jakémukoli prostředku a nastavit dobu platnosti lístku k kdykoli libovolný udělování lístek protokolu Kerberos. Tato falešných lístku TGT se označuje jako "Zlatý lístek" a útočníkům umožňuje, aby dosáhnout persistency v síti.

V této detekce výstrahy při lístek protokolu Kerberos udělování lístků se používá pro více než povoleném čase povolené zadané v [maximální doba života lístku uživatele](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx) zásady zabezpečení.

**Šetření**

1. Se někdo všechny poslední (během posledních několik hodin) změny provedené **maximální doba života lístku uživatele** nastavení v zásadách skupiny? Pokud ano, pak **Zavřít** výstrahy (byl falešně pozitivní).

2. Je samostatný senzoru Azure ATP účastnící se tato výstraha virtuálního počítače? Pokud ano, ji nedávno obnovit z uloženého stavu? Pokud ano, pak **Zavřít** této výstrahy.

3. Pokud je odpověď na výše uvedené otázky Ne, předpokládá, to se zlými úmysly.

**Nápravy**

Změňte heslo protokolu Kerberos lístku udělování lístků (KRBTGT) dvakrát podle pokynů v [KRBTGT účtu heslo resetovat skripty nyní dostupné pro zákazníky,](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/)pomocí [resetování hesla nebo klíče účtu KRBTGT Nástroj](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Resetování KRBTGT dvakrát zruší platnost všech Kerberos lístků v této doméně, takže Plánujte než tak učiníte. Navíc vzhledem k tomu, že vytváření zlatý lístek vyžaduje oprávnění správce domény, implementovat [předat doporučení hash](http://aka.ms/PtH).

## <a name="honeytoken-activity"></a>Aktivita Honeytokenu


**Popis**

Honeytokenu účty jsou účty vábničky nastavit tak, aby Vyhledávejte a sledujte podezřelé aktivity, které zahrnuje tyto účty. Účtů Honeytokenu by měl být ponecháno nevyužité, přitom má název atraktivní aby z útočníci (například SQL-správce). Všechny aktivity z nich může znamenat škodlivé chování.

Další informace o účtů honeytokenu najdete v tématu [nainstalovat ATP Azure - kroku 7](install-atp-step7.md).

**Šetření**

1.  Zkontrolujte, zda Vlastník zdrojového počítače použité k ověření, účtů Honeytokenu pomocí metody popsané na stránce podezřelé aktivity (například protokolu Kerberos, LDAP, protokol NTLM).

2.  Přejděte na stránky profilu počítačů zdroje a zkontrolujte, které účty, které ověření z nich. Pokud používají účtů Honeytokenu, obraťte se na vlastníci tyto účty.

3.  To může být neinteraktivní přihlášení, takže nezapomeňte zaškrtnout pro aplikace nebo skripty, které běží na zdrojovém počítači.

Pokud po provedení kroků 1 až 3, pokud nejsou důkazy neškodné použití, předpokládají, že to je škodlivý.

**Nápravy**

Ujistěte se, že Honeytokenu účtů se používají pouze pro jejich zamýšlený účel, jinak může vygenerovat velký počet výstrah.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Krádeži identity pomocí útoku Pass-the-Hash

**Popis**

Pass-the-Hash je laterální pohyb technika, ve kterém útočník získá hodnoty hash NTLM uživatele z jednoho počítače a použije ho k získání přístupu k jinému počítači. 

**Šetření**

Hodnota hash použila z počítače, cílový uživatel vlastní nebo pravidelně používá? Pokud ano, je to falešně pozitivní. Pokud ne, je pravděpodobně skutečně pozitivní.

**Nápravy**

1. Pokud není účet související se situací citlivé, poté resetujte heslo tohoto účtu. To brání útočník vytváření nové lístky protokolu Kerberos z hodnoty hash hesla, i když existujících lístků je můžete dále používat, dokud nevyprší jejich platnost. 

2. Pokud se jedná o citlivých účet, měli byste zvážit resetovat účet KRBTGT dvakrát jako podezřelou aktivitu zlatý lístek. Resetování KRBTGT dvakrát zruší platnost všech Kerberos lístků v této doméně, takže Plánujte než tak učiníte. Viz pokyny v [KRBTGT účtu heslo resetovat skripty nyní dostupné pro zákazníky,](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), také zjistit pomocí [resetování hesla nebo klíče nástroj účet KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Protože se jedná o laterální pohyb techniku, držte se osvědčených postupů z [předat doporučení hash](http://aka.ms/PtH).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Krádeži identity pomocí útoku Pass-the-Ticket

**Popis**

Pass-the-Ticket je laterální pohyb technika, ve kterém útočník získá lístek Kerberos z jednoho počítače a použije ho k získání přístupu k jinému počítači pomocí opakovaného použití odcizené lístku. V této detekce lístek protokolu Kerberos je seznámili použít v různých počítačích dva (nebo více).

**Šetření**

1. Klikněte **stáhnout podrobnosti o** tlačítko zobrazit úplný seznam IP adres související se situací. Ukládá IP adresu jednoho nebo obou počítače patřit do podsítě, které je přiděleno z fondu podměrečných DHCP, například VPN nebo Wi-Fi? Je IP adresa sdílená? Například tím, že zařízení NAT? Jsou jeden nebo více zdrojových IP adres, nebudou vyřešeny senzoru? (to může znamenat, že nejsou správně otevřené správné porty z senzoru do zařízení.) Pokud je odpověď na některý z těchto otázek Ano, je falešně pozitivní.

2. Je k dispozici vlastní aplikaci, která předá lístky jménem uživatelů? Pokud ano, je neškodné skutečně pozitivní.

**Nápravy**

1. Pokud není účet související se situací citlivé, poté resetujte heslo tohoto účtu. To brání útočník vytváření nové lístky protokolu Kerberos z hodnoty hash hesla, i když existujících lístků je můžete dále používat, dokud nevyprší jejich platnost.  

2. Pokud se jedná o citlivých účet, měli byste zvážit resetovat účet KRBTGT dvakrát jako podezřelou aktivitu zlatý lístek. Resetování KRBTGT dvakrát zruší platnost všech Kerberos lístků v této doméně, takže Plánujte než tak učiníte. Viz pokyny v [KRBTGT účtu heslo resetovat skripty nyní dostupné pro zákazníky,](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), také zjistit pomocí [resetování hesla nebo klíče nástroj účet KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Protože se jedná o laterální pohyb techniku, držte se osvědčených postupů v [předat doporučení hash](http://aka.ms/PtH).

## <a name="malicious-data-protection-private-information-request"></a>Škodlivá žádost o soukromé informace přes Data Protection

**Popis**

Data Protection API (DPAPI) se používá v systému Windows k ochraně bezpečně hesla uloží prostřednictvím prohlížeče, šifrované soubory a další citlivá data. Řadiče domény uložení zálohování hlavního klíče, který slouží k dešifrování všech tajných klíčů šifrován DPAPI na počítačích připojených k doméně systému Windows. Útočník může použít tento hlavní klíč k dešifrování všech tajných klíčů chráněných pomocí rozhraní DPAPI na všech počítačích připojených k doméně.
V této detekce výstrahy při rozhraní DPAPI se používá k načtení zálohování hlavního klíče.

**Šetření**

1. Je zdrojový počítač s, organizaci schválené rozšířený kontrolu zabezpečení pro službu Active Directory?

2. Pokud ano a ho by měl vždycky být tak, **zavřete a vyloučení** podezřelou aktivitu.

3. Pokud ano a je to neměli dělat, **Zavřít** podezřelou aktivitu.

**Nápravy**

Pokud chcete používat rozhraní DPAPI, musí útočník oprávnění správce domény. Implementace [předat doporučení hash](http://aka.ms/PtH).

## <a name="malicious-replication-requests"></a>Požadavky na škodlivou replikaci


**Popis**

Replikace služby Active Directory je proces, podle kterého jsou synchronizovány změny provedené na jeden řadič domény s jinými řadiči domény. Zadané potřebná oprávnění, útočníci můžete spustit požadavek na replikaci, což jim umožní načíst dat uložená ve službě Active Directory, včetně hodnot hash hesel.

V této detekce výstrahy při inicializuje požadavek na replikaci z počítače, který není řadičem domény.

**Šetření**

1. Je počítač v otázku řadiče domény? Například nově propagovaných řadiče domény, který měl potíže s replikací. Pokud ano, **zavřete a vyloučení** podezřelou aktivitu.  

2. Na dotyčném počítači by měl být replikaci dat ze služby Active Directory? Například Azure AD Connect. Pokud ano, **zavřete a vyloučení** podezřelou aktivitu.

**Nápravy**

Ověřte následující oprávnění: 

- Replikovat změny adresáře   

- Replikovat všechny změny adresáře  

Další informace najdete v tématu [oprávnění Grant Active Directory Domain Services pro profil synchronizace SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).
Můžete využít [AD seznamu ACL skener](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit skript prostředí Windows PowerShell k určení, kdo v doméně, má tato oprávnění.


## <a name="privilege-escalation-using-forged-authorization-data"></a>Pomocí zvýšení oprávnění forged data autorizace

**Popis**

Známé chyby zabezpečení v systému Windows Server starší verze útočníkovi umožnit, aby manipulaci privilegovaný PAC (Attribute Certificate), pole v lístku protokolu Kerberos, obsahující data autorizace uživatele (ve službě Active Directory je to členství ve skupině), udělení Útočníci další oprávnění.

**Šetření**

1. Klikněte na výstrahu zobrazíte stránku s jeho podrobnosti.

2. Je cílový počítač (v části **ACCESSED** sloupec) opravit s MS14-068 (řadič domény) nebo MS11-013 (server)? Pokud ano, **Zavřít** podezřelé aktivity (je falešně pozitivní).

3. Pokud ne, zdrojový počítač spouští (v části **FROM** sloupec) označuje změnit certifikát PAC operačního systému nebo aplikace? Pokud ano, **potlačit** podezřelé aktivity (je neškodné skutečně pozitivní).

4. Pokud odpověď byla již na výše uvedené dvě otázky, předpokládá to se zlými úmysly.

**Nápravy**

Zajistěte, aby na všech řadičích domény s operačním systémem až do verze Windows Server 2012 R2 byla nainstalovaná aktualizace [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) a na všech členských serverech a řadičích domény až do verze 2012 R2 byla nainstalovaná aktualizace KB2496930. Další informace najdete v článku [Stříbrný certifikát PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) a [Zfalšovaný certifikát PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-account-enumeration"></a>Rekognoskace pomocí výčtu účtů

**Popis**

V účtu výčtu rekognoskace útočník používá slovník s tisíci uživatelská jména nebo nástroje, jako je KrbGuess tak snadno uhodnout uživatelských jmen ve vaší doméně. Útočník díky požadavky protokolu Kerberos pomocí tyto názvy, abyste mohli zkusit najít platné uživatelské jméno ve vaší doméně. Pokud odhad úspěšně Určuje uživatelské jméno, útočník získá chyby protokolu Kerberos **požadované předběžné ověření** místo **neznámý objekt zabezpečení**. 

V této detekce Azure ATP může zjistit, odkud pochází útoku, celkový počet pokusů o odhad a kolik byly porovnány. Pokud jsou příliš mnoho uživatelů neznámé, Azure ATP ho detekuje jako podezřelou aktivitu. 

**Šetření**

1. Klikněte na výstrahu zobrazíte stránku s jeho podrobnosti. 

2. Má tento počítač hostitele dotaz na řadič domény, jestli neexistují účty (například servery Exchange Server)? <br></br>
Je skript nebo aplikace běžící na hostiteli, který může generovat toto chování? <br></br>
Pokud ano, je odpověď na jednu z těchto otázek **Zavřít** podezřelé aktivity (je neškodné skutečně pozitivní) a vyloučení, který hostitelem z podezřelé aktivity.

3. Stáhněte si podrobnosti výstrahy v tabulce aplikace Excel pohodlně zobrazíte seznam pokusy o účet, rozdělené do stávající a neexistující účty. Pokud se podíváte na jiný existující účty list v tabulce a účty vypadat povědomě, mohou být zakázané účty nebo zaměstnancům, kteří ve společnosti. V takovém případě nepravděpodobné, že pokus pochází ze slovníku. S největší pravděpodobností je aplikace nebo skript, který je zjišťujeme, které účty jsou stále existují ve službě Active Directory, což znamená, že se jedná o neškodný skutečně pozitivní.

3. Pokud jsou názvy z velké části obeznámeni, se všechny pokusy o odhad odpovídat existující názvy účtů ve službě Active Directory? Pokud nejsou nalezeny žádné shody, pokus byl zbytečné, ale měli byste věnovat pozornost výstrahy zda získá aktualizovány v čase.

4. Pokud žádné z odhad pokusů o odpovídající existující názvy účtů, útočník ví o existenci účty ve vašem prostředí a pokuste se použít pro přístup k vaší doméně pomocí zjištěných uživatelská jména hrubou silou. Zkontrolujte názvy odhadované účtů pro další podezřelé aktivity. Zkontrolujte, jestli všechny odpovídající účty jsou citlivé účty.


**Nápravy**

[Komplexní a dlouhá hesla](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) poskytovat potřebné první úrovně zabezpečení před útoky hrubou silou.


## <a name="reconnaissance-using-directory-services-queries"></a>Rekognoskace pomocí dotazů na adresářové služby

**Popis**

Adresář služby rekognoskace je používaných útočníky k namapování strukturu adresáře a cíle privilegovaných účtů pro pozdější kroky v útoku. Protokol vzdáleného správce zabezpečení účtů (SAM-R) je jedním z metody použité k dotazování adresáře k provedení takových mapování.

V této detekce by být žádné výstrahy aktivovány v první měsíc po nasazení Azure ATP. Při učení doby Azure ATP profily které dotazy SAM-R jsou vytvářeny ze kterých počítačů výčet a jednotlivé dotazy citlivé účty.

**Šetření**

1. Klikněte na výstrahu zobrazíte stránku s jeho podrobnosti. Zkontrolujte, které dotazy nebyly provedeny (pro příklad, Enterprise admins nebo správce) a jestli byli úspěšní.

2. Je takové dotazy mají být provedeny ze zdrojového počítače dotyčném?

3. Pokud ano a výstrahu získá aktualizovány, **potlačit** podezřelou aktivitu.

4. Pokud ano a je to dělat neměli už **Zavřít** podezřelou aktivitu.

5. Pokud obsahuje informace související se situací účtu: je takové dotazy mají být provedené tento účet nebo nemá tento účet normálně přihlásit ke zdrojovému počítači?

 - Pokud ano a výstrahu získá aktualizovány, **potlačit** podezřelou aktivitu.

 - Pokud ano a je to dělat neměli už **Zavřít** podezřelou aktivitu.

 - Pokud odpověď byla ne ke všem z výše uvedených, předpokládá se, toto je škodlivý.

6. Pokud nejsou žádné informace o účtu, který byl zahrnut, můžete přejít do koncového bodu a zkontrolovat, který účet byl přihlášen v době výstrahy.

**Nápravy**

Posílení zabezpečení vaše prostředí před Tato technika provedením následujících kroků:
1. Je počítač se službou ohrožení zabezpečení skenovacího nástroje?  
2. Zjistěte, jestli konkrétní dotazované uživatele a skupiny v útoku jsou účty privilegované nebo vysokou hodnotu (tj, CEO, ředitel, správu IT atd.).  Pokud ano, podívejte se na další aktivitu v koncovém bodě také a monitorovat počítače, které jsou předmětem dotazu účty se protokolují do, jako jsou pravděpodobně cíle pro laterální pohyb.

## <a name="reconnaissance-using-dns"></a>Rekognoskace pomocí DNS

**Popis**

DNS server obsahuje mapu všechny počítače, IP adresy a služby ve vaší síti. Tyto údaje používají útočníci ke zmapování struktury vaší sítě a zacílení zajímavých počítačů v pozdějších krocích útoku.

Protokol DNS obsahuje několik typů dotazů. Azure ATP zjistí AXFR (přenos) žádosti pocházející z jiných servery.

**Šetření**

1. Je zdrojový počítač (**pocházející z...** ) DNS server? Pokud ano, pak je to pravděpodobně falešně pozitivní. K ověření, klikněte na výstrahu zobrazíte stránku s jeho podrobnosti. V tabulce v části **dotazu**, zkontrolujte, které domény dotaz se poslal. Jsou tyto existující domény? Pokud ano, pak **Zavřít** podezřelé aktivity (je falešně pozitivní). Kromě toho zkontrolujte, zda je otevřený mezi senzor samostatné Azure ATP a zdrojový počítač, aby se zabránilo budoucí falešně pozitivních UDP port 53.

2. Zdrojový počítač je spuštěný kontrolu zabezpečení? Pokud ano, **vyloučit entity** v ATP, buď přímo pomocí **zavřete a vyloučení** nebo prostřednictvím **vyloučení** stránky (v části **konfigurace** – dostupné pro admins Azure ATP.)

3. Pokud odpověď na všechny předchozí otázky se předpokládá Ne, to se zlými úmysly.

**Nápravy**

Interní server DNS lze proti rekognoskaci pomocí DNS zabezpečit zakázáním nebo omezením přenosů zóny jen na konkrétní IP adresy. Další informace o omezení přenosy zóny, najdete v části [omezit přenosy zóny](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
Úprava přenosy zóny je jeden úkol mezi kontrolní seznam, který by měl být řešit pro [zabezpečení vaše servery DNS před útoky interních i externích](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).

## <a name="reconnaissance-using-smb-session-enumeration"></a>Rekognoskace pomocí výčtu relací SMB


**Popis**

Výčet serveru Message Block (SMB) umožňuje útočníkům získat informace, kde uživatelé nedávno přihlášení. Jakmile útočník tyto informace, se můžete následně k laterálnímu pohybu v síti přístup k citlivé určitého účtu.

V této detekce výstrahy při provádění výčet relací SMB vůči řadiči domény, protože to nemělo stát.

**Šetření**

1. Klikněte na výstrahu zobrazíte stránku s jeho podrobnosti. Zkontrolujte, který účet se provést operaci a účty, které byly vystaveny, pokud existuje.

 - Je nějaký druh kontrolu zabezpečení systémem zdrojového počítače? Pokud ano, **zavřete a vyloučení** podezřelou aktivitu.

2. Zkontrolujte, které hrající roli uživatele nebo s provést operaci. Za normálních okolností protokolují do zdrojového počítače nebo budou správci, kteří měli provádět tyto akce?  

3. Pokud ano a výstrahu získá aktualizovány, **potlačit** podezřelou aktivitu.  

4. Pokud ano a je to dělat neměli už **Zavřít** podezřelou aktivitu.

5. Pokud odpověď na všechny výše uvedené je Ne, předpokládají, že to je škodlivý.

**Nápravy**

Použití [Net Ustanou nástroj](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) k posílení zabezpečení vaše prostředí před tento útok.

## <a name="remote-execution-attempt-detected"></a>Pokus o vzdálené spuštění zjistil

**Popis**

Útočníci, kteří ohrozit přihlašovací údaje správce, nebo použijte zneužití den nasazení můžete spustit vzdálené příkazy na vašem řadiči domény. Toho mohou využít k trvalému průniku do sítě, shromažďování informací, útokům DoS (Denial of Service) nebo z jakéhokoli jiného důvodu. Azure ATP zjistí nástroje PSexec a rozhraní WMI pro vzdálená připojení.

**Šetření**

1. To je běžné pro pracovních stanic pro správu a členové týmu IT a účty služby, které provádět úlohy správy řadičem domény. Pokud se jedná o tento případ a výstrahu získá aktualizovány od stejné správce nebo počítače provádění úkolů, pak **potlačit** výstrahy.

2. Je **počítače** dotyčném oprávnění k provedení této vzdálené spuštění na vašem řadiči domény?

 - Je **účet** dotyčném oprávnění k provedení této vzdálené spuštění na vašem řadiči domény?

 - Pokud je odpověď na obě otázky *Ano*, pak **Zavřít** výstrahy.

3. Pokud je odpověď na obě otázky *žádné*, a to by se měly zvažovat skutečně pozitivní.

**Nápravy**

1. Zakažte vzdálený přístup k řadičům domény z počítačů, které nejsou ve vrstvě 0.

2. Implementace [privilegovaný přístup](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) povolit pouze posílené počítače pro připojení k řadiči domény pro správce.

## <a name="suspicious-authentication-failures"></a>Selhání podezřelé ověřování

**Popis**

V rámci útoku hrubou silou útočník pokusí ověřování pomocí mnoho různých hesla pro různé účty, dokud nebude nalezen správné heslo pro alespoň jeden účet. Jednou najde, útočník může přihlásit pomocí tohoto účtu.

Toto zjišťování výstraha se spustí, když došlo k mnoha selhání ověřování pomocí protokolu Kerberos nebo NTLM, může se jednat buď vodorovně s malou sadu hesla mezi mnoha uživateli; nebo svisle s velkým sady hesel ve pouze několik uživatelů; nebo libovolnou kombinaci těchto dvou možností. Minimální dobu, než může být výstraha je jeden týden.

**Šetření**

1. Pokud existuje mnoho účtů související se situací, klikněte na tlačítko **stáhnout podrobnosti o** pro zobrazení seznamu v tabulce aplikace Excel.

2. Klikněte na výstrahu, kterou chcete přejít na stránku s jeho podrobnosti. Kontrola Pokud pokusy o žádné přihlášení bylo dokončeno s úspěšné ověřování, ty by se zobrazí jako **uhádnout účty** na pravé straně infografice. Pokud ano, jsou některé z **uhádnout účty** běžně používaný ze zdrojového počítače? Pokud ano, **potlačit** podezřelou aktivitu.

3. Pokud neexistují žádné **uhádnout účty**, jsou některé z **napadení účty** běžně používaný ze zdrojového počítače? Pokud ano, **potlačit** podezřelou aktivitu.

**Nápravy**

[Komplexní a dlouhá hesla](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) poskytovat potřebné první úrovně zabezpečení před útoky hrubou silou.

## <a name="suspicious-service-creation---preview-feature"></a>Vytvoření podezřelé služby – funkce ve verzi Preview!

**Popis**

Podezřelé služby byl vytvořen na řadič domény ve vaší organizaci. Tato výstraha spoléhá na události 7045 za účelem zjištění tohoto podezřelých aktivit na koncové body. Událost 7045 předáte z koncových bodů ATP nakonfigurováním [předávání událostí systému Windows](configure-event-forwarding.md) nebo předávání do systému SIEM 7045 a [konfiguraci vašeho systému SIEM](configure-event-collection.md) jako zdroj dat, který předává události k ATP.

**Šetření**

1. Pokud je počítač v pracovní stanici správce nebo počítač, na které členové týmu IT a služby účty provádět úlohy správy, může to být falešně pozitivní a budete muset **potlačit** výstrahy a přidejte ho do Seznam vyloučení v případě potřeby.

2. Je služba něco, co rozpoznat v tomto počítači?

 - Je **účet** dotyčném dovoleno instalovat tuto službu?

 - Pokud je odpověď na obě otázky *Ano*, pak **Zavřít** výstrahy, nebo ho přidat do seznamu vyloučení.

3. Pokud je odpověď na obě otázky *žádné*, a to by se měly zvažovat skutečně pozitivní.

**Nápravy**

- Implementovat méně privilegovaný přístup v doméně počítače, které chcete povolit jenom konkrétní uživatelé práva k vytvoření nové služby.

## <a name="unusual-protocol-implementation"></a>Neobvyklá implementace protokolu


**Popis**

Útočníci pomocí nástrojů, které implementují různých protokolů (protokol SMB, protokolu Kerberos, NTLM) nestandardní způsoby. Když tento typ síťového provozu je přijat Windows bez upozornění, Azure ATP je rozpoznat potenciální zlými úmysly. Toto chování je určující pro techniky, jako je například přesahu-Pass-the-Hash a hrubou silou, jakož i zneužití používané pokročilé ransomware, například WannaCry.

**Šetření**

Identifikovat protokol, který neobvyklé – z časové ose podezřelé aktivity, klikněte na podezřelou aktivitu, abyste se dostali na stránku s jeho podrobnosti; protokol se zobrazí nad šipku: protokolu Kerberos nebo NTLM.

- **Protokol Kerberos**: to se často spustí Pokud hackerům nástroje, jako byl použit Mimikatz, potenciálně provedení útoku Overpass-the-Hash. Zkontrolujte, zda zdrojový počítač je spuštěna aplikace, která implementuje vlastní zásobník protokolu Kerberos, není v souladu s RFC protokolu Kerberos. Pokud je to tento případ, je neškodné skutečně pozitivní a můžete **Zavřít** výstrahy. Pokud zachová se výstraha a stále je případ, můžete **potlačit** výstrahy.

- **NTLM**: může být WannaCry nebo nástroje, jako je Metasploit, Medusa a Hydra.  

Pokud chcete zjistit, jestli se jedná o útoku WannaCry, proveďte následující kroky:

1. Zkontrolujte, zda zdrojový počítač je spuštěn nástroj na útok například Metasploit, Medusa nebo Hydra.

2. Pokud se nenajdou žádné nástroje útoku, zkontrolujte, zda zdrojový počítač je spuštěna aplikace, která implementuje vlastní zásobník protokolu NTLM nebo protokolu SMB.

3. Pokud ne, zkontrolujte, pokud je to způsobeno WannaCry spuštěním skriptu WannaCry skener, například [Tento skener](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner) proti zahrnutých v podezřelé aktivity zdrojového počítače. Pokud skeneru zjistí, že tento počítač jako nakažené nebo snadno napadnutelný, pracovních na opravy na počítač a odebrání malware a blokování ze sítě.

4. Pokud skript nebyl nalezen, že je počítač nakažené nebo snadno napadnutelný, pak může pořád nakažené, ale SMBv1 mohla být zakázána nebo tento počítač má zúčastněné, které by došlo k ovlivnění nástroj vyhledávání.

**Nápravy**

Oprava všechny počítače, zejména použití aktualizací zabezpečení.

1. [Zakázat SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Odebrat WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3. WanaKiwi mohly dešifrovat data do nesprávných rukou některé ransom softwaru, ale pouze, pokud uživatel restartovat nebo vypnout počítač. Další informace najdete v tématu [pokřik Ransomware, který chcete](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)


>! [POZNÁMKA] Chcete-li zakázat podezřelou aktivitu, kontaktujte podporu.


## <a name="see-also"></a>Viz také
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)

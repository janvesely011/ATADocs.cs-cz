---
title: Kurz služby Azure ATP Rekognoskace playbook | Dokumentace Microsoftu
description: Kurz playbook Rekognoskace ochrany ATP v programu Azure popisuje, jak simulovat Rekognoskace hrozeb pro zjišťování pomocí služby Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: mlottner
ms.author: mlottner
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: f96bfadf10acac015ca1ad5315aa7ef7759075d2
ms.sourcegitcommit: 4711f0ff4331e0bcc84663f46054216b7db9f98e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/28/2019
ms.locfileid: "56989087"
---
# <a name="tutorial-reconnaissance-playbook"></a>Kurz: Rekognoskace playbook

Druhé části kurzu této série čtyř částí pro výstrahy zabezpečení služby Azure ATP se playbook rekognoskace. Účelem ochrany ATP v programu Azure testovacího prostředí výstrahy zabezpečení je pro ilustraci **ochrany ATP v programu Azure**možnosti v identifikace a detekce podezřelých aktivit a potenciální útoky na vaší síti. Playbook vysvětluje, jak testujeme funkčnost ve některé služby Azure ATP *diskrétní* detekce a zaměřuje se na služby Azure ATP *podpis*– na základě funkcí. Playbook neobsahuje výstrahy nebo detekcí podle rozšířené strojové učení nebo uživatele/entity na základě behaviorální způsoby detekce, potřebují období učení s skutečné síťový provoz po dobu až 30 dnů. Další informace o jednotlivých kurzu této série najdete v článku [přehled výstrah laboratoře zabezpečení ochrany ATP v programu](atp-playbook-lab-overview.md).

Playbook ukazuje detekce hrozeb a výstrahy zabezpečení služby ochrany ATP v programu Azure pro simulované útoků z běžné každodenní praxe, veřejně dostupné nástroje hackerů a útoku.

V tomto kurzu provedete následující:
> [!div class="checklist"]
> * Simulovat sondování mapování sítě
> * Simulovat rekognoskace adresářové služby
> * Simulace uživatelů a rekognoskace IP adresa (SMB)
> * Zkontrolujte výstrahy zabezpečení ze simulovaného rekognoskace v Azure ATP

## <a name="prerequisites"></a>Požadavky

[Dokončení ochrany ATP v programu zabezpečení oznámení testovacího prostředí](atp-playbook-setup-lab.md)
  - Co možná nejvíce doporučujeme postupujte podle pokynů pro nastavení testovacího prostředí. Čím blíž testovacího prostředí je nastavení navrhované testovacího prostředí, tím snazší bude dodržovat testovacích postupů ochrany ATP v Azure.

## <a name="simulate-a-reconnaissance-attack"></a>Simulace útoku Rekognoskace

Jakmile útočník získá přítomnost ve vašem prostředí, začíná jejich kampaň rekognoskace. V této fázi útočník bude obvykle stráví, zkoumání. Se pokusí zjistit počítače, které vás zajímají, vytvořit výčet uživatelů a skupin, shromažďovat důležité IP adresy a mapování prostředků vaší organizace a slabá místa. Aktivity rekognoskace umožnit, aby Seznamte se podrobně a dokončete mapování prostředí pro pozdější použití.

Rekognoskace útoku testovací metody:

* Rekognoskace mapování sítě
* Rekognoskace služby adresáře
* Rekognoskace uživatele a IP adresa (SMB)

## <a name="network-mapping-reconnaissance-dns"></a>Rekognoskace mapování sítě (DNS)

Jeden z prvních věcí, které se útočník pokusí je pokusit se získat kopii všech informací DNS. V případě úspěchu, že útočník získá rozsáhlé informace o vašem prostředí, která potenciálně zahrnuje podobné informace o vašich prostředí nebo sítí.

### <a name="run-nslookup-from-victimpc"></a>Spusťte nslookup z VictimPC

K otestování rekognoskace DNS, použijeme nástroj příkazového řádku nativních *nslookup*, k zahájení přenosu zóny DNS. Servery DNS se správnou konfigurací odmítne dotazy tohoto typu a neumožní pokusit o přenos zóny.  

Přihlaste se do **VictimPC**, pomocí zneužití přihlašovacích údajů JeffL. Spusťte následující příkaz:

``` cmd
nslookup
```

Typ **server** pak plně kvalifikovaný název domény nebo IP adresu řadiče domény, ve kterém jsou nainstalované senzory ochrany ATP v programu.

```nslookup
server contosodc.contoso.azure
```

Pojďme si vyzkoušet přenést domény.

```nslookup
ls -d contoso.azure
```

- Měli byste nahradit contosodc.contoso.azure a contoso.azure plně kvalifikovaný název domény vaší služby Azure ATP ze senzorů a název domény v uvedeném pořadí.

 ![Pokus o příkaz nslookup pro výpis DNS server – chyba](media/playbook-recon-nslookup.png)

Pokud **ContsoDC** je vaší první nasazený senzor, počkejte 15 minut, aby databáze back-end pro dokončení nasazení nezbytné mikroslužeb.

### <a name="network-mapping-reconnaissance-dns-detected-in-azure-atp"></a>Mapování sítě rekognoskace (DNS) v Azure ATP

Viditelnost tohoto typu pokus (neúspěšné nebo úspěšné) je důležitá pro doménovou ochranu před internetovými útoky. Protože se právě nainstalovaná prostředí, nám budete muset přejít na časové ose logické aktivity můžete vidět aktivitu. 

Ve službě Azure Search ochrany ATP v programu, zadejte **VictimPC**, pak klikněte na něj a zobrazit časovou osu.

![Rekognoskace DNS detekoval AATP vyšší úroveň zobrazení](media/playbook-recon-nslookupdetection1.png)

Vyhledejte "Dotaz AXFR" aktivity. Ochrana ATP v programu Azure zjistí tento druh rekognoskace proti serveru DNS. 
  - Pokud máte velké množství aktivit, klikněte na tlačítko **filtrovat podle** a zrušte zaškrtnutí všech typů s výjimkou "Dotaz DNS".

![Podrobné zobrazení detekce rekognoskace DNS v AATP](media/playbook-recon-nslookupdetection2.png)

Pokud bezpečnostní analytik určit tuto aktivitu pocházející z kontrolu zabezpečení, můžete z další výstrahy detekce vyloučit konkrétní zařízení. V pravé horní části oblasti výstrahy klikněte na tři tečky. Vyberte **zavřít a vyloučit MySecurityScanner**. Zajištění toto upozornění nezobrazí akci při zjištění z "MySecurityScanner".

Rozpoznání nezdařených útoků může být například přehledné jako rozpoznání úspěšných útoků proti prostředí. Na portálu ochrany ATP v programu Azure umožňuje přesnou výsledek akce, které provádí možné útočník. V našich simulované DNS reconnaissance útoku scénáře můžeme funguje jako útočníci, jste zastavili z výpis záznamů DNS domény. Váš tým SecOps dozvěděla o našich pokusu o útok a které jsme použili v našich pokus o z dané výstraze zabezpečení služby Azure ATP počítače.

## <a name="directory-service-reconnaissance"></a>Rekognoskace služby adresáře

Funguje jako útočník, dalším cílem rekognoskace je pokus o vytvoření výčtu všech uživatelů a skupin v doménové struktuře. Ochrana ATP v programu Azure potlačí aktivita výčtu adresářové služby z časové osy podezřelých aktivit learning 30denního období je dokončen. V období učení ochrany ATP v programu Azure učí, co je běžné a neobvyklé pro vaši síť. Po uplynutí 30denní learning neobvyklé události výčet adresářová služba vyvolat výstrahu zabezpečení. Během období učení 30denní uvidíte ochrany ATP v programu Azure detekce těchto aktivit pomocí časové osy aktivity entity v síti. Detekce služby Azure ATP tyto aktivity jsou uvedeny v tomto testovacím prostředí.

Abychom si předvedli běžnou metodu rekognoskace adresářové služby, použijeme nativní binární soubor Microsoft *net*. Po našem pokus o zkoumání časové osy aktivity JeffL, naše ohrožených uživatelů, se zobrazí detekování této aktivity služby Azure ATP.

### <a name="directory-service-enumeration-via-net-from-victimpc"></a>Vytváření výčtu adresářových služeb prostřednictvím *net* z VictimPC

Všechny ověřené uživatele nebo počítače mohou potenciálně výčet další uživatelé a skupiny v doméně. Tato schopnost výčet se vyžaduje pro většinu aplikací fungovat správně. Ohrožení uživatelských JeffL, je účet bez oprávnění umožňovala zvlášť domény. V simulované útoku, uvidíme právě jak i bez oprávnění umožňovala zvlášť doménový účet může stále poskytovat cenné datových bodů útočníkovi.

1. Z **VictimPC**, spusťte následující příkaz:

    ``` cmd
    net user /domain
    ```

   Výstup zobrazuje všechny uživatele v doméně Contoso.Azure.

   ![Vytvoření výčtu všech uživatelů v doméně](media/playbook-recon-dsenumeration-netusers.png)

2. Zkusme vytvořit výčet všech skupin v doméně. Spusťte následující příkaz:

    ``` cmd
    net group /domain
    ```

   Výstup zobrazuje všechny skupiny v doméně Contoso.Azure. Všimněte si, že jednu skupinu zabezpečení, který není výchozí skupiny: **HelpDesk**.

   ![Vytvořit výčet všech skupin v doméně](media/playbook-recon-dsenumeration-netgroups.png)

3. Teď vyzkoušíme chcete získat výčet jenom skupiny Domain Admins. Spusťte následující příkaz:

    ``` cmd
    net group "Domain Admins" /domain
    ```

   ![Zobrazení výčtu všichni členové skupiny Domain Admins](media/playbook-recon-dsenumeration-netdomainadmins.png)

    Funguje jako útočník, naučili jsme se, že nejsou dva členy skupiny Domain Admins: **SamiraA** a **ContosoAdmin** (předdefinovaného účtu Administrator pro řadič domény). Vědomím, že neexistuje žádná hranice zabezpečení mezi naše domény a doménové struktury, je pokusit se výčet Enterprise Admins i náš Další.

4. Pokus o zobrazení výčtu Enterprise Admins, spusťte následující příkaz:

    ``` cmd
   net group "Enterprise Admins" /domain
   ```

   Jsme zjistili, že existuje pouze jeden správce podniku, ContosoAdmin. Tyto informace nebyl důležité, protože již věděl, že není k dispozici hranice zabezpečení mezi naše domény a doménové struktury.

   ![Enterprise Admins v doméně ve výčtu](media/playbook-recon-dsenumeration-netenterpriseadmins.png)

Informace shromážděné v našich rekognoskace víme o skupině zabezpečení Helpdesk. I když tyto informace není zajímavé *ještě*. Taky víme, že **SamiraA** je členem skupiny Domain Admins. Pokud nám můžete získat od SamiraA přihlašovacích údajů, jsme získat přístup samotný řadič domény.

### <a name="directory-service-enumeration-detected-in-azure-atp"></a>Vytváření výčtu adresářových služeb v Azure ATP

Pokud naše laboratorní *reálné živé aktivity po dobu 30 dnů pomocí služby Azure ATP nainstalované*, právě předvedl, jak JeffL by potenciálně klasifikovat jako neobvyklé aktivity. Neobvyklá aktivita by se objevoval na časové ose podezřelé aktivity. Ale protože právě nainstalovaná prostředí, jsme budete muset přejít na časové ose logické aktivity.

Ve službě Azure Search ochrany ATP v programu Podívejme se časové osy pro JeffL logické aktivity, která bude vypadat jako:

![Vyhledat logické aktivity časovou osu pro konkrétní entitu](media/playbook-recon-dsenumeration-searchlogicalactivity.png)

Můžeme vidět při JeffL podepsané na VictimPC, pomocí protokolu Kerberos. Kromě toho vidíme, že JeffL z VictimPC, vytvořil výčet všech uživatelů v doméně.

![Časové osy pro JeffL logické aktivity](media/playbook-recon-dsenumeration-jeffvlogicalactivity.png)

Řada aktivit jsou protokolovány v časové osy logické aktivity díky tomu je to hlavní schopnost provádění digitálních forenzních a odpověď Incident (DFIR). Můžete dokonce vidět aktivity při počátečním zjišťování nebyl z ochrany ATP v programu Azure, ale z ochrany ATP v programu Windows Defender, Office 365 a dalších.

A podívejte se na **ContosoDC na stránce**, můžeme také vidět počítače JeffL přihlášení.

![Počítače s přihlášením JeffL](media/playbook-recon-dsenumeration-jeffvloggedin.png)

Také jsme můžete získání dat z adresáře, včetně členství ve skupinách a řízení přístupu na JeffL vše z v rámci ochrany ATP v programu Azure.

![Společnosti JeffL datům adresáře v AATP](media/playbook-recon-dsenumeration-jeffvdirectorydata.png)

Nyní bude naši pozornost Posun směrem k výčet relací SMB.

## <a name="user-and-ip-address-reconnaissance-smb"></a>Rekognoskace uživatele a IP adresa (SMB)

Složka sysvol služby Active Directory je jedním z prvku, pokud není *a* nejdůležitější sdílené síťové složce v prostředí. Všechny počítače a uživatele, musí mít pro přístup k této sdílené složce konkrétního síťového stáhnout zásady skupiny. Útočník může získat goldmine informací od výčet, který má aktivní relace ve složce sysvol.

Naším dalším krokem je výčet relací SMB proti ContosoDC prostředku. Chceme, aby se dozvíte, kdo jiný používá relace s sdílené složce protokolu SMB a *z jaké IP adresy*.

### <a name="use-joewares-netsessexe-from-victimpc"></a>Použít na JoeWare NetSess.exe z VictimPC

Spustit na JoeWare **NetSess** nástroj proti ContosoDC v kontextu ověřeného uživatele, v tomto případě ContosoDC:

``` cmd
NetSess.exe ContosoDC
```

![Útočníci používají protokol SMB rekognoskace k identifikaci uživatelů a jejich IP adresy](media/playbook-recon-smbrecon.png)

Již víme, že SamiraA se správce domény. Tento útok nám zajistila SamiraA na IP adresu jako 10.0.24.6. Jako útočník jsme zjistili, přesně, které jsme ohrozit. My také síťové umístění, kde je přihlášen tyto přihlašovací údaje.

### <a name="user-and-ip-address-reconnaissance-smb-detected-in-azure-atp"></a>Rekognoskace uživatele a IP adresa (SMB) v Azure ATP

Teď vidíme, co nám zjistil ochrany ATP v programu Azure:

![Rekognoskace AATP zjišťování SMB](media/playbook-recon-smbrecon-detection1.png)

Nejenže jsme upozorněni na tuto aktivitu jsme také upozorněni na odhalené účty a jejich příslušné IP adresy *od tohoto okamžiku v čase*. Jako zabezpečení Operations Center (SOC), právě nemáme pokus a její stav, ale také co byla odeslána zpět pro útočníka. Tyto informace je výhodné šetřením.


## <a name="next-steps"></a>Další postup

V další fázi v řetězu událostí útoku je obvykle k pokusu o taktiky Lateral Movement.

> [!div class="nextstepaction"]
> [Playbook Azure ATP taktiky Lateral Movement](atp-playbook-lateral-movement.md)

## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) ještě dnes!


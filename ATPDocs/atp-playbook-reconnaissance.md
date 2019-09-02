---
title: Kurz k Azure ATP rekognoskace PlayBook | Microsoft Docs
description: Kurz Azure ATP rekognoskace PlayBook popisuje, jak simulovat rekognoskace hrozby pro detekci pomocí Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: mlottner
ms.author: mlottner
ms.date: 09/01/2019
ms.reviewer: itargoet
ms.openlocfilehash: 11312f033261dd74f13dc0b3b9c093617e2c281c
ms.sourcegitcommit: f7c75bc5715c5bda0b3110364e2aebddddce8a13
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/01/2019
ms.locfileid: "70209244"
---
# <a name="tutorial-reconnaissance-playbook"></a>Návodu Rekognoskace PlayBook

Druhý kurz v této čtyřech řadách pro výstrahy zabezpečení služby Azure ATP je rekognoskace PlayBook. Účelem testovacího prostředí pro výstrahy zabezpečení Azure ATP je Ukázat možnosti **ATP Azure**při identifikaci a detekci podezřelých aktivit a potenciálních útoků proti vaší síti. PlayBook vysvětluje, jak testovat z některých diskrétních detekcí služby Azure ATP a zaměřuje se na funkce založené na podpisechAzure atp. Tato PlayBook nezahrnuje výstrahy nebo detekce na základě pokročilých detekcí strojového učení nebo rozpoznávání chování založeného na uživateli nebo entitách, protože vyžadují období učení se skutečným provozem sítě po dobu až 30 dnů. Další informace o jednotlivých kurzech v této sérii najdete v tématu [Přehled testovacího prostředí výstrah zabezpečení ATP](atp-playbook-lab-overview.md).

Tento PlayBook ilustruje detekci hrozeb a bezpečnostní výstrahy služby Azure ATP pro simulované útoky ze běžných a veřejně dostupných nástrojů pro hackery a útoky.

V tomto kurzu provedete tyto kroky:
> [!div class="checklist"]
> * Simulovat mapování sítě rekognoskace
> * Simulace rekognoskace adresářové služby
> * Simulace uživatele a IP adresy (SMB) rekognoskace
> * Kontrola výstrah zabezpečení z simulovaných rekognoskace v Azure ATP

## <a name="prerequisites"></a>Požadavky

[Dokončené testovací prostředí výstrah zabezpečení ATP](atp-playbook-setup-lab.md)
  - Doporučujeme co nejpřesněji sledovat pokyny k instalaci testovacího prostředí. Tím, jak vaše testovací prostředí slouží k navrhovanému nastavení testovacího prostředí, je snazší postupovat podle testovacích postupů Azure ATP.

## <a name="simulate-a-reconnaissance-attack"></a>Simulace útoku rekognoskace

Jakmile útočník získá v prostředí přítomnost, zahájí jejich rekognoskace kampaň. V této fázi bude útočník obvykle ztrácet čas prohledáním. Snaží se najít počítače, které vás zajímají, vytvořit výčet uživatelů a skupin, shromáždit důležité IP adresy a namapovat prostředky a slabé stránky vaší organizace. Rekognoskace aktivity umožňují útočníkům získat důkladné porozumění a úplné mapování vašeho prostředí pro pozdější použití.

Metody testování útoků rekognoskace:

* Mapování sítě rekognoskace
* Rekognoskace adresářové služby
* Uživatel a IP adresa (SMB) rekognoskace

## <a name="network-mapping-reconnaissance-dns"></a>Rekognoskace mapování sítě (DNS)

Jedním z prvních věcí, které by se útočník pokusil vyzkoušet, je pokusit se získat kopii všech informací DNS. Po úspěšném útočníkovi získá rozsáhlé informace o vašem prostředí, které potenciálně obsahují podobné informace o vašich dalších prostředích nebo sítích.

Azure ATP potlačí rekognoskaceou síťovou službu mapování sítě z **časové osy podezřelé aktivity** , dokud se nedokončí období učení na osm dní. Ve výukovém období zjistí Azure ATP, co je pro vaši síť normální a neobvyklé. Po osmi dnech výukového období neobvyklá událost rekognoskace mapování sítě vyvolá související výstrahu zabezpečení. 

### <a name="run-nslookup-from-victimpc"></a>Spuštění příkazu nslookup z VictimPC

K otestování služby DNS rekognoskace použijeme nativní nástroj příkazového řádku *nslookup*, který spustí přenos zóny DNS. Servery DNS se správnou konfigurací budou odmítat dotazy tohoto typu a neumožní pokus o přenos zóny.  

Přihlaste se k **VictimPC**pomocí ohrožených pověření Jan. Spusťte následující příkaz:

``` cmd
nslookup
```

Jako typ **Server** zadejte plně kvalifikovaný název domény nebo IP adresu řadiče domény, na kterém je senzor ATP nainstalovaný.

```nslookup
server contosodc.contoso.azure
```

Zkusíme přenést doménu.

```nslookup
ls -d contoso.azure
```

- Nahraďte ContosoDC. contoso. Azure a contoso. Azure za plně kvalifikovaným názvem domény vašeho senzoru ATP a názvu domény v uvedeném pořadí.

 ![příkaz nslookup se pokusil zkopírovat server DNS – chyba](media/playbook-recon-nslookup.png)

Pokud je **ContsoDC** vaším prvním nasazeným senzorem, počkejte 15 minut, než se povolí back-end databáze pro dokončení nasazení nezbytných mikroslužeb.

### <a name="network-mapping-reconnaissance-dns-detected-in-azure-atp"></a>Služba DNS (Network-Mapping rekognoskace) zjištěná v Azure ATP

Získání přehledu o tomto typu pokusu (neúspěšné nebo úspěšné) je důležité pro ochranu před hrozbami v doméně. Po poslední instalaci prostředí budete muset pro zobrazení zjištěné aktivity přejít na časovou osu **logických aktivit** . 

Ve vyhledávání ATP Azure zadejte **VictimPC**a kliknutím na ni Zobrazte časovou osu.

![Rekognoskace DNS zjištěné AATP, zobrazení na nejvyšší úrovni](media/playbook-recon-nslookupdetection1.png)

Vyhledejte aktivitu "AXFR Query". Azure ATP detekuje tento typ rekognoskacey proti vašemu serveru DNS. 
  - Pokud máte velký počet aktivit, klikněte na **filtrovat podle** a zrušte výběr všech typů s výjimkou **dotazu DNS**.

![Podrobné zobrazení detekce rekognoskace DNS v AATP](media/playbook-recon-nslookupdetection2.png)

Pokud váš analytik zabezpečení tuto aktivitu určil z bezpečnostního skeneru, konkrétní zařízení je možné vyloučit z dalších upozornění na detekci. V pravé horní oblasti výstrahy klikněte na tři tečky. Pak vyberte **Zavřít a vyloučit MySecurityScanner**. Kontrola, že se tato výstraha po rozpoznání z "MySecurityScanner" nezobrazuje znovu.

Rozpoznání selhání může být jako přehledné při zjišťování úspěšných útoků na prostředí. Portál Azure ATP nám umožňuje zobrazit přesný výsledek akcí, které udělal případný útočník. V našem scénáři útoku DNS na rekognoskace jsme postupovali jako útočníci a zastavili jsme výpis záznamů DNS domény. Váš tým SecOps se dozvěděl o našem pokusu o útokech a o tom, který počítač jsme použili při pokusu z výstrahy zabezpečení Azure ATP.

## <a name="directory-service-reconnaissance"></a>Rekognoskace adresářové služby

Dalším cílem rekognoskace je pokus o výčet všech uživatelů a skupin v doménové struktuře. Azure ATP potlačuje aktivitu výčtu adresářových služeb z časové osy podezřelé aktivity, dokud se nedokončí období učení na 30 dní. Ve výukovém období zjistí Azure ATP, co je pro vaši síť normální a neobvyklé. Po uplynutí 30 dnů kurzu vyvolala abnormální události výčtu adresářových služeb výstrahu zabezpečení. Během 30 dnů učení se můžete podívat na detekci ATP Azure u těchto aktivit pomocí časové osy aktivity entity ve vaší síti. V tomto testovacím prostředí se zobrazí detekce ATP pro Azure.

K předvedení běžné rekognoskace metody adresářové služby použijeme nativní binární *síť*Microsoft. Po našem pokusu se podíváme na časovou osu aktivity Jan, náš ohrožený uživatel, zobrazí ATP Azure s detekcí této aktivity.

### <a name="directory-service-enumeration-via-net-from-victimpc"></a>Výčet adresářové služby prostřednictvím *sítě* z VictimPC

Každý ověřený uživatel nebo počítač může zobrazit výčet dalších uživatelů a skupin v doméně. Tato schopnost výčtu je nutná, aby většina aplikací fungovala správně. Náš ohrožený uživatel je Jan, jedná se o Neprivilegovaný účet domény. V tomto simulovaném útoku přesně uvidíte, jak dokonce Neprivilegovaný účet domény může stále poskytovat cenné datové body útočníkovi.

1. Z **VictimPC**spusťte následující příkaz:

    ``` cmd
    net user /domain
    ```

   Výstup zobrazuje všechny uživatele v doméně contoso. Azure.

   ![Zobrazit výčet všech uživatelů v doméně](media/playbook-recon-dsenumeration-netusers.png)

2. Zkusíme vytvořit výčet všech skupin v doméně. Spusťte následující příkaz:

    ``` cmd
    net group /domain
    ```

   Výstup zobrazuje všechny skupiny v doméně contoso. Azure. Všimněte si jedné skupiny zabezpečení, která není výchozí skupinou: **Helpdesk**.

   ![Zobrazit výčet všech skupin v doméně](media/playbook-recon-dsenumeration-netgroups.png)

3. Nyní se pokusíme vytvořit výčet pouze skupiny Domain Admins. Spusťte následující příkaz:

    ``` cmd
    net group "Domain Admins" /domain
    ```

   ![Zobrazit výčet všech členů skupiny Domain Admins](media/playbook-recon-dsenumeration-netdomainadmins.png)

    Zjistili jsme, že máme dva členy skupiny Domain Admins: **SamiraA** a **ContosoAdmin** (integrovaný správce pro řadič domény). Mezi naší doménou a doménovou strukturou neexistují žádné hranice zabezpečení, naší další přestupnější je zkusit vytvořit výčet Enterprise Admins.

4. Pokud se chcete pokusit vytvořit výčet podnikových správců, spusťte následující příkaz:

    ``` cmd
   net group "Enterprise Admins" /domain
   ```

   Zjistili jsme, že existuje jenom jeden podnikový správce, ContosoAdmin. Tyto informace nejsou důležité, protože už jsme věděli, že mezi naší doménou a doménovou strukturou není hranice zabezpečení.

   ![Skupiny Enterprise Admins jsou v doméně výčtové.](media/playbook-recon-dsenumeration-netenterpriseadmins.png)

S informacemi shromážděnými v našich rekognoskace nyní ví o skupině zabezpečení helpdesk. I když tyto informace *ještě*nejsou zajímavé. Víme také, že **SamiraA** je členem skupiny Domain Admins. Pokud můžeme shromažďovat přihlašovací údaje pro SamiraA, můžeme získat přístup k samotnému řadiči domény.

### <a name="directory-service-enumeration-detected-in-azure-atp"></a>V Azure ATP se zjistil výčet adresářové služby.

Pokud má naše laboratoř *skutečná živá aktivita po dobu 30 dnů s nainstalovanou službou Azure ATP*, aktivita, kterou jsme právě nastavili jako Jan, by mohla být klasifikována jako abnormální. V časové ose podezřelé aktivity se zobrazí neobvyklé aktivity. Vzhledem k tomu, že jsme ale prostředí právě nainstalovali, musíme přejít na časovou osu logických aktivit.

Ve vyhledávání ATP Azure se podívejme na to, jak vypadá časová osa logických aktivit.

![Vyhledejte časovou osu logické aktivity konkrétní entity.](media/playbook-recon-dsenumeration-searchlogicalactivity.png)

V případě, že je Jan přihlášený k VictimPC pomocí protokolu Kerberos, můžeme vidět. Kromě toho vidíme, že Jan z VictimPC vyčísluje všechny uživatele v doméně.

![Časová osa logických aktivit Jan](media/playbook-recon-dsenumeration-jeffvlogicalactivity.png)

Mnoho aktivit je zaznamenáno v časové ose logických aktivit, což má zásadní schopnost provádět digitální forenzní a reakci na incidenty (DFIR). Můžete dokonce zobrazit aktivity, když počáteční zjišťování nevzniklo z Azure ATP, ale z ochrany ATP v programu Windows Defender, Office 365 a dalších.

Když se podíváte na **stránku ContosoDC**, můžeme taky zobrazit počítače, které se přihlásily do.

![Jan přihlášený počítač](media/playbook-recon-dsenumeration-jeffvloggedin.png)

Také můžeme získat data adresáře, včetně členství Jan a řízení přístupu, a to všechno v rámci služby Azure ATP.

![Data adresáře Jan v AATP](media/playbook-recon-dsenumeration-jeffvdirectorydata.png)

Nyní bude tato pozornost posunuta k výčtu relací SMB.

## <a name="user-and-ip-address-reconnaissance-smb"></a>Uživatel a IP adresa rekognoskace (SMB)

Složka adresáře SYSVOL služby Active Directory je jedním z, pokud neníto nejdůležitější síťová sdílená složka v prostředí. Každý počítač a uživatel musí mít přístup k této konkrétní sdílené síťové složce, aby vypnuli zásady skupiny. Útočník může získat Goldmine informace ze zobrazení výčtu aktivních relací se složkou SYSVOL.

Náš další krok je výčet relací SMB pro prostředek ContosoDC. Chceme vědět, kdo jiný má relace se sdílenou složkou SMB a *z jaké IP adresy*.

### <a name="use-joewares-netsessexe-from-victimpc"></a>Použijte NetSess. exe JoeWare z VictimPC

Spustit nástroj JoeWare **NetSess** Tool proti ContosoDC v kontextu ověřeného uživatele, v tomto případě ContosoDC:

``` cmd
NetSess.exe ContosoDC
```

![Útočníci používají SMB rekognoskace k identifikaci uživatelů a jejich IP adres](media/playbook-recon-smbrecon.png)

Už víme, že SamiraA je správcem domény. Tento útok zavedl IP adresu SamiraA jako 10.0.24.6. Jako útočník jsme se dozvěděli přesně, kdo potřebuje napadnout. Máme taky síťové umístění, kde se přihlašovací údaje přihlásily.

### <a name="user-and-ip-address-reconnaissance-smb-detected-in-azure-atp"></a>V Azure ATP se zjistilo, že uživatel a IP adresa rekognoskace (SMB).

Teď můžeme zjistit, co pro nás zjistilo Azure ATP:

![AATP zjišťování protokolu SMB rekognoskace](media/playbook-recon-smbrecon-detection1.png)

K této aktivitě jsme upozorněni, ale v *daném časovém*okamžiku se také zobrazí upozornění na vystavené účty a příslušné IP adresy. Jako středisko Security Center (SOC) nepotřebujeme jenom tento pokus a jeho stav, ale také to, co se do útočníku poslalo zpátky. Tyto informace se dotýkaly našeho šetření.


## <a name="next-steps"></a>Další kroky

Další fází v řetězci dezaktivačního útoku je obvykle pokus při pohybu.

> [!div class="nextstepaction"]
> [Playbooky Azure ATP – boční pohyb](atp-playbook-lateral-movement.md)

## <a name="join-the-community"></a>Připojte se ke komunitě

Máte k dispozici další otázky nebo zájem o projednávání Azure ATP a souvisejícího zabezpečení s ostatními? Připojte se ke [komunitě ATP Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) ještě dnes!


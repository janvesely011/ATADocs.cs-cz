---
title: Kurz nastavení oznámení testovacího prostředí zabezpečení služby Azure ochrany ATP v programu | Dokumentace Microsoftu
description: V tomto kurzu nastavení Azure ATP testovacího prostředí pro simulaci hrozeb pro zjišťování pomocí služby Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: mlottner
ms.author: mlottner
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: 9ae630711b6ee7b7f84a233998d188e498af0a9e
ms.sourcegitcommit: 7a32dcb65edc38fb9b3d340763045b21ea92feee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/18/2019
ms.locfileid: "59745584"
---
# <a name="tutorial-setup-an-atp-security-alert-lab"></a>Kurz: Instalační program ochrany ATP v programu testovacího prostředí výstrahy zabezpečení 

 Účelem výstraha zabezpečení Azure ochrany ATP v programu testovacího prostředí je ilustrovat **ochrany ATP v programu Azure**možnosti v identifikace a detekce podezřelých aktivit a potenciální útoky na vaší síti. Tento první kurz ze specializované série čtyři části vás provede procesem vytvoření testovacího prostředí pro testování pro služby Azure ATP *diskrétní* detekcí. Cvičení výstrah zabezpečení se zaměřuje na služby Azure ATP *založené na signaturách* možnosti. Testovací prostředí není zahrnují rozšířené strojové učení, uživatele nebo na základě entity behaviorální způsoby detekování, protože tyto detekce vyžadují období učení s skutečné síťový provoz až po dobu 30 dnů. Další informace o jednotlivých kurzu této série najdete v článku [přehled výstrah laboratoře zabezpečení ochrany ATP v programu](atp-playbook-lab-overview.md). 


V tomto kurzu provedete následující: 

> [!div class="checklist"]
> * Nastavení testovacího prostředí serveru a počítačů
> * Konfigurace služby Active Directory s uživateli a skupinami
> * Nastavení a konfigurace služby Azure ATP
> * Instalační program místní zásady pro server a počítače
> * Napodobení scénář pro správu helpdesku pomocí naplánované úlohy

## <a name="prerequisites"></a>Požadavky

1. [Řadič domény testovacího prostředí a dvě pracovní stanice lab](#servers-and-computers).
   - Pokračujte a [hydrate Active Directory (AD) s uživateli](#bkmk_hydrate).
1. [Instance služby Azure ATP](install-atp-step1.md) , který je [připojení k AD](install-atp-step2.md).
1. [Stáhněte si](install-atp-step3.md) a [nainstalujte nejnovější verzi senzoru služby Azure ATP](install-atp-step4.md) na řadiči domény testovacího prostředí.
1. Znalost [pracovních stanic s privilegovaným přístupem](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/privileged-access-workstations) a [SAMR zásad](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="recommendations"></a>Doporučení

Co možná nejvíce doporučujeme postupujte podle pokynů pro nastavení testovacího prostředí. Čím blíž testovacího prostředí je nastavení navrhované testovacího prostředí, tím snazší bude dodržovat testovacích postupů ochrany ATP v Azure. Po dokončení nastavení testovacího prostředí budete moci provádět akce s navrhované hackerským výzkumné nástroje a projděte si služby Azure ATP detekce z těchto akcí.

Nastavení dokončení testovacího prostředí by mělo vypadat jako možnou následující diagram:

![Testování nastavení testovacího prostředí Azure ATP](media/playbook-atp-setup-lab.png)

### <a name="servers-and-computers"></a>Servery a počítače

Tato tabulka obsahuje podrobnosti o počítače a konfigurace potřeba. IP adresy jsou k dispozici pro referenční účely pouze, takže snadno můžete absolvovat.

V příkladech těchto kurzech, název NetBIOS doménové struktury je **CONTOSO. AZURE**.

|  PLNĚ KVALIFIKOVANÝ NÁZEV DOMÉNY | Operační systém | IP | Účel |
|------|-------|---------|--------------|
| ContosoDC.contoso.azure | Windows Server 2012 R2 | 10.0.24.4 | Řadič domény s daným senzorem ochrany ATP v programu Azure místně nainstalovaný |
| VictimPC.contoso.azure | Windows 10 | 10.0.24.5 |Napadený počítač |
| AdminPC.contoso.azure | Windows 10  | 10.0.24.6 | Počítač správce domény (někdy označovány jako "Zabezpečené pracovní stanice správce" nebo "Pracovní stanice privilegované správce") |

### <a name="active-directory-users-and-groups"></a>Uživatelé služby Active Directory a skupin

V tomto testovacím prostředí jsou tři hlavní uživatelů a jeden účet služby. Účet služby pro služby Azure ATP a se používá pro účely synchronizace LDAP a SAMR.

Není k dispozici "Helpdesku" zabezpečení skupiny (SG) který Ron HelpDesk je jejím členem. Tato SG napodobuje na Helpdesk. SG je spárovaná s objektu zásad skupiny, která poskytuje naši technickou podporu členové práva místního správce na příslušných počítačích. Toto nastavení slouží k simulaci reálné modelu správy v produkčním prostředí.

| Jméno a příjmení    | Účet SAM |Účel|
|--------------|------------|--------------------------------------------------------------------------------------------------|
| Jan Leatherman  | JeffL  | Brzy na obětí útoku cíleného phishingu efektivní phishing  |
| RON helpdesku  | RonHD  |RON je "go na osoba" ve společnosti Contoso IT tým. Je členem skupiny zabezpečení "Helpdesku". |
| Samira Abbasi | SamiraA  | Ve společnosti Contoso tento uživatel je naše správce domény. |
| Azure ATP Service | AATPService | Účet služby Azure ATP |

## <a name="azure-atp-base-lab-environment"></a>Azure ATP základní testovací prostředí

Ke konfiguraci základní testovací prostředí přidáme uživatele a skupiny do služby Active Directory, upravit zásadu SAM a citlivých skupin v Azure ATP.

### <a name="bkmk_hydrate"></a> Hydrate uživatelů služby Active Directory počítači ContosoDC

Pro zjednodušení tohoto prostředí, jsme automatizovat proces vytvoření fiktivní uživatele a skupiny ve službě Active Directory. Tento skript je spuštěn jako předpoklad pro účely tohoto kurzu. Můžete použít nebo upravte skript tak hydrate vašeho testovacího prostředí služby Active Directory. Pokud nechcete použít skript, můžete to provést ručně.

Na počítači ContosoDC jako správce domény, spusťte následující příkaz k hydrate naši uživatelé služby Active Directory:

``` PowerShell

# Store the user passwords as variables
$SamiraASecurePass = ConvertTo-SecureString -String 'NinjaCat123' -AsPlainText -Force
$ronHdSecurePass = ConvertTo-SecureString -String 'FightingTiger$' -AsPlainText -Force
$jefflSecurePass = ConvertTo-SecureString -String 'Password$fun' -AsPlainText -Force
$AATPService = ConvertTo-SecureString -String 'Password123!@#' -AsPlainText -Force

# Create new AD user SamiraA and add her to the domain admins group
New-ADUser -Name SamiraA -DisplayName "Samira Abbasi" -PasswordNeverExpires $true -AccountPassword $samiraASecurePass -Enabled $true
Add-ADGroupMember -Identity "Domain Admins" -Members SamiraA

# Create new AD user RonHD, create new Helpdesk SG, add RonHD to the Helpdesk SG
New-ADUser -Name RonHD -DisplayName "Ron Helpdesk" -PasswordNeverExpires $true -AccountPassword $ronHdSecurePass -Enabled $true
New-ADGroup -Name Helpdesk -GroupScope Global -GroupCategory Security
Add-ADGroupMember -Identity "Helpdesk" -Members "RonHD"

# Create new AD user JeffL
New-ADUser -Name JeffL -DisplayName "Jeff Leatherman" -PasswordNeverExpires $true -AccountPassword $jefflSecurePass -Enabled $true

# Take note of the "AATPService" user below which will be our service account for Azure ATP.
# Create new AD user Azure ATP Service

New-ADUser -Name AatpService -DisplayName "Azure ATP/ATA Service" -PasswordNeverExpires $true -AccountPassword $AATPService -Enabled $true

```

### <a name="configure-sam-r-capabilities-from-contosodc"></a>Konfigurovat možnosti SAM-R z ContosoDC

Pokud chcete povolit službu ochrany ATP v programu Azure provádět SAM-R výčet správně a vytvářet cesty taktiky Lateral Movement, budete muset upravit zásadu SAM.

1. Vyhledání zásady SAM v části: **Zásady \> nastavení Windows \> nastavení zabezpečení \> místní zásady \> možnosti zabezpečení\> "přístup k síti: Omezit klienti můžou vzdáleně volat SAM"**_

    ![Upravte zásady skupiny pro povolení ochrany ATP v programu Azure využívat funkce cesty laterální pohyb.](media/playbook-labsetup-localgrouppolicies3.png)

2. Účet služby Azure ATP AATPService, přidáte do seznamu schválených účtů schopen provést tuto akci do moderního systému Windows.

    ![Přidat službu](./media/samr-add-service.png)

### <a name="add-sensitive-group-to-azure-atp"></a>Přidání citlivou skupinu do služby Azure ATP

Přidání "Helpdesku" skupina zabezpečení jako **citlivou skupinu** budete moct použít funkci laterální pohyb grafu ochrany ATP v programu Azure. Osvědčeným postupem je označení vysoce citlivé uživatele a skupiny, jež nejsou nutně Domain Admins, ale máte oprávnění napříč mnoha prostředky.

1. Na portálu ochrany ATP v programu Azure klikněte **konfigurace** ozubeného kola v panelu nabídek.

2. V části **detekce** klikněte na tlačítko **značky entit**.

    ![Značky entit Azure ATP](media/entity-tags.png)

3. V **citlivé** části, zadejte název "Helpdesku" **citlivých skupin** a potom klikněte na tlačítko **+** přihlášení je přidat.

    ![Označení "Helpdesku" jako citlivé skupina ochrany ATP v programu Azure umožňující laterální pohyb grafy a sestavy pro tuto privilegované skupiny](media/playbook-labsetup-helpdesksensitivegroup.png)

4. Klikněte na **Uložit**.

### <a name="azure-atp-lab-base-setup-checklist"></a>Kontrolní seznam pro základní nastavení Azure ochrany ATP v programu testovacího prostředí

V tomto okamžiku byste měli mít základní ochrany ATP v programu Azure lab. Ochrana ATP v programu Azure by měl být připravený k použití a uživatelé jsou připravené. Projděte si kontrolní seznam, abyste měli jistotu, že základní testovací prostředí je kompletní.  

| Krok    | Akce | Stav |
|--------------|------------|------------------|
| 1  | Senzoru služby Azure ATP počítači ContosoDC (požadovaný krok)| - [ ] |
| 2  | Uživatelé a skupiny se vytvoří ve službě Active Directory  | - [ ] |
| 3  | Azure ATP oprávnění účtu služby správně nakonfigurovaný pro SAMR | - [ ] |
| 4  | Přidat jako skupiny zabezpečení HelpDesk **citlivou skupinu** do služby Azure ATP| - [ ] |

## <a name="set-up-the-lab-workstations"></a>Nastavení testovacího prostředí pracovních stanic

Jakmile ověříte, že je nastavený základní služby Azure ATP testovacího prostředí, můžete spustit konfiguraci pracovní stanice Příprava dalších tří kurzů této řady. Můžeme vám hydrate naše VictimPC a AdminPC budou do tohoto testovacího prostředí, podívejte se aktivní.

### <a name="victimpc-local-policies"></a>Místní zásady VictimPC

Další krok pro vaše testovací prostředí je k dokončení nastavení místních zásad. **VictimPC** má JeffL a skupiny zabezpečení Helpdesk jako členy místní skupiny Administrators. Stejně jako v mnoha organizacích JeffL je správce na své vlastní zařízení **VictimPC**.

Jako místní správce, nastavení místních zásad spuštěním automatizovaný skript prostředí PowerShell:

``` PowerShell
# Add JeffL to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\JeffL"
# Add Helpdesk to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
```

Zkontrolujte skupiny Administrators na **VictimPC**, zajistit, je zřejmě má alespoň technické podpory a JeffL jako členy:

![HelpDesk nd JeffV by měl být ve skupině místní správci pro VictimPC](media/playbook-labsetup-localgrouppolicies2.png)

### <a name="helpdesk-simulation"></a> Simulace podporu helpdesku na VictimPC

Pro simulaci pracovní a spravované sítě, vytvoření úlohy naplánované na **VictimPC** počítače ke spuštění procesu "cmd.exe" jako **RonHD**.

1. Ze **se zvýšenými oprávněními konzolu Powershellu** na VictimPC spuštěním následujícího kódu:

    ``` PowerShell
    $action = New-ScheduledTaskAction -Execute 'cmd.exe'
    $trigger = New-ScheduledTaskTrigger -AtLogOn
    $runAs = 'Contoso\RonHD'
    $ronHHDPass = 'FightingTiger$'
    Register-ScheduledTask -TaskName "RonHD Cmd.exe - AATP SA Playbook" -Trigger $trigger -User $runAs -Password $ronHHDPass -Action $action
    ```

2. Přihlaste se k počítači jako **JeffL**. Proces Cmd.exe se spustí v kontextu RonHD po přihlášení budete jen simulovat helpdesku Správa počítače.

### <a name="turn-off-antivirus-on-victimpc"></a>Vypnout antivirovou ochranu v VictimPC

Pro účely testování, vypněte všechny antivirových řešení spuštěné v testovacím prostředí. Tím se zajistí, že se můžeme zaměřit na služby Azure ATP během těchto cvičení a ne na možnost obejití antivirové techniky.

Bez vypnutí antivirových řešení první, nebudete moct stáhnout některé nástroje v další části. Kromě toho pokud antivirové ochrany v programu je povoleno po nástrojů útoku, připravené, bude potřeba znovu stáhněte nástroje po zakázání antivirového programu.

### <a name="stage-common-hacker-tools"></a>Běžné nástroje kyberzločinci fáze

> [!WARNING]
> Tyto nástroje jsou uvedeny jen pro výzkumné účely. Společnost Microsoft **není** vlastníkem těchto nástrojů a Microsoft nemůže a zaručit ani záruky jejich chování. Tyto nástroje musí spustit v prostředí testovací laboratoře **pouze**.

Pokud chcete spustit playbooky výstraha zabezpečení Azure ochrany ATP v programu, jsou potřeba následující nástroje.

| Nástroj | Adresa URL |
|----|-----|
| Nástroj Mimikatz | [GitHub - Mimikatz](https://github.com/gentilkiwi/mimikatz) |
| PowerSploit | [GitHub - PowerSploit](https://github.com/PowerShellMafia/PowerSploit) |
| PsExec | [Microsoft Docs](https://docs.microsoft.com/en-us/sysinternals/downloads/psexec) |
| Příkaz NetSess | [JoeWare nástroje](http://www.joeware.net/freetools) |

Děkujeme společnosti autoři tyto výzkumné nástroje k povolení web komunity, abyste lépe pochopili kybernetických rizika a dopady.

### <a name="adminpc-local-policies"></a>Místní zásady AdminPC

**AdminPC** potřebuje **helpdesku** přidán do místní skupiny Administrators. Potom odeberte "Domain Admins" z místní skupiny Administrators. Tento krok zajistí, že Samira, Domain Admins, není správce AdminPC. To je osvědčený postup pro kontrolu přihlašovacích údajů. Tento krok provést ručně nebo pomocí skriptu prostředí PowerShell, které jsou k dispozici.

1. Přidat **helpdesku** k **AdminPC** a *odebrat* Domain Admins z místní skupiny správců spuštěním následujícího skriptu prostředí PowerShell:

    ``` PowerShell
   # Add Helpdesk to local Administrators group
   Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
   # Remove Domain Admins from local Administrators group
   Remove-LocalGroupMember -Group "Administrators" -Member "Domain Admins"

   ```

2. Po spuštění skriptu, **helpdesku** se nachází v místní **správci** > **členy** seznam **AdminPC**.
![Technické podpory ve skupině místní správci pro AdminPC](media/playbook-labsetup-localgrouppolicies1.png)

### <a name="simulate-domain-activities-from-adminpc"></a>Simulovat aktivity domény z AdminPC

Aktivity simulované domény se vyžaduje od SamiraA. Tento krok můžete provést ručně nebo pomocí skriptu prostředí PowerShell, které jsou k dispozici. Skript Powershellu má přístup k řadiči domény každých 5 minut a bude mít za následek simulované síťové aktivity jako Samira.

Jako **SamiraA**, spusťte následující skript Powershellu řádku v AdminPC:

```PowerShell

while ($true)
{
    Invoke-Expression "dir \\ContosoDC\c$"
    Start-Sleep -Seconds 300
}

```

### <a name="workstation-setup-checklist"></a>Kontrolní seznam nastavení pracovní stanice

Projděte si kontrolní seznam, abyste měli jistotu, že pracovní stanice instalace byla dokončena.

| Krok    | Akce | Stav |
|--------------|------------|------------------|
| 1  | Jako místní správce na VictimPC přidat JeffL a technické podpory | - [ ] |
| 2  | Vytvoření naplánované úlohy jako RonHD systémem VictimPC | - [ ] |
| 3  | Vypnout antivirová řešení na VictimPC | - [ ] |
| 4  | Fáze pracovat na VictimPC nástroje| - [ ] |
| 5  | Přidat technickou podporu a odebrat ze skupiny místních správců na AdminPC Domain Admins| - [ ] |
| 6  | Spustit skript prostředí PowerShell jako Samira simulovat aktivity domény | - [ ] |

## <a name="mission-accomplished"></a>Mise splněna!

Vaše testovací prostředí ochrany ATP v programu Azure je teď připravený k použití. Metody používané v tomto nastavení vybral vědomím, že se musí spravovat prostředky (podle *něco* nebo *někdo*) a správy vyžaduje oprávnění místního správce. Existují jiné způsoby, jak simulovat pracovní postup správy v testovacím prostředí, například:

- Protokolování do a z VictimPC pomocí účtu uživatele RonHD
- Přidání jinou verzi naplánované úlohy
- Relaci RDP
- Provádění "runas na příkazovém řádku

 Nejlepších výsledků dosáhnete zvolte metodu simulace, které můžete ve vašem testovacím prostředí pro účely konzistence automatizovat.


## <a name="next-steps"></a>Další postup

Testovací prostředí laboratoře ochrany ATP v programu Azure pomocí playbooků výstraha zabezpečení Azure ochrany ATP v programu pro každou fázi řetězu událostí internetového útoku, začíná fáze rekognoskace.  

> [!div class="nextstepaction"]
> [Playbook Azure Rekognoskace ochrany ATP v programu](atp-playbook-reconnaissance.md)


## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) ještě dnes!


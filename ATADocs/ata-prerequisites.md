---
title: Požadavky Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje požadavky pro úspěšné nasazení ATA ve vašem prostředí.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f5a21b1b84d164542e04d77e3a6a57fe5c944102
ms.sourcegitcommit: 1b23381ca4551a902f6343428d98f44480077d30
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/27/2018
ms.locfileid: "47403195"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="ata-prerequisites"></a>Požadavky ATA
Tento článek popisuje požadavky pro úspěšné nasazení ATA ve vašem prostředí.

> [!NOTE]
> Informace týkající se plánování prostředků a kapacity najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md).


ATA se skládá z komponenty ATA Center, ATA Gateway a/nebo ATA Lightweight Gateway. Další informace o komponentách ATA najdete v tématu [Architektura ATA](ata-architecture.md).

Systém ATA funguje na hranici doménové struktury ve službě Active Directory a podporuje funkční úroveň doménové struktury (FFL) v systémech Windows 2003 a novějších.


[Než začnete](#before-you-start): V této části jsou uvedené informace, které byste měli získat, a účty a síťové entity, které byste měli mít před zahájením instalace ATA.

[ATA Center](#ata-center-requirements): V této části jsou uvedené požadavky komponenty ATA Center na hardware a software a taky nastavení, která musíte nakonfigurovat na příslušném serveru ATA Center.

[ATA Gateway](#ata-gateway-requirements): V této části jsou uvedené požadavky komponenty ATA Gateway na hardware a software a taky nastavení, která musíte nakonfigurovat na příslušné servery ATA Gateway.

[ATA Lightweight Gateway](#ata-lightweight-gateway-requirements): V této části jsou uvedené požadavky komponenty ATA Lightweight Gateway na hardware a software.

[Konzola ATA](#ata-console): V této části jsou uvedené požadavky na prohlížeč pro spuštění konzoly ATA.

![Diagram architektury ATA](media/ATA-architecture-topology.jpg)

## <a name="before-you-start"></a>Než začnete
Tato část uvádí informace, které byste měli získat, a také účty a síťové entity, které byste měli mít před zahájením instalace ATA.


-   Uživatelský účet a heslo s oprávněním ke čtení pro všechny objekty v monitorovaném domén.

    > [!NOTE]
    > Pokud jste pro různé organizační jednotky (OU) ve vaší doméně nastavili vlastní seznamy ACL, ujistěte se, že vybraný uživatel má pro tyto organizační jednotky oprávnění ke čtení.

-   Neinstalujte na ATA Gateway nebo Lightweight Gateway Microsoft Message Analyzer. Message Analyzer ovladač je v konfliktu s ovladači komponent ATA Gateway a Lightweight Gateway. Pokud na komponentě ATA Gateway spustíte Wireshark a následně zastavíte jeho zachytávání, budete muset restartovat službu Microsoft Advanced Threat Analytics Gateway. Pokud ne, brána přestane zachytávání provozu. Wireshark běžící na ATA Lightweight Gateway nijak nenarušuje ATA Lightweight Gateway.

-    Doporučené: Uživatel by měl mít oprávnění jen pro čtení kontejneru odstraněných objektů. To umožňuje ATA detekovat hromadné odstranění objektů v doméně. Informace o konfiguraci oprávnění jen pro čtení pro kontejner odstraněných objektů najdete v tématu **Změna oprávnění pro kontejner odstraněných objektů** tématu [zobrazení nebo nastavení oprávnění u objektu adresáře](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) článku.

-   Volitelné: Uživatelský účet uživatele s žádné síťové aktivity. Tento účet se dají konfigurovat jako uživatel Honeytokenu ATA. Při konfiguraci účtu jako uživatel Honeytokenu, pouze uživatelské jméno je povinné. Informace o konfiguraci Honeytokenu, naleznete v tématu [vyloučení konfigurace IP adres a uživatele Honeytokenu](install-ata-step7.md).

-   Volitelné: Kromě shromažďování a analýzy síťového provozu do a z řadičů domény, může ATA využít události Windows 4776, 4732, 4733, 4728, 4729, 4756 a 4757 dál vylepšit ATA Pass-the-Hash, útoky hrubou silou, úpravy citlivých skupin a Podezřelá detekce tokeny. Tyto události můžete dostat z vašeho systému SIEM nebo nastavením předávání událostí Windows z řadiče domény. Shromážděné události poskytují řešení ATA další informace, které není možné zjistit z monitorování provozu na řadiči domény.


## <a name="ata-center-requirements"></a>Požadavky pro ATA Center
V této části je uveden seznam požadavků pro ATA Center.
### <a name="general"></a>Obecné
ATA Center podporuje instalaci na serveru s Windows Serverem 2012 R2 nebo Windows Serverem 2016. 

 > [!NOTE]
 > Komponenty ATA Center nepodporuje jádra serveru systému Windows.

ATA Center se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.

Před instalací součásti ATA Center do systému Windows Server 2012 R2 zkontrolujte, jestli je nainstalovaná aktualizace [KB2919355](https://support.microsoft.com/kb/2919355/).

Toto ověření můžete provést spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.

Instalace komponenty ATA Center jako virtuálního počítače se podporuje. 

> [!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

Pokud ATA Center spouštíte jako virtuální počítač, před vytvořením nového kontrolního bodu vypněte server. Vyhnete se tak možnému poškození databází.

### <a name="server-specifications"></a>Specifikace serveru

Při práci na fyzickém serveru databáze ATA vyžaduje, abyste v systému BIOS **zakázali** neuniformní přístup k paměti (NUMA). Systému se NUMA může označovat také jako prokládání uzlů v takovém případě budete muset **povolit** prokládání uzlů, abyste NUMA zakázali. Další informace najdete v dokumentaci k systému BIOS.<br>

K zajištění optimálního výkonu nastavte **možnost napájení** pro ATA Center na hodnotu **Vysoký výkon**.<br>
Počet řadiče domény, kterou monitorujete a zatížení na jednotlivých řadičích určuje specifikace serveru potřeba. Další informace najdete v tématu [plánování kapacity ATA](ata-capacity-planning.md).


### <a name="time-synchronization"></a>Časová synchronizace

Server ATA Center, servery ATA Gateway a řadiče domény musí mít časově synchronizované do pěti minut od sebe navzájem.


### <a name="network-adapters"></a>Síťové adaptéry

Měli byste následující:
-   Alespoň jeden síťový adaptér (pokud používáte fyzický server v prostředí sítě VLAN, doporučujeme použít dva síťové adaptéry)

-   IP adresa pro komunikaci mezi komponentami ATA Center a ATA Gateway, která je zašifrovaná pomocí SSL na portu 443. (Služba ATA vytvoří vazbu na všechny IP adresy, které ATA Center má na portu 443.)

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, které musí být otevřené, aby služba ATA Center fungovala správně.

|Protokol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|**SSL** (komunikace ATA)|TCP|443|ATA Gateway|Příchozí|
|**HTTP** (volitelné)|TCP|80|Podniková síť|Příchozí|
|**HTTPS**|TCP|443|Podniková síť a ATA Gateway|Příchozí|
|**SMTP** (volitelné)|TCP|25|Server SMTP|Odchozí|
|**SMTPS** (volitelné)|TCP|465|Server SMTP|Odchozí|
|**Syslog** (volitelné)|Protokol TCP/UPS/TLS (Konfigurovat)|514 (výchozí)|Server syslog|Odchozí|
|**LDAP**|TCP a UDP|389|Řadiče domény|Odchozí|
|**LDAPS** (volitelné)|TCP|636|Řadiče domény|Odchozí|
|**DNS**|TCP a UDP|53|Servery DNS|Odchozí|
|**Kerberos** (volitelné při připojení k doméně)|TCP a UDP|88|Řadiče domény|Odchozí|
|**Čas Windows** (volitelné při připojení k doméně)|UDP|123|Řadiče domény|Odchozí|

> [!NOTE]
> LDAP je potřeba otestovat přihlašovací údaje pro použití mezi komponenty ATA Gateway a řadiče domény. Test se provádí z ATA Center s řadičem domény k testování platnosti tyto přihlašovací údaje, po jejichž uplynutí komponenty ATA Gateway využívá LDAP jako součást procesu jeho normální řešení.

### <a name="certificates"></a>Certifikáty

Při instalaci a rychlejší nasazení ATA, můžete během instalace nainstalovat certifikáty podepsané svým držitelem. Pokud jste se rozhodli použít certifikáty podepsané svým držitelem, po počátečním nasazení doporučujeme nahradit certifikáty podepsané svým držitelem certifikáty od certifikační autority používané komponenty ATA Center.


Ujistěte se, že ATA Center a ATA Gateway mají přístup k seznamu odvolaných certifikátů distribučnímu bodu. Pokud nemají přístup k Internetu, postupujte podle [postup pro ruční import seznamu CRL](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx), dbejte na to nainstalovat všechny seznamu CRL distribuční body pro celý řetězec.

Certifikát musí mít:
-   Privátní klíč
-   Typ zprostředkovatele zprostředkovatele kryptografických služeb (CSP) nebo zprostředkovatele úložiště klíčů (KSP)
-   Veřejný klíč o délce 2 048 bitů
-   Nastavit hodnotu pro KeyEncipherment a ServerAuthentication příznaky použití
-   Specifikace klíče (KeyNumber) hodnotu "Pro výměnu" (na\_pro výměnu). Všimněte si, že hodnota "Podpis" (na\_podpis) se nepodporuje. 

Například můžete použít standardní **webový server** nebo **počítače** šablony.

> [!WARNING]
> Postup obnovení existujícího certifikátu se nepodporuje. Jediný způsob, jak obnovit certifikát, je vytvoření nového certifikátu a konfiguraci řešení ATA možnost použití nového certifikátu.


> [!NOTE]
> - Pokud budete ke konzole ATA přistupovat z jiných počítačů, zkontrolujte, že tyto počítače důvěřují certifikátu používanému službou ATA Center jinak dostanete upozornění, že před získáním na přihlašovací stránce dojde k nějakému problému s certifikátem zabezpečení webu.
> - Od verze ATA verze 1.8 komponenty ATA Gateway a Lightweight Gateway spravujete své vlastní certifikáty a potřebujete zásah správce spravovat.

## <a name="ata-gateway-requirements"></a>Požadavky na ATA Gateway
V této části je uveden seznam požadavků pro ATA Gateway.
### <a name="general"></a>Obecné
ATA Gateway podporuje instalaci na serveru se systémem Windows Server 2012 R2 nebo Windows Server 2016 (včetně jádra serveru).
ATA Gateway se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.
ATA Gateway můžete použít k monitorování řadičů domény pomocí funkční úrovně domény v systému Windows 2003 a novějším.

Před instalací ATA Gateway do systému Windows Server 2012 R2 zkontrolujte, jestli je nainstalovaná aktualizace [KB2919355](https://support.microsoft.com/kb/2919355/).

Toto ověření můžete provést spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.


Informace o používání virtuálních počítačů se službou ATA Gateway najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md).

> [!NOTE]
> Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. Zahrnuje to prostor potřebný pro binární soubory ATA, protokoly ATA, a [protokolování výkonu](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Specifikace serveru
K zajištění optimálního výkonu nastavte **možnost napájení** pro ATA Gateway na hodnotu **Vysoký výkon**.<br>
ATA Gateway může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů z a do řadičů domény.

> [!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

Další informace o hardwarových požadavcích ATA Gateway najdete v tématu [plánování kapacity ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace
Server ATA Center, servery ATA Gateway a řadiče domény musí mít časově synchronizované do pěti minut od sebe navzájem.

### <a name="network-adapters"></a>Síťové adaptéry
ATA Gateway vyžaduje nejméně jen adaptér pro správu a jeden adaptér pro zachytávání:

-   **Adaptér pro správu** – používá se pro komunikaci ve vaší podnikové síti. Tento adaptér by měly být nakonfigurované následující nastavení:

    -   Statická IP adresa včetně výchozí brány

    -   Upřednostňovaný a alternativní server DNS

    -   **Příponou DNS pro toto připojení** by pro každou monitorovanou doménu měl být její název DNS.

        ![Konfigurace přípony DNS v rozšířeném nastavení protokolu TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Pokud je ATA Gateway členem domény, může konfigurace proběhnout automaticky.

-   **Adaptér pro zachytávání** – používá se pro zachycení provozu do a z řadičů domény.

    > [!IMPORTANT]
    > -   Nakonfigurujte zrcadlení portů pro adaptér pro zachytávání jako cíl síťového provozu řadiče domény. Další informace najdete v tématu [konfigurace zrcadlení portů](configure-port-mirroring.md). Obvykle budete muset spolupracovat s týmem sítí nebo virtualizace ke konfiguraci zrcadlení portů.
    > -   Pro vaše prostředí nakonfigurujte statickou nepřesměrovatelnou IP adresu bez výchozí brány a adresy serveru DNS. Příklad: 1.1.1.1/32. Tím se zajistí, že síťový adaptér pro zachytávání může zachytit maximální objem přenášených dat a že síťový adaptér pro správu se používá k odesílání a příjmu požadované síťové komunikace.

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, u kterých ATA Gateway vyžaduje, aby byly nakonfigurované na adaptéru pro správu:

|Protokol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP a UDP|389|Řadiče domény|Odchozí|
|Zabezpečený LDAP (LDAPS)|TCP|636|Řadiče domény|Odchozí|
|LDAP pro globální katalog|TCP|3268|Řadiče domény|Odchozí|
|LDAPS pro globální katalog|TCP|3269|Řadiče domény|Odchozí|
|Kerberos|TCP a UDP|88|Řadiče domény|Odchozí|
|Služba Netlogon (SMB, CIFS, SAM-R)|TCP a UDP|445|Všechna zařízení v síti|Odchozí|
|Čas Windows|UDP|123|Řadiče domény|Odchozí|
|DNS|TCP a UDP|53|Servery DNS|Odchozí|
|NTLM přes RPC|TCP|135|Všechna zařízení v síti|Obojí|
|NetBIOS|UDP|137|Všechna zařízení v síti|Obojí|
|SSL|TCP|443|ATA Center|Odchozí|
|Syslog (volitelné)|UDP|514|Server SIEM|Příchozí|


> [!NOTE]
> V rámci procesu překladu, který provádí ATA Gateway, musí být na zařízeních v síti následující porty otevřené pro příjem dat z ATA Gateway.
>
> -   NTLM přes RPC (port TCP 135)
> -   NetBIOS (port UDP 137)
> - Pomocí uživatelského účtu služby adresáře, ATA Gateway dotazuje koncových bodů ve vaší organizaci pro použití SAM-R (přihlášení k síti) k vytvoření místního správce [grafu cesty laterální pohyb](use-case-lateral-movement-path.md). Další informace najdete v tématu [konfigurace SAM-R požadovaná oprávnění](install-ata-step9-samr.md).
> - Musí být otevřené příchozí na zařízeních v síti z komponenty ATA Gateway následující porty:
>   -   NTLM přes RPC (TCP Port 135) pro účely řešení
>   -   NetBIOS (UDP port 137) pro účely řešení

## <a name="ata-lightweight-gateway-requirements"></a>Požadavky pro ATA Lightweight Gateway
V této části je uveden seznam požadavků pro ATA Lightweight Gateway.
### <a name="general"></a>Obecné
ATA Lightweight Gateway podporuje instalaci na řadičích domény se systémem Windows Server 2008 R2 SP1 (kromě jádra serveru), Windows Server 2012, Windows Server 2012 R2 nebo Windows Server 2016 (včetně jádra, ale ne Nano).

Řadič domény může být řadič domény jen pro čtení (RODC).

Před instalací ATA Lightweight Gateway na řadiči domény se systémem Windows Server 2012 R2 ověřte, že je nainstalovaná aktualizace [KB2919355](https://support.microsoft.com/kb/2919355/).

Můžete to ověřit spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.

Pokud se instalace provádí pro Windows Server 2012 R2 Server Core, musí být nainstalovaná také následující aktualizace: [KB3000850](https://support.microsoft.com/help/3000850/november-2014-update-rollup-for-windows-rt-8.1%2c-windows-8.1%2c-and-windows-server-2012-r2).

 Můžete to ověřit spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb3000850]`.


Během instalace se nainstaluje rozhraní .Net Framework 4.6.1 a může dojít k restartování řadiče domény.


> [!NOTE]
> Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. Zahrnuje to prostor potřebný pro binární soubory ATA, protokoly ATA, a [protokolování výkonu](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Specifikace serveru

ATA Lightweight Gateway vyžaduje nejméně 2 jádra a 6 GB paměti RAM nainstalované na řadiči domény.
K zajištění optimálního výkonu nastavte **možnost napájení** pro ATA Lightweight Gateway na hodnotu **Vysoký výkon**.
Komponenta ATA Lightweight Gateway se dá nasadit na řadiče domény s různým zatížením i velikostí, v závislosti na objemu síťového přenosu dat do a z řadiče domény a na počtu prostředků, které jsou na příslušném řadiči domény nainstalované.

> [!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

Další informace o hardwarových požadavcích ATA Lightweight Gateway najdete v tématu [plánování kapacity ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace

Server ATA Center, servery ATA Lightweight Gateway a řadiče domény musí mít časově synchronizované do pěti minut od sebe navzájem.

### <a name="network-adapters"></a>Síťové adaptéry

ATA Lightweight Gateway monitoruje místní provoz na všech síťových adaptérech příslušného řadiče domény. <br>
Po nasazení můžete pomocí konzoly ATA případně změnit, které síťové adaptéry se monitorují.

> [!NOTE]
> Lightweight Gateway se nepodporuje v doméně, řadiče se systémem Windows 2008 R2 pomocí seskupování síťových adaptérů Broadcom povolena.

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, které ATA Lightweight Gateway vyžaduje:

|Protokol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP a UDP|53|Servery DNS|Odchozí|
|NTLM přes RPC|TCP|135|Všechna zařízení v síti|Obojí|
|NetBIOS|UDP|137|Všechna zařízení v síti|Obojí|
|SSL|TCP|443|ATA Center|Odchozí|
|Syslog (volitelné)|UDP|514|Server SIEM|Příchozí|
|Služba Netlogon (SMB, CIFS, SAM-R)|TCP a UDP|445|Všechna zařízení v síti|Odchozí|

> [!NOTE]
> V rámci procesu překladu, který provádí ATA Lightweight Gateway, musí být na zařízeních v síti následující porty otevřené pro příjem dat z ATA Lightweight Gateway.
>
> -   NTLM přes RPC
> -   NetBIOS
> - Pomocí uživatelského účtu služby adresáře, ATA Lightweight Gateway dotazuje koncových bodů ve vaší organizaci pro použití SAM-R (přihlášení k síti) k vytvoření místního správce [grafu cesty laterální pohyb](use-case-lateral-movement-path.md). Další informace najdete v tématu [konfigurace SAM-R požadovaná oprávnění](install-ata-step9-samr.md).
> - Musí být otevřené příchozí na zařízeních v síti z komponenty ATA Gateway následující porty:
>   -   NTLM přes RPC (TCP Port 135) pro účely řešení
>   -   NetBIOS (UDP port 137) pro účely řešení

## <a name="ata-console"></a>Konzola ATA
Přístup ke konzole ATA je prostřednictvím prohlížeče. podporují prohlížeče a nastavení:

-   Internet Explorer verze 10 a novější

-   Microsoft Edge

-   Google Chrome 40 a novější

-   Minimální rozlišení obrazovky na šířku 1 700 pixelů

## <a name="related-videos"></a>Související videa
- [Volba správného typu komponenty ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Architektura ATA](ata-architecture.md)
- [Instalace ATA](install-ata-step1.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



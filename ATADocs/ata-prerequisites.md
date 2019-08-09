---
title: Požadavky Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje požadavky pro úspěšné nasazení ATA ve vašem prostředí.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 08/07/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 139ea7e4eaecadeaf3fd57fb8ed7afe1dd8ea096
ms.sourcegitcommit: db35bae8354fa35644e9334bfc37b9ffbafdaacc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/09/2019
ms.locfileid: "68862570"
---
# <a name="ata-prerequisites"></a>Požadavky ATA

*Platí pro: Advanced Threat Analytics verze 1,9*

Tento článek popisuje požadavky na úspěšné nasazení ATA ve vašem prostředí.

> [!NOTE]
> Informace týkající se plánování prostředků a kapacity najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md).


ATA se skládá z ATA Center, ATA Gateway a/nebo ATA Lightweight Gateway. Další informace o komponentách ATA najdete v tématu [Architektura ATA](ata-architecture.md).

Systém ATA funguje na hranici doménové struktury ve službě Active Directory a podporuje funkční úroveň doménové struktury (FFL) v systémech Windows 2003 a novějších.


[Než začnete](#before-you-start): V této části jsou uvedené informace, které byste měli mít před zahájením instalace ATA mít za shromáždění a účty a síťové entity, které byste měli mít.

[ATA Center](#ata-center-requirements): V této části jsou uvedené požadavky komponenty ATA Center na hardware a software a také na nastavení, která potřebujete nakonfigurovat na serveru ATA Center.

[ATA Gateway](#ata-gateway-requirements): V této části jsou uvedené požadavky na hardware a software ATA Gateway a taky nastavení, která musíte nakonfigurovat na serverech ATA Gateway.

[ATA Lightweight Gateway](#ata-lightweight-gateway-requirements): V této části jsou uvedené požadavky ATA Lightweight Gateway na hardware a software.

[Konzola ATA](#ata-console): V této části jsou uvedené požadavky na prohlížeč pro spuštění konzoly ATA.

![Diagram architektury ATA](media/ATA-architecture-topology.jpg)

## <a name="before-you-start"></a>Než začnete
V této části jsou uvedené informace, které byste měli shromažďovat, a také účty a síťové entity, které byste měli mít před zahájením instalace ATA.


-   Uživatelský účet a heslo s přístupem pro čtení ke všem objektům ve sledovaných doménách.

    > [!NOTE]
    > Pokud jste pro různé organizační jednotky (OU) ve vaší doméně nastavili vlastní seznamy ACL, ujistěte se, že vybraný uživatel má pro tyto organizační jednotky oprávnění ke čtení.

-   Neinstalujte Microsoft Message Analyzer do komponenty ATA Gateway nebo Lightweight Gateway. Ovladač analyzátoru zpráv je v konfliktu s ovladači ATA Gateway a Lightweight Gateway. Pokud na komponentě ATA Gateway spustíte Wireshark a následně zastavíte jeho zachytávání, budete muset restartovat službu Microsoft Advanced Threat Analytics Gateway. V takovém případě brána zastaví zachytávání provozu. Spuštění nástroje Wireshark v ATA Lightweight Gateway nekoliduje s ATA Lightweight Gateway.

-    Doporučujeme: Uživatel by měl mít oprávnění jen pro čtení pro kontejner odstraněných objektů. Díky tomu může ATA detekovat hromadné odstranění objektů v doméně. Informace o konfiguraci oprávnění jen pro čtení pro kontejner odstraněných objektů naleznete v části **Změna oprávnění v kontejneru odstraněného objektu** v článku [zobrazení nebo nastavení oprávnění pro objekt adresáře](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) .

-   Volitelné: Uživatelský účet uživatele bez síťových aktivit. Tento účet se dá nakonfigurovat jako uživatel ATA Honeytokenu. Pokud chcete účet nakonfigurovat jako uživatele Honeytokenu, musíte zadat jenom uživatelské jméno. Informace o konfiguraci Honeytokenu najdete v tématu [konfigurace vyloučení IP adres a uživatele honeytokenu](install-ata-step7.md).

-   Volitelné: Kromě shromažďování a analýzy síťového provozu do a z řadičů domény může ATA použít události Windows 4776, 4732, 4733, 4728, 4729, 4756 a 4757 k dalšímu vylepšení ATA pass-the-hash, hrubou silou, modifikaci citlivých skupin a tokenů medu. detekce. Tyto události je možné přijímat z SIEM nebo nastavením předávání událostí systému Windows z řadiče domény. Shromážděné události poskytují řešení ATA další informace, které není možné zjistit z monitorování provozu na řadiči domény.


## <a name="ata-center-requirements"></a>Požadavky pro ATA Center
V této části je uveden seznam požadavků pro ATA Center.

### <a name="general"></a>Obecné
ATA Center podporuje instalaci na serveru se systémem Windows Server 2012 R2 Windows Server 2016 a Windows Server 2019. 

 > [!NOTE]
 > ATA Center nepodporuje jádro Windows serveru.

ATA Center se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.

Než nainstalujete ATA Center se systémem Windows 2012 R2, potvrďte, že je nainstalovaná následující aktualizace: [KB2919355](https://support.microsoft.com/kb/2919355/).

Toto ověření můžete provést spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.

Instalace komponenty ATA Center jako virtuálního počítače se podporuje. 

### <a name="dynamic-memory"></a>Dynamická paměť

> [!NOTE] 
> Když centrum spouštíte jako virtuální počítač (VM), vyžaduje to, aby se k VIRTUÁLNÍmu počítači přidělila veškerá paměť.

|Virtuální počítač spuštěný v|Popis|
|------------|-------------|
|Hyper-V|Ujistěte se, že pro virtuální počítač není povolená **možnost povolit dynamická paměť** .|
|Hostiteli|Zajistěte, aby byla nakonfigurovaná velikost paměti a vyhrazená paměť shodná, nebo v nastavení virtuálního počítače vyberte následující možnost – **rezervovat veškerou paměť hosta (všechna zamčená)** .|
|Jiný Hostitel virtualizace|V dokumentaci dodávané dodavatelem najdete informace o tom, jak zajistit, aby virtuální počítač byl vždy plně přidělen. |
|

Pokud ATA Center spouštíte jako virtuální počítač, před vytvořením nového kontrolního bodu vypněte server. Vyhnete se tak možnému poškození databází.

### <a name="server-specifications"></a>Specifikace serveru

Při práci na fyzickém serveru databáze ATA vyžaduje, abyste v systému BIOS **zakázali** neuniformní přístup k paměti (NUMA). Váš systém může na architektuře NUMA odkazovat jako na prokládání uzlů. v takovém případě je nutné **Povolit** prokládání uzlů, aby bylo možné technologii NUMA zakázat. Další informace najdete v dokumentaci k systému BIOS.<br>

K zajištění optimálního výkonu nastavte **možnost napájení** pro ATA Center na hodnotu **Vysoký výkon**.<br>
Počet řadičů domény, které sledujete, a zatížení jednotlivých řadičů domény určuje, jaké požadavky na serveru jsou potřeba. Další informace najdete v tématu [plánování kapacity ATA](ata-capacity-planning.md).


### <a name="time-synchronization"></a>Časová synchronizace

Server ATA Center, servery ATA Gateway a řadiče domény musí mít během pěti minut čas synchronizovaný.


### <a name="network-adapters"></a>Síťové adaptéry

Měli byste mít následující sadu:
-   Alespoň jeden síťový adaptér (pokud používáte fyzický server v prostředí sítě VLAN, doporučujeme použít dva síťové adaptéry)

-   IP adresa pro komunikaci mezi komponentami ATA Center a ATA Gateway, která je zašifrovaná pomocí SSL na portu 443. (Služba ATA se váže ke všem IP adresám, které ATA Center má na portu 443.)

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, které musí být otevřené, aby služba ATA Center fungovala správně.

|Protocol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|**SSL** (komunikace ATA)|TCP|443|ATA Gateway|Příchozí|
|**HTTP** (volitelné)|TCP|80|Podniková síť|Příchozí|
|**HTTPS**|TCP|443|Podniková síť a ATA Gateway|Příchozí|
|**SMTP** (volitelné)|TCP|25|Server SMTP|Odchozí|
|**SMTPS** (volitelné)|TCP|465|Server SMTP|Odchozí|
|**Syslog** (volitelné)|TCP/UPS/TLS (konfigurovatelné)|514 (výchozí)|Server syslog|Odchozí|
|**LDAP**|TCP a UDP|389|Řadiče domény|Odchozí|
|**LDAPS** (volitelné)|TCP|636|Řadiče domény|Odchozí|
|**DNS**|TCP a UDP|53|Servery DNS|Odchozí|
|**Kerberos** (volitelné při připojení k doméně)|TCP a UDP|88|Řadiče domény|Odchozí|
|**Čas systému Windows** (volitelné, pokud je připojeno k doméně)|UDP|123|Řadiče domény|Odchozí|

> [!NOTE]
> Protokol LDAP je nutný k otestování přihlašovacích údajů, které se mají používat mezi komponentami ATA Gateway a řadiči domény. Test se provádí z komponenty ATA Center na řadič domény, aby se otestovala platnost těchto přihlašovacích údajů, po které ATA Gateway používá protokol LDAP jako součást svého běžného řešení.

### <a name="certificates"></a>Certifikáty

K rychlejší instalaci a nasazení ATA můžete během instalace nainstalovat certifikáty podepsané svým držitelem. Pokud jste se rozhodli používat certifikáty podepsané svým držitelem, doporučuje se po počátečním nasazení nahradit certifikáty podepsané svým držitelem certifikáty od interní certifikační autority, kterou bude používat ATA Center.


Ujistěte se, že komponenty ATA Center a ATA Gateway mají přístup k distribučnímu bodu seznamu CRL. Pokud nemají přístup k Internetu, postupujte podle pokynů [k ručnímu importování seznamu CRL](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx)a dbejte na to, abyste nainstalovali všechny distribuční body CRL pro celý řetězec.

Certifikát musí mít:
-   Privátní klíč
-   Typ poskytovatele buď poskytovatele kryptografických služeb (CSP), nebo zprostředkovatel úložiště klíčů (KSP)
-   Délka veřejného klíče 2048 bitů
-   Hodnota nastavená pro příznaky použití KeyEncipherment a ServerAuthentication
-   Hodnota specifikace klíče (číslo klíče) "Výměna klíče" (při\_výměně klíče). Všimněte si, že hodnota "signatura"\_(u podpisu) není podporována. 

Můžete například použít standardní **webový server** nebo šablony **počítače** .

> [!WARNING]
> Proces obnovení existujícího certifikátu není podporován. Jediným způsobem, jak obnovit certifikát, je vytvoření nového certifikátu a konfigurace ATA pro použití nového certifikátu.


> [!NOTE]
> - Pokud budete k konzole ATA přistupovat z jiných počítačů, ujistěte se, že tyto počítače důvěřují certifikátu používanému službou ATA Center. v opačném případě se zobrazí upozornění, že došlo k potížím s certifikátem zabezpečení webu předtím, než se přihlásíte na přihlašovací stránku.
> - Od verze ATA 1,8 komponenty ATA Gateway a Lightweight Gateway spravují vlastní certifikáty a nepotřebují pro jejich správu žádnou interakci se správcem.

## <a name="ata-gateway-requirements"></a>Požadavky na ATA Gateway
V této části je uveden seznam požadavků pro ATA Gateway.
### <a name="general"></a>Obecné
ATA Gateway podporuje instalaci na serveru se systémem Windows Server 2012 R2 nebo Windows Server 2016 a Windows Server 2019 (včetně jádra serveru).
ATA Gateway se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.
ATA Gateway můžete použít k monitorování řadičů domény pomocí funkční úrovně domény v systému Windows 2003 a novějším.

Před instalací ATA Gateway se systémem Windows 2012 R2 potvrďte, že je nainstalovaná následující aktualizace: [KB2919355](https://support.microsoft.com/kb/2919355/).

Toto ověření můžete provést spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.


Informace o používání virtuálních počítačů se službou ATA Gateway najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md).

> [!NOTE]
> Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. To zahrnuje prostor potřebný pro binární soubory ATA, protokoly ATA a [protokoly výkonu](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Specifikace serveru
K zajištění optimálního výkonu nastavte **možnost napájení** pro ATA Gateway na hodnotu **Vysoký výkon**.<br>
ATA Gateway může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů z a do řadičů domény.

Další informace o dynamické paměti nebo jiné funkci správy paměti virtuálních počítačů najdete v tématu [dynamická paměť](#dynamic-memory).

Další informace o požadavcích na hardware ATA Gateway najdete v tématu [plánování kapacity ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace
Server ATA Center, servery ATA Gateway a řadiče domény musí mít během pěti minut čas synchronizovaný.

### <a name="network-adapters"></a>Síťové adaptéry
ATA Gateway vyžaduje nejméně jen adaptér pro správu a jeden adaptér pro zachytávání:

-   **Adaptér pro správu** – používá se pro komunikaci ve vaší podnikové síti. Tento adaptér by měl být nakonfigurovaný s následujícím nastavením:

    -   Statická IP adresa včetně výchozí brány

    -   Upřednostňovaný a alternativní server DNS

    -   **Příponou DNS pro toto připojení** by pro každou monitorovanou doménu měl být její název DNS.

        ![Konfigurace přípony DNS v rozšířeném nastavení protokolu TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Pokud je ATA Gateway členem domény, může konfigurace proběhnout automaticky.

-   **Adaptér** pro zachytávání – používá se k zaznamenání provozu do a z řadičů domény.

    > [!IMPORTANT]
    > -   Nakonfigurujte zrcadlení portů pro adaptér pro zachytávání jako cíl síťového provozu řadiče domény. Další informace najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md). K nakonfigurování zrcadlení portů obvykle potřebujete pracovat s týmem sítě nebo s virtualizačním týmem.
    > -   Pro vaše prostředí nakonfigurujte statickou nepřesměrovatelnou IP adresu bez výchozí brány a adresy serveru DNS. Příklad: 1.1.1.1/32. Tím zajistíte, že síťový adaptér pro zachytávání může zachytit maximální objem provozu a že síťový adaptér pro správu se používá k posílání a přijímání potřebných síťových přenosů.

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, u kterých ATA Gateway vyžaduje, aby byly nakonfigurované na adaptéru pro správu:

|Protocol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP a UDP|389|Řadiče domény|Odchozí|
|Zabezpečený LDAP (LDAPS)|TCP|636|Řadiče domény|Odchozí|
|LDAP pro globální katalog|TCP|3268|Řadiče domény|Odchozí|
|LDAPS pro globální katalog|TCP|3269|Řadiče domény|Odchozí|
|Kerberos|TCP a UDP|88|Řadiče domény|Odchozí|
|Netlogon (SMB, CIFS, SAM-R)|TCP a UDP|445|Všechna zařízení v síti|Odchozí|
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
> - Pomocí uživatelského účtu adresářových služeb Služba ATA Gateway dotazuje koncové body ve vaší organizaci pro místní správce pomocí SAM-R (přihlášení k síti), aby bylo možné vytvořit [graf cesty bočního pohybu](use-case-lateral-movement-path.md). Další informace najdete v tématu [Konfigurace požadovaných oprávnění Sam-R](install-ata-step9-samr.md).
> - Na zařízeních v síti musí být v bráně ATA Gateway otevřené příchozí připojení:
>   -   Protokol NTLM přes RPC (TCP port 135) pro účely řešení
>   -   NetBIOS (port UDP 137) pro účely překladu

## <a name="ata-lightweight-gateway-requirements"></a>Požadavky pro ATA Lightweight Gateway
V této části je uveden seznam požadavků pro ATA Lightweight Gateway.
### <a name="general"></a>Obecné
ATA Lightweight Gateway podporuje instalaci na řadičích domény se systémem Windows Server 2008 R2 SP1 (kromě jádra serveru), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 a Windows Server 2019 (včetně jádra, ale ne nano).

Řadič domény může být řadičem domény jen pro čtení (RODC).

Než nainstalujete ATA Lightweight Gateway na řadič domény se systémem Windows Server 2012 R2, zkontrolujte, že je nainstalovaná následující aktualizace: [KB2919355](https://support.microsoft.com/kb/2919355/).

Můžete to ověřit spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.

Pokud je instalace pro Windows Server 2012 R2 Server Core, musí být nainstalovaná i tato aktualizace: [KB3000850](https://support.microsoft.com/help/3000850/november-2014-update-rollup-for-windows-rt-8.1%2c-windows-8.1%2c-and-windows-server-2012-r2).

 Můžete to ověřit spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb3000850]`.


Během instalace se nainstaluje rozhraní .Net Framework 4.6.1 a může dojít k restartování řadiče domény.


> [!NOTE]
> Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. To zahrnuje prostor potřebný pro binární soubory ATA, protokoly ATA a [protokoly výkonu](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Specifikace serveru

ATA Lightweight Gateway vyžaduje nejméně 2 jádra a 6 GB paměti RAM nainstalované na řadiči domény.
K zajištění optimálního výkonu nastavte **možnost napájení** pro ATA Lightweight Gateway na hodnotu **Vysoký výkon**.
Komponenta ATA Lightweight Gateway se dá nasadit na řadiče domény s různým zatížením i velikostí, v závislosti na objemu síťového přenosu dat do a z řadiče domény a na počtu prostředků, které jsou na příslušném řadiči domény nainstalované.

Další informace o dynamické paměti nebo jiné funkci správy paměti virtuálních počítačů najdete v tématu [dynamická paměť](#dynamic-memory).

Další informace o požadavcích na hardware ATA Lightweight Gateway najdete v tématu [plánování kapacity ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace

Server ATA Center, servery ATA Lightweight Gateway a řadiče domény musí mít během pěti minut čas synchronizovaný.

### <a name="network-adapters"></a>Síťové adaptéry

ATA Lightweight Gateway monitoruje místní provoz na všech síťových adaptérech příslušného řadiče domény. <br>
Po nasazení můžete pomocí konzoly ATA případně změnit, které síťové adaptéry se monitorují.

> [!NOTE]
> Zjednodušená brána není podporovaná na řadičích domény se systémem Windows 2008 R2 se zapnutým seskupováním síťových adaptérů Broadcom.

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, které ATA Lightweight Gateway vyžaduje:

|Protocol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP a UDP|53|Servery DNS|Odchozí|
|NTLM přes RPC|TCP|135|Všechna zařízení v síti|Obojí|
|NetBIOS|UDP|137|Všechna zařízení v síti|Obojí|
|SSL|TCP|443|ATA Center|Odchozí|
|Syslog (volitelné)|UDP|514|Server SIEM|Příchozí|
|Netlogon (SMB, CIFS, SAM-R)|TCP a UDP|445|Všechna zařízení v síti|Odchozí|

> [!NOTE]
> V rámci procesu překladu, který provádí ATA Lightweight Gateway, musí být na zařízeních v síti následující porty otevřené pro příjem dat z ATA Lightweight Gateway.
>
> -   NTLM přes RPC
> -   NetBIOS
> - Pomocí uživatelského účtu adresářových služeb ATA Lightweight Gateway dotazuje koncové body ve vaší organizaci pro místní správce pomocí SAM-R (přihlášení k síti), aby bylo možné vytvořit [graf cesty bočního pohybu](use-case-lateral-movement-path.md). Další informace najdete v tématu [Konfigurace požadovaných oprávnění Sam-R](install-ata-step9-samr.md).
> - Na zařízeních v síti musí být v bráně ATA Gateway otevřené příchozí připojení:
>   -   Protokol NTLM přes RPC (TCP port 135) pro účely řešení
>   -   NetBIOS (port UDP 137) pro účely překladu

## <a name="ata-console"></a>Konzola ATA
Přístup ke konzole ATA je prostřednictvím prohlížeče, který podporuje prohlížeče a nastavení:

-   Internet Explorer verze 10 a novější

-   Microsoft Edge

-   Google Chrome 40 a novější

-   Minimální rozlišení obrazovky na šířku 1 700 pixelů

## <a name="related-videos"></a>Související videa
- [Výběr správného typu ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Nástroj pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Architektura ATA](ata-architecture.md)
- [Instalace ATA](install-ata-step1.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



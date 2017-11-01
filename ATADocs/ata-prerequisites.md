---
title: "Požadavky Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Popisuje požadavky pro úspěšné nasazení ATA ve vašem prostředí."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/25/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2f720118b1d9ac08f26b7057e5c7b6706ff4b0b1
ms.sourcegitcommit: 0cc999b20e919abe4d6edaedee78185788a3e3b9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="ata-prerequisites"></a>Požadavky ATA
Tento článek popisuje požadavky pro úspěšné nasazení ATA ve vašem prostředí.

>[!NOTE]
> Informace týkající se plánování prostředků a kapacity najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md).


ATA se skládá z komponenty ATA Center, ATA Gateway nebo ATA Lightweight Gateway. Další informace o komponentách ATA najdete v tématu [Architektura ATA](ata-architecture.md).

Systém ATA funguje na hranici doménové struktury ve službě Active Directory a podporuje funkční úroveň doménové struktury (FFL) v systémech Windows 2003 a novějších.


[Než začnete](#before-you-start): V této části jsou uvedené informace, které byste měli získat, a účty a síťové entity, které byste měli mít před zahájením instalace ATA.

[ATA Center](#ata-center-requirements): V této části jsou uvedené požadavky komponenty ATA Center na hardware a software a taky nastavení, která musíte nakonfigurovat na příslušném serveru ATA Center.

[ATA Gateway](#ata-gateway-requirements): V této části jsou uvedené požadavky komponenty ATA Gateway na hardware a software a taky nastavení, která musíte nakonfigurovat na příslušné servery ATA Gateway.

[ATA Lightweight Gateway](#ata-lightweight-gateway-requirements): V této části jsou uvedené požadavky komponenty ATA Lightweight Gateway na hardware a software.

[Konzola ATA](#ata-console): V této části jsou uvedené požadavky na prohlížeč pro spuštění konzoly ATA.

![Diagram architektury ATA](media/ATA-architecture-topology.jpg)

## <a name="before-you-start"></a>Než začnete
V této části jsou uvedené informace, které byste měli získat, a účty a síťové entity, které byste měli mít před zahájením instalace ATA.


-   Uživatelský účet a heslo s přístupem pro čtení pro všechny objekty v monitorovaném domén.

    > [!NOTE]
    > Pokud jste pro různé organizační jednotky (OU) ve vaší doméně nastavili vlastní seznamy ACL, ujistěte se, že vybraný uživatel má pro tyto organizační jednotky oprávnění ke čtení.

-   Neinstalujte Microsoft Message Analyzer na ATA Gateway nebo Lightweight Gateway. Ovladač nástroje Message Analyzer koliduje s ovladači komponent ATA Gateway a Lightweight Gateway. Pokud na komponentě ATA Gateway spustíte Wireshark a následně zastavíte jeho zachytávání, budete muset restartovat službu Microsoft Advanced Threat Analytics Gateway. Pokud ne, brána zastaví zachycení provozu. Wireshark běžící na komponentě ATA Lightweight Gateway nijak nenarušuje její činnost.

-    Doporučujeme: Uživatel by měl mít oprávnění jen pro čtení v kontejneru odstraněné objekty. To umožňuje ATA detekovat hromadné odstranění objektů v doméně. Informace o konfiguraci oprávnění jen pro čtení pro kontejner odstraněných objektů najdete v tématu **Změna oprávnění pro kontejner odstraněných objektů** tématu [zobrazení nebo nastavení oprávnění pro objekt adresáře](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) tématu.

-   Volitelné: Uživatelský účet uživatele, který nemá žádné síťové aktivity. Tento účet je nakonfigurovaný jako uživatel Honeytokenu ATA. Ke konfiguraci uživatele Honeytokenu, potřebovat SID účtu uživatele, nikoli jeho uživatelské jméno. Další informace najdete v tématu [vyloučení konfigurace IP adres a uživatele Honeytokenu](install-ata-step7.md).

-   Volitelné: Kromě shromažďování a analýzy síťových přenosů do a z řadičů domény, může ATA využít události systému Windows 4776, 4732, 4733, 4728, 4729, 4756 a 4757 k dalšímu vylepšení útoků ATA Pass-the-Hash, útoků hrubou silou, změny citlivých skupin a Sloužícím jako návnada detekce tokeny. Tyto události mohou být přijímány ze služby SIEM nebo nastavením předávání událostí Windows z řadiče domény. Shromážděné události poskytují řešení ATA další informace, které není možné zjistit z monitorování provozu na řadiči domény.


## <a name="ata-center-requirements"></a>Požadavky pro ATA Center
V této části je uveden seznam požadavků pro ATA Center.
### <a name="general"></a>Obecné
ATA Center podporuje instalaci na serveru s Windows Serverem 2012 R2 nebo Windows Serverem 2016. ATA Center se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.

Před instalací součásti ATA Center do systému Windows Server 2012 R2 zkontrolujte, jestli je nainstalovaná aktualizace [KB2919355](https://support.microsoft.com/kb/2919355/).

Toto ověření můžete provést spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.

Instalace komponenty ATA Center jako virtuálního počítače se podporuje. 

>[!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

Pokud ATA Center spouštíte jako virtuální počítač, před vytvořením nového kontrolního bodu vypněte server. Vyhnete se tak možnému poškození databází.
### <a name="server-specifications"></a>Specifikace serveru
Při práci na fyzickém serveru databáze ATA vyžaduje, abyste v systému BIOS **zakázali** neuniformní přístup k paměti (NUMA). Systému se NUMA může označovat jako prokládání uzlů v takovém případě budete muset **povolit** prokládání uzlů, abyste NUMA zakázali. Další informace najdete v dokumentaci systému BIOS. Tento postup není relevantní, pokud ATA Center běží na virtuálním serveru.<br>
K zajištění optimálního výkonu nastavte **možnost napájení**  pro ATA Center na hodnotu **Vysoký výkon**.<br>
Počet řadičů domény, které monitorujete a zatížení na jednotlivých řadičích určuje specifikaci serveru potřeba. Další informace najdete v tématu [plánování kapacity ATA](ata-capacity-planning.md).


### <a name="time-synchronization"></a>Časová synchronizace
Server ATA Center, servery ATA Gateway a řadiče domény musí mít časově synchronizované intervalu než pět minut.


### <a name="network-adapters"></a>Síťové adaptéry
Musí mít následující:
-   Alespoň jeden síťový adaptér (pokud používáte fyzický server v prostředí sítě VLAN, doporučujeme použít dva síťové adaptéry)

-   IP adresa pro komunikaci mezi ATA Center a ATA Gateway, která je zašifrovaná pomocí SSL na portu 443. (Služba ATA se váže k všechny IP adresy, které ATA Center má na portu 443.)

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, které musí být otevřené, aby služba ATA Center fungovala správně.

|Protokol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|**SSL** (komunikace ATA)|TCP|443 nebo konfigurovatelné|ATA Gateway|Příchozí|
|**HTTP** (volitelné)|TCP|80|Podniková síť|Příchozí|
|**HTTPS**|TCP|443|Podniková síť a ATA Gateway|Příchozí|
|**SMTP** (volitelné)|TCP|25|Server SMTP|Odchozí|
|**SMTPS** (volitelné)|TCP|465|Server SMTP|Odchozí|
|**Syslog** (volitelné)|TCP|514|Server syslog|Odchozí|
|**LDAP**|TCP a UDP|389|Řadiče domény|Odchozí|
|**LDAPS** (volitelné)|TCP|636|Řadiče domény|Odchozí|
|**DNS**|TCP a UDP|53|Servery DNS|Odchozí|
|**Kerberos** (volitelné při připojení k doméně)|TCP a UDP|88|Řadiče domény|Odchozí|
|**Přihlašování k síti** (volitelné při připojení k doméně)|TCP a UDP|445|Řadiče domény|Odchozí|
|**Systémový čas** (volitelné, pokud je připojený k doméně)|UDP|123|Řadiče domény|Odchozí|

> [!NOTE]
> LDAP je potřeba otestovat pověření pro použití mezi komponenty ATA Gateway a řadiče domény. Test se provádí z ATA Center na řadič domény k testování platnosti tyto přihlašovací údaje, po kterých ATA Gateway využívá LDAP jako součást procesu jeho normální řešení.

### <a name="certificates"></a>Certifikáty

K usnadnění instalace ATA můžete během instalace nainstalovat certifikáty podepsané jejich držiteli. Po nasazení, měli byste nahradit podepsaný certifikát od interní certifikační autority, který se má použít pro ATA Center.


Zajistěte, aby ATA Center a ATA Gateway mají přístup k seznamu odvolaných certifikátů distribučnímu bodu. Pokud nemají přístup k Internetu, postupujte podle [postup pro ruční import seznamu CRL](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx), dbejte nainstalovat všechny CRL distribuční body pro celý řetězec.

Certifikát musí mít:
-   Privátní klíč
-   Typ zprostředkovatele zprostředkovatele kryptografických služeb (CSP) nebo zprostředkovatele úložiště klíčů (KSP)
-   Veřejný klíč o délce 2 048 bitů
-   Nastavte hodnotu pro KeyEncipherment a ServerAuthentication příznaky využití

Například můžete použít standardní **webový server** nebo **počítače** šablony.

> [!WARNING]
> - Proces obnovení existujícího certifikátu není podporována. Jediný způsob, jak obnovit certifikát, je vytvoření nového certifikátu a konfiguraci ATA na použití nového certifikátu.


> [!NOTE]
> - Pokud budete ke konzole ATA přistupovat z jiných počítačů, ujistěte se, že tyto počítače důvěřují certifikátu používanému službou ATA Center jinak získáte na stránce upozornění, že došlo k potížím s certifikátem zabezpečení webu před získáním přihlašovací stránky.
> - Od verze ATA verze 1.8 komponenty ATA Gateway a Lightweight Gateway spravujete vlastní certifikáty a potřebovat zásahu správce spravovat.

## <a name="ata-gateway-requirements"></a>Požadavky na ATA Gateway
V této části je uveden seznam požadavků pro ATA Gateway.
### <a name="general"></a>Obecné
ATA Gateway podporuje instalaci na serveru s Windows Serverem 2012 R2 nebo Windows Serverem 2016 (včetně jádra serveru).
ATA Gateway se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.
ATA Gateway můžete použít k monitorování řadičů domény pomocí funkční úrovně domény v systému Windows 2003 a novějším.

Před instalací ATA Gateway do systému Windows Server 2012 R2 zkontrolujte, jestli je nainstalovaná aktualizace [KB2919355](https://support.microsoft.com/kb/2919355/).

Toto ověření můžete provést spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.


Informace o používání virtuálních počítačů se službou ATA Gateway najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md).

> [!NOTE]
> Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. To zahrnuje prostor potřebný pro binárních souborů ATA, [protokoly ATA, a [protokolování výkonu](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Specifikace serveru
K zajištění optimálního výkonu nastavte **možnost napájení**  pro ATA Gateway na hodnotu **Vysoký výkon**.<br>
ATA Gateway může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů z a do řadičů domény.

>[!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

Další informace o požadavcích na hardware ATA Gateway najdete v tématu [plánování kapacity ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace
Server ATA Center, servery ATA Gateway a řadiče domény musí mít časově synchronizované intervalu než pět minut.

### <a name="network-adapters"></a>Síťové adaptéry
ATA Gateway vyžaduje nejméně jen adaptér pro správu a jeden adaptér pro zachytávání:

-   **Adaptér pro správu** – používá pro komunikaci ve vaší podnikové síti. Tento adaptér by měl být nakonfigurován s následujícím nastavením:

    -   Statická IP adresa včetně výchozí brány

    -   Upřednostňovaný a alternativní server DNS

    -   **Příponou DNS pro toto připojení** by pro každou monitorovanou doménu měl být její název DNS.

        ![Konfigurace přípony DNS v rozšířeném nastavení protokolu TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Pokud je ATA Gateway členem domény, může konfigurace proběhnout automaticky.

-   **Adaptér pro zachytávání** se použije pro zachycení přenosu dat z a do řadičů domény.

    > [!IMPORTANT]
    > -   Nakonfigurujte zrcadlení portů pro adaptér pro zachytávání jako cíl síťového provozu řadiče domény. Další informace najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md). Obvykle musíte spolupracovat s týmem podpory sítí nebo virtualizace konfigurace zrcadlení portů.
    > -   Pro vaše prostředí nakonfigurujte statickou nepřesměrovatelnou IP adresu bez výchozí brány a adresy serveru DNS. Příklad: 1.1.1.1/32. To zajišťuje, že síťového adaptéru pro zachytávání může zachytit maximální objem přenášených dat a že síťový adaptér pro správu se používá k odesílání a příjmu požadované síťové komunikace.

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, u kterých ATA Gateway vyžaduje, aby byly nakonfigurované na adaptéru pro správu:

|Protokol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP a UDP|389|Řadiče domény|Odchozí|
|Zabezpečený LDAP (LDAPS)|TCP|636|Řadiče domény|Odchozí|
|LDAP pro globální katalog|TCP|3268|Řadiče domény|Odchozí|
|LDAPS pro globální katalog|TCP|3269|Řadiče domény|Odchozí|
|Kerberos|TCP a UDP|88|Řadiče domény|Odchozí|
|Netlogon|TCP a UDP|445|Řadiče domény|Odchozí|
|Čas Windows|UDP|123|Řadiče domény|Odchozí|
|DNS|TCP a UDP|53|Servery DNS|Odchozí|
|NTLM přes RPC|TCP|135|Všechna zařízení v síti|Odchozí|
|NetBIOS|UDP|137|Všechna zařízení v síti|Odchozí|
|SSL|TCP|443 nebo podle konfigurace pro službu Center|ATA Center:<br /><br />– IP adresa pro službu Center<br />- IP adresa konzoly|Odchozí|
|Syslog (volitelné)|UDP|514|Server SIEM|Příchozí|

> [!NOTE]
> V rámci procesu překladu, který provádí ATA Gateway, musí být na zařízeních v síti následující porty otevřené pro příjem dat z ATA Gateway.
>
> -   NTLM přes RPC (port TCP 135)
> -   NetBIOS (port UDP 137)

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
> Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. To zahrnuje prostor potřebný pro binárních souborů ATA, [protokoly ATA, a [protokolování výkonu](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Specifikace serveru

ATA Lightweight Gateway vyžaduje minimálně dvě jádra a 6 GB paměti RAM nainstalované na řadiči domény.
K zajištění optimálního výkonu nastavte **možnost napájení**  pro ATA Lightweight Gateway na hodnotu **Vysoký výkon**.
Komponenta ATA Lightweight Gateway se dá nasadit na řadiče domény s různým zatížením i velikostí, v závislosti na objemu síťového přenosu dat do a z řadiče domény a na počtu prostředků, které jsou na příslušném řadiči domény nainstalované.

>[!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

Další informace o požadavcích na hardware ATA Lightweight Gateway najdete v tématu [plánování kapacity ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace
Server ATA Center, servery ATA Lightweight Gateway a řadiče domény musí mít časově synchronizované intervalu než pět minut.
### <a name="network-adapters"></a>Síťové adaptéry
ATA Lightweight Gateway monitoruje místní provoz na všech síťových adaptérech příslušného řadiče domény. <br>
Po nasazení můžete pomocí konzoly ATA případně změnit, které síťové adaptéry se monitorují.

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, které ATA Lightweight Gateway vyžaduje:

|Protokol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP a UDP|53|Servery DNS|Odchozí|
|NTLM přes RPC|TCP|135|Všechna zařízení v síti|Odchozí|
|NetBIOS|UDP|137|Všechna zařízení v síti|Odchozí|
|SSL|TCP|443 nebo podle konfigurace pro službu Center|ATA Center:<br /><br />– IP adresa pro službu Center<br />- IP adresa konzoly|Odchozí|
|Syslog (volitelné)|UDP|514|Server SIEM|Příchozí|

> [!NOTE]
> V rámci procesu překladu, který provádí ATA Lightweight Gateway, musí být na zařízeních v síti následující porty otevřené pro příjem dat z ATA Lightweight Gateway.
>
> -   NTLM přes RPC
> -   NetBIOS

## <a name="ata-console"></a>Konzola ATA
Přístup ke konzole ATA je prostřednictvím prohlížeče, podpora prohlížeče a nastavení:

-   Internet Explorer verze 10 a novější

-   Microsoft Edge

-   Google Chrome 40 a novější

-   Minimální rozlišení obrazovky na šířku 1 700 pixelů

## <a name="related-videos"></a>Související videa
- [Výběr správné typu ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Architektura ATA](ata-architecture.md)
- [Instalace ATA](install-ata-step1.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



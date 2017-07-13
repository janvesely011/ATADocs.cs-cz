---
title: "Požadavky Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Popisuje požadavky pro úspěšné nasazení ATA ve vašem prostředí."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b810d066c59ea4663157027894eb7e2a39f7ff14
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/05/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# Požadavky ATA
<a id="ata-prerequisites" class="xliff"></a>
Tento článek popisuje požadavky pro úspěšné nasazení ATA ve vašem prostředí.

>[!NOTE]
> Informace týkající se plánování prostředků a kapacity najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md).


Řešení ATA se skládá z těchto komponent: ATA Center, ATA Gateway a/nebo ATA Lightweight Gateway. Další informace o komponentách ATA najdete v tématu [Architektura ATA](ata-architecture.md).

Systém ATA funguje na hranici doménové struktury ve službě Active Directory a podporuje funkční úroveň doménové struktury (FFL) v systémech Windows 2003 a novějších.


[Než začnete](#before-you-start): V této části jsou uvedené informace, které byste měli získat, a účty a síťové entity, které byste měli mít před zahájením instalace ATA.

[ATA Center](#ata-center-requirements): V této části jsou uvedené požadavky komponenty ATA Center na hardware a software a taky nastavení, která musíte nakonfigurovat na příslušném serveru ATA Center.

[ATA Gateway](#ata-gateway-requirements): V této části jsou uvedené požadavky komponenty ATA Gateway na hardware a software a taky nastavení, která musíte nakonfigurovat na příslušné servery ATA Gateway.

[ATA Lightweight Gateway](#ata-lightweight-gateway-requirements): V této části jsou uvedené požadavky komponenty ATA Lightweight Gateway na hardware a software.

[Konzola ATA](#ata-console): V této části jsou uvedené požadavky na prohlížeč pro spuštění konzoly ATA.

![Diagram architektury ATA](media/ATA-architecture-topology.jpg)

## Než začnete
<a id="before-you-start" class="xliff"></a>
V této části jsou uvedené informace, které byste měli získat, a účty a síťové entity, které byste měli mít před zahájením instalace ATA.


-   Uživatelský účet a heslo s přístupem pro čtení ke všem objektům v doménách, které se budou monitorovat.

    > [!NOTE]
    > Pokud jste pro různé organizační jednotky (OU) ve vaší doméně nastavili vlastní seznamy ACL, ujistěte se, že vybraný uživatel má pro tyto organizační jednotky oprávnění ke čtení.

-   Neinstalujte na ATA Gateway ani Lightweight Gateway nástroj Microsoftu Message Analyzer. Ovladač nástroje Message Analyzer koliduje s ovladači komponent ATA Gateway a Lightweight Gateway. Pokud na komponentě ATA Gateway spustíte Wireshark a následně zastavíte jeho zachytávání, budete muset restartovat službu Microsoft Advanced Threat Analytics Gateway. Když to neuděláte, nebude brána zachytávat žádný provoz. Wireshark běžící na komponentě ATA Lightweight Gateway nijak nenarušuje její činnost.

-    Doporučené: Uživatel by měl mít ke kontejneru odstraněných objektů oprávnění jen pro čtení. Díky tomu dokáže ATA detekovat hromadné odstranění objektů v doméně. Informace o konfiguraci oprávnění jen pro čtení pro kontejner odstraněných objektů najdete v části **Změna oprávnění pro kontejner odstraněných objektů** v tématu [Zobrazení nebo nastavení oprávnění pro objekt adresáře](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Volitelné: Uživatelský účet uživatele, který nemá žádné síťové aktivity. Tento účet se nakonfiguruje jako uživatel honeytokenu ATA. Ke konfiguraci uživatele honeytokenu budete potřebovat SID účtu uživatele, nikoli jeho uživatelské jméno. Další informace najdete v tématu [Práce s nastavením detekce ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/deploy-use/working-with-detection-settings).

-   Volitelné: Kromě shromažďování a analýzy síťového provozu na řadičích domén může ATA pomocí událostí Windows 4776, 4732, 4733, 4728, 4729, 4756 a 4757 dál vylepšit detekce předání hodnoty hash, hrubé síly a úpravy citlivých skupin a honeytokenů. Tyto události mohou být přijímány ze služby SIEM nebo nastavením předávání událostí Windows z řadiče domény. Shromážděné události poskytují řešení ATA další informace, které není možné zjistit z monitorování provozu na řadiči domény.


## Požadavky pro ATA Center
<a id="ata-center-requirements" class="xliff"></a>
V této části je uveden seznam požadavků pro ATA Center.
### Obecné
<a id="general" class="xliff"></a>
ATA Center podporuje instalaci na serveru s Windows Serverem 2012 R2 nebo Windows Serverem 2016. ATA Center se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.

Před instalací součásti ATA Center do systému Windows Server 2012 R2 zkontrolujte, jestli je nainstalovaná aktualizace [KB2919355](https://support.microsoft.com/kb/2919355/).

Toto ověření můžete provést spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.

Instalace komponenty ATA Center jako virtuálního počítače se podporuje. 

>[!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

Pokud ATA Center spouštíte jako virtuální počítač, před vytvořením nového kontrolního bodu vypněte server. Vyhnete se tak možnému poškození databází.
### Specifikace serveru
<a id="server-specifications" class="xliff"></a>
Při práci na fyzickém serveru databáze ATA vyžaduje, abyste v systému BIOS **zakázali** neuniformní přístup k paměti (NUMA). Ve vašem systému se NUMA může označovat také jako prokládání uzlů. V takovém případě bude potřeba prokládání uzlů **povolit**, abyste NUMA zakázali. Další informace najdete v dokumentaci k systému BIOS. Pokud ATA Center běží na virtuálním serveru, není tento text relevantní.<br>
K zajištění optimálního výkonu nastavte **možnost napájení**  pro ATA Center na hodnotu **Vysoký výkon**.<br>
Počet řadičů domény, které monitorujete, a zatížení na jednotlivých řadičích určuje potřebnou specifikaci serveru. Další informace najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md).


### Časová synchronizace
<a id="time-synchronization" class="xliff"></a>
Server ATA Center, servery ATA Gateway a řadiče domény musí být vzájemně časově synchronizované (s tolerancí 5 minut).


### Síťové adaptéry
<a id="network-adapters" class="xliff"></a>
Měli byste mít:
-   Alespoň jeden síťový adaptér (pokud používáte fyzický server v prostředí sítě VLAN, doporučujeme použít dva síťové adaptéry)

-   Dvě IP adresy (doporučuje se, ale nevyžaduje)

Komunikace mezi komponentami ATA Center a ATA Gateway je zašifrovaná pomocí SSL na portu 443. Kromě toho konzole ATA také používá protokol SSL na portu 443. Doporučují se **dvě IP adresy**. Služba ATA Center vytvoří vazbu mezi portem 443 a první IP adresou a konzole ATA vytvoří vazbu mezi portem 443 a druhou IP adresou.

> [!NOTE]
> Může se použít jedna IP adresa se dvěma různými porty, ale doporučuje se použití dvou IP adres.

### Porty
<a id="ports" class="xliff"></a>
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
|**Čas Windows** (volitelné při připojení k doméně)|UDP|123|Řadiče domény|Odchozí|

### Certifikáty
<a id="certificates" class="xliff"></a>
Zkontrolujte, jestli ATA Center má přístup k distribučnímu bodu CRL. Pokud služby ATA Gateway nemají přístup k internetu, použijte [ruční import seznamu CRL](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx) a dbejte na to, abyste nainstalovali všechny distribuční body CRL pro celý řetězec.

K usnadnění instalace ATA můžete během instalace nainstalovat certifikáty podepsané jejich držiteli. Po nasazení můžete certifikát podepsaný svým držitelem nahradit certifikátem certifikační autority, který bude používat ATA Gateway.<br>
> [!NOTE]
> Jako typ zprostředkovatele certifikátu můžete použít zprostředkovatele kryptografických služeb (CSP) nebo zprostředkovatele úložiště klíčů (KSP).


> Použití automatického obnovení certifikátu není podporované.


> [!NOTE]
> Pokud budete ke konzole ATA přistupovat z jiných počítačů, zkontrolujte, že tyto počítače důvěřují certifikátu používanému konzolou ATA, jinak se před ještě zobrazením přihlašovací stránky zobrazí upozornění, že došlo k potížím s certifikátem zabezpečení webu.

## Požadavky na ATA Gateway
<a id="ata-gateway-requirements" class="xliff"></a>
V této části je uveden seznam požadavků pro ATA Gateway.
### Obecné
<a id="general" class="xliff"></a>
ATA Gateway podporuje instalaci na serveru s Windows Serverem 2012 R2 nebo Windows Serverem 2016 (včetně jádra serveru).
ATA Gateway se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.
ATA Gateway můžete použít k monitorování řadičů domény pomocí funkční úrovně domény v systému Windows 2003 a novějším.

Před instalací ATA Gateway do systému Windows Server 2012 R2 zkontrolujte, jestli je nainstalovaná aktualizace [KB2919355](https://support.microsoft.com/kb/2919355/).

Toto ověření můžete provést spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.


Informace o používání virtuálních počítačů se službou ATA Gateway najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md).

> [!NOTE]
> Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. Zahrnuje to prostor potřebný pro binární soubory ATA, [protokoly ATA](troubleshooting-ata-using-logs.md) a [protokoly výkonu](troubleshooting-ata-using-perf-counters.md).

### Specifikace serveru
<a id="server-specifications" class="xliff"></a>
K zajištění optimálního výkonu nastavte **možnost napájení**  pro ATA Gateway na hodnotu **Vysoký výkon**.<br>
ATA Gateway může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů z a do řadičů domény.

>[!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

Další informace o hardwarových požadavcích ATA Gateway najdete v článku [Plánování kapacity ATA](ata-capacity-planning.md).

### Časová synchronizace
<a id="time-synchronization" class="xliff"></a>
Server ATA Center, servery ATA Gateway a řadiče domény musí být vzájemně časově synchronizované (s tolerancí 5 minut).

### Síťové adaptéry
<a id="network-adapters" class="xliff"></a>
ATA Gateway vyžaduje nejméně jen adaptér pro správu a jeden adaptér pro zachytávání:

-   **Adaptér pro správu** se použije pro komunikace ve vaší firemní síti. Pro tento adaptér by měly být nakonfigurované tyto parametry:

    -   Statická IP adresa včetně výchozí brány

    -   Upřednostňovaný a alternativní server DNS

    -   **Příponou DNS pro toto připojení** by pro každou monitorovanou doménu měl být její název DNS.

        ![Konfigurace přípony DNS v rozšířeném nastavení protokolu TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Pokud je ATA Gateway členem domény, může konfigurace proběhnout automaticky.

-   **Adaptér pro zachytávání** se použije pro zachycení přenosu dat z a do řadičů domény.

    > [!IMPORTANT]
    > -   Nakonfigurujte zrcadlení portů pro adaptér pro zachytávání jako cíl síťového provozu řadiče domény. Další informace najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md). Při konfiguraci zrcadlení portů budete obvykle spolupracovat s týmem pro sítě nebo virtualizace.
    > -   Pro vaše prostředí nakonfigurujte statickou nepřesměrovatelnou IP adresu bez výchozí brány a adresy serveru DNS. Příklad: 1.1.1.1/32. Zajistíte tak, že síťový adaptér pro zachytávání může zachytit maximální objem přenášených dat a síťový adaptér pro správu se bude používat k odesílání a příjmu požadované síťové komunikace.

### Porty
<a id="ports" class="xliff"></a>
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

## Požadavky pro ATA Lightweight Gateway
<a id="ata-lightweight-gateway-requirements" class="xliff"></a>
V této části je uveden seznam požadavků pro ATA Lightweight Gateway.
### Obecné
<a id="general" class="xliff"></a>
ATA Lightweight Gateway podporuje instalaci na řadičích domény se systémem Windows Server 2008 R2 SP1 (kromě jádra serveru), Windows Server 2012, Windows Server 2012 R2 nebo Windows Server 2016 (včetně jádra, ale ne Nano).

Řadičem domény může být řadič domény jen pro čtení (RODC).

Před instalací ATA Lightweight Gateway na řadiči domény se systémem Windows Server 2012 R2 ověřte, že je nainstalovaná aktualizace [KB2919355](https://support.microsoft.com/kb/2919355/).

Můžete to ověřit spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.

Pokud se instalace provádí pro Windows Server 2012 R2 Server Core, musí být nainstalovaná také následující aktualizace: [KB3000850](https://support.microsoft.com/help/3000850/november-2014-update-rollup-for-windows-rt-8.1%2c-windows-8.1%2c-and-windows-server-2012-r2).

 Můžete to ověřit spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb3000850]`.


Během instalace se nainstaluje rozhraní .Net Framework 4.6.1 a může dojít k restartování řadiče domény.


> [!NOTE]
> Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. Zahrnuje to prostor potřebný pro binární soubory ATA, [protokoly ATA](troubleshooting-ata-using-logs.md) a [protokoly výkonu](troubleshooting-ata-using-perf-counters.md).

### Specifikace serveru
<a id="server-specifications" class="xliff"></a>

ATA Lightweight Gateway vyžaduje nejméně 2 jádra a 6 GB paměti RAM nainstalované na řadiči domény.
K zajištění optimálního výkonu nastavte **možnost napájení**  pro ATA Lightweight Gateway na hodnotu **Vysoký výkon**.
Komponenta ATA Lightweight Gateway se dá nasadit na řadiče domény s různým zatížením i velikostí, v závislosti na objemu síťového přenosu dat do a z řadiče domény a na počtu prostředků, které jsou na příslušném řadiči domény nainstalované.

>[!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

Další informace o hardwarových požadavcích ATA Lightweight Gateway najdete v článku [Plánování kapacity ATA](ata-capacity-planning.md).

### Časová synchronizace
<a id="time-synchronization" class="xliff"></a>
Server ATA Center, servery ATA Lightweight Gateway a řadiče domény musí být vzájemně časově synchronizované (s tolerancí 5 minut).
### Síťové adaptéry
<a id="network-adapters" class="xliff"></a>
ATA Lightweight Gateway monitoruje místní provoz na všech síťových adaptérech příslušného řadiče domény. <br>
Po nasazení můžete pomocí konzoly ATA případně změnit, které síťové adaptéry se monitorují.

### Porty
<a id="ports" class="xliff"></a>
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

## Konzola ATA
<a id="ata-console" class="xliff"></a>
Přístup ke konzole ATA je prostřednictvím prohlížeče. Podporují se tyto:

-   Internet Explorer verze 10 a novější

-   Microsoft Edge

-   Google Chrome 40 a novější

-   Minimální rozlišení obrazovky na šířku 1 700 pixelů

## Viz také
<a id="see-also" class="xliff"></a>

- [Architektura ATA](ata-architecture.md)
- [Instalace ATA](install-ata-step1.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



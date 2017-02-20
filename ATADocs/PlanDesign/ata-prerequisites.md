---
title: "Požadavky Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Popisuje požadavky pro úspěšné nasazení ATA ve vašem prostředí."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/16/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f61bbb895e4a2f239f91328f8d8b2b5260452cc2
ms.openlocfilehash: 764d20fd113b8d40d359a8976c175e889f554dba


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="ata-prerequisites"></a>Požadavky ATA
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

## <a name="before-you-start"></a>Než začnete
V této části jsou uvedené informace, které byste měli získat, a účty a síťové entity, které byste měli mít před zahájením instalace ATA.


-   Uživatelský účet a heslo s přístupem pro čtení ke všem objektům v doménách, které se budou monitorovat.

    > [!NOTE]
    > Pokud jste pro různé organizační jednotky (OU) ve vaší doméně nastavili vlastní seznamy ACL, ujistěte se, že vybraný uživatel má pro tyto organizační jednotky oprávnění ke čtení.

-   Zkontrolujte, jestli na počítačích se součástmi ATA Gateway není nainstalovaný Message Analyzer nebo Wire Shark.
-    Doporučené: Uživatel by měl mít ke kontejneru odstraněných objektů oprávnění jen pro čtení. Díky tomu dokáže ATA detekovat hromadné odstranění objektů v doméně. Informace o konfiguraci oprávnění jen pro čtení pro kontejner odstraněných objektů najdete v části **Změna oprávnění pro kontejner odstraněných objektů** v tématu [Zobrazení nebo nastavení oprávnění pro objekt adresáře](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Volitelné: Uživatelský účet uživatele, který nemá žádné síťové aktivity. Tento účet se nakonfiguruje jako uživatel honeytokenu ATA. Ke konfiguraci uživatele honeytokenu budete potřebovat SID účtu uživatele, nikoli jeho uživatelské jméno. Další informace najdete v tématu [Práce s nastavením detekce ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/deploy-use/working-with-detection-settings).

-   Volitelné: Kromě shromažďování a analýzy síťových přenosů z a do řadičů domény může ATA využít událost 4776 systému Windows k dalšímu vylepšení detekce útoků Pass-the-Hash. Tato událost může být přijata ze služby SIEM nebo nastavením předávání událostí systému Windows z řadiče domény. Shromážděné události poskytují řešení ATA další informace, které není možné zjistit z monitorování provozu na řadiči domény.


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
Při práci na fyzickém serveru databáze ATA vyžaduje, abyste v systému BIOS **zakázali** neuniformní přístup k paměti (NUMA). Ve vašem systému se NUMA může označovat také jako prokládání uzlů. V takovém případě bude potřeba prokládání uzlů **povolit**, abyste NUMA zakázali. Další informace najdete v dokumentaci k systému BIOS. Pokud ATA Center běží na virtuálním serveru, není tento text relevantní.<br>
K zajištění optimálního výkonu nastavte **možnost napájení ** pro ATA Center na hodnotu **Vysoký výkon**.<br>
Počet řadičů domény, které monitorujete, a zatížení na jednotlivých řadičích určuje potřebnou specifikaci serveru. Další informace najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md).


### <a name="time-synchronization"></a>Časová synchronizace
Server ATA Center, servery ATA Gateway a řadiče domény musí být vzájemně časově synchronizované (s tolerancí 5 minut).


### <a name="network-adapters"></a>Síťové adaptéry
Měli byste mít:
-   Alespoň jeden síťový adaptér (pokud používáte fyzický server v prostředí sítě VLAN, doporučujeme použít dva síťové adaptéry)

-   Dvě IP adresy (doporučuje se, ale nevyžaduje)

Komunikace mezi komponentami ATA Center a ATA Gateway je zašifrovaná pomocí SSL na portu 443. Kromě toho konzole ATA také používá protokol SSL na portu 443. Doporučují se **dvě IP adresy**. Služba ATA Center vytvoří vazbu mezi portem 443 a první IP adresou a konzole ATA vytvoří vazbu mezi portem 443 a druhou IP adresou.

> [!NOTE]
> Může se použít jedna IP adresa se dvěma různými porty, ale doporučuje se použití dvou IP adres.

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, které musí být otevřené, aby služba ATA Center fungovala správně.

V této tabulce je IP adresa 1 svázaná se součástí ATA Center a IP adresa 2 je svázaná s konzolou ATA:

|Protokol|Přenos|Port|Směr|Direction|IP adresa|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (komunikace ATA)|TCP|443 nebo konfigurovatelné|ATA Gateway|Příchozí|IP adresa 1|
|**HTTP**|TCP|80|Podniková síť|Příchozí|IP adresa 2|
|**HTTPS**|TCP|443|Podniková síť a ATA Gateway|Příchozí|IP adresa 2|
|**SMTP** (volitelné)|TCP|25|Server SMTP|Odchozí|IP adresa 2|
|**SMTPS** (volitelné)|TCP|465|Server SMTP|Odchozí|IP adresa 2|
|**Syslog** (volitelné)|TCP|514|Server syslog|Odchozí|IP adresa 2|

### <a name="certificates"></a>Certifikáty
Zkontrolujte, jestli ATA Center má přístup k distribučnímu bodu CRL. Pokud služby ATA Gateway nemají přístup k internetu, použijte [ruční import seznamu CRL](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx) a dbejte na to, abyste nainstalovali všechny distribuční body CRL pro celý řetězec.

K usnadnění instalace ATA můžete během instalace nainstalovat certifikáty podepsané jejich držiteli. Po nasazení můžete certifikát podepsaný svým držitelem nahradit certifikátem certifikační autority, který bude používat ATA Gateway.<br>
> [!NOTE]
> Poskytovatelem certifikátu musí být zprostředkovatel kryptografických služeb (CPS).


> Použití automatického obnovení certifikátu není podporované.


> [!NOTE]
> Pokud budete ke konzole ATA přistupovat z jiných počítačů, zkontrolujte, že tyto počítače důvěřují certifikátu používanému konzolou ATA, jinak se před ještě zobrazením přihlašovací stránky zobrazí upozornění, že došlo k potížím s certifikátem zabezpečení webu.

## <a name="ata-gateway-requirements"></a>Požadavky na ATA Gateway
V této části je uveden seznam požadavků pro ATA Gateway.
### <a name="general"></a>Obecné
ATA Gateway podporuje instalaci na serveru s Windows Serverem 2012 R2 nebo Windows Serverem 2016 (včetně jádra serveru).
ATA Gateway se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.
ATA Gateway můžete použít k monitorování řadičů domény pomocí funkční úrovně domény v systému Windows 2003 a novějším.

Před instalací ATA Gateway do systému Windows Server 2012 R2 zkontrolujte, jestli je nainstalovaná aktualizace [KB2919355](https://support.microsoft.com/kb/2919355/).

Toto ověření můžete provést spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.

Informace o používání virtuálních počítačů se službou ATA Gateway najdete v tématu [Konfigurace zrcadlení portů](/advanced-threat-analytics/deploy-use/configure-port-mirroring).

> [!NOTE]
> Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. Zahrnuje to prostor potřebný pro binární soubory ATA, [protokoly ATA](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-logs) a [protokoly výkonu](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-perf-counters).

### <a name="server-specifications"></a>Specifikace serveru
K zajištění optimálního výkonu nastavte **možnost napájení ** pro ATA Gateway na hodnotu **Vysoký výkon**.<br>
ATA Gateway může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů z a do řadičů domény.

>[!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

Další informace o hardwarových požadavcích ATA Gateway najdete v článku [Plánování kapacity ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace
Server ATA Center, servery ATA Gateway a řadiče domény musí být vzájemně časově synchronizované (s tolerancí 5 minut).

### <a name="network-adapters"></a>Síťové adaptéry
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
    > -   Nakonfigurujte zrcadlení portů pro adaptér pro zachytávání jako cíl síťového provozu řadiče domény. Další informace najdete v tématu [Konfigurace zrcadlení portů](/advanced-threat-analytics/deploy-use/configure-port-mirroring). Při konfiguraci zrcadlení portů budete obvykle spolupracovat s týmem pro sítě nebo virtualizace.
    > -   Pro vaše prostředí nakonfigurujte statickou nepřesměrovatelnou IP adresu bez výchozí brány a adresy serveru DNS. Příklad: 1.1.1.1/32. Zajistíte tak, že síťový adaptér pro zachytávání může zachytit maximální objem přenášených dat a síťový adaptér pro správu se bude používat k odesílání a příjmu požadované síťové komunikace.

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

### <a name="certificates"></a>Certifikáty
Zkontrolujte, jestli ATA Center má přístup k distribučnímu bodu CRL. Pokud komponenty ATA Gateway nemají přístup k internetu, použijte ruční import seznamu CRL a dbejte na to, abyste nainstalovali všechny distribuční body CRL pro celý řetězec.<br>
K usnadnění instalace ATA můžete během instalace nainstalovat certifikáty podepsané jejich držiteli. Po nasazení můžete certifikát podepsaný svým držitelem nahradit certifikátem certifikační autority, který bude používat ATA Gateway.

> [!NOTE]
> Poskytovatelem certifikátu musí být zprostředkovatel kryptografických služeb (CPS).<br>

V úložišti Počítač služby ATA Gateway v úložišti Místní počítač musí být nainstalovaný certifikát podporující **ověření serveru**. Tento certifikát musí být pro ATA Center důvěryhodný.

## <a name="ata-lightweight-gateway-requirements"></a>Požadavky pro ATA Lightweight Gateway
V této části je uveden seznam požadavků pro ATA Lightweight Gateway.
### <a name="general"></a>Obecné
ATA Lightweight Gateway podporuje instalaci na řadičích domény se systémem Windows Server 2008 R2 SP1 (kromě jádra serveru), Windows Server 2012, Windows Server 2012 R2 nebo Windows Server 2016 (včetně jádra, ale ne Nano).

Řadičem domény může být řadič domény jen pro čtení (RODC).

Před instalací ATA Lightweight Gateway na řadiči domény se systémem Windows Server 2012 R2 ověřte, že je nainstalovaná aktualizace [KB2919355](https://support.microsoft.com/kb/2919355/).

Můžete to ověřit spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.

Pokud se instalace provádí pro Windows Server 2012 R2 Server Core, musí být nainstalovaná také následující aktualizace:  [KB3000850](https://support.microsoft.com/help/3000850/november-2014-update-rollup-for-windows-rt-8.1%2c-windows-8.1%2c-and-windows-server-2012-r2).

 Můžete to ověřit spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb3000850]`.

> [!NOTE]
> Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. Zahrnuje to prostor potřebný pro binární soubory ATA, [protokoly ATA](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-logs.md) a [protokoly výkonu](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Specifikace serveru

ATA Lightweight Gateway vyžaduje nejméně 2 jádra a 6 GB paměti RAM nainstalované na řadiči domény.
K zajištění optimálního výkonu nastavte **možnost napájení ** pro ATA Lightweight Gateway na hodnotu **Vysoký výkon**.
Komponenta ATA Lightweight Gateway se dá nasadit na řadiče domény s různým zatížením i velikostí, v závislosti na objemu síťového přenosu dat do a z řadiče domény a na počtu prostředků, které jsou na příslušném řadiči domény nainstalované.

>[!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

Další informace o hardwarových požadavcích ATA Lightweight Gateway najdete v článku [Plánování kapacity ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace
Server ATA Center, servery ATA Lightweight Gateway a řadiče domény musí být vzájemně časově synchronizované (s tolerancí 5 minut).
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

### <a name="certificates"></a>Certifikáty
Zkontrolujte, jestli ATA Center má přístup k distribučnímu bodu CRL. Pokud komponenty ATA Lightweight Gateway nemají přístup k internetu, použijte ruční import seznamu CRL a dbejte na to, abyste nainstalovali všechny distribuční body CRL pro celý řetězec.
K usnadnění instalace ATA můžete během instalace nainstalovat certifikáty podepsané jejich držiteli. Po nasazení můžete certifikát podepsaný svým držitelem nahradit certifikátem certifikační autority, který bude používat ATA Lightweight Gateway.
> [!NOTE]
> Poskytovatelem certifikátu musí být zprostředkovatel kryptografických služeb (CPS).

V úložišti Počítač služby ATA Lightweight Gateway v úložišti Místní počítač musí být nainstalovaný certifikát podporující ověření serveru. Tento certifikát musí být pro ATA Center důvěryhodný.

## <a name="ata-console"></a>Konzola ATA
Přístup ke konzole ATA je prostřednictvím prohlížeče. Podporují se tyto:

-   Internet Explorer verze 10 a novější

-   Microsoft Edge

-   Google Chrome 40 a novější

-   Minimální rozlišení obrazovky na šířku 1 700 pixelů

## <a name="see-also"></a>Viz také

- [Architektura ATA](ata-architecture.md)
- [Instalace ATA](/advanced-threat-analytics/deploy-use/install-ata)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)





<!--HONumber=Feb17_HO3-->



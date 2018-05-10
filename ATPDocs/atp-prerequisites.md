---
title: Požadavky Azure Advanced Threat Protection | Microsoft Docs
description: Popisuje požadavky pro úspěšné nasazení Azure ATP ve vašem prostředí
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/8/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ae859121fbe856c93b8568ef38bf0b4bdb77837a
ms.sourcegitcommit: 8472f3f46fc90da7471cd1065cdb2f6a1d5a9f69
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/08/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="azure-atp-prerequisites"></a>Požadavky Azure ATP
Tento článek popisuje požadavky pro úspěšné nasazení Azure ATP ve vašem prostředí.

>[!NOTE]
> Informace týkající se plánování prostředků a kapacity najdete v tématu [plánování kapacity Azure ATP](atp-capacity-planning.md).


Azure ATP se skládá z cloudové služby Azure ATP, který se skládá z portálu pro správu prostoru a portálu pracovního prostoru, senzoru samostatné Azure ATP a Azure ATP senzoru. Další informace o komponentách Azure ATP najdete v tématu [Azure ATP architektura](atp-architecture.md).

Každý pracovní prostor Azure ATP podporuje hranice doménové struktury Active Directory a doménovou strukturu funkční úroveň (FFL) systému Windows 2003 a vyšší. U nasazení s více doménovými strukturami samostatné prostoru Azure ATP se vyžaduje pro každou doménovou strukturu.


[Před zahájením](#before-you-start): Tato část obsahuje informace, které byste měli získat a účty a síťové entity, které byste měli mít před zahájením instalace Azure ATP.

[Azure portálu pro správu prostoru ATP](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): Tato část popisuje požadavky na pracovní prostor Správa portálu prohlížeče.

[Portál Azure prostoru ATP](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): Tato část popisuje požadavky na prohlížeč pro spuštění portálu Azure ATP pracovního prostoru.

[Azure senzor samostatné ATP](#azure-atp-sensor-requirements): Tato část uvádí Azure ATP samostatné senzor hardware, požadavky na software a taky nastavení budete muset nakonfigurovat na serverech Azure ATP samostatné senzor.

[Azure senzor ATP](#azure-atp-lightweight-sensor-requirements): Tato část obsahuje Azure ATP senzor hardwaru a požadavky na software.

![Diagram architektury Azure ATP](media/ATP-architecture-topology.png)

## <a name="before-you-start"></a>Než začnete
Tato část obsahuje informace, které byste měli získat a účty a síťové entity, které byste měli mít před zahájením instalace Azure ATP.


-   **Místní** AD uživatelský účet a heslo s přístupem pro čtení pro všechny objekty v monitorovaném domén.

    > [!NOTE]
    > Pokud jste pro různé organizační jednotky (OU) ve vaší doméně nastavili vlastní seznamy ACL, ujistěte se, že vybraný uživatel má pro tyto organizační jednotky oprávnění ke čtení.

-   Pokud spustíte Wireshark na samostatné senzor Azure ATP, musíte po je nutné zastavit zachycení Wireshark restartovat senzoru Azure Advanced Threat Protection Service. Pokud ne, senzoru zastaví zachycení provozu.

- Pokud se pokusíte nainstalovat senzoru ATP na počítači nakonfigurované s adaptérem seskupování síťových adaptérů, obdržíte chybu instalace. Pokud chcete nainstalovat senzoru ATP na počítači nakonfigurovaná se Seskupováním síťových adaptérů, obraťte se na zástupce podpory Azure ATP.

-    Doporučujeme: Uživatel by měl mít oprávnění jen pro čtení v kontejneru odstraněné objekty. To umožňuje Azure ATP detekovat hromadné odstranění objektů v doméně. Informace o konfiguraci oprávnění jen pro čtení pro kontejner odstraněných objektů najdete v tématu **Změna oprávnění pro kontejner odstraněných objektů** tématu [zobrazení nebo nastavení oprávnění pro objekt adresáře](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) článku.

-   Volitelné: Uživatelský účet uživatele, který nemá žádné síťové aktivity. Tento účet je nakonfigurovaný jako uživatel Honeytokenu ATP Azure. Další informace najdete v tématu [konfigurovat vyloučení a uživatele Honeytokenu](install-atp-step7.md).

-   Volitelné: Při nasazení samostatné senzoru, je nutné předávání událostí systému Windows 4776, 4732, 4733, 4728, 4729, 4756, 4757 a 7045 ATP dále vylepšit Azure ATP Pass-the-Hash, útoků hrubou silou, změny citlivých skupin, pod těmito detekce a vytvoření škodlivý služby. V Azure ATP senzoru jsou tyto události přijímány automaticky. V samostatné senzoru Azure ATP mohou tyto události přijímat z vašeho systému SIEM nebo nastavením předávání událostí systému Windows z řadiče domény. Shromážděné události poskytují Azure ATP společně s dalšími informacemi, které nejsou dostupné prostřednictvím síťových přenosů řadičů domény.


## <a name="azure-atp-workspace-management-portal-and-workspace-portal-requirements"></a>Azure ATP prostoru portálu a prostoru portálu požadavky na správu
Přístup k portálu Azure ATP prostoru a portálu pro správu prostoru Azure ATP je prostřednictvím prohlížeče. podporují se následující nastavení a prohlížeče:
-   Microsoft Edge
-   Internet Explorer verze 10 a novější
-   Google Chrome 4.0 a vyšší
-   Minimální rozlišení obrazovky na šířku 1 700 pixelů
-   Brány firewall a proxy open - ke komunikaci s cloudovou službou Azure ATP, musí mít otevřete: *. atp.azure.com port 443 brány firewall nebo proxy serveru. 

## <a name="azure-atp-standalone-sensor-requirements"></a>Požadavky Azure senzor samostatné ATP
Tato část uvádí požadavky pro Azure ATP samostatné senzoru.
### <a name="general"></a>Obecné
Senzor samostatné Azure ATP podporuje instalaci na serveru se systémem Windows Server 2012 R2 nebo Windows Server 2016 (zahrnout jádra serveru).
Senzor samostatné Azure ATP lze nainstalovat na server, který je členem domény nebo pracovní skupiny.
Senzor samostatné Azure ATP slouží k monitorování řadičů domény s domény funkční úrovni systému Windows 2003 a vyšší.

Pro řadiče domény ke komunikaci s cloudovou službou, musíte otevřít port 443 v bran firewall a proxy servery k *. atp.azure.com.


Informace o používání virtuálních počítačů s senzoru samostatné Azure ATP najdete v tématu [konfigurace zrcadlení portů](configure-port-mirroring.md).

> [!NOTE]
> Je vyžadován minimálně 5 GB místa na disku a doporučuje se 10 GB. To zahrnuje prostor potřebný pro binární soubory Azure ATP, Azure ATP protokoly a výkonu protokoly.

### <a name="server-specifications"></a>Specifikace serveru
Pro zajištění optimálního výkonu nastavte **možnost napájení** snímače samostatné Azure ATP k **vysoký výkon**.<br>
Azure ATP samostatné senzor může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů do a z řadičů domény.

>[!NOTE] 
> Když spustíte jako virtuální počítač, dynamickou paměť nebo jakékoli jiné funkce rozšiřování rozsahů stránek paměti není podporována.

Další informace o požadavcích na hardware senzor samostatné Azure ATP, najdete v části [plánování kapacity Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace

Servery a řadiče domény, na kterých je nainstalovaný senzoru musí být časově synchronizované intervalu než pět minut.


### <a name="network-adapters"></a>Síťové adaptéry
Senzor samostatné Azure ATP vyžaduje minimálně jeden adaptér pro správu a minimálně jeden adaptér pro zachytávání:

-   **Adaptér pro správu** – používá pro komunikaci ve vaší podnikové síti. Senzoru budou používat tento adaptér dotazovat řadiče domény je ochrana a překladu pro účty počítače. <br>Tento adaptér by měl být nakonfigurován s následujícím nastavením:

    -   Statická IP adresa včetně výchozí brány

    -   Upřednostňovaný a alternativní server DNS

    -   **Příponou DNS pro toto připojení** by pro každou monitorovanou doménu měl být její název DNS.

        ![Konfigurace přípony DNS v rozšířeném nastavení protokolu TCP/IP](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > Pokud samostatné senzoru Azure ATP je členem domény, může tak konfigurace automaticky.

-   **Adaptér pro zachytávání** – použité pro zachycení přenosu dat do a z řadičů domény.

    > [!IMPORTANT]
    > -   Nakonfigurujte zrcadlení portů pro adaptér pro zachytávání jako cíl síťového provozu řadiče domény. Další informace najdete v tématu [konfigurace zrcadlení portů](configure-port-mirroring.md). Obvykle musíte spolupracovat s týmem podpory sítí nebo virtualizace konfigurace zrcadlení portů.
    > -   Nakonfigurujte směrovat statickou IP adresu pro vaše prostředí s žádné výchozí senzor a žádné adresy serverů DNS. Příklad: 1.1.1.1/32. To zajišťuje, že síťového adaptéru pro zachytávání může zachytit maximální objem přenášených dat a že síťový adaptér pro správu se používá k odesílání a příjmu požadované síťové komunikace.

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, které vyžaduje samostatné senzoru Azure ATP nakonfigurované na adaptéru pro správu:

|Protokol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|**Porty Internetu**|||||
|SSL (*.atp.azure.com)|TCP|443|Cloudovou službu Azure ATP|Odchozí|
|**Interní porty**|||||
|LDAP|TCP a UDP|389|Řadiče domény|Odchozí|
|Zabezpečený LDAP (LDAPS)|TCP|636|Řadiče domény|Odchozí|
|LDAP pro globální katalog|TCP|3268|Řadiče domény|Odchozí|
|LDAPS pro globální katalog|TCP|3269|Řadiče domény|Odchozí|
|Kerberos|TCP a UDP|88|Řadiče domény|Odchozí|
|Netlogon (SMB, CIFS, SAM-R)|TCP a UDP|445|Všechna zařízení v síti|Odchozí|
|Čas Windows|UDP|123|Řadiče domény|Odchozí|
|DNS|TCP a UDP|53|Servery DNS|Odchozí|
|NTLM přes RPC|TCP|135|Všechna zařízení v síti|Odchozí|
|NetBIOS|UDP|137|Všechna zařízení v síti|Odchozí|
|Syslog (volitelné)|TCP/UDP|514, v závislosti na konfiguraci|Server SIEM|Příchozí|
|RADIUS|UDDP|1813|RADIUS|Příchozí|
|PROTOKOLU RDP|TCP|3389|Všechna zařízení v síti|Odchozí|

> [!NOTE]
> - Používáte účet uživatele adresářové služby, senzoru dotazuje koncových bodů ve vaší organizaci pro použití SAM-R (přihlášením k síti) k vytvoření místního správce [laterální pohyb cesta grafu](use-case-lateral-movement-path.md). Další informace najdete v tématu [konfigurace SAM-R požadovaná oprávnění](install-atp-step8-samr.md).
> - Musí být otevřený příchozí na zařízení v síti ze senzorů samostatné Azure ATP následující porty:
>   -   NTLM přes RPC (TCP Port 135) pro účely řešení
>   -   Pro rozhraní NetBIOS (UDP port 137) pro účely řešení
>   -   Protokol RDP (TCP port 3389), pouze první paket *Client hello*, pro účely řešení<br> Všimněte si, že na všech portech neprobíhá žádné ověřování.

## <a name="azure-atp-sensor-requirements"></a>Požadavky pro Azure senzor ATP
Tato část uvádí požadavky pro Azure ATP senzoru.
### <a name="general"></a>Obecné
Senzor Azure ATP podporuje instalaci na řadič domény se systémem Windows Server 2008 R2 SP1 (včetně není jádra serveru), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (včetně jádra, ale není Nano).

Řadič domény může být řadič domény jen pro čtení (RODC).

Pro řadiče domény ke komunikaci s cloudovou službou, musíte otevřít port 443 v bran firewall a proxy servery k *. atp.azure.com.

Během instalace rozhraní .net Framework 4.7 je nainstalován a může vyžadovat restartování řadiče domény, pokud se už čeká na restartování.


> [!NOTE]
> Je vyžadován minimálně 5 GB místa na disku a doporučuje se 10 GB. To zahrnuje prostor potřebný pro binární soubory Azure ATP, Azure ATP protokoly a výkonu protokoly.

### <a name="server-specifications"></a>Specifikace serveru

Senzor Azure ATP vyžaduje minimálně dvě jádra a 6 GB paměti RAM nainstalované na řadiči domény.
Pro zajištění optimálního výkonu nastavte **možnost napájení** snímače Azure ATP k **vysoký výkon**.
Senzor Azure ATP se dá nasadit na řadiče domény s různým zatížením i velikostí, v závislosti na objemu síťových přenosů do a z řadičů domény a objem prostředků, které jsou nainstalované na tomto řadiči domény.

>[!NOTE] 
> Když spustíte jako virtuální počítač, dynamickou paměť nebo jakékoli jiné funkce rozšiřování rozsahů stránek paměti není podporována.

Další informace o požadavcích na hardware senzor Azure ATP najdete v tématu [plánování kapacity Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace

Servery a řadiče domény, na kterých je nainstalovaný senzoru musí být časově synchronizované intervalu než pět minut.

### <a name="network-adapters"></a>Síťové adaptéry

Senzor Azure ATP monitoruje místní provoz na všech síťových adaptérech příslušného řadiče domény. <br>
Po nasazení můžete na portálu Azure ATP pracovního prostoru, pokud někdy budete chtít změnit, které síťové adaptéry se monitorují.

Senzoru není podporována na domény, řadiče se systémem Windows 2008 R2 s Broadcom seskupování síťových adaptérů povoleno.

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, které vyžaduje senzoru Azure ATP:

|Protokol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|**Porty Internetu**|||||
|SSL (*.atp.azure.com)|TCP|443|Cloudovou službu Azure ATP|Odchozí|
|**Interní porty**|||||
|DNS|TCP a UDP|53|Servery DNS|Odchozí|
|NTLM přes RPC|TCP|135|Všechna zařízení v síti|Odchozí|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|Všechna zařízení v síti|Odchozí|
|NetBIOS|UDP|137|Všechna zařízení v síti|Odchozí|
|Syslog (volitelné)|TCP/UDP|514, v závislosti na konfiguraci|Server SIEM|Příchozí|
|RADIUS|UDDP|1813|RADIUS|Příchozí|
|Protokol TLS k portu RDP|TCP|3389|Všechna zařízení v síti|Odchozí|

> [!NOTE]
> - Používáte účet uživatele adresářové služby, senzoru dotazuje koncových bodů ve vaší organizaci pro použití SAM-R (přihlášením k síti) k vytvoření místního správce [laterální pohyb cesta grafu](use-case-lateral-movement-path.md). Další informace najdete v tématu [konfigurace SAM-R požadovaná oprávnění](install-atp-step8-samr.md).
> - Musí být otevřený příchozí na zařízení v síti ze senzorů samostatné Azure ATP následující porty:
>   -   NTLM přes RPC (TCP Port 135) pro účely řešení
>   -   Pro rozhraní NetBIOS (UDP port 137) pro účely řešení
>   -   Protokol RDP (TCP port 3389), pouze první paket *Client hello*, pro účely řešení<br> Všimněte si, že na všech portech neprobíhá žádné ověřování.




## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Architektura služby Azure ATP](atp-architecture.md)
- [Nainstalujte ATP](install-atp-step1.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)


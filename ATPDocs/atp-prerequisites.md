---
title: Požadavky rozšířené ochrany před internetovými útoky pro Azure | Microsoft Docs
description: Popisuje požadavky na úspěšné nasazení služby Azure ATP ve vašem prostředí.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0ccb4339e1190bc1bc92684cd939b58c88394354
ms.sourcegitcommit: f7c75bc5715c5bda0b3110364e2aebddddce8a13
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/01/2019
ms.locfileid: "70209218"
---
# <a name="azure-atp-prerequisites"></a>Požadavky služby Azure ATP

Tento článek popisuje požadavky na úspěšné nasazení služby Azure ATP ve vašem prostředí.

>[!NOTE]
> Informace o plánování prostředků a kapacity najdete v tématu [plánování kapacity ATP Azure](atp-capacity-planning.md).


Azure ATP se skládá z cloudové služby Azure ATP, která se skládá z portálu Azure ATP, senzoru ATP Azure a/nebo samostatného senzoru služby Azure ATP. Další informace o jednotlivých součástech Azure ATP najdete v tématu [Architektura ATP Azure](atp-architecture.md).

Azure ATP chrání vaše místní uživatele nebo uživatele služby Active Directory synchronizované s vaším Azure Active Directory. Informace o ochraně prostředí tvořeného jenom uživateli AAD najdete v tématu [AAD Identity Protection](https://docs.microsoft.com/azure/active-directory/identity-protection/overview). 

Pokud chcete vytvořit instanci ATP Azure, budete potřebovat tenanta AAD aspoň s jedním globálním správcem nebo správcem zabezpečení. Každá instance služby Azure ATP podporuje několik hranic doménové struktury Active Directory a úroveň funkčnosti doménové struktury (FFL) systému Windows 2003 a vyšší úrovně. 

Tato součást Průvodce je rozdělená do následujících částí, abyste měli jistotu, že máte všechno, co potřebujete k úspěšnému nasazení ATP Azure. 

[Než začnete](#before-you-start): Vypíše informace pro shromažďování a účty a síťové entity, které budete muset před zahájením instalace nainstalovat.

[Portál Azure ATP](#azure-atp-portal-requirements): Popisuje požadavky prohlížeče na portál Azure ATP.

[Senzor ATP Azure](#azure-atp-sensor-requirements): Uvádí hardware snímače ATP a požadavky na software.

[Samostatný senzor Azure ATP](#azure-atp-standalone-sensor-requirements): Zobrazuje hardware samostatného senzoru Azure ATP, požadavky na software a nastavení, které potřebujete nakonfigurovat na serverech samostatného senzoru Azure ATP.

## <a name="before-you-start"></a>Než začnete
V této části jsou uvedené informace, které byste měli shromažďovat a také informace o účtech a síťové entitě, které byste měli mít před zahájením instalace služby Azure ATP.

- Získejte licenci na Enterprise Mobility + Security 5 (EMS E5) přímo přes [portál Microsoft 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) nebo použijte licenční model partner Cloud Solution partner (CSP). K dispozici jsou také samostatné licence Azure ATP.  

- Ověřte, jestli máte řadiče domény, které máte v úmyslu nainstalovat senzory Azure ATP, připojení k Internetu do cloudové služby Azure ATP. Senzor ATP Azure podporuje použití proxy serveru. Další informace o konfiguraci proxy serveru najdete v tématu [konfigurace proxy serveru pro službu Azure ATP](configure-proxy.md).  

-   **Místní** uživatelský účet služby AD a heslo s přístupem pro čtení ke všem objektům ve sledovaných doménách.

    > [!NOTE]
    > Pokud jste pro různé organizační jednotky (OU) ve vaší doméně nastavili vlastní seznamy ACL, ujistěte se, že vybraný uživatel má pro tyto organizační jednotky oprávnění ke čtení.

-   Pokud spouštíte nástroj Wireshark na samostatném senzoru služby Azure ATP, po zastavení zachytávání nástroje Wireshark restartujte službu Azure Advanced Threat Protection snímač. Pokud službu senzoru nerestartujete, senzor zastaví zachytávání provozu.

- Pokud se pokusíte nainstalovat senzor Azure ATP na počítač nakonfigurovaný s adaptérem pro seskupování síťových adaptérů, dojde k chybě instalace. Pokud chcete senzor Azure ATP nainstalovat na počítač nakonfigurovaný se seskupováním síťových adaptérů, přečtěte si [problém seskupování síťových adaptérů senzorů Azure ATP](troubleshooting-atp-known-issues.md#nic-teaming).

- Doporučení kontejneru odstraněných **objektů** : Uživatel by měl mít oprávnění jen pro čtení pro kontejner odstraněných objektů. Oprávnění jen pro čtení tohoto kontejneru umožňují službě Azure ATP detekovat odstranění uživatelů ze služby Active Directory. Informace o konfiguraci oprávnění jen pro čtení u kontejneru odstraněných objektů najdete v části **Změna oprávnění v kontejneru odstraněného objektu** v tématu [zobrazení nebo nastavení oprávnění pro objekt adresáře](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) .

- Volitelné **honeytokenu**: Uživatelský účet uživatele, který nemá žádné síťové aktivity. Tento účet je nakonfigurovaný jako Honeytokenu uživatel Azure ATP. Další informace o použití Honeytokens najdete v tématu [konfigurace vyloučení a uživatel honeytokenu](install-atp-step7.md).

- Volitelné: Při nasazování samostatného senzoru je nutné předávat události systému Windows 4776, 4732, 4733, 4728, 4729, 4756, 4757 a 7045 do služby Azure ATP, aby bylo možné dále vylepšit Azure ATP pass-the-hash, hrubou silou, úpravu citlivých skupin, Honeytokens detekci a Vytvoření škodlivé služby. Senzor ATP Azure tyto události přijímá automaticky. V rámci samostatného senzoru Azure ATP můžete tyto události přijímat z SIEM nebo nastavením předávání událostí systému Windows z řadiče domény. Shromážděné události poskytují Azure ATP dalšími informacemi, které nejsou k dispozici prostřednictvím síťového provozu řadiče domény.

## <a name="azure-atp-portal-requirements"></a>Požadavky na portál Azure ATP
Přístup k portálu Azure ATP je prostřednictvím prohlížeče, který podporuje následující prohlížeče a nastavení:
-   Microsoft Edge
-   Internet Explorer verze 10 a novější
-   Google Chrome 4,0 a novější
-   Minimální rozlišení obrazovky na šířku 1 700 pixelů
-   Brána firewall/proxy Open-ke komunikaci s cloudovou službou Azure ATP *. atp.azure.com port 443 musí být v bráně firewall nebo proxy serveru otevřené.

 ![Diagram architektury Azure ATP](media/azure-atp-architecture.png)


> [!NOTE]
> Ve výchozím nastavení podporuje Azure ATP až 200 senzorů. Pokud chcete nainstalovat víc, obraťte se na podporu ATP Azure.


## <a name="azure-atp-network-name-resolution-nnr-requirements"></a>Požadavky na překlad síťových adres pro Azure ATP (útoků)
Překlad síťových adres (útoků) je hlavní součástí funkcí služby Azure ATP. Aby služba Azure ATP pracovala správně, musí být pro senzory ATP v Azure dostupná aspoň jedna z následujících metod útoků:
1. **TLM přes RPC** (Port TCP 135)
2. **Rozhraní NetBIOS** (Port UDP 137)
3. Protokol **RDP** (Port TCP 3389) – pouze první paket klienta Hello
4. **Dotazy serveru DNS pomocí zpětného vyhledávání DNS IP adresy** (UDP 53)

Aby metody 1, 2 a 3 fungovaly, musí být příslušné porty otevřené od senzorů Azure ATP až po zařízení v síti. Další informace o službě Azure ATP a útoků najdete v tématu [zásady útoků pro Azure ATP](atp-nnr-policy.md). 

## <a name="azure-atp-sensor-requirements"></a>Požadavky na senzor ATP Azure
V této části jsou uvedené požadavky na senzor ATP Azure.

### <a name="general"></a>Obecné

> [!NOTE]
> Ujistěte se, že je při použití serveru 2019 nainstalovaná [KB4487044](https://support.microsoft.com/help/4487044/windows-10-update-kb4487044) . Senzory Azure ATP, které jsou už nainstalované na serverech 2019, bez této aktualizace se automaticky zastaví.
 
Senzor ATP Azure podporuje instalaci na řadič domény se systémem Windows Server 2008 R2 SP1 (nezahrnuje jádro serveru), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (včetně jádra Windows serveru, ale ne Windows nano Server), Windows Server 2019 (včetně Windows Core, ale ne Windows nano serveru).

Řadič domény může být řadičem domény jen pro čtení (RODC).

Aby řadiče domény komunikovaly s cloudovou službou, musíte v bránách firewall a proxy serverech otevřít port 443 na *. atp.azure.com.

Během instalace je nainstalováno rozhraní .NET Framework 4,7 a může vyžadovat restartování řadiče domény, pokud už restartování čeká na vyřízení.


> [!NOTE]
> Vyžaduje se minimálně 5 GB místa na disku a doporučuje se 10 GB. To zahrnuje prostor potřebný pro binární soubory ATP Azure, protokoly ATP Azure a protokoly výkonu.

### <a name="server-specifications"></a>Specifikace serveru

Senzor ATP Azure vyžaduje minimálně 2 jádra a 6 GB paměti RAM nainstalované na řadiči domény.
Pro zajištění optimálního výkonu nastavte **možnost napájení** snímače ATP Azure na **vysoký výkon**.

Senzory Azure ATP se dají nasadit na řadiče domény různých zatížení a velikostí v závislosti na objemu síťových přenosů do a z řadičů domény a na množství nainstalovaných prostředků.

Pro operační systémy Windows 2008 R2 a 2012 není senzor Azure ATP podporován v režimu [více procesorů](https://docs.microsoft.com/windows/win32/procthread/processor-groups) . Další informace o režimu skupiny s více procesory najdete v tématu [řešení potíží](troubleshooting-atp-known-issues.md##multi-processor-group-mode). 

>[!NOTE] 
> Při spuštění jako virtuální počítač není podporována dynamická paměť nebo jakákoli jiná funkce pro vybublinování paměti.

Další informace o požadavcích na hardware pro senzory ATP (Azure ATP) najdete v tématu [plánování kapacity Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace

Servery a řadiče domény, na kterých je senzor nainstalovaný, musí mít během pěti minut čas synchronizovaný.

### <a name="network-adapters"></a>Síťové adaptéry

Senzor ATP Azure monitoruje místní provoz na všech síťových adaptérech řadiče domény. <br>
Po nasazení použijte portál Azure ATP k úpravě síťových adaptérů, které jsou monitorovány.

Senzor není podporován na řadičích domény se systémem Windows 2008 R2 se zapnutým seskupováním síťových adaptérů Broadcom.

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, které vyžaduje senzor Azure ATP:

|Protocol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|**Internetové porty**|||||
|SSL (*.atp.azure.com)|TCP|443|Cloudová služba Azure ATP|Odchozí|
|**Interní porty**|||||
|DNS|TCP a UDP|53|Servery DNS|Odchozí|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|Všechna zařízení v síti|Odchozí|
|Syslog (volitelné)|TCP/UDP|514, v závislosti na konfiguraci|Server SIEM|Příchozí|
|Protokol RADIUS|UDP|1813|Protokol RADIUS|Příchozí|
|

### <a name="windows-event-logs"></a>Protokoly událostí Windows
Zjišťování ATP Azure spoléhá na konkrétní protokoly událostí Windows, které senzor dokáže analyzovat z řadiče domény. Aby byly správné auditované události auditovány a součástí události Windows og, vyžadují řadiče domény přesné rozšířené nastavení zásad auditu. Další informace najdete v tématu [Kontrola rozšířených zásad auditu](atp-advanced-audit-policy.md).


> [!NOTE]
> - Pomocí uživatelského účtu adresářové služby se senzor dotazuje ve vaší organizaci pro místní správce pomocí SAM-R (přihlášení k síti), aby bylo možné vytvořit [graf cesty bočního pohybu](use-case-lateral-movement-path.md). Další informace najdete v tématu [Konfigurace požadovaných oprávnění Sam-R](install-atp-step8-samr.md).
> - Na zařízeních v síti musí být otevřený vstup z senzorů Azure ATP:
>   -   Protokol NTLM přes RPC (TCP port 135) pro účely řešení
>   -   NetBIOS (port UDP 137) pro účely překladu
<br> Neprovádí se žádné ověřování na žádném z těchto portů.

## <a name="azure-atp-standalone-sensor-requirements"></a>Požadavky na samostatné senzory Azure ATP
V této části jsou uvedené požadavky na samostatný senzor Azure ATP.

### <a name="general"></a>Obecné
Samostatný senzor Azure ATP podporuje instalaci na serveru se systémem Windows Server 2012 R2 nebo Windows Server 2016 (včetně jádra serveru).
Samostatný senzor Azure ATP se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.
Samostatný senzor Azure ATP se dá použít k monitorování řadičů domény s úrovní funkčnosti domény systému Windows 2003 a vyšší.

Aby váš samostatný senzor komunikoval s cloudovou službou, musí být otevřený port 443 ve vašich branách firewall a proxy serverech *. atp.azure.com.


Informace o používání virtuálních počítačů s využitím samostatného senzoru Azure ATP najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md).

> [!NOTE]
> Vyžaduje se minimálně 5 GB místa na disku a doporučuje se 10 GB. To zahrnuje prostor potřebný pro binární soubory ATP Azure, protokoly ATP Azure a protokoly výkonu.

### <a name="server-specifications"></a>Specifikace serveru
Pro zajištění optimálního výkonu nastavte **možnost napájení** samostatného senzoru Azure ATP na **vysoký výkon**.<br>
Samostatné senzory Azure ATP můžou podporovat monitorování více řadičů domény v závislosti na objemu síťového provozu do a z řadičů domény.

>[!NOTE] 
> Při spuštění jako virtuální počítač není podporována dynamická paměť nebo jakákoli jiná funkce pro vybublinování paměti.

Další informace o požadavcích na hardware pro samostatné senzory Azure ATP najdete v tématu [plánování kapacity Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Časová synchronizace

Servery a řadiče domény, na kterých je senzor nainstalovaný, musí mít během pěti minut čas synchronizovaný.

### <a name="network-adapters"></a>Síťové adaptéry
Samostatný senzor Azure ATP vyžaduje aspoň jeden adaptér pro správu a aspoň jeden adaptér pro zachytávání:

-   **Adaptér pro správu** – používá se pro komunikaci ve vaší podnikové síti. Senzor použije tento adaptér k dotazování na řadič domény, který chrání a provádí řešení účtů počítačů. <br>Tento adaptér by měl být nakonfigurovaný s následujícím nastavením:

    -   Statická IP adresa včetně výchozí brány

    -   Upřednostňovaný a alternativní server DNS

    -   **Příponou DNS pro toto připojení** by pro každou monitorovanou doménu měl být její název DNS.

        ![Konfigurace přípony DNS v rozšířeném nastavení protokolu TCP/IP](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > Pokud je samostatný senzor Azure ATP členem domény, dá se konfigurovat automaticky.

-   **Adaptér** pro zachytávání – používá se k zaznamenání provozu do a z řadičů domény.

    > [!IMPORTANT]
    > -   Nakonfigurujte zrcadlení portů pro adaptér pro zachytávání jako cíl síťového provozu řadiče domény. Další informace najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md). K nakonfigurování zrcadlení portů obvykle potřebujete pracovat s týmem sítě nebo s virtualizačním týmem.
    > -   Nakonfigurujte statickou IP adresu Nesměrovatelné IP adresy (s maskou/32) pro vaše prostředí bez výchozí brány snímače ani adres serverů DNS. Například 10.10.0.10/32. Tím zajistíte, že síťový adaptér pro zachytávání může zachytit maximální objem provozu a že síťový adaptér pro správu se používá k posílání a přijímání potřebných síťových přenosů.

### <a name="ports"></a>Porty
Následující tabulka uvádí minimální porty, které vyžaduje samostatný senzor Azure ATP nakonfigurované na adaptéru pro správu:

|Protocol|Přenos|Port|Směr|Direction|
|------------|-------------|--------|-----------|-------------|
|**Internetové porty**|||||
|SSL (*.atp.azure.com)|TCP|443|Cloudová služba Azure ATP|Odchozí|
|**Interní porty**|||||
|LDAP|TCP a UDP|389|Řadiče domény|Odchozí|
|Zabezpečený LDAP (LDAPS)|TCP|636|Řadiče domény|Odchozí|
|LDAP pro globální katalog|TCP|3268|Řadiče domény|Odchozí|
|LDAPS pro globální katalog|TCP|3269|Řadiče domény|Odchozí|
|Kerberos|TCP a UDP|88|Řadiče domény|Odchozí|
|Netlogon (SMB, CIFS, SAM-R)|TCP a UDP|445|Všechna zařízení v síti|Odchozí|
|Čas Windows|UDP|123|Řadiče domény|Odchozí|
|DNS|TCP a UDP|53|Servery DNS|Odchozí|
|Syslog (volitelné)|TCP/UDP|514, v závislosti na konfiguraci|Server SIEM|Příchozí|
|Protokol RADIUS|UDP|1813|Protokol RADIUS|Příchozí|
|

> [!NOTE]
> - Pomocí uživatelského účtu adresářové služby se senzor dotazuje ve vaší organizaci pro místní správce pomocí SAM-R (přihlášení k síti), aby bylo možné vytvořit [graf cesty bočního pohybu](use-case-lateral-movement-path.md). Další informace najdete v tématu [Konfigurace požadovaných oprávnění Sam-R](install-atp-step8-samr.md).
> - Na zařízeních v síti z jednotlivých senzorů Azure ATP musí být otevřený vstup z následujících portů:
>   -   Protokol NTLM přes RPC (TCP port 135) pro účely řešení
>   -   NetBIOS (port UDP 137) pro účely překladu
<br> Neprovádí se žádné ověřování na žádném z těchto portů.



## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Architektura služby Azure ATP](atp-architecture.md)
- [Instalace ATP Azure](install-atp-step1.md)
- [Rozlišení názvu sítě (útoků)](atp-nnr-policy.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)



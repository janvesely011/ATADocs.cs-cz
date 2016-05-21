---
# required metadata

title: Požadavky ATA | Microsoft Advanced Threat Analytics
description: Popisuje požadavky pro úspěšné nasazení ATA ve vašem prostředí.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Požadavky ATA
Tento článek popisuje požadavky pro úspěšné nasazení ATA ve vašem prostředí.

ATA tvoří dvě komponenty, ATA Center a ATA Gateway. Další informace o komponentách ATA najdete v tématu [Architektura ATA](/advanced-threat-analytics/understand-explore/ata-architecture)..

[Než začnete](#before-you-start): V této části jsou uvedené informace, které byste měli získat, a účty a síťové entity, které byste měli mít před zahájením instalace ATA.

[ATA Center](#ata-center-requirements): V této části jsou uvedené požadavky komponenty ATA Center na hardware a software a taky nastavení, která musíte nakonfigurovat na příslušném serveru ATA Center.

[ATA Gateway](#ata-gateway-requirements): V této části jsou uvedené požadavky komponenty ATA Gateway na hardware a software a taky nastavení, která musíte nakonfigurovat na příslušné servery ATA Gateway.

[Konzola ATA](#ata-console): V této části jsou uvedené požadavky na prohlížeč pro spuštění konzoly ATA.

![Diagram architektury ATA](media/ATA-architecture-topology.jpg)

## Než začnete
V této části jsou uvedené informace, které byste měli získat, a účty a síťové entity, které byste měli mít před zahájením instalace ATA.

-   **Řadiče domény** spuštěné v systému Windows Server 2008 nebo novějším.

-   **Uživatelský účet a heslo** s přístupem pro čtení ke **všem objektům** v doménách, které se budou monitorovat.

    > [!NOTE]
    > Pokud jste pro různé organizační jednotky (OU) ve vaší doméně nastavili vlastní seznamy ACL, ujistěte se, že vybraný uživatel má pro tyto organizační jednotky oprávnění ke čtení.

    Volitelné: Uživatel by měl mít ke kontejneru odstraněných objektů oprávnění jen pro čtení. Díky tomu dokáže ATA detekovat hromadné odstranění objektů v doméně. Informace o konfiguraci oprávnění jen pro čtení pro kontejner odstraněných objektů najdete v části **Změna oprávnění pro kontejner odstraněných objektů** v tématu [Zobrazení nebo nastavení oprávnění pro objekt adresáře](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Volitelné: Uživatelský účet uživatele, který nemá žádné síťové aktivity. Tento účet se nakonfiguruje jako uživatel honeytokenu ATA. Ke konfiguraci uživatele honeytokenu budete potřebovat SID účtu uživatele, nikoli jeho uživatelské jméno.

-   Volitelné: Kromě shromažďování a analýzy síťových přenosů z a do řadičů domény může ATA využít událost 4776 systému Windows k dalšímu vylepšení detekce útoků Pass-the-Hash. Tato událost může být přijata ze služby SIEM nebo nastavením předávání událostí systému Windows z řadiče domény. Shromážděné události systému ATA poskytují další informace, které nejsou dostupné prostřednictvím síťových přenosů řadičů domény.

-   Může být užitečné připravit si seznam všech podsítí použitých ve vaší síti pro VPN a Wi-Fi, které v průběhu velmi krátké doby (řádově sekund nebo minut) mění přiřazení IP adres mezi zařízeními.  Tyto podsítě s krátkodobým zapůjčením je potřeba určit, aby bylo možné omezit životnost jejich mezipaměti a vyhovět rychlé změně přiřazení mezi zařízeními. Informace o konfiguraci podsítí s krátkodobým zapůjčením najdete v tématu [Instalace ATA](/advanced-threat-analytics/deploy-useinstall-ata).

## Požadavky pro ATA Center
V této části je uveden seznam požadavků pro ATA Center.

ATA Center podporuje instalaci na serveru s Windows Serverem 2012 R2. Spusťte službu Windows Update a ujistěte se, že všechny důležité aktualizace jsou nainstalované.
 Počet řadičů domény, které monitorujete, a zatížení na jednotlivých řadičích určuje požadavky na hardware.

Instalace komponenty ATA Center jako virtuálního počítače se podporuje. Další informace najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md)..

Pokud ATA Center spouštíte jako virtuální počítač, před vytvořením nového kontrolního bodu vypněte server. Vyhnete se tak možnému poškození databází.

> [!NOTE]
> - ATA Center se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.
>
> - Pro vypracování analýzy chování uživatelů ATA Center vyžaduje data za nejméně 21 dnů.
>
> - Další informace o požadavcích na hardware najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md)..


### Časová synchronizace
Server ATA Center, servery ATA Gateway a řadiče domény musí být vzájemně časově synchronizované (s tolerancí 5 minut).

### Nastavení systému BIOS
Databáze ATA vyžaduje, abyste v systému BIOS **zakázali** neuniformní přístup k paměti (NUMA). Ve vašem systému se NUMA může označovat také jako prokládání uzlů. V takovém případě bude potřeba prokládání uzlů **povolit**. Další informace najdete v dokumentaci k systému BIOS.

### Síťové adaptéry
Požadavky:

-   Jeden síťový adaptér

-   Dvě IP adresy

Komunikace mezi komponentami ATA Center a ATA Gateway je zašifrovaná pomocí SSL na portu 443. Konzola ATA je spuštěná ve službě IIS a zabezpečená pomocí SSL na portu 443. Doporučují se **dvě IP adresy**. Služba ATA Center vytvoří vazbu mezi portem 443 a první IP adresou a služba IIS vytvoří vazbu mezi portem 443 a druhou IP adresou.

> [!NOTE]
> Může se použít jedna IP adresa se dvěma různými porty, ale doporučuje se použití dvou IP adres.

### Porty
Následující tabulka uvádí minimální porty, které musí být otevřené, aby služba ATA Center fungovala správně.

V této tabulce je IP adresa 1 svázaná se službou ATA Center a IP adresa 2 je svázaná se službou IIS pro konzolu ATA.

|Protokol|Přenos|Port|Směr|Direction|IP adresa|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (komunikace ATA)|TCP|443 nebo konfigurovatelné|ATA Gateway|Příchozí|IP adresa 1|
|**HTTP**|TCP|80|Podniková síť|Příchozí|IP adresa 2|
|**HTTPS**|TCP|443|Podniková síť a ATA Gateway|Příchozí|IP adresa 2|
|**SMTP** (volitelné)|TCP|25|Server SMTP|Odchozí|IP adresa 2|
|**SMTPS** (volitelné)|TCP|465|Server SMTP|Odchozí|IP adresa 2|
|**Syslog** (volitelné)|TCP|514|Server syslog|Odchozí|IP adresa 2|

### Certifikáty
Zkontrolujte, jestli služby ATA Gateway mají přístup k distribučnímu bodu CRL. Pokud služby ATA Gateway nemají přístup k internetu, použijte [ruční import seznamu CRL](https://technet.microsoft.com/en-us/library/aa996972%28v=exchg.65%29.aspx) a dbejte na to, abyste nainstalovali všechny distribuční body CRL pro celý řetězec.

K usnadnění instalace služby ATA Center můžete nainstalovat certifikát podepsaný svým držitelem (self-signed certificate). Po nasazení můžete certifikát podepsaný svým držitelem nahradit certifikátem certifikační autority, který bude používat ATA Gateway.

> [!NOTE]
> Certifikáty podepsané svým držitelem by se měly používat jenom v testovacím nasazení.

ATA Center vyžaduje certifikáty pro následující služby:

-   Internetová informační služba (IIS) – certifikát webového serveru

-   Služba ATA Center – ověřovací certifikát serveru

> [!NOTE]
> Pokud budete ke konzole ATA přistupovat z jiných počítačů, zkontrolujte, že tyto počítače důvěřují certifikátu používanému službou IIS, jinak se před ještě zobrazením přihlašovací stránky zobrazí upozornění, že došlo k potížím s certifikátem zabezpečení webu.

## Požadavky na ATA Gateway
ATA Gateway podporuje instalaci na serveru s Windows Serverem 2012 R2.

Spusťte službu Windows Update a ujistěte se, že všechny **důležité** aktualizace jsou nainstalované.
Před instalací služby ATA Gateway zkontrolujte, že byla nainstalovaná tato aktualizace: [KB2919355](https://support.microsoft.com/en-us/kb/2919355/)..

Toto ověření můžete provést spuštěním následující rutiny Windows PowerShellu: `[Get-HotFix -Id kb2919355]`.

> [!NOTE]
> -   ATA Gateway se dá nainstalovat na server, který je členem domény nebo pracovní skupiny.
> -   ATA Gateway nelze nainstalovat na řadič domény.

Informace o používání virtuálních počítačů se službou ATA Gateway najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md)..

> [!NOTE]
> Pokud ATA Gateway spouštíte jako virtuální počítač, před vytvořením nového kontrolního bodu vypněte server. Vyhnete se tak možnému poškození databází.

ATA Gateway může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů z a do řadičů domény.
Další informace najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md)..

### Nastavení napájení
K zajištění optimálního výkonu nastavte **možnost napájení ** pro ATA Gateway na hodnotu **Vysoký výkon**..

### Časová synchronizace
Server ATA Center a server ATA Gateway musí být vzájemně časově synchronizované (s tolerancí 5 minut).

Navíc musí být vzájemně časově synchronizované (s tolerancí 5 minut) i ATA Gateway a řadiče domény.

### Síťové adaptéry
ATA Gateway vyžaduje nejméně jen adaptér pro správu a jeden adaptér pro zachytávání:

-   **Adaptér pro správu** se použije pro komunikace ve vaší firemní síti. Pro tento adaptér by měly být nakonfigurované tyto parametry:

    -   Statická IP adresa včetně výchozí brány

    -   Upřednostňovaný a alternativní server DNS

    -   **Příponou DNS pro toto připojení** by pro každou monitorovanou doménu měl být její název DNS.

        ![Konfigurace přípony DNS v rozšířeném nastavení protokolu TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Pokud je ATA Gateway členem domény, probíhá konfigurace automaticky.

-   **Adaptér pro zachytávání** se použije pro zachycení přenosu dat z a do řadičů domény.

    > [!IMPORTANT]
    > -   Nakonfigurujte zrcadlení portů pro adaptér pro zachytávání jako cíl síťového provozu řadiče domény. Další informace najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md). Při konfiguraci zrcadlení portů budete obvykle spolupracovat s týmem pro sítě nebo virtualizace.
    > -   Pro vaše prostředí nakonfigurujte statickou nepřesměrovatelnou IP adresu bez výchozí brány a adresy serveru DNS. Příklad: 1.1.1.1/32. Zajistíte tak, že síťový adaptér pro zachytávání může zachytit maximální objem přenášených dat a síťový adaptér pro správu se bude používat k odesílání a příjmu požadované síťové komunikace.

### Porty
Následující tabulka uvádí minimální porty, u kterých ATA Gateway vyžaduje, aby byly nakonfigurované na adaptéru pro správu.

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
|SSL|TCP|443 nebo podle konfigurace pro službu Center|ATA Center:<br /><br />– IP adresa pro službu Center<br />– IP adresa pro IIS|Odchozí|
|Syslog (volitelné)|UDP|514|Server SIEM|Příchozí|

> [!NOTE]
> V rámci procesu překladu, který provádí ATA Gateway, musí být na zařízeních v síti následující porty otevřené pro příjem dat z ATA Gateway.
>
> -   NTLM přes RPC
> -   NetBIOS

### Certifikáty
K usnadnění instalace služby ATA Center můžete nainstalovat certifikát podepsaný svým držitelem (self-signed certificate). Po nasazení můžete certifikát podepsaný svým držitelem nahradit certifikátem certifikační autority, který bude používat ATA Gateway.

> [!NOTE]
> Certifikáty podepsané svým držitelem by se měly používat jenom v testovacím nasazení.

V úložišti Počítač služby ATA Gateway v úložišti Místní počítač musí být nainstalovaný certifikát podporující **ověření serveru**. Tento certifikát musí být pro ATA Center důvěryhodný.

## Konzola ATA
Přístup ke konzole ATA je prostřednictvím prohlížeče. Podporují se tyto:

-   Internet Explorer verze 10 a novější

-   Google Chrome 40 a novější

-   Minimální rozlišení obrazovky na šířku 1 700 pixelů

## Viz také
- [Architektura ATA](/advanced-threat-analytics/understand-explore/ata-architecture)
- [Instalace ATA](/advanced-threat-analytics/deploy-useinstall-ata)
- [Podporu získáte na našem fóru!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO4-->



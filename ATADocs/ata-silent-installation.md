---
title: "Bezobslužná instalace Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Popisuje postup při bezobslužné instalaci ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/20/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7e130da2b5a177658e176a428101c11d02bc2a3f
ms.sourcegitcommit: 42ce07e3207da10e8dd7585af0e34b51983c4998
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/25/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="ata-silent-installation"></a>Bezobslužná instalace ATA
Tento článek poskytuje podrobné pokyny k bezobslužné instalaci ATA.
## <a name="prerequisites"></a>Požadavky

ATA verze 1.8 vyžaduje instalaci rozhraní Microsoft .NET Framework 4.6.1. 

Když instalujete nebo aktualizujete ATA, jako součást nasazení Microsoft ATA se automaticky nainstaluje .Net Framework 4.6.1.

> [!Note] 
> Instalace rozhraní .Net Framework 4.6.1 může vyžadovat restartování serveru. Když instalujete ATA Gateway na řadiče domény, zvažte naplánování časového období údržby pro tyto řadiče.
Při použití metody bezobslužné instalace ATA je instalační program nakonfigurovaný tak, aby po ukončení instalace (v případě potřeby) automaticky restartoval server. Vzhledem k tomu, že je v Instalační službě systému Windows chyba, není možné spolehlivě použít příznak norestart a zajistit tak, že se server nebude restartovat. Během údržby tedy musí běžet jenom tichá instalace.

Pokud chcete sledovat průběh nasazení, monitorujte instalační protokoly ATA, které jsou umístěné ve složce **%AppData%\Local\Temp**.


## <a name="install-the-ata-center"></a>Instalace ATA Center

K instalaci komponenty ACA Center použijte následující příkaz:

**Syntaxe**:

    "Microsoft ATA Center Setup.exe" [/quiet] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments="/q"] [InstallationPath="<InstallPath>"] [DatabaseDataPath= "<DBPath>"] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint="<CertThumbprint>"] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint="<CertThumbprint >"]
    
**Možnosti instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|
|LicenseAccepted|--LicenseAccepted|Ano|Udává, že licence byla přečtena a schválena. U bezobslužné instalace musí být nastavené.|

**Parametry instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath="<InstallPath>"|Ne|Nastavuje cestu pro instalaci binárních souborů ATA. Výchozí cesta: C:\Program Files\Microsoft Advanced Threat Analytics\Center|
|DatabaseDataPath|DatabaseDataPath= "<DBPath>"|Ne|Nastavuje cestu k datové složce databáze ATA. Výchozí cesta: C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|Ano|Nastaví IP adresu služby ATA Center.|
|CenterPort|CenterPort=<CenterPort>|Ano|Nastaví síťový port služby ATA Center.|
|CenterCertificateThumbprint|CenterCertificateThumbprint="<CertThumbprint>"|Ne|Nastaví kryptografický otisk certifikátu pro službu ATA Center. Tento certifikát slouží k zabezpečení komunikace mezi komponentami ATA Center a ATA Gateway. Pokud není nastavený, instalace vytvoří certifikát podepsaný svým držitelem (self-signed certificate).|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|Ano|Nastaví IP adresu konzoly ATA.|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint="<CertThumbprint >"|Ne|Nastaví kryptografický otisk certifikátu pro konzolu ATA. Tento certifikát slouží k ověření identity webu konzoly ATA. Pokud není nastavený, instalace vytvoří certifikát podepsaný svým držitelem (self-signed certificate).|

**Příklady**: Instalace komponenty ATA Center s výchozími instalačními cestami a jednou IP adresou:

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

Instalace komponenty ATA Center s výchozími instalačními cestami, dvěma IP adresami a uživatelsky definovanými kryptografickými otisky certifikátu:

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F"
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint="G9530253C976BFA9342FD1A716C0EC94207BFD5A"

## <a name="update-the-ata-center"></a>Aktualizace ATA Center

K aktualizaci komponenty ACA Center použijte následující příkaz:

**Syntaxe**:

    "Microsoft ATA Center Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Možnosti instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|


Při aktualizaci instalační program automaticky rozpozná, že služba ATA už je na serveru nainstalovaná, a nevyžaduje se žádná možnost pro instalaci aktualizace.

**Příklady**: Bezobslužná aktualizace komponenty ATA Center: V rozsáhlých prostředích může dokončení aktualizace komponenty ATA Center nějakou dobu trvat. Průběh aktualizace můžete sledovat prostřednictvím protokolů ATA.

        "Microsoft ATA Center Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-center-silently"></a>Bezobslužná odinstalace komponenty ATA Center

K provedení bezobslužné odinstalace komponenty ATA Center použijte následující příkaz:**Syntaxe**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/Help]
     [--DeleteExistingDatabaseData]

**Možnosti instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou odinstalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí odinstalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Odinstalace|/uninstall|Ano|Spustí bezobslužnou odinstalaci komponenty ATA Center ze serveru.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|

**Parametry instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou odinstalaci?|Popis|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|Ne|Odstraní všechny soubory ve stávající databázi.|

**Příklady**: Bezobslužná odinstalace komponenty ATA Center ze serveru s odebráním všech stávajících databázových dat:


    "Microsoft ATA Center Setup.exe" /quiet /uninstall --DeleteExistingDatabaseData

## <a name="ata-gateway-silent-installation"></a>Bezobslužná instalace ATA Gateway
K bezobslužné instalaci komponenty ACA Gateway použijte následující příkaz:

**Syntaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [ConsoleAccountName="<AccountName>"] 
    [ConsoleAccountPassword="<AccountPassword>"]

> [!NOTE]
> Pokud pracujete na počítači připojeném do domény a přihlásili jste se svým uživatelským jménem a heslem správce ATA, svoje přihlašovací údaje tady zadávat nemusíte.


**Možnosti instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|

**Parametry instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|ConsoleAccountName|ConsoleAccountName="<AccountName>"|Ano|Nastaví název uživatelského účtu (user@domain.com), který se použije k registraci komponenty ATA Gateway ve službě ATA Center.|
|ConsoleAccountPassword|ConsoleAccountPassword="<AccountPassword>"|Ano|Nastaví heslo uživatelského účtu (user@domain.com), který se použije k registraci komponenty ATA Gateway ve službě ATA Center.|

**Příklady**: Aby byla možná tichá instalace ATA Gateway na počítač připojený do domény, přihlaste se svými přihlašovacími údaji správce ATA a nebudete muset zadávat přihlašovací údaje. V opačném případě použijte k registraci v ATA Center uvedené přihlašovací údaje:

    "Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName="user@contoso.com" ConsoleAccountPassword="userpwd"
    

## <a name="update-the-ata-gateway"></a>Aktualizace ATA Gateway

K bezobslužné aktualizaci komponenty ACA Gateway použijte následující příkaz:

**Syntaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Možnosti instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|


**Příklady**: Bezobslužná aktualizace komponenty ATA Gateway:

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-gateway-silently"></a>Bezobslužná odinstalace komponenty ATA Gateway

K provedení bezobslužné odinstalace komponenty ATA Gateway použijte následující příkaz: **Syntaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Možnosti instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou odinstalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí odinstalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Odinstalace|/uninstall|Ano|Spustí bezobslužnou odinstalaci komponenty ATA Gateway ze serveru.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|

**Příklady**: Bezobslužná odinstalace komponenty ATA Gateway ze serveru:


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## <a name="see-also"></a>Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)
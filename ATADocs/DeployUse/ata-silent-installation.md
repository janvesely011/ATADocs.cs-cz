---
title: "Bezobslužná instalace ATA | Microsoft Advanced Threat Analytics"
description: "Popisuje postup při bezobslužné instalaci ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: 2e51bc9cac43ff90000ca74cccd158e119cc6ec0


---

# Bezobslužná instalace ATA
Tento článek poskytuje podrobné pokyny k bezobslužné instalaci ATA.
## Požadavky

Microsoft ATA v1.6 vyžaduje instalaci rozhraní Microsoft .NET Framework 4.6.1. 

Když instalujete nebo aktualizujete ATA, jako součást nasazení Microsoft ATA se automaticky nainstaluje .Net Framework 4.6.1.

> [!Note] 
> Instalace rozhraní .Net Framework 4.6.1 může vyžadovat restartování serveru. Když instalujete ATA Gateway na řadiče domény, zvažte naplánování časového období údržby pro tyto řadiče.
Při použití metody bezobslužné instalace ATA je instalační program nakonfigurovaný tak, aby po ukončení instalace (v případě potřeby) automaticky restartoval server. Pokud se chcete restartování serveru v rámci instalace vyhnout, použijte příznak `-NoRestart`. Pokud se při použití příznaku `-NoRestart` bude jako součást instalace vyžadovat restartování, instalační program se pozastaví, než se server restartuje. Pokud chcete sledovat průběh nasazení, monitorujte instalační protokoly ATA, které jsou umístěné ve složce **%AppData%\Local\Temp**.


## Instalace ATA Center

K instalaci komponenty ACA Center použijte následující příkaz:

**Syntaxe**:

    “Microsoft ATA Center Setup.exe” [/quiet] [/NoRestart] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments=”/q”] [InstallationPath=“<InstallPath>”] [DatabaseDataPath= “<DBPath>”] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint=“<CertThumbprint>”] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint=”<CertThumbprint >”]
    
**Možnosti instalace**:

|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|NoRestart|/norestart|Ne|Potlačí všechny pokusy o restartování. Ve výchozím nastavení uživatelské rozhraní před restartováním zobrazí výzvu.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|
|LicenseAccepted|--LicenseAccepted|Ano|Udává, že licence byla přečtena a schválena. U bezobslužné instalace musí být nastavené.|

**Parametry instalace**:

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

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

Instalace komponenty ATA Center s výchozími instalačními cestami, dvěma IP adresami a uživatelsky definovanými kryptografickými otisky certifikátu:

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F”
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint=”G9530253C976BFA9342FD1A716C0EC94207BFD5A”

## Aktualizace ATA Center

K aktualizaci komponenty ACA Center použijte následující příkaz:

**Syntaxe**:

    Microsoft ATA Center Setup.exe” [/quiet] [-NoRestart] /Help] [NetFrameworkCommandLineArguments=”/q”]


**Možnosti instalace**:

|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|NoRestart|/norestart|Ne|Potlačí všechny pokusy o restartování. Ve výchozím nastavení uživatelské rozhraní před restartováním zobrazí výzvu.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|


Při aktualizaci instalační program automaticky rozpozná, že služba ATA už je na serveru nainstalovaná, a nevyžaduje se žádná možnost pro instalaci aktualizace.

**Příklady**: Bezobslužná aktualizace komponenty ATA Center: V rozsáhlých prostředích může dokončení aktualizace komponenty ATA Center nějakou dobu trvat. Průběh aktualizace můžete sledovat prostřednictvím protokolů ATA.

        “Microsoft ATA Center Setup.exe” /quiet NetFrameworkCommandLineArguments="/q"

## Bezobslužná odinstalace komponenty ATA Center

K provedení bezobslužné odinstalace komponenty ATA Center použijte následující příkaz:**Syntaxe**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
     [--DeleteExistingDatabaseData]

**Možnosti instalace**:

|Název|Syntaxe|Povinné pro bezobslužnou odinstalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí odinstalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Odinstalace|/uninstall|Ano|Spustí bezobslužnou odinstalaci komponenty ATA Center ze serveru.|
|NoRestart|/norestart|Ne|Potlačí všechny pokusy o restartování. Ve výchozím nastavení uživatelské rozhraní před restartováním zobrazí výzvu.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|

**Parametry instalace**:

|Název|Syntaxe|Povinné pro bezobslužnou odinstalaci?|Popis|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|Ne|Odstraní všechny soubory ve stávající databázi.|

**Příklady**: Bezobslužná odinstalace komponenty ATA Center ze serveru s odebráním všech stávajících databázových dat:


    “Microsoft ATA Center Setup.exe” /quiet /uninstall --DeleteExistingDatabaseData

## Bezobslužná instalace ATA Gateway
K bezobslužné instalaci komponenty ACA Gateway použijte následující příkaz:

**Syntaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [GatewayCertificateThumbprint=”<CertThumbprint >”] [ConsoleAccountName=”<AccountName>”] 
    [ConsoleAccountPassword=”<AccountPassword>”]

**Možnosti instalace**:

|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|NoRestart|/norestart|Ne|Potlačí všechny pokusy o restartování. Ve výchozím nastavení uživatelské rozhraní před restartováním zobrazí výzvu.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|
|LicenseAccepted|--LicenseAccepted|Ano|Udává, že licence byla přečtena a schválena. U bezobslužné instalace musí být nastavené.|

**Parametry instalace**:

|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|GatewayCertificateThumbprint|GatewayCertificateThumbprint=”<CertThumbprint >”|Ne|Nastaví kryptografický otisk certifikátu pro službu ATA Center. Tento certifikát slouží k zabezpečení komunikace mezi komponentami ATA Center a ATA Gateway. Pokud není nastavený, instalace vytvoří certifikát podepsaný svým držitelem (self-signed certificate).|
|ConsoleAccountName|ConsoleAccountName=”<AccountName>”|Ano|Nastaví název uživatelského účtu (uzivatel@domena.com), který se použije k registraci komponenty ATA Gateway ve službě ATA Center.|
|ConsoleAccountPassword|ConsoleAccountPassword=”<AccountPassword>”|Ano|Nastaví heslo pro uživatelský účet (uzivatel@domena.com), který se použije k registraci komponenty ATA Gateway ve službě ATA Center.|

**Příklady**: Bezobslužná instalace komponenty ATA Gateway a její registrace ve službě ATA Center pomocí zadaných přihlašovacích údajů:

    “Microsoft ATA Gateway Setup.exe” /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName=”user@contoso.com” ConsoleAccountPassword=“userpwd”
    

## Aktualizace ATA Gateway

K bezobslužné aktualizaci komponenty ACA Gateway použijte následující příkaz:

**Syntaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] /Help] [NetFrameworkCommandLineArguments="/q"]


**Možnosti instalace**:

|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|NoRestart|/norestart|Ne|Potlačí všechny pokusy o restartování. Ve výchozím nastavení uživatelské rozhraní před restartováním zobrazí výzvu.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|


**Příklady**: Bezobslužná aktualizace komponenty ATA Gateway:

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## Bezobslužná odinstalace komponenty ATA Gateway

K provedení bezobslužné odinstalace komponenty ATA Gateway použijte následující příkaz: **Syntaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
    
**Možnosti instalace**:

|Název|Syntaxe|Povinné pro bezobslužnou odinstalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí odinstalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Odinstalace|/uninstall|Ano|Spustí bezobslužnou odinstalaci komponenty ATA Gateway ze serveru.|
|NoRestart|/norestart|Ne|Potlačí všechny pokusy o restartování. Ve výchozím nastavení uživatelské rozhraní před restartováním zobrazí výzvu.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|

**Příklady**: Bezobslužná odinstalace komponenty ATA Gateway ze serveru:


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=Jun16_HO4-->



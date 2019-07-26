---
title: Bezobslužná instalace Azure Advanced Threat Protection | Microsoft Docs
description: Tento článek popisuje, jak tiše nainstalovat službu Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6fca63fb488aef6fb26f4f501c4f6af896e223bd
ms.sourcegitcommit: 4662ad41addf92727367874d909937fa331fb866
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/25/2019
ms.locfileid: "68485066"
---
# <a name="azure-atp-switches-and-silent-installation"></a>Přepínače Azure ATP a bezobslužná instalace
Tento článek poskytuje pokyny a pokyny pro přepínače Azure ATP a tichou instalaci.

## <a name="prerequisites"></a>Požadavky

Azure ATP vyžaduje instalaci Microsoft .NET Framework 4,7. 

Při instalaci služby Azure ATP se rozhraní .NET Framework 4,7 automaticky nainstaluje jako součást nasazení služby Azure ATP.

> [!IMPORTANT] 
> Ujistěte se, že máte nainstalovanou nejnovější verzi rozhraní .NET Framework. Pokud je nainstalovaná předchozí verze rozhraní .NET, vaše tichá instalace ATP Azure se zablokuje ve smyčce a instalace se nezdaří. 

> [!NOTE] 
> Instalace rozhraní .NET Framework 4,7 může vyžadovat restartování serveru. Při instalaci senzoru ATP Azure na řadiče domény zvažte plánování časového období údržby pro řadiče domény.
Při použití bezobslužné instalace Azure ATP je Instalační služba nakonfigurovaná tak, aby na konci instalace automaticky restartovala server (v případě potřeby). Nezapomeňte spustit bezobslužnou instalaci pouze během časového období údržby. Kvůli chybě Instalační služba systému Windows nelze spolehlivě použít  příznak nerestartu, aby bylo zajištěno, že se server nerestartuje.

Pokud chcete sledovat průběh nasazení, Sledujte protokoly instalačního programu Azure ATP, které se nacházejí v **složce%AppData%\local\temp**.


## <a name="azure-atp-sensor-silent-installation"></a>Tichá instalace senzoru ATP Azure

> [!NOTE]
> Při tichém nasazení senzoru služby Azure ATP prostřednictvím System Center Configuration Manager nebo jiného systému nasazení softwaru doporučujeme vytvořit dva balíčky pro nasazení:</br>– NET Framework 4,7, které mohou zahrnovat restartování řadiče domény</br>– Senzor ATP Azure. </br>Zajistěte, aby byl balíček senzorů Azure ATP závislý na nasazení nasazení balíčku rozhraní .NET Framework. </br>Získejte [balíček pro nasazení rozhraní .NET Framework 4,7 offline](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows). 


Pomocí následujícího příkazu proveďte plně tichou instalaci senzoru ATP Azure:


**Syntaxe**:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"

> [!NOTE]
> Zkopírujte přístupový klíč z **konfiguračního** oddílu portálu Azure ATP na stránce **senzoru** .


**Možnosti instalace**:

> [!div class="mx-tableFixed"]
> 
> |Name|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
> |Help|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|

**Parametry instalace**:

> [!div class="mx-tableFixed"]
> 
> |Name|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
> |-------------|----------|---------|---------|
> |AccessKey|AccessKey="\*\*"|Ano|Nastaví přístupový klíč, který se používá k registraci snímače ATP Azure s instancí ATP Azure.|

**Příklady**: K tiché instalaci senzoru služby Azure ATP použijte následující příkaz:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="mmAOkLYCzfH8L/zUIsH24BIJBevlAWu7wUcSfIkRJufpuEojaDHYdjrNs0P3zpD+/bObKfLS0puD7biT5KDf3g=="

## <a name="proxy-authentication"></a>Ověřování proxy

K dokončení ověřování proxy použijte následující příkazy:

**Syntaxe**:


> [!div class="mx-tableFixed"]
> 
> |Name|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl = "https\://proxy.contoso.com:8080"|Ne|Určuje ProxyUrl a číslo portu snímače ATP Azure.|
> |ProxyUserName|ProxyUserName = "Contoso\ProxyUser"|Ne|Pokud vaše proxy služba vyžaduje ověření, zadejte uživatelské jméno ve formátu doména \ uživatel.|
> |ProxyUserPassword|ProxyUserPassword = "P@ssw0rd"|Ne|Určuje heslo pro uživatelské jméno proxy serveru. \* Přihlašovací údaje jsou šifrované a ukládají se místně pomocí snímače ATP Azure.|

## <a name="update-the-azure-atp-sensor"></a>Aktualizace snímače ATP Azure

K tiché aktualizaci senzoru služby Azure ATP použijte následující příkaz:

**Syntaxe**:

    Azure ATP sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Možnosti instalace**:

> [!div class="mx-tableFixed"]
> 
> |Name|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
> |Help|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|


**Příklady**: Postup při bezobslužné aktualizaci senzoru Azure ATP:

    Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Bezobslužná odinstalace senzoru Azure ATP

K provedení tiché odinstalace senzoru služby Azure ATP použijte následující příkaz: **Syntaxe**:

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]

**Možnosti instalace**:

> [!div class="mx-tableFixed"]
> 
> |Name|Syntaxe|Povinné pro bezobslužnou odinstalaci?|Popis|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Ano|Spustí odinstalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
> |Odinstalace|/uninstall|Ano|Spustí tichou odinstalaci snímače ATP Azure ze serveru.|
> |Help|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|

**Příklady**: Postup bezobslužné odinstalace senzoru služby Azure ATP ze serveru:


    Azure ATP sensor Setup.exe /quiet /uninstall




## <a name="see-also"></a>Viz také

- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Instalace senzoru služby Azure ATP](install-atp-step4.md)
- [Konfigurace senzoru služby Azure ATP](install-atp-step5.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

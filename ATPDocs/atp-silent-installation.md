---
title: Instalace Azure tiše rozšířené ochrany před internetovými útoky | Dokumentace Microsoftu
description: Popisuje postup při bezobslužné instalaci služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 12/05/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 76076a643b5edac6e2393b9c23045e89aee275a3
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077700"
---
# <a name="azure-atp-switches-and-silent-installation"></a>Azure ATP přepínače a bezobslužná instalace
Tento článek obsahuje pokyny pro služby Azure ATP přepínače a tichou instalaci.

## <a name="prerequisites"></a>Požadavky

Ochrana ATP v programu Azure vyžaduje instalaci rozhraní Microsoft .NET Framework 4.7. 

Při instalaci služby Azure ATP rozhraní .net Framework 4.7 je automaticky nainstalován jako součást svého nasazení služby Azure ATP.

> [!IMPORTANT] 
> Ujistěte se, že máte nejnovější verzi rozhraní .net Framework nainstalované. Pokud je nainstalována předchozí verze rozhraní .net, tichou instalaci vaší služby Azure ATP se zablokuje ve smyčce a schopen provést instalaci. 

> [!NOTE] 
> Instalace rozhraní .net framework 4.7 může vyžadovat restartování serveru. Při instalaci senzoru služby Azure ATP na řadičích domény, zvažte naplánování časového období údržby pro řadiče domény.
Pomocí služby Azure ATP tichou instalaci, instalační program je nakonfigurován na automatické restartování serveru na konci instalace (v případě potřeby). Ujistěte se, že spuštění bezobslužné instalace pouze během časového období údržby. Kvůli chybě Instalační služby systému Windows *norestart* příznak není možné spolehlivě použít k Ujistěte se, že server nerestartuje.

Můžete sledovat průběh nasazení, monitorujte instalační protokoly ochrany ATP v programu Azure, které jsou umístěny v **%AppData%\Local\Temp**.


## <a name="azure-atp-sensor-silent-installation"></a>Ochrana ATP v programu senzor tiché instalace služby Azure

> [!NOTE]
> Při tiché nasazení senzoru služby Azure ATP přes System Center Configuration Manager nebo jiného systému pro nasazení softwaru, doporučuje se vytvořit dva balíčky pro nasazení:</br>-Net frameworkem 4.7, které mohou zahrnovat restartování řadiče domény</br>– Snímač azure ochrany ATP v programu. </br>Ujistěte se, balíčku senzoru služby Azure ATP závisí na nasazení rozhraní .net Framework nasazení balíčku. </br>Získejte [rozhraní .net Framework 4.7 balíček pro offline nasazení](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows). 


Použijte následující příkaz k provedení plně tiché instalace senzoru služby Azure ATP:


**Syntaxe**:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"

> [!NOTE]
> Zkopírovat přístupový klíč z portálu služby Azure ATP **konfigurace** části **senzor** stránky.


**Možnosti instalace**:

> [!div class="mx-tableFixed"]
> 
> |Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
> |Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|

**Parametry instalace**:

> [!div class="mx-tableFixed"]
> 
> |Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
> |-------------|----------|---------|---------|
> |AccessKey|AccessKey="\*\*"|Ano|Nastaví přístupový klíč, který se použije k registraci senzoru služby Azure ATP s instancí služby Azure ATP.|

**Příklady**: Bezobslužná instalace senzoru služby Azure ATP použijte následující příkaz:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="mmAOkLYCzfH8L/zUIsH24BIJBevlAWu7wUcSfIkRJufpuEojaDHYdjrNs0P3zpD+/bObKfLS0puD7biT5KDf3g=="


## <a name="update-the-azure-atp-sensor"></a>Aktualizace senzoru služby Azure ATP

K bezobslužné aktualizaci senzoru služby Azure ATP použijte následující příkaz:

**Syntaxe**:

    Azure ATP sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Možnosti instalace**:

> [!div class="mx-tableFixed"]
> 
> |Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
> |Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|


**Příklady**: Bezobslužná aktualizace senzoru služby Azure ATP:

    Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Bezobslužná odinstalace senzoru služby Azure ATP

Použijte následující příkaz k provedení bezobslužné odinstalace senzoru služby Azure ATP: **Syntaxe**:

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]

**Možnosti instalace**:

> [!div class="mx-tableFixed"]
> 
> |Název|Syntaxe|Povinné pro bezobslužnou odinstalaci?|Popis|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Ano|Spustí odinstalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
> |Odinstalace|/uninstall|Ano|Spustí bezobslužnou odinstalaci senzoru služby Azure ATP ze serveru.|
> |Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|

**Příklady**: Bezobslužná odinstalace senzoru služby Azure ATP ze serveru:


    Azure ATP sensor Setup.exe /quiet /uninstall




## <a name="see-also"></a>Viz také

- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Instalace senzoru služby Azure ATP](install-atp-step4.md)
- [Konfigurace senzoru služby Azure ATP](install-atp-step5.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

---
title: Instalace Azure tiše rozšířené ochrany před internetovými útoky | Dokumentace Microsoftu
description: Popisuje postup při bezobslužné instalaci služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/7/2017
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 363400531fe2b4e2634fa80ec1f65ad80923606f
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125783"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


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
> Při tiché nasazení senzoru služby Azure ATP přes System Center Configuration Manager nebo jiného systému pro nasazení softwaru, doporučuje se vytvořit dva balíčky pro nasazení:</br>-Net frameworkem 4.7 včetně restartování řadiče domény</br>– Snímač azure ochrany ATP v programu. </br>Ujistěte se, balíčku senzoru služby Azure ATP závisí na nasazení rozhraní .net Framework nasazení balíčku. </br>Získejte [rozhraní .net Framework 4.7 balíček pro offline nasazení](https://www.microsoft.com/download/details.aspx?id=49982). 


Použijte následující příkaz k provedení plně tiché instalace senzoru služby Azure ATP:


**Syntaxe**:

    Azure ATP sensor Setup.exe /AccessKey=<Access Key> /quiet NetFrameworkCommandLineArguments ="/q" 
   

> [!NOTE]
> Zkopírovat přístupový klíč z portálu pracovního prostoru v části **konfigurace** a potom **senzor**.


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
|accessKey|AccessKey = "\*\*"|Ano|Nastaví přístupový klíč, který se použije k registraci senzoru služby Azure ATP s pracovním prostorem služby Azure ATP.|

**Příklady**: bezobslužné instalace senzoru služby Azure ATP, přihlaste se k doméně připojené k počítači pomocí přihlašovacích údajů správce ochrany ATP v programu Azure tak, že není potřeba zadat přihlašovací údaje jako součást instalace. V opačném případě ho zaregistrujte s cloudovou službou ochrany ATP v programu Azure, pomocí zadaných přihlašovacích údajů:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    AccessKey="3WlO0uKW7lY6Lk0+dfkfkJQ0qZV6aSq5WxLf71+fuBhggCl/BMs9JxfAwi7oy9vYGviazUS1EPpzte7z8s4grw==" 
    

## <a name="update-the-azure-atp-sensor"></a>Aktualizace senzoru služby Azure ATP

K bezobslužné aktualizaci senzoru služby Azure ATP použijte následující příkaz:

**Syntaxe**:

    Azure ATP sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Možnosti instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|


**Příklady**: bezobslužná aktualizace senzoru služby Azure ATP:

    Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Bezobslužná odinstalace senzoru služby Azure ATP

Použijte následující příkaz k provedení bezobslužné odinstalace senzoru služby Azure ATP: **syntaxe**:

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Možnosti instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou odinstalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí odinstalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Odinstalace|/uninstall|Ano|Spustí bezobslužnou odinstalaci senzoru služby Azure ATP ze serveru.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|

**Příklady**: bezobslužná odinstalace senzoru služby Azure ATP ze serveru:


    Azure ATP sensor Setup.exe /quiet /uninstall
    



## <a name="see-also"></a>Viz také

- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)

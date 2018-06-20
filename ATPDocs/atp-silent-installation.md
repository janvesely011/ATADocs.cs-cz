---
title: Instalace Azure Advanced Threat Protection bezobslužně | Microsoft Docs
description: Popisuje postup při bezobslužné instalaci Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/11/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f27020f1b4a5fa7aa8fefbda28eac0c2ad6c64d0
ms.sourcegitcommit: 912e453753156902618ae6ebb8489c2320c06fc6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/12/2018
ms.locfileid: "29856477"
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="azure-atp-silent-installation"></a>Azure ATP tichou instalaci
Tento článek obsahuje pokyny k bezobslužné instalaci Azure ATP.

## <a name="prerequisites"></a>Požadavky

Azure ATP vyžaduje instalaci rozhraní Microsoft .NET Framework 4.7. 

Když instalujete Azure ATP, rozhraní .net Framework 4.7 je automaticky nainstalován jako součást nasazení Azure ATP.

> [!IMPORTANT] 
> Ujistěte se, že máte nejnovější verzi rozhraní .net Framework nainstalované. Pokud je nainstalovaná předchozí verze rozhraní .net, Azure ATP bezobslužné instalace se zablokuje ve smyčce a instalace se nezdařilo. 

> [!NOTE] 
> Instalace rozhraní .net Framework 4.7 může vyžadovat restartování serveru. Při instalaci Azure ATP senzor na řadičích domény, zvažte naplánování časového období údržby pro tyto řadiče domény.
Při použití metody bezobslužné instalace Azure ATP, instalační program je nakonfigurován na automatické restartování serveru na konci instalace (v případě potřeby). Z důvodu chyby Instalační služby systému Windows *norestart* příznak nelze použít spolehlivě a ujistěte se server nerestartuje, takže nezapomeňte spustit tichou instalaci pouze během časového období údržby.

Pokud chcete sledovat průběh nasazení, monitorujte instalační protokoly Azure ATP, které jsou umístěny v **%AppData%\Local\Temp**.



## <a name="azure-atp-sensor-silent-installation"></a>Azure ATP senzor tichou instalaci

> [!NOTE]
> Pokud nasazujete bezobslužně senzoru Azure ATP přes System Center Configuration Manager nebo jiné systémy nasazení softwaru, se doporučuje vytvořit dva balíčky pro nasazení:</br>-Net Framework 4.7 včetně restartování řadiče domény</br>-Azure senzor ATP. </br>Balíček Azure ATP senzor, aby závislé na nasazení .net Framework – nasazení balíčku. </br>Získat [rozhraní .net Framework 4.7 offline nasazení balíčku](https://www.microsoft.com/download/details.aspx?id=49982). 


K bezobslužné instalaci senzoru Azure ATP použijte následující příkaz:

**Syntaxe**:

    Azure ATP sensor Setup.exe [/AccessKey=<Access Key>] [/quiet] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
   

> [!NOTE]
> Zkopírovat přístupový klíč z portálu prostoru v části **konfigurace** a potom **senzor**.


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
|AccessKey|AccessKey="**"|Ano|Nastaví přístupový klíč, který se použije k registraci senzoru Azure ATP s Azure ATP prostoru.|

**Příklady**: K bezobslužné instalaci Azure ATP senzoru, přihlaste se k doméně připojený k počítači pomocí přihlašovacích údajů správce Azure ATP tak, že není potřeba zadat přihlašovací údaje jako součást instalace. Jinak zaregistrujte si ho cloudové službě Azure ATP pomocí zadaných přihlašovacích údajů:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    AccessKey="3WlO0uKW7lY6Lk0+dfkfkJQ0qZV6aSq5WxLf71+fuBhggCl/BMs9JxfAwi7oy9vYGviazUS1EPpzte7z8s4grw==" 
    

## <a name="update-the-azure-atp-sensor"></a>Aktualizace senzoru Azure ATP

K bezobslužné aktualizaci senzoru Azure ATP použijte následující příkaz:

**Syntaxe**:

    Azure ATP  sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Možnosti instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí instalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ano|Určuje parametry pro instalaci rozhraní .Net Framework. K vynucení bezobslužné instalace rozhraní .Net Framework musí být nastavené.|


**Příklady**: bezobslužná aktualizace senzoru Azure ATP:

        Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Bezobslužná odinstalace senzoru Azure ATP

Použijte následující příkaz k provedení bezobslužné odinstalace senzoru Azure ATP: **syntaxe**:

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Možnosti instalace**:

> [!div class="mx-tableFixed"]
|Název|Syntaxe|Povinné pro bezobslužnou odinstalaci?|Popis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ano|Spustí odinstalační program, který nezobrazuje žádné uživatelské rozhraní ani výzvy.|
|Odinstalace|/uninstall|Ano|Spustí bezobslužnou odinstalaci senzoru Azure ATP ze serveru.|
|Nápověda|/help|Ne|Poskytuje nápovědu a stručnou referenční příručku. Zobrazí správné použití instalačních příkazů včetně seznamu všech možností a jejich chování.|

**Příklady**: bezobslužná odinstalace senzoru Azure ATP ze serveru:


    Azure ATP sensor Setup.exe /quiet /uninstall
    



## <a name="see-also"></a>Viz také

- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
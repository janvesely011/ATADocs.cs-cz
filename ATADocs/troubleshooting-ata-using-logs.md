---
title: Řešení potíží s Advanced Threat Analytics pomocí protokolů | Dokumentace Microsoftu
description: Popisuje, jak můžete protokoly ATA použít k řešení potíží.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 8/27/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cd4af40af83b060093b0b5822d0e9110a4ada4f0
ms.sourcegitcommit: bb33e24591acf11688955318b5938bc3d662a398
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2019
ms.locfileid: "70076644"
---
# <a name="troubleshooting-ata-using-the-ata-logs"></a>Řešení potíží s ATA pomocí protokolů ATA

*Platí pro: Advanced Threat Analytics verze 1,9*

Protokoly ATA poskytují přehled o tom, co jednotlivé komponenty ATA v libovolném časovém okamžiku dělají.

## <a name="ata-gateway-logs"></a>Protokoly ATA Gateway
V této části všechny odkazy na ATA Gateway platí také pro ATA Lightweight Gateway. 

Protokoly ATA Gateway jsou umístěné v podsložce s názvem **protokoly** , kde je nainstalovaný ATA. výchozí umístění je: **C:\Program Files\Microsoft Advanced Threat Analytics\\** . Ve výchozím umístění instalace je možné ji najít na adrese: **C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs**.

ATA Gateway využívá tyto protokoly:

-   **Microsoft.Tri.Gateway.log** – Tento protokol obsahuje všechno, co se děje v ATA Gateway (včetně překladu a chyb). Nejčastěji se využívá ke zjištění celkového stavu všech operací v chronologickém pořadí, ve kterém k nim došlo.

-   **Microsoft.Tri.Gateway-Resolution.log** – Tento protokol obsahuje podrobné informace o překladech entit, na které komponenta ATA Gateway narazila v provozu. Nejčastěji se využívá ke zkoumání příčin problémů s překladem entit.

-   **Microsoft.Tri.Gateway-Errors.log** – Tento protokol obsahuje jenom chyby, které zachytila komponenta ATA Gateway. Nejčastěji se využívá k provádění kontroly stavu a zkoumání příčin problémů, které je potřeba časově zařadit.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – V tomto protokolu jsou seskupeny všechny podobné chyby a výjimky a je zjištěn jejich počet.
    Tento protokol je při každém spuštění služby ATA Gateway prázdný a aktualizuje se každou minutu. Nejčastěji se využívá ke zjištění, jestli v komponentě ATA Gateway dochází k nějakým novým chybám nebo problémům (vzhledem k tomu, že chyby jsou seskupené, jsou přehlednější a je jednodušší zjistit, jestli dochází k nějakým novým problémům).
-   **Microsoft. Tri. Gateway.** provedet. log – Tento protokol se používá pro proces aktualizace brány, který zodpovídá za aktualizaci komponenty ATA Gateway, pokud je nakonfigurovaná tak, aby se automaticky provede. V případě ATA Lightweight Gateway je aktualizační proces také odpovědný za omezení prostředků ATA Lightweight Gateway.
-   **Microsoft.Tri.Gateway.Updater-ExceptionStatistics.log** – V tomto protokolu jsou seskupeny všechny podobné chyby a výjimky a je zjištěn jejich počet. Tento protokol je při každém spuštění služby ATA Updater prázdný a aktualizuje se každou minutu. Umožňuje zjistit, jestli ve službě ATA Updater nedošlo k novým chybám nebo problémům. Chyby jsou seskupené, jsou přehlednější a je jednodušší zjistit, jestli došlo k chybám nebo problémům nového typu.

> [!NOTE]
> První tři soubory protokolů mají maximální velikost až 50 MB. Při dosažení této velikosti se otevře nový soubor protokolu a předchozí je přejmenován na &lt;původní název souboru&gt;-Archived-00000 (číslo při každém přejmenování zvětší). Pokud již existuje více než 10 souborů stejného typu, budou nejstarší z nich ve výchozím nastavení odstraněny.

## <a name="ata-center-logs"></a>Protokoly ATA Center
Protokoly ATA Center jsou umístěné v podsložce s názvem **Logs**. Ve výchozím umístění instalace je možné ji najít na adrese: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs**".
> [!Note]
> Protokoly konzoly ATA, které se dříve ukládaly v protokolech služby IIS, se teď nachází v protokolech služby ATA Center.

ATA Center využívá tyto protokoly:

-   **Microsoft.Tri.Center.log** – – Tento protokol obsahuje všechno, co se děje v ATA Center (včetně detekce a chyb). Nejčastěji se využívá ke zjištění celkového stavu všech operací v chronologickém pořadí, ve kterém k nim došlo.

-   **Microsoft.Tri.Center-Detection.log** – Tento protokol obsahuje jenom podrobné informace o detekci komponenty ATA Center. Nejčastěji se využívá ke zkoumání příčin problémů s detekcí.

-   **Microsoft.Tri.Center-Errors.log** – Tento protokol obsahuje jenom chyby, které zachytila komponenta ATA Center. Nejčastěji se využívá k provádění kontroly stavu a zkoumání příčin problémů, které je potřeba časově zařadit.

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – V tomto protokolu jsou seskupeny všechny podobné chyby a výjimky a je zjištěn jejich počet.
    Tento protokol je při každém spuštění služby ATA Center prázdný a aktualizuje se každou minutu. Jeho hlavní použití je porozumění v případě, že došlo k nějakým novým chybám nebo problémům s komponentou ATA Center – protože chyby jsou seskupené, je snazší rychle pochopit, jestli došlo k nové chybě nebo problému.

> [!NOTE]
> První tři soubory protokolů mají maximální velikost až 50 MB. Při dosažení této velikosti se otevře nový soubor protokolu a předchozí je přejmenován na &lt;původní název souboru&gt;-Archived-00000 (číslo při každém přejmenování zvětší). Pokud již existuje více než 10 souborů stejného typu, budou nejstarší z nich ve výchozím nastavení odstraněny.


## <a name="ata-deployment-logs"></a>Protokoly nasazení ATA
Protokoly nasazení ATA jsou umístěné v adresáři temp uživatele, který příslušný produkt nainstaloval. Ve výchozím umístění instalace je možné ji najít na adrese: C:\Users přihlášeného **uživatele>\AppData\Local\Temp(nebojedenadresářnad%Temp%)\<** .

Protokoly nasazení komponenty ATA Center:

-   **Microsoft Advanced Threat Analytics Center_RRRRMMDDHHMMSS.log** – V tomto protokolu jsou uvedené kroky procesu nasazení komponenty ATA Center. Nejčastěji se využívá ke sledování procesu nasazení ATA Center.

-   **Microsoft Advanced Threat Analytics Center_RRRRMMDDHHMMSS_0_MongoDBPackage.log** – V tomto protokolu jsou uvedené kroky procesu nasazení MongoDB v komponentě ATA Center. Nejčastěji se využívá ke sledování procesu nasazení MongoDB.

-   **Microsoft Advanced Threat Analytics Center_RRRRMMDDHHMMSS_1_MsiPackage.log** – V tomto protokolu jsou uvedené kroky procesu nasazení binárních souborů ATA Center. Nejčastěji se využívá ke sledování nasazení binárních souborů ATA Center.

Protokoly nasazení ATA Gateway a ATA Lightweight Gateway:

-   **Microsoft Advanced Threat Analytics Gateway_RRRRMMDDHHMMSS.log** – V tomto protokolu jsou uvedené kroky procesu nasazení komponenty ATA Gateway. Nejčastěji se využívá ke sledování procesu nasazení ATA Gateway.

-   **Microsoft Advanced Threat Analytics Gateway_RRRRMMDDHHMMSS_001_MsiPackage.log** – V tomto protokolu jsou uvedené kroky procesu nasazení binárních souborů ATA Gateway. Nejčastěji se využívá ke sledování nasazení binárních souborů ATA Gateway.


> [!NOTE] 
> Kromě zde uvedených protokolů nasazení jsou k dispozici další protokoly, které začínají řetězcem Microsoft Advanced Threat Analytics. V nich můžete najít další informace k procesu nasazení.


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

---
title: "Řešení potíží s Advanced Threat Analytics pomocí protokolů | Dokumentace Microsoftu"
description: "Popisuje, jak můžete protokoly ATA použít k řešení potíží."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5bde3ff8abbdace3c56bb86b8889b53320470b00
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="troubleshooting-ata-using-the-ata-logs"></a>Řešení potíží s ATA pomocí protokolů ATA
Protokoly ATA poskytují přehled o tom, co jednotlivé komponenty ATA v libovolném časovém okamžiku dělají.

## <a name="ata-gateway-logs"></a>Protokoly ATA Gateway
V této části všechny odkazy na ATA Gateway platí také pro ATA Lightweight Gateway. 

Protokoly ATA Gateway jsou umístěné v podsložce s názvem **Protokoly** v místě, kde je služba ATA nainstalovaná. Výchozí umístění je **C:\Program Files\Microsoft Advanced Threat Analytics\**. Ve výchozí instalaci ji najdete tady: **C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs**.

ATA Gateway využívá tyto protokoly:

-   **Microsoft.Tri.Gateway.log** – Tento protokol obsahuje všechno, co se děje v ATA Gateway (včetně překladu a chyb). Nejčastěji se využívá ke zjištění celkového stavu všech operací v chronologickém pořadí, ve kterém k nim došlo.

-   **Microsoft.Tri.Gateway-Resolution.log** – Tento protokol obsahuje podrobné informace o překladech entit, na které komponenta ATA Gateway narazila v provozu. Nejčastěji se využívá ke zkoumání příčin problémů s překladem entit.

-   **Microsoft.Tri.Gateway-Errors.log** – Tento protokol obsahuje jenom chyby, které zachytila komponenta ATA Gateway. Nejčastěji se využívá k provádění kontroly stavu a zkoumání příčin problémů, které je potřeba časově zařadit.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – V tomto protokolu jsou seskupeny všechny podobné chyby a výjimky a je zjištěn jejich počet.
    Tento protokol je při každém spuštění služby ATA Gateway prázdný a aktualizuje se každou minutu. Nejčastěji se využívá ke zjištění, jestli v komponentě ATA Gateway dochází k nějakým novým chybám nebo problémům (vzhledem k tomu, že chyby jsou seskupené, jsou přehlednější a je jednodušší zjistit, jestli dochází k nějakým novým problémům).
-    **Microsoft.Tri.Gateway.Updater.log** – Tento protokol se používá pro aktualizační proces brány, který je zodpovědný za automatickou aktualizaci brány, pokud je tak nakonfigurován. V případě ATA Lightweight Gateway je aktualizační proces také odpovědný za omezení prostředků ATA Lightweight Gateway.
-    **Microsoft.Tri.Gateway.Updater-ExceptionStatistics.log** – V tomto protokolu jsou seskupeny všechny podobné chyby a výjimky a je zjištěn jejich počet. Tento protokol je při každém spuštění služby ATA Updater prázdný a aktualizuje se každou minutu. Umožňuje zjistit, jestli ve službě ATA Updater nedošlo k novým chybám nebo problémům. Chyby jsou seskupené, jsou přehlednější a je jednodušší zjistit, jestli došlo k chybám nebo problémům nového typu.

> [!NOTE]
> První tři soubory protokolů mají maximální velikost až 50 MB. Při dosažení této velikosti se otevře nový soubor protokolu a předchozí je přejmenován na &lt;původní název souboru&gt;-Archived-00000 (číslo při každém přejmenování zvětší). Pokud již existuje více než 10 souborů stejného typu, budou nejstarší z nich ve výchozím nastavení odstraněny.

## <a name="ata-center-logs"></a>Protokoly ATA Center
Protokoly ATA Center jsou umístěné v podsložce s názvem **Logs**. Ve výchozí instalaci ji najdete tady: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs**.
> [!Note]
> Protokoly konzoly ATA, které se dříve ukládaly v protokolech služby IIS, se teď nachází v protokolech služby ATA Center.

ATA Center využívá tyto protokoly:

-   **Microsoft.Tri.Center.log** – – Tento protokol obsahuje všechno, co se děje v ATA Center (včetně detekce a chyb). Nejčastěji se využívá ke zjištění celkového stavu všech operací v chronologickém pořadí, ve kterém k nim došlo.

-   **Microsoft.Tri.Center-Detection.log** – Tento protokol obsahuje jenom podrobné informace o detekci komponenty ATA Center. Nejčastěji se využívá ke zkoumání příčin problémů s detekcí.

-   **Microsoft.Tri.Center-Errors.log** – Tento protokol obsahuje jenom chyby, které zachytila komponenta ATA Center. Nejčastěji se využívá k provádění kontroly stavu a zkoumání příčin problémů, které je potřeba časově zařadit.

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – V tomto protokolu jsou seskupeny všechny podobné chyby a výjimky a je zjištěn jejich počet.
    Tento protokol je při každém spuštění služby ATA Center prázdný a aktualizuje se každou minutu. Nejčastěji se využívá ke zjištění, jestli ve službě ATA Center dochází k nějakým novým chybám nebo problémům. Vzhledem k tomu, že chyby jsou seskupené, jsou přehlednější a je jednodušší rychle zjistit, jestli došlo k novým chybám nebo problémům.

> [!NOTE]
> První tři soubory protokolů mají maximální velikost až 50 MB. Při dosažení této velikosti se otevře nový soubor protokolu a předchozí je přejmenován na &lt;původní název souboru&gt;-Archived-00000 (číslo při každém přejmenování zvětší). Pokud již existuje více než 10 souborů stejného typu, budou nejstarší z nich ve výchozím nastavení odstraněny.


## <a name="ata-deployment-logs"></a>Protokoly nasazení ATA
Protokoly nasazení ATA jsou umístěné v adresáři temp uživatele, který příslušný produkt nainstaloval. Ve výchozí instalaci tento adresář najdete tady: **C:\Users\Administrator\AppData\Local\Temp** (nebo v adresáři bezprostředně nadřazeném adresáři %temp%).

Protokoly nasazení komponenty ATA Center:

-   **Microsoft Advanced Threat Analytics Center_RRRRMMDDHHMMSS.log** – V tomto protokolu jsou uvedené kroky procesu nasazení komponenty ATA Center. Nejčastěji se využívá ke sledování procesu nasazení ATA Center.

-   **Microsoft Advanced Threat Analytics Center_RRRRMMDDHHMMSS_0_MongoDBPackage.log** – V tomto protokolu jsou uvedené kroky procesu nasazení MongoDB v komponentě ATA Center. Nejčastěji se využívá ke sledování procesu nasazení MongoDB.

-   **Microsoft Advanced Threat Analytics Center_RRRRMMDDHHMMSS_1_MsiPackage.log** – V tomto protokolu jsou uvedené kroky procesu nasazení binárních souborů ATA Center. Nejčastěji se využívá ke sledování nasazení binárních souborů ATA Center.

Protokoly nasazení ATA Gateway a ATA Lightweight Gateway:

-   **Microsoft Advanced Threat Analytics Gateway_RRRRMMDDHHMMSS.log** – V tomto protokolu jsou uvedené kroky procesu nasazení komponenty ATA Gateway. Nejčastěji se využívá ke sledování procesu nasazení ATA Gateway.

-   **Microsoft Advanced Threat Analytics Gateway_RRRRMMDDHHMMSS_001_MsiPackage.log** – V tomto protokolu jsou uvedené kroky procesu nasazení binárních souborů ATA Gateway. Nejčastěji se využívá ke sledování nasazení binárních souborů ATA Gateway.


## <a name="see-also"></a>Viz také
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurace shromažďování událostí](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurace předávání událostí systému Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

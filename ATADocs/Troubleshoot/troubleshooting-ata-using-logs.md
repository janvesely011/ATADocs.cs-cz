---
title: "Řešení potíží s ATA pomocí protokolů ATA | Microsoft Advanced Threat Analytics"
description: "Popisuje, jak můžete protokoly ATA použít k řešení potíží."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 4f02b0fba381eb76ad500e198392ec7624a3028a


---

# Řešení potíží s ATA pomocí protokolů ATA
Protokoly ATA poskytují přehled o tom, co jednotlivé komponenty ATA v libovolném časovém okamžiku dělají.

## Protokoly ATA Gateway
V této části všechny odkazy na ATA Gateway platí také pro ATA Lightweight Gateway. 

Protokoly ATA Gateway jsou umístěné v podsložce s názvem **Logs**. Ve výchozí instalaci ji najdete tady: **C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs**.

ATA Gateway využívá tyto protokoly:

-   **Microsoft.Tri.Gateway.log** – Tento protokol obsahuje všechno, co se děje v ATA Gateway (včetně překladu a chyb). Nejčastěji se využívá ke zjištění celkového stavu všech operací v chronologickém pořadí, ve kterém k nim došlo.

-   **Microsoft.Tri.Gateway-Resolution.log** – Tento protokol obsahuje podrobné informace o překladech entit, na které komponenta ATA Gateway narazila v provozu. Nejčastěji se využívá ke zkoumání příčin problémů s překladem entit.

-   **Microsoft.Tri.Gateway-Errors.log** – Tento protokol obsahuje jenom chyby, které zachytila komponenta ATA Gateway. Nejčastěji se využívá k provádění kontroly stavu a zkoumání příčin problémů, které je potřeba časově zařadit.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – V tomto protokolu jsou seskupeny všechny podobné chyby a výjimky a je zjištěn jejich počet.
    Tento protokol je při každém spuštění služby ATA Gateway prázdný a aktualizuje se každou minutu. Nejčastěji se využívá ke zjištění, jestli v komponentě ATA Gateway dochází k nějakým novým chybám nebo problémům. Vzhledem k tomu, že chyby jsou seskupené, jsou přehlednější a je jednodušší zjistit, jestli došlo k chybě nebo problému nového typu.

> [!NOTE]
> První tři soubory protokolů mají maximální velikost až 50 MB. Při dosažení této velikosti se otevře nový soubor protokolu a předchozí je přejmenován na &lt;původní název souboru&gt;-Archived-00000 (číslo při každém přejmenování zvětší).

## Protokoly ATA Center
Protokoly ATA Center jsou umístěné v podsložce s názvem **Logs**. Ve výchozí instalaci ji najdete tady: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs**.

ATA Center využívá tyto protokoly:

-   **Microsoft.Tri.Center.log** – – Tento protokol obsahuje všechno, co se děje v ATA Center (včetně detekce a chyb). Nejčastěji se využívá ke zjištění celkového stavu všech operací v chronologickém pořadí, ve kterém k nim došlo.

-   **Microsoft.Tri.Center-Detection.log** – Tento protokol obsahuje jenom podrobné informace o detekci komponenty ATA Center. Nejčastěji se využívá ke zkoumání příčin problémů s detekcí.

-   **Microsoft.Tri.Center-Errors.log** – Tento protokol obsahuje jenom chyby, které zachytila komponenta ATA Center. Nejčastěji se využívá k provádění kontroly stavu a zkoumání příčin problémů, které je potřeba časově zařadit.

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – V tomto protokolu jsou seskupeny všechny podobné chyby a výjimky a je zjištěn jejich počet.
    Tento protokol je při každém spuštění služby ATA Center prázdný a aktualizuje se každou minutu. Nejčastěji se využívá ke zjištění, jestli v komponentě ATA Center dochází k nějakým novým chybám nebo problémům. Vzhledem k tomu, že chyby jsou seskupené, jsou přehlednější a je jednodušší zjistit, jestli došlo k chybě nebo problému nového typu.

> [!NOTE]
> První tři soubory protokolů mají maximální velikost až 50 MB. Při dosažení této velikosti se otevře nový soubor protokolu a předchozí je přejmenován na &lt;původní název souboru&gt;-Archived-00000 (číslo při každém přejmenování zvětší).

## Protokoly konzoly ATA
Protokoly konzoly ATA (protokoly rozhraní API pro správu) jsou umístěné v podsložce s názvem **Logs**. Ve výchozí instalaci ji najdete tady: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Management\Logs**.

Konzola ATA využívá tyto protokoly:

-   **w3wp.log** – Tento protokol obsahuje všechno, k čemu dojde v procesu správy (IIS).


-   **w3wp-Errors.log** – Tento protokol obsahuje jenom chyby, které zachytil proces správy (IIS).


-   **8e75f9f1-ExceptionStatistics.log** – V tomto protokolu jsou seskupeny všechny podobné chyby a výjimky a je zjištěn jejich počet.
    Tento protokol je při každém spuštění služby brány prázdný a aktualizuje se každou minutu. Nejčastěji se využívá ke zjištění, jestli v komponentě ATA Center dochází k nějakým novým chybám nebo problémům. Vzhledem k tomu, že chyby jsou seskupené, jsou přehlednější a je jednodušší zjistit, jestli došlo k chybě nebo problému nového typu.

> [!NOTE]
> První dva soubory protokolů mají maximální velikost až 50 MB. Při dosažení této velikosti se otevře nový soubor protokolu a předchozí je přejmenován na &lt;původní název souboru&gt;-Archived-00000 (číslo při každém přejmenování zvětší).

## Protokoly nasazení ATA
Protokoly nasazení ATA jsou umístěné v adresáři temp uživatele, který příslušný produkt nainstaloval. Ve výchozí instalaci tento adresář najdete tady: **C:\Users\Administrator\AppData\Local\Temp** (nebo v adresáři bezprostředně nadřazeném adresáři %temp%).

Protokoly nasazení komponenty ATA Center:

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log** – V tomto protokolu jsou uvedené kroky procesu nasazení komponenty ATA Center. Nejčastěji se využívá ke sledování procesu nasazení ATA Center.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log** – V tomto protokolu jsou uvedené kroky procesu nasazení MongoDB v komponentě ATA Center. Nejčastěji se využívá ke sledování procesu nasazení MongoDB.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log** – V tomto protokolu jsou uvedené kroky procesu nasazení binárních souborů ATA Center. Nejčastěji se využívá ke sledování nasazení binárních souborů ATA Center.

Protokoly nasazení ATA Gateway a ATA Lightweight Gateway:

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log** – V tomto protokolu jsou uvedené kroky procesu nasazení komponenty ATA Gateway. Nejčastěji se využívá ke sledování procesu nasazení ATA Gateway.

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log** – V tomto protokolu jsou uvedené kroky procesu nasazení binárních souborů ATA Gateway. Nejčastěji se využívá ke sledování nasazení binárních souborů ATA Gateway.

## Viz také
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurace sběru událostí](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurace předávání událostí systému Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->



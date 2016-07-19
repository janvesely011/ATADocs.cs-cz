---
title: "Správa nastavení telemetrie | Microsoft Advanced Threat Analytics"
description: "Popisuje data shromážděná ATA a poskytuje postup, jak shromažďování dat vypnout."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: c6b3196f6093b909e8d97f9a9ac230e35807eb72


---

# Správa nastavení telemetrie
Advanced Threat Analytics (ATA) shromažďuje anonymních telemetrická data o ATA a odesílá je přes připojení HTTPS na servery Microsoftu.  Tato data Microsoft používá k vylepšení budoucích verzích ATA.

## Shromažďovaná data
Shromážděná anonymizovaná data zahrnují následující:

-   Čítače výkonu z ATA Center a ATA Gateway

-   ID produktu z licencovaných kopií ATA

-   Datum nasazení ATA Center

-   Počet nasazených ATA Gateway

-   Následující anonymizované informace služby Active Directory:

    -   ID domény pro doménu, jejíž název bude první při abecedním řazení

    -   Počet řadičů domény

    -   Počet řadičů domény monitorovaných pomocí ATA prostřednictvím zrcadlení portů

    -   Počet webů

    -   Počet počítačů

    -   Počet skupin

    -   Počet uživatelů

-   Podezřelé aktivity – Pro každou podezřelou aktivitu se shromažďují následující data:

    (Názvy počítačů, uživatelská jména a IP adresy se **neshromažďují**.)

    -   Typ podezřelé aktivity

    -   ID podezřelé aktivity

    -   Stav

    -   Počáteční a koncový čas

    -   Zadaný vstup

### Zakázání shromažďování dat
Chcete-li zastavit shromažďování a odesílání telemetrických dat Microsoftu, proveďte následující kroky:

1.  Přihlaste se ke konzole ATA, na panelu nástrojů klikněte na tlačítko se třemi tečkami a vyberte **O aplikaci**.

2.  Zrušte zaškrtnutí políčka **Send us usage information to help improve your customer experience in the future** (Posílat nám informace o použití k vylepšení zkušeností uživatelů v budoucnosti).

## Viz také
- [Co je nového ve verzi 1.6](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->



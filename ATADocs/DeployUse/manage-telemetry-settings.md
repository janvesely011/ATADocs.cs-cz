---
title: "Správa nastavení telemetrie | Dokumentace Microsoftu"
description: "Popisuje data shromážděná ATA a poskytuje postup, jak shromažďování dat vypnout."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: c7366dcc2cbd7a9eba1503e5af3290ec4ac73c32


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="manage-telemetry-settings"></a>Správa nastavení telemetrie
Advanced Threat Analytics (ATA) shromažďuje anonymních telemetrická data o ATA a odesílá je přes připojení HTTPS na servery Microsoftu.  Tato data Microsoft používá k vylepšení budoucích verzích ATA.

## <a name="data-collected"></a>Shromažďovaná data
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

- Problémy se stavem – pro každý problém se stavem jsou shromažďovány následující anonymizované údaje:

    (Názvy počítačů, uživatelská jména a IP adresy se neshromažďují.)

    -   Typ problému se stavem

    -   ID problému se stavem

    -   Stav

    -   Počáteční a koncový čas

- Adresa URL konzoly ATA – adresy URL při používání konzoly ATA, tzn. navštívené stránky v konzole ATA.


### <a name="disable-data-collection"></a>Zakázání shromažďování dat
Chcete-li zastavit shromažďování a odesílání telemetrických dat Microsoftu, proveďte následující kroky:

1.  Přihlaste se ke konzole ATA, na panelu nástrojů klikněte na tlačítko se třemi tečkami a vyberte **O aplikaci**.

2.  Zrušte zaškrtnutí políčka **Send us usage information to help improve your customer experience in the future** (Posílat nám informace o použití k vylepšení zkušeností uživatelů v budoucnosti).

## <a name="see-also"></a>Viz také
- [Co je nového ve verzi 1.6](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jan17_HO1-->



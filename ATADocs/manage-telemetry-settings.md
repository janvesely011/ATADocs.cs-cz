---
title: Správa protokolů generována Advanced Threat Analytics | Microsoft Docs
description: Popisuje data shromážděná ATA a poskytuje postup, jak shromažďování dat vypnout.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 17e5778543b9f08d3157ed91cb0a7a73ea268c0a
ms.sourcegitcommit: 3539dd3f9ab7729e5326b904fc64985c808bc8ce
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2018
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="manage-system-generated-logs-note"></a>Spravovat generována protokoly > [!NOTE]
> Pokud vás zajímá zobrazení nebo odstranění osobních údajů, přečtěte si pokyny společnosti Microsoft v [správce dodržování předpisů Microsoft](https://servicetrust.microsoft.com/ComplianceManager) a v [GDPR části webu Microsoft 365 Enterprise dodržování předpisů] (https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr]. Pokud hledáte obecné informace o GDPR, přečtěte si téma [GDPR části portálu služby důvěřovat](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).


Advanced Threat Analytics (ATA) shromažďuje anonymizovaná data protokolu generována týkající se ATA a odesílá je přes připojení HTTPS k serverům Microsoftu.  Tato data Microsoft používá k vylepšení budoucích verzích ATA.

## <a name="data-collected"></a>Shromažďovaná data
Shromážděná anonymizovaná data zahrnují následující parametry:

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

- Adresa URL konzoly ATA adresy - adresy URL při použití konzoly ATA, to znamená, navštívené stránky v konzole ATA.


### <a name="disable-data-collection"></a>Zakázání shromažďování dat
Chcete-li zastavit shromažďování a odesílání telemetrických dat Microsoftu, proveďte následující kroky:

1.  Přihlaste se ke konzole ATA, na panelu nástrojů klikněte na tlačítko se třemi tečkami a vyberte **O aplikaci**.

2.  Zrušte zaškrtnutí políčka **Send us usage information to help improve your customer experience in the future** (Posílat nám informace o použití k vylepšení zkušeností uživatelů v budoucnosti).

## <a name="see-also"></a>Viz také
- [Řešení problémů s ATA pomocí protokolu událostí](troubleshooting-ata-using-logs.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

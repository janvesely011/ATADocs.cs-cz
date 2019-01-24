---
title: Správa systémem generovaných protokolů Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje data shromážděná ATA a poskytuje postup, jak shromažďování dat vypnout.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/19/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 36ba5f6e79743065ba3579fa72aa752ad8a63534
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2019
ms.locfileid: "54839596"
---
# <a name="manage-system-generated-logs"></a>Správa systémem generovaných protokolů

*Platí pro: Advanced Threat Analytics verze 1.9*

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

 > [!NOTE]
 > Advanced Threat Analytics (ATA) shromažďuje anonymizované systémem generovaných protokolů týkající se ATA a odesílá je přes připojení HTTPS k serverům Microsoftu. Tato data Microsoft používá k vylepšení budoucích verzích ATA.

## <a name="data-collected"></a>Data shromážděná

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

- Adresa URL konzoly ATA – adresy URL při používání konzoly ATA, to znamená, navštívené stránky v konzole ATA.


### <a name="disable-data-collection"></a>Zakázat shromažďování dat
Chcete-li zastavit shromažďování a odesílání telemetrických dat Microsoftu, proveďte následující kroky:

1.  Přihlaste se ke konzole ATA, na panelu nástrojů klikněte na tlačítko se třemi tečkami a vyberte **O aplikaci**.

2.  Zrušte zaškrtnutí políčka **Send us usage information to help improve your customer experience in the future** (Posílat nám informace o použití k vylepšení zkušeností uživatelů v budoucnosti).

## <a name="see-also"></a>Viz také
- [Řešení problémů s ATA pomocí protokolu událostí](troubleshooting-ata-using-logs.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

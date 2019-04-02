---
title: Správa systémem generovaných protokolů Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje data shromážděná ATA a poskytuje postup, jak shromažďování dat vypnout.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 8/19/2018
ms.topic: article
ms.prod: advanced-threat-analytics
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e5766e409a1e2bb3f463e10459045f5a233c1fe1
ms.sourcegitcommit: 38b68d96fbf04fe40e1f9a62a1af3d1d00e63614
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/02/2019
ms.locfileid: "58808134"
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

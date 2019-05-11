---
title: Monitorování stavu a událostí systému Advanced Threat Analytics | Dokumentace Microsoftu
description: ATA Health Center vám umožňuje zjistit, jak služba ATA funguje, a upozorní vás na potenciální problémy. Systémové události si můžete prohlédnout v Prohlížeči událostí.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b425e4cbd923cfe75269eb22e47da3128fbf4d78
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196269"
---
# <a name="working-with-ata-system-health-and-events"></a>Práce se stavem a událostmi systému ATA

*Platí pro: Advanced Threat Analytics verze 1.9*

## <a name="ata-health-center"></a>ATA Health Center

ATA Health Center umožňuje sledovat, jak funguje služba ATA, a upozorňuje na problémy.

## <a name="working-with-the-ata-health-center"></a>Práce s ATA Health Center
ATA Health Center vás upozorní na problém zobrazením výstrahy (červené tečky) nad ikonou Health Center v řádku nabídek.

![Panel nástrojů s červenou tečkou ATA Health Center](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Správa stavu ATA
Pokud chcete zkontrolovat celkový stav systému, klepněte na ikonu Health Center v řádku nabídek. ![Ikona ATA Health Center](media/ATA-red-dot.png)

-   Všechny otevřené výstrahy můžete spravovat jejich nastavením na **Zavřít**, **potlačit**, nebo **odstranit** kliknutím na tři tečky v pravém rohu výstrahy a zvolení požadované možnosti.

-   **Otevřít**: V tomto seznamu se zobrazí všechny nové podezřelé aktivity.

-   **Zavřít**: Slouží ke sledování podezřelých aktivit, které identifikovali, prozkoumali a opravili zmírnit.

    > [!NOTE]
    > ATA může znovu otevřít uzavřené aktivitu, pokud se stejná aktivita zjistí během krátké doby znovu.

-   **Potlačit**: Potlačení aktivity znamená, že chcete prozatím ignorovat a pouze znovu upozorněni při novou instanci. Pokud je podobná upozornění ATA nebude ho znovu otevřít. Ale pokud výstrahy po dobu sedmi dní zastaví a pak se znovu objeví, budete upozorněni znovu.

- **Odstranit**: Pokud výstrahu odstraníte, odstraní se ze systému, z databáze a nebudete moci obnovit. Po kliknutí na možnost pro odstranění budete moct odstranit všechny podezřelé aktivity stejného typu.



![Obrázek problémů ATA Health Center](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Viz také

- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

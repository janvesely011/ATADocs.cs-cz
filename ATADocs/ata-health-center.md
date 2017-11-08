---
title: "Monitorování stavu a událostí systému Advanced Threat Analytics | Dokumentace Microsoftu"
description: "ATA Health Center vám umožňuje zjistit, jak služba ATA funguje, a upozorní vás na potenciální problémy. Systémové události si můžete prohlédnout v Prohlížeči událostí."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e5009d126f3c1b9d73f064787049068b071c5319
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*


# <a name="working-with-ata-system-health-and-events"></a>Práce se stavem a událostmi systému ATA

## <a name="ata-health-center"></a>ATA Health Center
ATA Health Center umožňuje sledovat, jak funguje služba ATA, a upozorňuje na problémy.

## <a name="working-with-the-ata-health-center"></a>Práce s ATA Health Center
ATA Health Center vás upozorní na problém zobrazením výstrahy (červené tečky) nad ikonou Health Center v řádku nabídek.

![Panel nástrojů s červenou tečkou ATA Health Center](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Správa stavu ATA
Pokud chcete zkontrolovat celkový stav systému, klepněte na ikonu Health Center v řádku nabídek. ![Ikona ATA Health Center](media/ATA-red-dot.png)

-   Všechny otevřené výstrahy můžete spravovat jejich nastavením na **Zavřít**, **potlačit**, nebo **odstranit** kliknutím na tlačítko se třemi tečkami v horním rohu výstrahy a provedením váš výběr.

-   **Open** (Otevřeno): V tomto seznamu se zobrazí všechny nové podezřelé aktivity.

-   **Zavřít**: slouží ke sledování podezřelých aktivit, které určili, prozkoumali a opravili omezeny.

    > [!NOTE]
    > ATA může znovu otevřít uzavřenou aktivitu, pokud se stejná aktivita zjistí během krátké doby znovu.

-   **Suppressed** (Potlačeno): Potlačení aktivity znamená, že ji chcete prozatím ignorovat a upozornění chcete zobrazit, jenom pokud se bude jednat o novou instanci. Pokud je podobné výstrahy ATA nebude ho znovu otevřít. Ale pokud výstrahu zastaví sedm dní a potom je opět zobrazit, budete upozorněni znovu.

- **Odstranit**: Pokud odstraníte výstrahu, je odstraněn ze systému, z databáze a nebudete moci obnovit. Po kliknutí na možnost pro odstranění budete moct odstranit všechny podezřelé aktivity stejného typu.



![Obrázek problémů ATA Health Center](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Viz také

- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

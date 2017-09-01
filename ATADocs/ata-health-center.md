---
title: "Monitorování stavu a událostí systému Advanced Threat Analytics | Dokumentace Microsoftu"
description: "ATA Health Center vám umožňuje zjistit, jak služba ATA funguje, a upozorní vás na potenciální problémy. Systémové události si můžete prohlédnout v Prohlížeči událostí."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/28/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cdd046eeaca1d8aeb7ea3afa001b34b82cb468b0
ms.sourcegitcommit: 46dd0e695f16a0dd23bbfa140eba15ea6a34d7af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2017
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

-   **Closed** (Uzavřeno): Slouží ke sledování podezřelých aktivit, které jste identifikovali, prozkoumali a opravili s cílem zmírnit jejich dopad.

    > [!NOTE]
    > ATA může znovu otevřít uzavřenou aktivitu, pokud se stejná aktivita zjistí během krátké doby znovu.

-   **Suppressed** (Potlačeno): Potlačení aktivity znamená, že ji chcete prozatím ignorovat a upozornění chcete zobrazit, jenom pokud se bude jednat o novou instanci. Znamená to, že pokud se vyskytne podobná výstraha, služba ATA ji neotevře. Pokud se ale výstraha na 7 dní zastaví a pak se znovu objeví, budete znovu upozorněni.

- **Delete** (Odstranit): Pokud výstrahu odstraníte, odstraní se z databáze v systému a NEBUDE možné ji obnovit. Po kliknutí na možnost pro odstranění budete moct odstranit všechny podezřelé aktivity stejného typu.



![Obrázek problémů ATA Health Center](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Viz také

- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

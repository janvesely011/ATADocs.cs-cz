---
title: "Sledování výstrah Advanced Threat Analytics Health Center | Dokumentace Microsoftu"
description: "ATA Health Center slouží ke kontrole, jak funguje služba ATA, a upozorňuje na potenciální problémy."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e929714ca33dfaa82bdf93dbaf230abadef1b86d
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="ata-health-center"></a>ATA Health Center
ATA Health Center umožňuje sledovat, jak funguje služba ATA, a upozorňuje na problémy.

## <a name="working-with-the-ata-health-center"></a>Práce s ATA Health Center
ATA Health Center vás upozorní na problém zobrazením výstrahy (červené tečky) nad ikonou Health Center v řádku nabídek.

![Panel nástrojů s červenou tečkou ATA Health Center](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Správa stavu ATA
Pokud chcete zkontrolovat celkový stav systému, klepněte na ikonu Health Center v řádku nabídek. ![Ikona ATA Health Center](media/ATA-red-dot.png)

-   Všechny otevřené výstrahy můžete spravovat jejich nastavením na **Vyřešeno** nebo **Zamítnuto**. Ve výstraze klikněte na **Otevřete** a přejděte dolů buď na **Vyřešeno** nebo **Zamítnuto**.

-   Pokud vyřešíte problém a ATA zjistí, že problém trvá, přesune se problém automaticky zpátky do seznamu **otevřených** problémů. Pokud ATA zjistí, že otevřený problém se vyřešil, přesune se automaticky do seznamu **vyřešených** problémů.

-   **Zamítnuté** problémy jsou problémy, které nemá ATA nadále kontrolovat. Pokud se například zobrazí upozornění na problém, o kterém víte a který nemáte v plánu řešit, ale nechcete o něm dostávat oznámení a nechcete ho zobrazovat v seznamu **otevřených** problémů, můžete ho nastavit na **Zamítnuto**.

![Obrázek problémů ATA Health Center](media/ATA-Health-Issue.JPG)

## <a name="see-also"></a>Viz také
- [Práce s nastavením detekce ATA](working-with-detection-settings.md)
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

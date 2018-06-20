---
title: Sledování stavu systému Azure Advanced Threat Protection a událostí | Microsoft Docs
description: Použití Azure ATP prostoru health center zkontrolujte, jak funguje služba Azure ATP a upozorňuje na potenciální problémy a zobrazení události systému v prohlížeči událostí.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 86eb90f452d5aee2504e525e64bfc62c22207880
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446019"
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="working-with-azure-atp-workspace-health-and-events"></a>Práce s Azure ATP prostoru stavu a události

## <a name="azure-atp-workspace-health-center"></a>Azure ATP prostoru health center 

Azure ATP prostoru health center vás informuje, jaký je výkon pracovního prostoru Azure ATP a problémů, když dochází k problémům.

## <a name="working-with-the-azure-atp-workspace-health-center"></a>Práce s Azure ATP prostoru health center

Azure ATP prostoru health center umožňuje vědět, že je problém zobrazením výstrahy (červené tečky) nad ikonou Health Center v řádku nabídek.

![Azure ATP prostoru health center červené tečky panelu nástrojů](media/atp-health-bar.png)

### <a name="managing-azure-atp-workspace-health"></a>Správa stavu prostoru Azure ATP
Pokud chcete zkontrolovat na celkový stav pracovního prostoru, klikněte na ikonu Health Center v řádku nabídek ![Ikona health center Azure ATP pracovního prostoru](media/atp-red-dot.png)

-   Všechny otevřené problémy lze spravovat jejich nastavením na **Zavřít**, nebo **potlačit**, kliknutím na tlačítko se třemi tečkami v horním rohu výstrahy a provedením váš výběr.

-   **Open** (Otevřeno): V tomto seznamu se zobrazí všechny nové podezřelé aktivity.

-   **Zavřít**: slouží ke sledování podezřelých aktivit, které určili, prozkoumali a opravili omezeny.

    > [!NOTE]
    > Azure ATP může znovu otevřít uzavřenou aktivitu, pokud se stejná aktivita zjistí během krátké doby znovu.
    > Každý pracovní prostor má svou vlastní health center.

-   **Suppressed** (Potlačeno): Potlačení aktivity znamená, že ji chcete prozatím ignorovat a upozornění chcete zobrazit, jenom pokud se bude jednat o novou instanci. Pokud je o podobnou výstrahu jako Azure ATP nepodporuje ho znovu otevřít. Ale pokud výstrahu zastaví sedm dní a potom je opět zobrazit, budete upozorněni znovu.

-   **Znovu otevřete**: Pokud zavřete nebo potlačit problém, můžete ho znovu otevřít tak, aby se otevřete v časové ose znovu.
- 
- **Odstranit**: Z v rámci časové osy podezřelých aktivit, máte také možnost odstranit potíže se stavem. Pokud odstraníte výstrahu, odstraní se z pracovního prostoru a nebudete moci obnovit. Po kliknutí na možnost pro odstranění budete moct odstranit všechny podezřelé aktivity stejného typu.



![Azure ATP prostoru health center problémy image](media/atp-health-issue.png)






## <a name="see-also"></a>Viz také

- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)

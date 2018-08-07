---
title: Monitorování stavu systému Azure Advanced Threat Protection a událostí | Dokumentace Microsoftu
description: Health center pracovní prostor ochrany ATP v programu Azure použít ke kontrole, jak funguje služba ochrany ATP v programu Azure a upozorní vás na potenciální problémy a zobrazit systémové události v prohlížeči událostí.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/05/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5fb4acaca989922ad894cee4a799378bb912643d
ms.sourcegitcommit: 14c05a210ae92d35100c984ff8c6d171db7c3856
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2018
ms.locfileid: "39567980"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="working-with-azure-atp-workspace-health-and-events"></a>Práce s události a stav pracovního prostoru služby Azure ATP

## <a name="azure-atp-workspace-health-center"></a>Centrum stavu pracovního prostoru Azure ochrany ATP v programu 

Health center pracovní prostor ochrany ATP v programu Azure vám umožňuje vědět, jaký je výkon vašeho pracovního prostoru ochrana ATP v programu Azure a vás upozorní, když dochází k problémům.

## <a name="working-with-the-azure-atp-workspace-health-center"></a>Práce s health center pracovní prostor služby Azure ATP

Health center pracovní prostor ochrany ATP v programu Azure vám umožňuje vědět, že dojde k problému zobrazením výstrahy (červené tečky) nad ikonou Health Center v řádku nabídek.

![Ochrana ATP v programu pracovní prostor health center červená tečka nástrojů webu Azure](media/atp-health-bar.png)

### <a name="managing-azure-atp-workspace-health"></a>Správa stavu pracovního prostoru služby Azure ATP
Pokud chcete zkontrolovat celkový stav pracovního prostoru, klikněte na ikonu Health Center v řádku nabídek ![Ikona stavu centra Azure ochrany ATP v programu pracovního prostoru](media/atp-red-dot.png)

-   Všechny otevřené problémy můžete spravovat jejich nastavením na **Zavřít**, nebo **potlačit**, kliknutím na tři tečky v pravém rohu výstrahy a zvolení požadované možnosti.

-   **Open** (Otevřeno): V tomto seznamu se zobrazí všechny nové podezřelé aktivity.

-   **Zavřít**: slouží ke sledování podezřelých aktivit, které identifikovali, prozkoumali a opravili zmírnit.

    > [!NOTE]
    > Ochrana ATP v programu Azure může znovu otevřít uzavřené aktivitu, pokud se stejná aktivita zjistí během krátké doby znovu.
    > Každý pracovní prostor má svůj vlastní stav centra.

-   **Suppressed** (Potlačeno): Potlačení aktivity znamená, že ji chcete prozatím ignorovat a upozornění chcete zobrazit, jenom pokud se bude jednat o novou instanci. Pokud je o podobnou výstrahu jako ochrana ATP v programu Azure nebude ho znovu otevřít. Ale pokud výstrahy po dobu sedmi dní zastaví a pak se znovu objeví, budete upozorněni znovu.

-   **Znovu otevřít**: aby se zobrazovala Open můžete znovu otevřít uzavřeného nebo Potlačené problém znovu na časové ose.
- 
- **Odstranit**: Z v rámci časové osy podezřelých aktivit, máte také možnost odstranění problému se stavem. Pokud výstrahu odstraníte, odstraní se z pracovního prostoru a nebudete moci obnovit. Po kliknutí na možnost pro odstranění budete moct odstranit všechny podezřelé aktivity stejného typu.



![Azure ochrany ATP v programu pracovní prostor health center problémy image](media/atp-health-issue.png)






## <a name="see-also"></a>Viz také

- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)

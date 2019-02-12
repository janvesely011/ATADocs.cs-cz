---
title: Monitorování stavu systému Azure Advanced Threat Protection a událostí | Dokumentace Microsoftu
description: Pomocí služby Azure ATP health center zkontrolujte fungování služby Azure ATP a upozorní vás na potenciální problémy a zobrazit systémové události v prohlížeči událostí.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/3/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: be907aa307a0ac8f7d8b7a971e1c891bfa318bad
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076330"
---
# <a name="work-with-azure-atp-health-and-events"></a>Práce s události a stav služby Azure ATP

## <a name="azure-atp-health-center"></a>Centrum stavu služby Azure ochrany ATP v programu 

Health center ochrany ATP v programu Azure vám umožňuje vědět, jaký je výkon vaší instance služby Azure ATP a vás upozorní, když dochází k problémům.

## <a name="working-with-the-azure-atp-health-center"></a>Práce s Azure ATP health center

Health center ochrany ATP v programu Azure vám umožňuje vědět, že dojde k problému zobrazením výstrahy (červené tečky) nad ikonou Health Center v řádku nabídek.

![Azure ochrany ATP v programu health center červená tečka nástrojů](media/atp-health-bar.png)

### <a name="managing-azure-atp-health"></a>Správa stavu služby Azure ATP
Pokud chcete zkontrolovat celkový stav vaší instance služby Azure ATP, klikněte na ikonu Health Center v řádku nabídek ![Azure ikona center stavu ochrany ATP v programu](media/atp-red-dot.png)

-   Všechny otevřené problémy můžete spravovat jejich nastavením na **Zavřít**, nebo **potlačit**, kliknutím na tři tečky v pravém rohu výstrahy a zvolení požadované možnosti.

-   **Otevřít**: V tomto seznamu se zobrazí všechny nové podezřelé aktivity.

-   **Zavřít**: Slouží ke sledování podezřelých aktivit, které identifikovali, prozkoumali a opravili zmírnit.

    > [!NOTE]
    > Ochrana ATP v programu Azure může znovu otevřít uzavřené aktivitu, pokud se stejná aktivita zjistí během krátké doby znovu.
    
-   **Potlačit**: Potlačení aktivity znamená, že chcete prozatím ignorovat a pouze znovu upozorněni při novou instanci. Pokud je o podobnou výstrahu jako ochrana ATP v programu Azure nebude ho znovu otevřít. Ale pokud výstrahy po dobu sedmi dní zastaví a pak se znovu objeví, budete upozorněni, znovu.

-   **Znovu otevřít**: Aby se zobrazovala jako můžete znovu otevřít uzavřeného nebo Potlačená výstraha **otevřít** znovu na časové ose.

-   **Odstranit**: Z v rámci časové osy výstrah zabezpečení, máte také možnost odstranění problému se stavem. Pokud výstrahu odstraníte, odstraní se z instance a nebudete moci obnovit. Po kliknutí na odstranit, budete moct odstranit všechny výstrahy zabezpečení stejného typu.



![Azure problémy obrázek ochrany ATP v programu health center](media/atp-health-issue.png)






## <a name="see-also"></a>Viz také

- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

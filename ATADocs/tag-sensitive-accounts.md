---
title: "Značka citlivé účty s ATA | Microsoft Docs"
description: "Popisuje, jak k označování citlivé účty pomocí Advanced Threat Analytics (ATA)"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d9666c0a4fb3aad027ac1f85719bc533e919d75a
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/22/2018
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="tag-sensitive-accounts"></a>Značka citlivé účty

Můžete ručně označit skupiny nebo účty jako citlivé pro zlepšení detekce. Je důležité, abyste měli jistotu, že to je aktualizovat, protože některé ATA detekuje, jako je například zjišťování úpravy citlivou skupinu a cestu laterální pohyb, závisí na které skupiny a účty se považují za citlivé. Dříve, ATA automaticky považováno entity *citlivé* Pokud byl uživatel členem na konkrétní seznam skupin. Můžete teď ručně označit jiné uživatele nebo skupiny jako písmena, například členové Rady, vedení společnosti, ředitel prodeje, atd., a ATA bude zvažovat je citlivé.

1.  V konzole ATA klikněte na **konfigurace** ozubené kolo v panelu nabídek.

2.  V části **detekce,** klikněte na tlačítko **značek entit**.

    ![Značky entity ATA](media/entity-tags.png)

3.  V **citlivé** části, zadejte název **citlivé účty** a **citlivých skupin** a pak klikněte na  **+**  Přihlaste se do je přidejte.

    ![Ukázka zpřístupnění citlivých účtů ATA](media/sensitive-account-sample.png)

4. Klikněte na **Uložit**.

5. Přejděte na stránku profil entity kliknutím na název entity. Zde bude moci zobrazit, proč entity jsou považovány za citlivé – ať už z důvodu členství ve skupině nebo z důvodu ruční označování jako důvěrné.

     
## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

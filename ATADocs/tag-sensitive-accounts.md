---
title: Označit citlivých účtů pomocí ATA | Dokumentace Microsoftu
description: Popisuje, jak k označování citlivých účtů s využitím Advanced Threat Analytics (ATA)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cea6d666d3d969070541fc8dcc4fd59726ac8c38
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2018
ms.locfileid: "46134077"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="tag-sensitive-accounts"></a>Označování citlivých účtů

Můžete ručně označit skupiny nebo účty jako citlivé vylepšit detekce. Je důležité, abyste měli jistotu, že to je aktualizovat, protože některé detekce ATA, jako je například zjišťování úpravy citlivých skupin a cesty laterální pohyb, závisí na jaké skupiny a účty se považují za citlivé. Dříve, ATA automaticky považována za entity *citlivé* Pokud byl členem konkrétní seznam skupin. Nově můžete ručně označit jiné uživatele nebo skupiny jako citlivé, jako je například členů vedení společnosti, ředitel pro prodej, atd. a ATA bude předpokládat, že jejich citlivé.

1.  V konzole ATA klikněte **konfigurace** ozubeného kola v panelu nabídek.

2.  V části **detekce,** klikněte na tlačítko **značky entit**.

    ![Značky entit ATA](media/entity-tags.png)

3.  V **citlivé** části, zadejte název **citlivých účtů** a **citlivých skupin** a potom klikněte na tlačítko **+** podpis je přidat.

    ![Ukázka ATA k citlivým účtům](media/sensitive-account-sample.png)

4. Klikněte na **Uložit**.

5. Přejděte na stránku profil entity kliknutím na název entity. Tady budete moci zobrazit, proč entity se považuje za citlivé – ať už kvůli členství ve skupině nebo z důvodu ruční označování jako citlivé.


## <a name="sensitive-groups"></a>Citlivé skupiny

Následující seznam skupin se považují za citlivé řešením ATA. Za citlivou se považuje každá entita, která je členem těchto skupin:

-   Administrators
-   Power Users
-   Account Operators
-   Server Operators
-   Print Operators
-   Backup Operators
-   Replicators
-   Remote Desktop Users 
-   Network Configuration Operators 
-   Incoming Forest Trust Builders
-   Domain Admins
-   Domain Controllers
-   Group Policy Creator Owners 
-   Řadiče domény jen pro čtení 
-   Enterprise Read-only Domain Controllers 
-   Schema Admins 
-   Enterprise Admins
     
## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

---
title: Značka citlivé účty s Azure ATP | Microsoft Docs
description: Popisuje, jak k označování citlivé účty pomocí Azure Advanced Threat Protection (ATP)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4270ebda76309e19518f9d49b72bbce7f9bb5f32
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446054"
---
*Platí pro: Azure Advanced Threat Protection verze 1.9*



# <a name="working-with-sensitive-accounts"></a>Práce s citlivé účty

## <a name="sensitive-groups"></a>Citlivé skupiny

Následující seznam skupin se považují za citlivé Azure ATP. Za citlivou se považuje každá entita, která je členem těchto skupin:

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
-   Řadiče domény jen pro čtení Enterprise 
-   Schema Admins 
-   Enterprise Admins


## <a name="tagging-sensitive-accounts"></a>Označování citlivé účty

Kromě těchto skupin můžete ručně označit skupiny nebo účty jako citlivé pro zlepšení detekce. To je důležité, protože využívají detekce, některá ATP Azure, jako je detekce úpravy citlivou skupinu a laterální pohyb cestu, na které skupiny a účty se považují za citlivé. Můžete ručně označit jiné uživatele nebo skupiny jako písmena, například členové Rady, vedení společnosti, ředitel prodeje, atd., a Azure ATP je považuje za citlivé.

1.  Na portálu Azure ATP pracovního prostoru klikněte **konfigurace** ozubené kolo v panelu nabídek.

2.  V části **detekce** klikněte na tlačítko **značek entit**.

    ![Azure značek entit ATP](media/entity-tags.png)

3.  V **citlivé** části, zadejte název **citlivé účty** a **citlivých skupin** a pak klikněte na  **+**  Přihlaste se do je přidejte.

    ![Ukázka zpřístupnění citlivých účtů Azure ATP](media/sensitive-account-sample.png)

4. Klikněte na **Uložit**.

    
## <a name="see-also"></a>Viz také

- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
---
title: Označit citlivých účtů pomocí služby Azure ATP | Dokumentace Microsoftu
description: Popisuje, jak k označování citlivých účtů pomocí Azure Advanced Threat Protection (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ccb87ab6b3fabed5edaf7c32324701c74259f098
ms.sourcegitcommit: 5ff50807f855db1051b977a64eb6e90487ea196c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750433"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="working-with-sensitive-accounts"></a>Práce s citlivými účty

## <a name="sensitive-groups"></a>Citlivé skupiny

Následující seznam skupin se považují za citlivé ochrany ATP v programu Azure. Za citlivou se považuje každá entita, která je členem těchto skupin:

-   Administrators
-   Power Users
-   Account Operators
-   Server Operators
-   Print Operators
-   Backup Operators
-   Replicators
-   Network Configuration Operators 
-   Incoming Forest Trust Builders
-   Domain Admins
-   Domain Controllers
-   Group Policy Creator Owners 
-   Řadiče domény jen pro čtení 
-   Enterprise Read-only Domain Controllers 
-   Schema Admins 
-   Enterprise Admins

 > [!NOTE]
 > . Září 2018 Remote Desktop Users byly také automaticky považují za citlivé pomocí služby Azure ATP. Vzdálené plochy entity nebo přidat po tohoto data již nebude automaticky označené jako citlivé při vzdálené plochy entity nebo skupiny přidat před tímto datem může zůstat označeno jako citlivé. Toto citlivá nastavení lze změnit teď ručně.  

## <a name="tagging-sensitive-accounts"></a>Označování citlivých účtů

Kromě těchto skupin můžete ručně označit skupiny nebo účty jako citlivé vylepšit detekce. To je důležité, protože využívají některé služby Azure ATP detekce, jako je například zjišťování úpravy citlivých skupin a cesty laterální pohyb, které skupiny a účty se považují za citlivé. Můžete ručně označit jiné uživatele nebo skupiny jako citlivé, jako je například členů vedení společnosti, ředitel pro prodej, atd., a ochrana ATP v programu Azure je považuje za citlivé.

1.  Na portálu ochrany ATP v programu Azure pracovní prostor, klikněte na tlačítko **konfigurace** ozubeného kola v panelu nabídek.

2.  V části **detekce** klikněte na tlačítko **značky entit**.

    ![Značky entit Azure ATP](media/entity-tags.png)

3.  V **citlivé** části, zadejte název **citlivých účtů** a **citlivých skupin** a potom klikněte na tlačítko **+** podpis je přidat.

    ![Ukázkový k citlivým účtům Azure ATP](media/sensitive-account-sample.png)

4. Klikněte na **Uložit**.

    
## <a name="see-also"></a>Viz také

- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
---
title: Označit citlivých účtů pomocí služby Azure ATP | Dokumentace Microsoftu
description: Popisuje, jak k označování citlivých účtů pomocí Azure Advanced Threat Protection (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 10/04/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3314c91dfab988ad128d97f68ab435764f589fe8
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263331"
---
# <a name="working-with-sensitive-accounts"></a>Práce s citlivými účty

## <a name="sensitive-groups"></a>Citlivé skupiny

Následující seznam skupin se považují za citlivé ochrany ATP v programu Azure. Za citlivou se považuje každá entita, která je členem těchto skupin:

- Správci
- Power Users
- Account Operators
- Server Operators
- Print Operators
- Backup Operators
- Replicators
- Network Configuration Operators 
- Incoming Forest Trust Builders
- Domain Admins
- Domain Controllers
- Group Policy Creator Owners 
- Řadiče domény jen pro čtení 
- Enterprise Read-only Domain Controllers 
- Schema Admins 
- Enterprise Admins

  > [!NOTE]
  > Do září 2018 Remote Desktop Users byly také automaticky považují za citlivé pomocí služby Azure ATP. Vzdálené plochy entity nebo přidat po tohoto data již nebude automaticky označené jako citlivé při vzdálené plochy entity nebo skupiny přidat před tímto datem může zůstat označeno jako citlivé. Toto citlivá nastavení lze změnit teď ručně.  

## <a name="tagging-sensitive-accounts"></a>Označování citlivých účtů

Kromě těchto skupin můžete ručně označit skupiny nebo účty jako citlivé vylepšit detekce. To je důležité, protože využívají některé služby Azure ATP detekce, jako je například zjišťování úpravy citlivých skupin a cesty laterální pohyb, které skupiny a účty se považují za citlivé. Můžete ručně označit jiné uživatele nebo skupiny jako citlivé, jako je například členů vedení společnosti, ředitel pro prodej, atd., a ochrana ATP v programu Azure je považuje za citlivé.

1.  Na portálu ochrany ATP v programu Azure klikněte **konfigurace** ozubeného kola v panelu nabídek.

2.  V části **detekce** klikněte na tlačítko **značky entit**.

    ![Značky entit Azure ATP](media/entity-tags.png)

3.  V **citlivé** části, zadejte název **citlivých účtů** a **citlivých skupin** a potom klikněte na tlačítko **+** podpis je přidat.

    ![Ukázkový k citlivým účtům Azure ATP](media/sensitive-account-sample.png)

4. Klikněte na **Uložit**.

    
## <a name="see-also"></a>Viz také:

- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

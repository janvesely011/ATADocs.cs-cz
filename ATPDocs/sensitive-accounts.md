---
title: Označit citlivých účtů pomocí služby Azure ATP | Dokumentace Microsoftu
description: Popisuje, jak k označování citlivých účtů pomocí Azure Advanced Threat Protection (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/29/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2342a10f932664568065d2ef906d863a875c8096
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196448"
---
# <a name="working-with-sensitive-accounts"></a>Práce s citlivými účty

## <a name="sensitive-entites"></a>Citlivých entit

Následující seznam skupin jsou považovány za **citlivé** pomocí služby Azure ATP. Každá entita, která je členem jedné z těchto skupin se považuje za citlivé:

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
- Microsoft Exchange Servers

  > [!NOTE]
  > Do září 2018 Remote Desktop Users byly také automaticky považují za citlivé pomocí služby Azure ATP. Vzdálené plochy entity nebo přidat po tohoto data již nebude automaticky označené jako citlivé při vzdálené plochy entity nebo skupiny přidat před tímto datem může zůstat označeno jako citlivé. Toto citlivá nastavení lze změnit teď ručně.  

## <a name="tagging-sensitive-accounts"></a>Označování citlivých účtů

Kromě těchto skupin můžete ručně označit skupiny nebo účty jako citlivé vylepšit detekce. To je důležité, protože využívají některé služby Azure ATP detekce, jako je například citlivou skupinu úpravy detekce a laterální pohyb cesty, které skupiny a účty se považují za citlivé. Můžete ručně označit jiné uživatele nebo skupiny jako citlivé, jako je například členů vedení společnosti, ředitel pro prodej, atd., a ochrana ATP v programu Azure je považuje za citlivé.

1.  Na portálu ochrany ATP v programu Azure klikněte **konfigurace** ozubeného kola v panelu nabídek.

2.  V části **detekce** klikněte na tlačítko **značky entit**.

    ![Značky entit Azure ATP](media/entity-tags.png)

3.  V **citlivé** části, zadejte název **citlivých účtů** a **citlivých skupin** a potom klikněte na tlačítko **+** podpis je přidat.

    ![Ukázkový k citlivým účtům Azure ATP](media/sensitive-account-sample.png)

4. Klikněte na **Uložit**.

    
## <a name="see-also"></a>Viz také:

- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

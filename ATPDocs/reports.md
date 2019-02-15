---
title: Práce se sestavami ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Popisuje, jak můžete generovat sestavy služby Azure ATP pro monitorování vaší sítě.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 11/26/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0b5eec603b2402551eca464917e0311a46a8f5dd
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263212"
---
# <a name="azure-atp-reports"></a>Sestavy služby Azure ATP

Část sestavy ochrany ATP v programu Azure na portálu ochrany ATP v programu Azure umožňuje naplánovat nebo okamžitě vygenerování a stažení sestavy, které vám poskytnou informace o stavu systému a entity. Z funkce sestavy můžete vytvořit sestavy o stavu systému, výstrahy zabezpečení a potenciální cesty taktiky Lateral Movement zjištěných ve vašem prostředí.


Pokud chcete získat přístup na stránku sestav, klikněte na ikonu sestav na řádku nabídek: ![ikona sestav](./media/atp-report-icon.png).
Jsou k dispozici sestavy: 

- **Souhrnná sestava**: Souhrnná sestava představuje řídicí panel stavu systému. Můžete zobrazit tři karty – **Souhrn** co bylo zjištěno ve vaší síti **otevřené podezřelé aktivity** , který obsahuje seznam podezřelých aktivit, které byste měli věnovat pozornost, a **otevřete stavu problémy s** , že seznamy můžete problémy se stavem služby Azure ATP byste měli věnovat pozornost. Podezřelé aktivity, které jsou uvedené, jsou rozdělené podle typu, stejně jako problémy se stavem. 

- **Úprava citlivých skupin**: Tato sestava obsahuje seznam pokaždé, když změny citlivých skupin (například správce, nebo ručně označené účty nebo skupiny). Pokud používáte služby Azure ATP samostatné snímačů, aby bylo možné zobrazit úplnou sestavu o citlivých skupin, ujistěte se, že [události jsou předány z řadičů domény senzorů samostatné](configure-event-forwarding.md). 

- **Hesla odhalená v nešifrovaném textu**: Některé služby používat nezabezpečené protokolu LDAP k odesílání přihlašovací údaje k účtu v prostém textu. To může nastat i pro citlivé účty. Útočníci monitorování síťového provozu můžete zachytit a pak znovu použít tyto přihlašovací údaje ke škodlivým účelům. Tato sestava uvádí všechny počítače a účtu hesla zdroje detekovaných službou Azure ATP odesílány ve formátu prostého textu. 

- **Laterální pohyb cesty k citlivým účtům**: Tato sestava obsahuje citlivé účty, které jsou zveřejňovány prostřednictvím cesty taktiky Lateral Movement. Další informace najdete v tématu [laterální pohyb cesty](use-case-lateral-movement-path.md). Tato sestava shromáždí potenciální cesty taktiky Lateral Movement, které byly zjištěny v období vytváření sestav, které vyberete. 

Existují dva způsoby, jak vygenerovat sestavu: na vyžádání nebo na základě naplánování pravidelného odesílání sestav e-mailem.

Vygenerování sestavy na vyžádání:

1. V řádku nabídek portálu ochrany ATP v programu Azure klikněte na ikonu sestav na řádku nabídek: ![ikona sestav](./media/atp-report-icon.png).

2. V části Typ vybranou sestavu, nastavit **z** a **k** kalendářních dat a klikněte na tlačítko **Stáhnout**. 
 ![sestavy](./media/reports.png)

Nastavení naplánované sestavy:
 
1. V **sestavy** klikněte na **nastavit plánované sestavy**, nebo na stránce Konfigurace portálu ochrany ATP v programu Azure v rámci oznámení a sestavy, klikněte na tlačítko **naplánované sestavy**.

   ![Plánování sestav](./media/atp-sched-reports.png)
 
   > [!NOTE]
   > Ve výchozím nastavení denními sestavami jsou určeny k odeslány brzy po půlnoci UTC. Můžete si vyberte vlastní čas pomocí možnosti Výběr času. 

2. Klikněte na tlačítko **plán** vedle vašeho typu vybranou sestavu, nastavit četnost a e-mailovou adresu pro doručení sestavy. Je sestava, kterou vyberete četností informace obsažené v sestavě. Přidat e-mailové adresy, klikněte na znaménko plus vedle pole e-mailové adresy, zadejte adresu a klepněte na **Uložit**.

   ![Naplánování četnosti sestav a e-mailů](./media/sched-report1.png)


## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

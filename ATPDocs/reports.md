---
title: Práce se sestavami ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Popisuje, jak můžete generovat sestavy služby Azure ATP pro monitorování vaší sítě.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 367ad07bd1d0be80486bfc10c2b70546d360805c
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783181"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="azure-atp-reports"></a>Sestavy služby Azure ATP

Část sestavy ochrany ATP v programu Azure na portálu ochrany ATP v programu Azure umožňuje generovat sestavy, které vám poskytnou informace o stavu systému, stavu systému a sestavu o podezřelých aktivitách zjištěných ve vašem prostředí.


Pokud chcete získat přístup na stránku sestav, klikněte na ikonu sestav na řádku nabídek: ![ikona sestav](./media/atp-report-icon.png).
Dostupné sestavy: 

- **Souhrnná sestava**: Souhrnná sestava představuje řídicí panel stavu systému. Můžete zobrazit tři karty – **Souhrn** co bylo zjištěno ve vaší síti **otevřené podezřelé aktivity** , který obsahuje seznam podezřelých aktivit, které byste měli věnovat pozornost, a **otevřete stavu problémy s** , že seznamy můžete problémy se stavem služby Azure ATP byste měli věnovat pozornost. Podezřelé aktivity, které jsou uvedené, jsou rozdělené podle typu, stejně jako problémy se stavem. 

- **Úprava citlivých skupin**: Tato sestava obsahuje seznam pokaždé, když změny citlivých skupin (například správce, nebo ručně označené účty nebo skupiny). Pokud používáte služby Azure ATP samostatné senzory, chcete-li zobrazit úplnou sestavu o citlivých skupin, je třeba Ujistěte se, že [události jsou předány z řadičů domény senzorů samostatné](configure-event-forwarding.md). 

- **Hesla odhalená v nešifrovaném textu**: Některé služby používat nezabezpečené protokolu LDAP k odesílání přihlašovací údaje k účtu v prostém textu. To může nastat i pro citlivé účty. Útočníci monitorování síťového provozu můžete zachytit a pak znovu použít tyto přihlašovací údaje ke škodlivým účelům. Tato sestava obsahuje seznam všech zdrojového počítače a hesla k účtům, které služby Azure ATP zjistilo, že se odesílají ve formátu prostého textu. 

- **Laterální pohyb cesty k citlivým účtům**: Tato sestava obsahuje citlivé účty, které jsou zveřejňovány prostřednictvím cesty taktiky Lateral Movement. Další informace najdete v tématu [laterální pohyb cesty](use-case-lateral-movement-path.md). Tato sestava shromáždí cesty, které se vytvořily za posledních 60 dnů, na rozdíl od informace zobrazí na portálu pracovního prostoru, která představuje jenom dva dny.

Existují dva způsoby, jak vygenerovat sestavu: na vyžádání nebo na základě naplánování pravidelného odesílání sestav e-mailem.

Vygenerování sestavy na vyžádání:

1. V řádku nabídek portálu ochrany ATP v programu Azure klikněte na ikonu sestav na řádku nabídek: ![ikona sestav](./media/atp-report-icon.png).

2. V části Typ vybranou sestavu, nastavit **z** a **k** kalendářních dat a klikněte na tlačítko **Stáhnout**. 
 ![sestavy](./media/reports.png)

Nastavení naplánované sestavy:
 
1. V **sestavy** klikněte na **nastavit plánované sestavy**, nebo na stránce Konfigurace portálu pracovního prostoru ochrana ATP v programu Azure v rámci oznámení a sestavy, klikněte na tlačítko **naplánované sestavy**.

   ![Plánování sestav](./media/atp-sched-reports.png)
 
 > [!NOTE]
 > Denní sestavy jsou určeny k odeslány brzy po půlnoci UTC.

2. Klikněte na tlačítko **plán** vedle vašeho typu vybranou sestavu, nastavit četnost a e-mailovou adresu pro doručení sestav a klikněte na znaménko plus vedle e-mailové adresy je přidat, a klikněte na **Uložit**.

   ![Naplánování četnosti sestav a e-mailů](./media/sched-report1.png)


## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
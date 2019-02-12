---
title: Práce se sestavami ATA | Dokumentace Microsoftu
description: V tomto tématu je popsáno, jak můžete generovat sestavy ATA k monitorování sítě.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2f25df9545fb4c7b0c269679d92b1a08d2330666
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076211"
---
# <a name="ata-reports"></a>Sestavy ATA


*Platí pro: Advanced Threat Analytics verze 1.9*

Část pro sestavy ATA v konzole umožňuje generovat sestavy, které poskytují informace o stavu systému obsahující informace o stavu i podezřelých aktivitách zjištěných ve vašem prostředí.

Pokud chcete získat přístup na stránku sestav, klikněte na ikonu sestav na řádku nabídek: ![ikona sestav](./media/ata-report-icon.png).
Dostupné sestavy: 

- **Souhrnná sestava**: Souhrnná sestava představuje řídicí panel stavu systému. Můžete zobrazit tři karty – **Summary** (Souhrn) se souhrnnými informacemi o tom, co bylo zjištěno ve vaší síti, **Open suspicious activities** (Otevřít podezřelé aktivity) s informacemi o podezřelých aktivitách, kterým byste měli věnovat pozornost, a **Open health issues** (Otevřené problémy se stavem), kde najdete seznam problémů se stavem služby ATA, kterým byste měli věnovat pozornost. Podezřelé aktivity, které jsou uvedené, jsou rozdělené podle typu, stejně jako problémy se stavem. 

- **Úprava citlivých skupin**: Tato sestava obsahuje seznam pokaždé, když změny citlivých skupin (např. admins).

- **Hesla odhalená v nešifrovaném textu**: Některé služby používat nezabezpečené protokolu LDAP k odesílání přihlašovací údaje k účtu v prostém textu. To může nastat i pro citlivé účty. Útočníci monitorování síťového provozu můžete zachytit a pak znovu použít tyto přihlašovací údaje ke škodlivým účelům. Tato sestava uvádí všechny počítače a účtu hesla zdroje, které ATA zjistilo, že se odesílají ve formátu prostého textu. 

- **Laterální pohyb cesty k citlivým účtům**: Tato sestava obsahuje citlivé účty, které jsou zveřejňovány prostřednictvím cesty taktiky Lateral Movement. Další informace najdete v tématu [laterální pohyb cesty](use-case-lateral-movement-path.md)

Existují dva způsoby, jak vygenerovat sestavu: na vyžádání nebo na základě naplánování pravidelného odesílání sestav e-mailem.

Vygenerování sestavy na vyžádání:

1. Na řádku nabídek na konzole ATA klikněte na ikonu sestav: ![ikona sestav](./media/ata-report-icon.png).

2. V části Typ vybranou sestavu, nastavit **z** a **k** kalendářních dat a klikněte na tlačítko **Stáhnout**. 
 ![sestavy](./media/reports.png)

Nastavení naplánované sestavy:
 
1. Na stránce **Reports** (Sestavy) klikněte na **Set scheduled reports** (Nastavit plánované sestavy) nebo na stránce konfigurace konzoly ATA v části Notifications and Reports (Oznámení a sestavy) klikněte na **Scheduled reports** (Naplánované sestavy).

   ![Plánování sestav](./media/ata-sched-reports.png)

   > [!NOTE]
   > Denní sestavy jsou určeny k odeslány brzy po půlnoci UTC.

2. Klikněte na tlačítko **plán** vedle vašeho typu vybranou sestavu, nastavit četnost a e-mailovou adresu pro doručení sestav a klikněte na znaménko plus vedle e-mailové adresy je přidat, a klikněte na **Uložit**.

   ![Naplánování četnosti sestav a e-mailů](./media/sched-report1.png)


> [!NOTE]
> Naplánované sestavy jsou doručovány e-mailem a může odeslat pouze pokud jste už nakonfigurovali e-mailový server v části **konfigurace** a pak v části **oznámení a sestavy**vyberte **e-mailu Server**.


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

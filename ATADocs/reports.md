---
title: Práce se sestavami ATA | Dokumentace Microsoftu
description: V tomto tématu je popsáno, jak můžete generovat sestavy ATA k monitorování sítě.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/27/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 9a113d8d090c5a90a07043a0ef75e1be0fc840c3
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
*Platí pro: Advanced Threat Analytics verze 1.9*


# <a name="ata-reports"></a>Sestavy ATA

Část pro sestavy ATA v konzole umožňuje generovat sestavy, které poskytují informace o stavu systému obsahující informace o stavu i podezřelých aktivitách zjištěných ve vašem prostředí.

Pokud chcete získat přístup na stránku sestav, klikněte na ikonu sestav na řádku nabídek: ![ikona sestav](./media/ata-report-icon.png).
Dostupné sestavy: 

- **Souhrnná sestava**: Souhrnná sestava uvede řídicí panel stavu systému. Můžete zobrazit tři karty – **Summary** (Souhrn) se souhrnnými informacemi o tom, co bylo zjištěno ve vaší síti, **Open suspicious activities** (Otevřít podezřelé aktivity) s informacemi o podezřelých aktivitách, kterým byste měli věnovat pozornost, a **Open health issues** (Otevřené problémy se stavem), kde najdete seznam problémů se stavem služby ATA, kterým byste měli věnovat pozornost. Podezřelé aktivity, které jsou uvedené, jsou rozdělené podle typu, stejně jako problémy se stavem. 

- **Úprava citlivých skupin**: Tato sestava obsahuje seznam pokaždé, když změny do citlivých skupin (například admins).

- **Hesla, které jsou zveřejněné jako nezašifrovaný text**: Některé služby používat nezabezpečené protokolu LDAP k odesílání přihlašovací údaje účtu ve formátu prostého textu. Tomu může dojít i pro citlivé účty. Útočníci monitorování síťového provozu můžete zachytit a pak znovu použít tyto přihlašovací údaje zlými úmysly. Tato sestava obsahuje seznam všech zdrojového počítače a účtu hesel, která ATA zjistil, že je odesláno jako nezašifrovaný text. 

- **Pomoci odhalit laterální pohyb cesty k citlivým účtům**: Tato sestava obsahuje seznam citlivé účty, které jsou zveřejňovány prostřednictvím cesty laterální pohyb. Další informace najdete v tématu [pomoci odhalit laterální pohyb cesty](use-case-lateral-movement-path.md)

Existují dva způsoby, jak vygenerovat sestavu: na vyžádání nebo na základě naplánování pravidelného odesílání sestav e-mailem.

Vygenerování sestavy na vyžádání:

1. Na řádku nabídek na konzole ATA klikněte na ikonu sestav: ![ikona sestav](./media/ata-report-icon.png).

2. V části buď typ vašeho vybranou sestavu, nastavit **z** a **k** kalendářních dat a klikněte na tlačítko **Stáhnout**. 
 ![sestavy](./media/reports.png)

Nastavení naplánované sestavy:
 
1. Na stránce **Reports** (Sestavy) klikněte na **Set scheduled reports** (Nastavit plánované sestavy) nebo na stránce konfigurace konzoly ATA v části Notifications and Reports (Oznámení a sestavy) klikněte na **Scheduled reports** (Naplánované sestavy).

   ![Plánování sestav](./media/ata-sched-reports.png)

  > [!NOTE]
  > Denní zprávy jsou navrženy pro odeslání krátce po půlnoci času UTC.

2. Klikněte na tlačítko **plán** vedle vašeho typu vybranou sestavu, nastavit četnost a e-mailovou adresu pro doručení sestavy, a klikněte na znaménko plus vedle e-mailové adresy je přidat, a klikněte na **Uložit**.

   ![Naplánování četnosti sestav a e-mailů](./media/sched-report1.png)


> [!NOTE]
> Naplánované sestavy jsou doručovány prostřednictvím e-mailu a může odeslat pouze pokud jste již nakonfigurovali e-mailový server v části **konfigurace** a pak v části **oznámení a sestavy**, vyberte **e-mailu Server**.


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

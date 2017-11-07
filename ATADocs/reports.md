---
title: "Práce se sestavami ATA | Dokumentace Microsoftu"
description: "V tomto tématu je popsáno, jak můžete generovat sestavy ATA k monitorování sítě."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ecc249ca6a16e151f250c2596e8b2d21d9314499
ms.sourcegitcommit: e2cb3af9c1dbb0b75946dc70cc439b19d654541c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/06/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*


# <a name="ata-reports"></a>Sestavy ATA

Část pro sestavy ATA v konzole umožňuje generovat sestavy, které poskytují informace o stavu systému obsahující informace o stavu i podezřelých aktivitách zjištěných ve vašem prostředí.

Pokud chcete získat přístup na stránku sestav, klikněte na ikonu sestav na řádku nabídek: ![ikona sestav](./media/ata-report-icon.png).
Dostupné sestavy: 
- Souhrnná sestava: Souhrnná sestava představuje řídicí panel stavu systému. Můžete zobrazit tři karty – **Summary** (Souhrn) se souhrnnými informacemi o tom, co bylo zjištěno ve vaší síti, **Open suspicious activities** (Otevřít podezřelé aktivity) s informacemi o podezřelých aktivitách, kterým byste měli věnovat pozornost, a **Open health issues** (Otevřené problémy se stavem), kde najdete seznam problémů se stavem služby ATA, kterým byste měli věnovat pozornost. Podezřelé aktivity, které jsou uvedené, jsou rozdělené podle typu, stejně jako problémy se stavem. 
- Změny citlivých skupin: V této sestavě je uvedená každá změna provedená v důvěrných skupinách (např. admins).

Existují dva způsoby, jak vygenerovat sestavu: na vyžádání nebo na základě naplánování pravidelného odesílání sestav e-mailem.

Vygenerování sestavy na vyžádání:

1. Na řádku nabídek na konzole ATA klikněte na ikonu sestav: ![ikona sestav](./media/ata-report-icon.png).
2. V části **Summary** (Souhrn) nebo **Modifications to sensitive groups** (Úpravy důvěrných skupin) nastavte datum **From** (Od) a **To** (Do) a klikněte na **Download** (Stáhnout). 
![sestavy](./media/reports.png)

Nastavení naplánované sestavy:
 
1. Na stránce **Reports** (Sestavy) klikněte na **Set scheduled reports** (Nastavit plánované sestavy) nebo na stránce konfigurace konzoly ATA v části Notifications and Reports (Oznámení a sestavy) klikněte na **Scheduled reports** (Naplánované sestavy).

   ![Plánování sestav](./media/ata-sched-reports.png)

2. Klikněte na **Schedule** (Plán) vedle možnosti **Summary** (Souhrn) nebo **Modification to sensitive groups** (Úpravy důvěrných skupin), nastavte četnost a e-mailovou adresu pro doručení sestav a klikněte na znaménko plus vedle e-mailových adres, které chcete přidat. Potom klikněte na **Save** (Uložit).

   ![Naplánování četnosti sestav a e-mailů](./media/sched-report1.png)


> [!NOTE]
> Naplánované sestavy jsou doručovány e-mailem a je možné je posílat, jenom pokud jste už nakonfigurovali e-mailový server v části **Configuration** (Konfigurace). V části Notifications and Reports (Oznámení a sestavy) pak vyberte **Mail server** (Poštovní server).


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

---
title: "Práce s Azure ATP sestavy | Microsoft Docs"
description: "Popisuje, jak můžete generovat sestavy v Azure ATP k monitorování vaší sítě."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2ebc0d9bb860bd93f14c4c511b034c740b59dffb
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="azure-atp-reports"></a>Azure ATP sestavy

Části sestavy Azure ATP v prostoru portálu můžete generovat sestavy, které poskytují informace o stavu systému, stavu systému a sestavy podezřelých aktivit zjistil ve vašem prostředí.

Pokud chcete získat přístup na stránku sestav, klikněte na ikonu sestav na řádku nabídek: ![ikona sestav](./media/atp-report-icon.png).
Dostupné sestavy: 

- **Souhrnná sestava**: Souhrnná sestava uvede řídicí panel stavu systému. Můžete zobrazit tři karty – jednu pro **Souhrn** z na vaší síti, co byla zjištěna **otevřené podezřelé aktivity** podezřelé aktivity, které jste měli postará o, ve kterém jsou a **otevřete stavu problémy** seznamy problémů Azure ATP stavu by měl postará o. Podezřelé aktivity, které jsou uvedené, jsou rozdělené podle typu, stejně jako problémy se stavem. 

- **Úprava citlivých skupin**: Tato sestava obsahuje seznam pokaždé, když změny do citlivých skupin (například správci, nebo ručně s příznakem účtů nebo skupin). Pokud používáte Azure ATP samostatné senzorů, získání úplné zprávy o citlivých skupin, je potřeba Ujistěte se, že [události jsou předávány z řadičů domény do samostatné snímače](configure-event-forwarding.md). 

- **Hesla, které jsou zveřejněné jako nezašifrovaný text**: Některé služby používat nezabezpečené protokolu LDAP k odesílání přihlašovací údaje účtu ve formátu prostého textu. Tomu může dojít i pro citlivé účty. Útočníci monitorování síťového provozu můžete zachytit a pak znovu použít tyto přihlašovací údaje zlými úmysly. Tato sestava obsahuje seznam všech zdrojového počítače a hesla účtů, které Azure ATP zjistil, že je odesláno jako nezašifrovaný text. 

- **Pomoci odhalit laterální pohyb cesty k citlivým účtům**: Tato sestava obsahuje seznam citlivé účty, které jsou zveřejňovány prostřednictvím cesty laterální pohyb. Další informace najdete v tématu [pomoci odhalit laterální pohyb cesty](use-case-lateral-movement-path.md). Tato sestava shromáždí cesty, které byly vytvořeny za posledních 60 dní, a informace zobrazené v portálu pracovní prostor, který představuje jen 2 dny.

Existují dva způsoby, jak vygenerovat sestavu: na vyžádání nebo na základě naplánování pravidelného odesílání sestav e-mailem.

Vygenerování sestavy na vyžádání:

1. V řádku nabídek portálu Azure ATP pracovního prostoru klikněte na ikonu sestav v panelu nabídek: ![ikona sestav](./media/atp-report-icon.png).

2. V části buď typ vašeho vybranou sestavu, nastavit **z** a **k** kalendářních dat a klikněte na tlačítko **Stáhnout**. 
 ![sestavy](./media/reports.png)

Nastavení naplánované sestavy:
 
1. V **sestavy** klikněte na tlačítko **nastavit plánované sestavy**, nebo na stránce Konfigurace portálu prostoru Azure ATP v rámci oznámení a sestavy, klikněte na tlačítko **naplánované sestavy**.

   ![Plánování sestav](./media/atp-sched-reports.png)

2. Klikněte na tlačítko **plán** vedle vašeho typu vybranou sestavu, nastavit četnost a e-mailovou adresu pro doručení sestavy, a klikněte na znaménko plus vedle e-mailové adresy je přidat, a klikněte na **Uložit**.

   ![Naplánování četnosti sestav a e-mailů](./media/sched-report1.png)


## <a name="see-also"></a>Viz také
- [Požadavky Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
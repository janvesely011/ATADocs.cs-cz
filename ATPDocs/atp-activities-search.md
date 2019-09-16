---
title: Filtr a hledání sledovaných aktivit Azure Advanced Threat Protection | Microsoft Docs
description: Tento článek poskytuje přehled o tom, jak filtrovat a prohledávat monitorované aktivity pomocí Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a546703b-d5a9-404d-9e87-125523bb8421
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 975aa8562b1ae7e8a830d31da7905c428f08f31e
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71004715"
---
# <a name="azure-atp-monitored-activities-search-and-filter"></a>Hledání a filtrování aktivit monitorovaných aktivit Azure ATP 

> [!NOTE]
> Funkce ATP Azure, které jsou na této stránce popsané, jsou dostupné taky pomocí nového [portálu](https://portal.cloudappsecurity.com).

Aktivity zjištěné v Azure ATP ve vaší síti je možné prohledávat a filtrovat, aby se při výzkumu a vyšetřování zobrazovaly výstrahy zabezpečení.  

V časové ose Azure ATP vyberte libovolnou entitu v síti (řadič domény, počítač nebo uživatel) jako přístupový bod filtru. Potom vyberte, že chcete filtrovat podle **výstrahy zabezpečení**, typu **aktivity** nebo jakékoli kombinace. Po použití filtru se časová osa této entity aktualizuje pomocí filtrovaných informací. Vaše vyfiltrované výstrahy a aktivity je také možné stáhnout, aby bylo možné pokračovat v šetření nebo sledování v jiných nástrojích. 

![Filtrovat výstrahy a aktivity](./media/activities-filter.png)

Filtrování výstrah a aktivit:
 1. Vyberte entitu, kterou chcete prozkoumat z časové osy Azure ATP. 
 2. Klikněte na **filtrovat podle**a pak vyberte výstrahy a aktivity, které chcete filtrovat. 
 3. Klikněte na tlačítko **Použít**. Časová osa entity se aktualizuje podle vybraných filtrů. 
 4. Chcete-li stáhnout filtrované aktivity, klikněte na tlačítko **Stáhnout aktivity** a vyberte rozsah dat pro sestavu ke stažení. 
 5. Chcete-li obnovit časovou osu entit pro zobrazení všech výstrah a aktivit, klikněte na tlačítko **obnovit** nebo zavřít filtr. 


## <a name="see-also"></a>Viz také
- [Zkoumání entit](investigate-entity.md)
- [Monitorování výstrah](monitoring-alerts.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)

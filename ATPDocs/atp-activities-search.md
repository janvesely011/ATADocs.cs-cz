---
title: Rozšířená ochrana před internetovými útoky monitorované aktivity filtrovat a hledat | Dokumentace Microsoftu
description: Tento článek poskytuje přehled o tom, jak filtrovat a aktivit vyhledávání, které jsou monitorovány pomocí služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/28/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a546703b-d5a9-404d-9e87-125523bb8421
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fb3839d5348f11b13176375be84ecd46d44fa365
ms.sourcegitcommit: 3ab48f180aa0276f4e19cf7cd567581c7b4324cc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/28/2018
ms.locfileid: "50202496"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="azure-atp-monitored-activities-search-and-filter"></a>Ochrana ATP v programu Azure monitorovat aktivity vyhledávání a filtrování 

Aktivity ve vaší síti zjištěno službou ochrany ATP v programu Azure můžete prohledávat a filtrují pro snadné procházení podrobností a organizaci při výzkumu a vyšetřování výstrah zabezpečení.  

Na časové ose ochrany ATP v programu Azure vyberte entitu v síti (řadič domény, počítače nebo uživatele) jako filtr přístupový bod. V dalším kroku vyberte můžete filtrovat podle **výstraha zabezpečení**, **aktivity** typu nebo libovolnou kombinaci. Jakmile se filtr použije, hrozeb časová osa entity se aktualizuje filtrované informacemi. Filtrované upozornění a aktivity si také stáhnout pokračovat šetření nebo sledování v jiných nástrojích. 

![Filtr upozornění a aktivity](./media/activities-filter.png)

Chcete-li filtrovat výstrahy a aktivity:
 1. Vyberte entitu, abychom z časové osy ochrany ATP v programu Azure. 
 2. Klikněte na tlačítko **filtrovat podle**, pak vyberte výstrahy a/nebo aktivity k filtrování. 
 3. Klikněte na tlačítko **použít**. Časová osa entity se aktualizují podle filtry, které jste vybrali. 
 4. Stáhnout filtrované aktivity, klikněte na tlačítko **aktivit stahování** a vyberte rozsah dat pro sestavy ke stažení. 
 5. Pokud chcete resetovat časová osa entity, chcete-li zobrazit všechny výstrahy a aktivity, klikněte na tlačítko **resetování** nebo zavřít filtru. 


## <a name="see-also"></a>Viz také
- [Prošetřování entit](investigate-entity.md)
- [Monitorování výstrah](monitoring-alerts.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)

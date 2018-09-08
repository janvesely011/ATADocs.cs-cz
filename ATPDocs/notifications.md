---
title: Nastavení oznámení rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje postup nastavení služby Azure ATP upozornění, zobrazí se upozornění při zjištění podezřelých aktivit.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 080b3469c862d4063db5a4832f63dd3614905fac
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166053"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="set-azure-atp-notifications"></a>Nastavení oznámení služby Azure ATP

Ochrana ATP v programu Azure může upozornit, když zjistí podezřelou aktivitu nebo upozornění stavu e-mailem. 

Pokud chcete dostávat oznámení na konkrétní e-mailovou adresu, nastavte následující parametry:


1. Na portálu ochrany ATP v programu Azure pracovního prostoru, vyberte na panelu nástrojů a vyberte možnost nastavení **konfigurace**.

![Ikona nastavení konfigurace služby Azure ATP](media/atp-config-menu.png)

2. Klikněte na tlačítko **oznámení**.
3. V části **Mail notifications**, určete oznámení, která se mají odesílat e-mailem – mohou být odesílány pro nové výstrahy (podezřelých aktivit) a nové problémy se stavem. 
 
 >  [!NOTE]
 >   E-mailové výstrahy pro podezřelé aktivity se odesílají jenom při vytvoření podezřelé aktivity.

5. Klikněte na **Uložit**.

 ![Oznámení Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Viz také

- [Konfigurace shromažďování událostí](configure-event-collection.md)

- [Nastavení protokolu Syslog](setting-syslog.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
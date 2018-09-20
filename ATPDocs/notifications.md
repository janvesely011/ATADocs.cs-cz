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
ms.openlocfilehash: c3fc5adbb700c4b8df66c243a655cf98aacc79af
ms.sourcegitcommit: 9f02f0f6669b25f39b616bb0885bb55b8c4f050b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2018
ms.locfileid: "46362421"
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
 
4. Klikněte na **Uložit**.

 ![Oznámení Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Viz také

- [Konfigurace shromažďování událostí](configure-event-collection.md)

- [Nastavení protokolu Syslog](setting-syslog.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)

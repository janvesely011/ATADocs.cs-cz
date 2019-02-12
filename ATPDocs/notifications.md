---
title: Nastavení oznámení rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje, jak nastavit výstrahy zabezpečení služby Azure ATP, aby se upozornění při zjištění podezřelých aktivit.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7551455b883bbf69068cfa6cde035c848168ac17
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076262"
---
# <a name="set-azure-atp-notifications"></a>Nastavení oznámení služby Azure ATP

Ochrana ATP v programu Azure může upozornit, když zjistí podezřelou aktivitu a vydá výstrahu zabezpečení nebo e-mailem upozornění stavu. 

Pokud chcete dostávat oznámení na konkrétní e-mailovou adresu, nastavte následující parametry:


1. Na portálu ochrany ATP v programu Azure, vyberte na panelu nástrojů a vyberte možnost nastavení **konfigurace**.

   ![Ikona nastavení konfigurace služby Azure ATP](media/atp-config-menu.png)

2. Klikněte na tlačítko **oznámení**.
3. V části **Mail notifications**, určete oznámení, která se mají odesílat e-mailem – mohou být odesílány pro nové výstrahy (podezřelých aktivit) a nové problémy se stavem. 
 
   > [!NOTE]
   > E-mailové výstrahy pro podezřelé aktivity se odesílají jenom při vytvoření podezřelé aktivity.
 
4. Klikněte na **Uložit**.

   ![Oznámení Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Viz také

- [Konfigurace shromažďování událostí](configure-event-collection.md)

- [Nastavení protokolu Syslog](setting-syslog.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

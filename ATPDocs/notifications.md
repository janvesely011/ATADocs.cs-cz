---
title: Nastavení oznámení rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje, jak nastavit výstrahy zabezpečení služby Azure ATP, aby se upozornění při zjištění podezřelých aktivit.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e6f3647ecaab82a32950fadd0a101385a2cc0051
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783045"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="set-azure-atp-notifications"></a>Nastavení oznámení služby Azure ATP

Ochrana ATP v programu Azure může upozornit, když zjistí podezřelou aktivitu a vydá výstrahu zabezpečení nebo e-mailem upozornění stavu. 

Pokud chcete dostávat oznámení na konkrétní e-mailovou adresu, nastavte následující parametry:


1. Na portálu ochrany ATP v programu Azure, vyberte na panelu nástrojů a vyberte možnost nastavení **konfigurace**.

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
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

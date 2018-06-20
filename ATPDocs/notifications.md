---
title: Nastavení oznámení Azure Advanced Threat Protection | Microsoft Docs
description: Popisuje, jak nastavit výstrahy Azure ATP, zobrazí se upozornění při zjištění podezřelých aktivit.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 85fe887df373d8132df932cdb3d1eaf5ab954a1d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
ms.locfileid: "29445977"
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="set-azure-atp-notifications"></a>Sada Azure ATP oznámení

Azure ATP vás může upozornit, když zjistí podezřelou aktivitu nebo upozornění na stav e-mailem. 

Pokud chcete dostávat oznámení na konkrétní e-mailovou adresu, nastavte následující parametry:


1. Na portálu Azure ATP pracovního prostoru, vyberte na panelu nástrojů a vyberte možnost nastavení **konfigurace**.

![Ikona nastavení konfigurace Azure ATP](media/atp-config-menu.png)

2. Klikněte na tlačítko **oznámení**.
3. V části **poštovní oznámení**, určete oznámení, která se mají odesílat e-mailem – odesláním pro nové výstrahy (podezřelé aktivity) a nové problémy v oblasti stavu. 
 
 >  [!NOTE]
 >   E-mailové výstrahy pro podezřelé aktivity se odesílají jenom při vytvoření podezřelé aktivity.

5. Klikněte na **Uložit**.

 ![Azure ATP oznámení](media/atp-notifications.png)



## <a name="see-also"></a>Viz také

- [Konfigurace shromažďování událostí](configure-event-collection.md)

- [Nastavení procesu Syslog](setting-syslog.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
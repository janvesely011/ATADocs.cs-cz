---
title: Nastavení oznámení Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje, jak nastavit výstrahy ATA, abyste byli při zjištění podezřelých aktivit upozorněni.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e88477f8ea7293a1927f6195b5540a6d0a1f7a81
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076160"
---
# <a name="set-ata-notifications"></a>Nastavení oznámení ATA

*Platí pro: Advanced Threat Analytics verze 1.9*

ATA vás může upozornit, když zjistí podezřelou aktivitu, a to buď e-mailem, nebo pomocí funkce předávání událostí ATA a předáním události na váš server SIEM/syslog. Před výběrem oznámení, která chcete dostávat, musíte [nastavit svůj e-mailový server a server Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   E-mailová oznámení zahrnují odkaz, který uživatele přímo k podezřelé aktivitě, která byla zjištěna. Část názvu hostitele v odkazu je převzatá z nastavení adresy URL konzoly ATA na stránce ATA Center. Ve výchozím nastavení adresa URL konzoly ATA je IP adresa vybraná při instalaci ATA Center. Pokud chcete nakonfigurovat e-mailová oznámení, doporučujeme použít jako adresu URL konzoly ATA plně kvalifikovaný název domény.
> -   Oznámení se z ATA Center posílají na server SMTP, nebo na server Syslog.


Pokud chcete dostávat oznámení, nastavte následující parametry:


1. V konzole ATA vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**.
    
    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.png)
    
1. V části **Notifications & Reports (Oznámení a sestavy)** vyberte **Notifications** (Oznámení).
1. V části **Mail notifications** (Oznámení e-mailem) zadejte, která oznámení se mají posílat e-mailem – nové podezřelé aktivity a nové problémy v oblasti stavu. Můžete nastavit oddělené e-mailové adresy, na které se mají odesílat informace o podezřelých aktivitách a výstrahy týkající se stavu samostatně tak, aby například analytik zabezpečení dostával oznámení o podezřelých aktivitách a správce IT oznámení týkající se stavu.
    
    > [!NOTE]
    > E-mailové výstrahy pro podezřelé aktivity se odesílají jenom při vytvoření podezřelé aktivity.

1. V části **oznámení Syslogu**, určete oznámení, která se mají odesílat na váš server Syslog – nové podezřelé aktivity, aktualizované podezřelé aktivity a nové problémy v oblasti stavu.
1. Klikněte na **Uložit**.
    
    ![Obrázek nastavení e-mailových upozornění ATA](media/ata-mail-notification-settings.png)




## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

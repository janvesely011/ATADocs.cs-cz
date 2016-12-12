---
title: "Nastavení oznámení ATA | Dokumentace Microsoftu"
description: "Popisuje, jak nastavit výstrahy ATA, abyste byli při zjištění podezřelých aktivit upozorněni."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/29/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7dc860fe31da1374a4466f8e56e55e6520bc10dc
ms.openlocfilehash: f069f910e99c537e08b34b9a0b65aab7dcd08452


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="set-ata-notifications"></a>Nastavení oznámení ATA
ATA vás může upozornit, když zjistí podezřelou aktivitu, a to buď e-mailem, nebo pomocí funkce předávání událostí ATA a předáním události na váš server SIEM/syslog. Před výběrem oznámení, která chcete dostávat, musíte [nastavit svůj e-mailový server a server Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   E-mailová oznámení zahrnují odkaz, který přenese uživatele přímo k podezřelé aktivitě, která byla zjištěna. Část názvu hostitele v odkazu je převzatá z nastavení adresy URL konzoly ATA na stránce ATA Center. Ve výchozím nastavení adresa URL konzoly ATA je IP adresa vybraná při instalaci ATA Center.  Pokud chcete nakonfigurovat e-mailová oznámení, doporučuje se použít jako adresu URL konzoly ATA plně kvalifikovaný název domény.
> -   Oznámení se z ATA Center posílají na server SMTP, nebo na server Syslog.

## <a name="mail-notifications"></a>E-mailová oznámení
Pokud chcete dostávat e-mailová oznámení, nastavte následující:


1. V konzole ATA vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**.
![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

2. V části **Oznámení** vyberte **Nastavení**.
3. Pod položkou **Příjemci e-mailu** zadejte příjemce, kteří obdrží tato e-mailová oznámení.
>   [!NOTE]
>   E-mailové výstrahy pro podezřelé aktivity se odesílají jenom při vytvoření podezřelé aktivity.

4. V části **Upozornit když** pomocí přepínačů vyberte, jaká oznámení se mají posílat:
  - Detekce nové podezřelé aktivity
  - Detekce nového stavového problému
  - Dostupnost nové aktualizace softwaru

5. Klikněte na **Uložit**.

![Obrázek nastavení e-mailových upozornění ATA](media/ATA-mail-notification-settings-1.7.png)


## <a name="syslog-notification"></a>Oznámení Syslog

Pokud chcete dostávat oznámení Syslog, nastavte následující:


1. V konzole ATA vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**.
![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

2. V části **Oznámení** vyberte **Nastavení**.
3. V části **Oznámení syslog** pomocí přepínačů vyberte, jaká oznámení se mají posílat:


    - Detekce nové podezřelé aktivity
    - Aktualizace stávající podezřelé aktivity
    - Detekce nového stavového problému
5. Klikněte na **Uložit**.

![Obrázek nastavení upozornění ATA](media/ATA-syslog-notification-settings-1.7.png)




## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Nov16_HO5-->



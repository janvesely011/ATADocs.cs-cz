---
# required metadata

title: Nastavení oznámení ATA | Microsoft Advanced Threat Analytics
description: Popisuje, jak vám má ATA doručovat upozornění (e-mailem nebo předáváním událostí ATA) při zjištění podezřelých aktivit. 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Nastavení oznámení ATA
ATA vás může upozornit, když zjistí podezřelou aktivitu, a to buď e-mailem, nebo pomocí funkce předávání událostí ATA a předáním události na váš server SIEM/syslog. Před výběrem oznámení, která chcete dostávat, musíte [nastavit svůj e-mailový server a server Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   E-mailová oznámení zahrnují odkaz, který přenese uživatele přímo k podezřelé aktivitě, která byla zjištěna. Část názvu hostitele v odkazu je převzatá z nastavení adresy URL konzoly ATA na stránce ATA Center. Ve výchozím nastavení adresa URL konzoly ATA je IP adresa vybraná při instalaci ATA Center.  Pokud chcete nakonfigurovat e-mailová oznámení, doporučuje se použít jako adresu URL konzoly ATA plně kvalifikovaný název domény.
> -   Oznámení se z ATA Center posílají na server SMTP, nebo na server Syslog.

Pokud chcete dostávat e-mailová oznámení, nastavte následující:


1. V konzole ATA vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**.
![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

2. Vyberte **Oznámení**.
3. V části **E-mailová oznámení** pomocí přepínačů vyberte, jaká oznámení se mají posílat:


    - Detekce nové podezřelé aktivity
    - Detekce nového stavového problému
    - Dostupnost nové aktualizace softwaru

4. Zadejte příjemce, kteří obdrží tato oznámení e-mailem.

    [Poznámka:] E-mailové výstrahy pro podezřelé aktivity se odesílají jenom při vytvoření podezřelé aktivity.


5. Klikněte na **Uložit**.

Pokud chcete dostávat oznámení Syslog, nastavte následující:


1. V konzole ATA vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**.
![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

2. Vyberte **Oznámení**.
3. V části **Oznámení syslog** pomocí přepínačů vyberte, jaká oznámení se mají posílat:


    - Detekce nové podezřelé aktivity
    - Aktualizace stávající podezřelé aktivity
    - Detekce nového stavového problému
5. Klikněte na **Uložit**.
![Obrázek nastavení upozornění ATA](media/ATA-notification-settings.png)




## Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Jun16_HO1-->



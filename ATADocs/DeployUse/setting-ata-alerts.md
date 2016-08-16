---
title: "Nastavení oznámení ATA | Microsoft ATA"
description: "Popisuje, jak nastavit výstrahy ATA, abyste byli při zjištění podezřelých aktivit upozorněni."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 47796a385ce92217fe36040df0723f31e4cb8701


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
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->



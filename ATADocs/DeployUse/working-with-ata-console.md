---
# required metadata

title: Práce s konzolou ATA | Microsoft Advanced Threat Analytics
description: Popisuje způsob přihlášení ke konzole ATA a její komponenty.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Práce s konzolou ATA

Konzolu ATA použijte k monitorování a reakci na podezřelé aktivity, které detekuje ATA.

## Povolení přístupu ke konzole ATA
Oprávnění pro přihlášení ke konzole ATA a správě nastavení ATA má každý uživatel, který je členem místní skupiny Administrators na serveru ATA Center.
Pokud chcete, aby uživatel měl přístup ke konzole ATA a nebyl přitom správce, přidejte ho do místní skupiny **Microsoft Advanced Threat Analytics Administrators**.

## Přihlášení ke konzole ATA

1. Na serveru ATA Center klikněte na ikonu **konzoly Microsoft ATA** na ploše nebo otevřete prohlížeč a vyhledejte konzolu ATA.

    ![Ikona serveru ATA](media/ata-server-icon.png)

    > [!NOTE] Můžete také otevřít prohlížeč z komponenty ATA Center nebo ATA Gateway a vyhledat IP adresu, kterou jste při instalaci komponenty ATA Center nakonfigurovali pro konzolu ATA.    

2.  Zadejte uživatelské jméno a heslo a klikněte na **Přihlásit**.

![Obrázek přihlašovací obrazovky ATA](media/ATA-log-in-screen.jpg)

    > [!NOTE]
    > You have to log in with a user who is a member of the local administrator group OR of the Microsoft Advanced Threat Analytics Administrators group.

## Konzola ATA

Konzola ATA poskytuje rychlé zobrazení všech podezřelých aktivit v chronologickém pořadí. Umožňuje přejít k podrobnostem libovolné aktivity a provádět akce založené na těchto aktivitách. Konzola také zobrazuje výstrahy a oznámení, které upozorňují na problémy se sítí ATA na nové aktivity, které se považují za podezřelé.

Toto jsou klíčové prvky konzoly ATA.


### Časová osa útoků

Toto je výchozí cílová stránka, která se vám zobrazí po přihlášení ke konzole ATA. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Časová osa útoků umožňuje filtrovat a zobrazit všechny podezřelé aktivity nebo jenom otevřené, vyřešené nebo zamítnuté aktivity. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila.

![Obrázek časové osy útoku ATA](media/attack-timeline.png)

Další informace najdete v tématu [Práce s podezřelými aktivitami](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities).

### Oznamovací pruh

Když se detekuje nová podezřelá aktivita, na pravé straně se automaticky otevře oznamovací pruh. Pokud byly od posledního přihlášení zjištěné nové podezřelé aktivity, oznamovací pruh se otevře hned po vašem úspěšném přihlášení. Oznamovací pruh můžete kdykoli vyvolat kliknutím na šipku napravo.

![Obrázek oznamovacího pruhu ATA](media/notification-bar.png)

### Panel filtrování

Na základě stavu a závažnosti umožňuje filtrovat, které podezřelé aktivity se zobrazí na časové ose útoků nebo na kartě podezřelých aktivit profilu entity.

### Panel hledání

Panel hledání najdete v horní nabídce. Umožňuje v ATA vyhledat konkrétního uživatele, počítač nebo skupiny. Pokud si ho chcete vyzkoušet, stačí začít psát.

![Obrázek hledání na konzole ATA](media/ATA-console-search.png)

### Health Center

Health Center zobrazuje výstrahy, pokud v nasazení ATA něco nefunguje tak, jak má.

![Obrázek ATA Health Center](media/health-center.png)

Kdykoli váš systém narazí na problém, jako je třeba chyba připojení nebo odpojení komponenty ATA Gateway, ikona Health Center vás na tuto skutečnost upozorní zobrazením červené tečky. ![Obrázek červené tečky ATA Health Center](media/ATA-Health-Center-Alert-red-dot.png)

Výstrahy komponenty Health Center se dají vyřešit nebo zamítnout a na základě závažnosti jsou zařazené do kategorií Vysoká, Střední nebo Nízká. Pokud vyřešíte výstrahu, kterou služba ATA detekuje jako stále aktivní, automaticky se přesune do seznamu otevřených výstrah. Pokud systém zjistí, že pro výstrahu už není důvod (situace byla vyřešena), automaticky ji přesune do seznamu vyřešených výstrah.

### Profily uživatelů a počítačů

ATA vytvoří profil pro každého uživatele a každý počítač v síti. V profilu uživatele ATA zobrazuje obecné informace, jako jsou členství ve skupinách, poslední přihlášení a prostředky s posledním přístupem.

![Profil uživatele](media/user-profile.png)

V profilu počítače ATA zobrazuje obecné informace, jako jsou poslední přihlášení a prostředky s posledním přístupem.

![Profil počítače](media/computer-profile.png)

ATA poskytuje další informace o entitách (počítače, zařízení, uživatelé) na těchto stránkách: Souhrn, Aktivity a Podezřelé aktivity.

Profil, který ATA nemůže úplně vyřešit, se označí ikonou napůl vyplněného kruhu.


![Obrázek nevyřešeného profilu ATA](media/ATA-Unresolved-Profile.jpg)

### Miniprofil

Pokud na libovolném místě konzoly, kde se prezentuje jedna entita, jako je uživatel nebo počítač, najedete myší na entitu, automaticky se otevře miniprofil, ve kterém se zobrazí následující informace (pokud jsou dostupné):

![Obrázek miniprofilu ATA](media/ATA-mini-profile.jpg)

-   Název

-   Obrázek

-   E-mailu

-   Telefon

-   Počet podezřelých aktivit podle závažnosti



## Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Jun16_HO1-->



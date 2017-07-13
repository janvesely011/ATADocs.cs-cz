---
title: Principy konzoly Advanced Threat Analytics | Dokumentace Microsoftu
description: "Popisuje způsob přihlášení ke konzole ATA a její komponenty."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3d687087dd9e1ae7f7642f9fdd7d89420f3bec27
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/03/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# Práce s konzolou ATA
<a id="working-with-the-ata-console" class="xliff"></a>

Konzolu ATA použijte k monitorování a reakci na podezřelé aktivity, které detekuje ATA.

Stisknutím klávesy ? zobrazíte klávesové zkratky pro přístupnost portálu ATA. 

## Povolení přístupu ke konzole ATA
<a id="enabling-access-to-the-ata-console" class="xliff"></a>
Na úspěšně přihlášení ke konzole ATA je nutné se přihlásit jako uživatel, který byl přiřazen správné roli ATA pro přístup ke konzole ATA. Další informace o řízení přístupu na základě rolí (RBAC) v ATA najdete v článku [Práce se skupinami rolí ATA](ata-role-groups.md).

## Přihlášení ke konzole ATA
<a id="logging-into-the-ata-console" class="xliff"></a>

1. Na serveru ATA Center klikněte na ikonu **konzoly Microsoft ATA** na ploše nebo otevřete prohlížeč a vyhledejte konzolu ATA.

    ![Ikona serveru ATA](media/ata-server-icon.png)

>[!NOTE]
> Můžete také otevřít prohlížeč z komponenty ATA Center nebo ATA Gateway a vyhledat IP adresu, kterou jste při instalaci komponenty ATA Center nakonfigurovali pro konzolu ATA.    

2.  Pokud jsou počítač, na kterém je nainstalovaná komponenta ATA Center, a počítač, ze kterého se snažíte získat přístup ke konzole ATA, připojené k doméně, podporuje ATA jednotné přihlašování integrované s ověřováním Windows, takže pokud už jste přihlášení k počítači, použije ATA tento token pro přihlášení ke konzole ATA. K přihlášení můžete použít také čipovou kartu. Oprávnění, která máte v ATA, budou odpovídat vaší [roli správce](ata-role-groups.md).

> [!NOTE]
> K počítači, ze kterého chcete získat přístup ke konzole ATA, se přihlaste pomocí uživatelského jména a hesla správce ATA. Alternativně můžete spustit prohlížeč jako jiný uživatel nebo se odhlásit z Windows a přihlásit se jako uživatel s rolí správce ATA. Pokud chcete, aby vás konzola ATA vyzvala k zadání přihlašovacích údajů, použijte pro přístup ke konzole IP adresu.

Pokud chcete použít jednotné přihlašování, zajistěte, aby byl web konzoly ATA definovaný v prohlížeči jako místní intranetový server. K přístupu pak můžete použít krátký název nebo locahost.

> [!NOTE]
> Kromě protokolování všech podezřelých aktivit a upozornění na stav se každá změna konfigurace, kterou uděláte v konzole ATA, audituje v protokolu událostí Windows na počítači s komponentou ATA Center, a to v oblasti **Protokoly aplikací a služeb** > **Microsoft ATA**. Stejně tak se audituje každé přihlášení ke konzole ATA.<br></br>  Do protokolu událostí Windows na počítači s komponentou ATA Gateway se protokoluje také konfigurace, která tuto komponentu ovlivňuje. 



## Konzola ATA
<a id="the-ata-console" class="xliff"></a>

Konzola ATA poskytuje rychlé zobrazení všech podezřelých aktivit v chronologickém pořadí. Umožňuje přejít k podrobnostem libovolné aktivity a provádět akce založené na těchto aktivitách. Konzola také zobrazuje výstrahy a oznámení, které upozorňují na problémy se sítí ATA na nové aktivity, které se považují za podezřelé.

Toto jsou klíčové prvky konzoly ATA.


### Časová osa útoků
<a id="attack-time-line" class="xliff"></a>

Toto je výchozí cílová stránka, která se vám zobrazí po přihlášení ke konzole ATA. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Časová osa útoků umožňuje filtrovat a zobrazit všechny podezřelé aktivity nebo jenom otevřené, vyřešené nebo zamítnuté aktivity. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila.

![Obrázek časové osy útoku ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Další informace najdete v tématu [Práce s podezřelými aktivitami](working-with-suspicious-activities.md).

### Oznamovací pruh
<a id="notification-bar" class="xliff"></a>

Když se detekuje nová podezřelá aktivita, na pravé straně se automaticky otevře oznamovací pruh. Pokud byly od posledního přihlášení zjištěné nové podezřelé aktivity, oznamovací pruh se otevře hned po vašem úspěšném přihlášení. Oznamovací pruh můžete kdykoli vyvolat kliknutím na šipku napravo.

![Obrázek oznamovacího pruhu ATA](media/notification-bar-1.7.png)

### Panel filtrování
<a id="filtering-panel" class="xliff"></a>

Na základě stavu a závažnosti umožňuje filtrovat, které podezřelé aktivity se zobrazí na časové ose útoků nebo na kartě podezřelých aktivit profilu entity.

### Panel hledání
<a id="search-bar" class="xliff"></a>

Panel hledání najdete v horní nabídce. Umožňuje v ATA vyhledat konkrétního uživatele, počítač nebo skupiny. Pokud si ho chcete vyzkoušet, stačí začít psát.

![Obrázek hledání na konzole ATA](media/ATA-console-search.png)

### Health Center
<a id="health-center" class="xliff"></a>

Health Center zobrazuje výstrahy, pokud v nasazení ATA něco nefunguje tak, jak má.

![Obrázek ATA Health Center](media/ATA-Health-Issue.jpg)

Kdykoli váš systém narazí na problém, jako je třeba chyba připojení nebo odpojení komponenty ATA Gateway, ikona Health Center vás na tuto skutečnost upozorní zobrazením červené tečky. ![Obrázek červené tečky ATA Health Center](media/ATA-Health-Center-Alert-red-dot.png)

Výstrahy komponenty Health Center se dají vyřešit nebo zamítnout a na základě závažnosti jsou zařazené do kategorií Vysoká, Střední nebo Nízká. Pokud vyřešíte výstrahu, kterou služba ATA detekuje jako stále aktivní, automaticky se přesune do seznamu otevřených výstrah. Pokud systém zjistí, že pro výstrahu už není důvod (situace byla vyřešena), automaticky ji přesune do seznamu vyřešených výstrah.

### Profily uživatelů a počítačů
<a id="user-and-computer-profiles" class="xliff"></a>

ATA vytvoří profil pro každého uživatele a každý počítač v síti. V profilu uživatele ATA zobrazuje obecné informace, jako jsou členství ve skupinách, poslední přihlášení a prostředky s posledním přístupem. Obsahuje také seznam lokalit, kde se uživatel připojil přes síť VPN. Níže najdete seznam členství ve skupinách, které ATA považuje za citlivé.

![Profil uživatele](media/user-profile.png)

V profilu počítače ATA zobrazuje obecné informace, jako jsou nedávná přihlášení a prostředky s nedávným přístupem.

![Profil počítače](media/computer-profile.png)

ATA poskytuje další informace o entitách (počítače, zařízení, uživatelé) na těchto stránkách: Souhrn, Aktivity a Podezřelé aktivity.

Profil, který ATA nemůže úplně vyřešit, se označí ikonou napůl vyplněného kruhu.


![Obrázek nevyřešeného profilu ATA](media/ATA-Unresolved-Profile.jpg)

### Citlivé skupiny
<a id="sensitive-groups" class="xliff"></a>

Následující seznam skupin považuje ATA za **citlivé**. Jedná se o skupiny, které budou označeny příznakem, že mají oprávnění ke správě, a vyvolají upozornění odpovídající citlivým účtům:

- Enterprise Read Only Domain Controllers 
- Domain Admins 
- Domain Controllers 
- Schema Admins
- Enterprise Admins 
- Group Policy Creator Owners 
- Read Only Domain Controllers 
- Administrators  
- Power Users  
- Account Operators  
- Server Operators   
- Print Operators
- Backup Operators
- Replicators 
- Remote Desktop Users 
- Network Configuration Operators 
- Incoming Forest Trust Builders 
- DNS Admins 


### Miniprofil
<a id="mini-profile" class="xliff"></a>

Pokud na libovolném místě konzoly, kde se prezentuje jedna entita, jako je uživatel nebo počítač, najedete myší na entitu, automaticky se otevře miniprofil, ve kterém se zobrazí následující informace (pokud jsou dostupné):

![Obrázek miniprofilu ATA](media/ATA-mini-profile.jpg)

-   Název

-   Obrázek

-   E-mailu

-   Telefon

-   Počet podezřelých aktivit podle závažnosti



## Viz také
<a id="see-also" class="xliff"></a>
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

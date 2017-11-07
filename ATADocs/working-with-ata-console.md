---
title: Principy konzoly Advanced Threat Analytics | Dokumentace Microsoftu
description: "Popisuje způsob přihlášení ke konzole ATA a její komponenty."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7e6570ee1e35631a3dba90466b31542e9fd0cd66
ms.sourcegitcommit: e2cb3af9c1dbb0b75946dc70cc439b19d654541c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/06/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="working-with-the-ata-console"></a>Práce s konzolou ATA

Konzolu ATA použijte k monitorování a reakci na podezřelé aktivity, které detekuje ATA.

Stisknutím klávesy ? zobrazíte klávesové zkratky pro přístupnost portálu ATA. 

## <a name="enabling-access-to-the-ata-console"></a>Povolení přístupu ke konzole ATA
Na úspěšně přihlášení ke konzole ATA je nutné se přihlásit jako uživatel, který byl přiřazen správné roli ATA pro přístup ke konzole ATA. Další informace o řízení přístupu na základě rolí (RBAC) v ATA najdete v článku [Práce se skupinami rolí ATA](ata-role-groups.md).

## <a name="logging-into-the-ata-console"></a>Přihlášení ke konzole ATA

>[!NOTE]
 > Od verze ATA 1.8 se proces přihlašování ke konzole ATA provádí pomocí jednotného přihlašování.

1. Na serveru ATA Center klikněte na ikonu **konzoly Microsoft ATA** na ploše nebo otevřete prohlížeč a vyhledejte konzolu ATA.

    ![Ikona serveru ATA](media/ata-server-icon.png)

 >[!NOTE]
 > Můžete také otevřít prohlížeč z komponenty ATA Center nebo ATA Gateway a vyhledat IP adresu, kterou jste při instalaci komponenty ATA Center nakonfigurovali pro konzolu ATA.    

2.  Pokud jsou počítač, na kterém je nainstalovaná komponenta ATA Center, a počítač, ze kterého se snažíte získat přístup ke konzole ATA, připojené k doméně, podporuje ATA jednotné přihlašování integrované s ověřováním Windows, takže pokud už jste přihlášení k počítači, použije ATA tento token pro přihlášení ke konzole ATA. K přihlášení můžete použít také čipovou kartu. Oprávnění, která máte v ATA, budou odpovídat vaší [roli správce](ata-role-groups.md).

 > [!NOTE]
 > K počítači, ze kterého chcete získat přístup ke konzole ATA, se přihlaste pomocí uživatelského jména a hesla správce ATA. Alternativně můžete spustit prohlížeč jako jiný uživatel nebo se odhlásit z Windows a přihlásit se jako uživatel s rolí správce ATA. Pokud chcete, aby vás konzola ATA vyzvala k zadání přihlašovacích údajů, použijte pro přístup ke konzole IP adresu.

3. Pokud chcete použít jednotné přihlašování, zajistěte, aby byl web konzoly ATA definovaný v prohlížeči jako místní intranetový server. K přístupu pak můžete použít krátký název nebo locahost.

> [!NOTE]
> Kromě protokolování všech podezřelých aktivit a upozornění na stav se každá změna konfigurace, kterou uděláte v konzole ATA, audituje v protokolu událostí Windows na počítači s komponentou ATA Center, a to v oblasti **Protokoly aplikací a služeb** > **Microsoft ATA**. Stejně tak se audituje každé přihlášení ke konzole ATA.<br></br>  Do protokolu událostí Windows na počítači s komponentou ATA Gateway se protokoluje také konfigurace, která tuto komponentu ovlivňuje. 



## <a name="the-ata-console"></a>Konzola ATA

Konzola ATA poskytuje rychlé zobrazení všech podezřelých aktivit v chronologickém pořadí. Umožňuje přejít k podrobnostem libovolné aktivity a provádět akce založené na těchto aktivitách. Konzola také zobrazuje výstrahy a oznámení, které upozorňují na problémy se sítí ATA na nové aktivity, které se považují za podezřelé.

Toto jsou klíčové prvky konzoly ATA.


### <a name="attack-time-line"></a>Časová osa útoků

Toto je výchozí cílová stránka, která se vám zobrazí po přihlášení ke konzole ATA. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Můžete filtrovat a zobrazit všechny časové ose útoků otevřít, Suppressed nebo zamítnuté podezřelé aktivity. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila.

![Obrázek časové osy útoku ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Další informace najdete v tématu [Práce s podezřelými aktivitami](working-with-suspicious-activities.md).

### <a name="notification-bar"></a>Oznamovací pruh

Když se detekuje nová podezřelá aktivita, na pravé straně se automaticky otevře oznamovací pruh. Pokud byly od posledního přihlášení zjištěné nové podezřelé aktivity, oznamovací pruh se otevře hned po vašem úspěšném přihlášení. Oznamovací pruh můžete kdykoli vyvolat kliknutím na šipku napravo.

![Obrázek oznamovacího pruhu ATA](media/notification-bar-1.7.png)

### <a name="filtering-panel"></a>Panel filtrování

Na základě stavu a závažnosti umožňuje filtrovat, které podezřelé aktivity se zobrazí na časové ose útoků nebo na kartě podezřelých aktivit profilu entity.

### <a name="search-bar"></a>Panel hledání

Panel hledání najdete v horní nabídce. Umožňuje v ATA vyhledat konkrétního uživatele, počítač nebo skupiny. Pokud si ho chcete vyzkoušet, stačí začít psát.

![Obrázek hledání na konzole ATA](media/ATA-console-search.png)

### <a name="health-center"></a>Health Center

Health Center zobrazuje výstrahy, pokud v nasazení ATA něco nefunguje tak, jak má.

![Obrázek ATA Health Center](media/ATA-Health-Issue.jpg)

Kdykoli váš systém narazí na problém, jako je třeba chyba připojení nebo odpojení komponenty ATA Gateway, ikona Health Center vás na tuto skutečnost upozorní zobrazením červené tečky. ![Obrázek červené tečky ATA Health Center](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="user-and-computer-profiles"></a>Profily uživatelů a počítačů

ATA vytvoří profil pro každého uživatele a každý počítač v síti. V profilu uživatele ATA zobrazuje obecné informace, jako jsou členství ve skupinách, poslední přihlášení a prostředky s posledním přístupem. Obsahuje také seznam lokalit, kde se uživatel připojil přes síť VPN. Níže najdete seznam členství ve skupinách, které ATA považuje za citlivé.

![Profil uživatele](media/user-profile.png)

V profilu počítače ATA zobrazuje obecné informace, jako jsou nedávná přihlášení a prostředky s nedávným přístupem.

![Profil počítače](media/computer-profile.png)

ATA poskytuje další informace o entitách (počítače, zařízení, uživatelé) na těchto stránkách: Souhrn, Aktivity a Podezřelé aktivity.

Profil, který ATA nemůže úplně vyřešit, se označí ikonou napůl vyplněného kruhu.


![Obrázek nevyřešeného profilu ATA](media/ATA-Unresolved-Profile.jpg)

### <a name="sensitive-groups"></a>Citlivé skupiny

Následující seznam skupin považuje ATA za **citlivé**. Za citlivou se považuje každá entita, která je členem těchto skupin:

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


### <a name="mini-profile"></a>Miniprofil

Pokud na libovolném místě konzoly, kde se prezentuje jedna entita, jako je uživatel nebo počítač, najedete myší na entitu, automaticky se otevře miniprofil, ve kterém se zobrazí následující informace (pokud jsou dostupné):

![Obrázek miniprofilu ATA](media/ATA-mini-profile.jpg)

-   Název

-   Obrázek

-   E-mailu

-   Telefon

-   Počet podezřelých aktivit podle závažnosti



## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

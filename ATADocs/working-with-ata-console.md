---
title: Principy konzoly Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje způsob přihlášení ke konzole ATA a její komponenty.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f25cdcf03be079f17adaf16b43be62b29c904bc2
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2019
ms.locfileid: "54841062"
---
# <a name="working-with-the-ata-console"></a>Práce s konzolou ATA


*Platí pro: Advanced Threat Analytics verze 1.9*

Konzolu ATA použijte k monitorování a reakci na podezřelé aktivity, které detekuje ATA.

Psát `?` klíč poskytuje klávesové zkratky pro přístupnost portálu ATA. 

## <a name="enabling-access-to-the-ata-console"></a>Povolení přístupu ke konzole ATA
Chcete-li úspěšně přihlášení ke konzole ATA, budete muset přihlásit jako uživatel, který byl přiřazen správné roli ATA pro přístup ke konzole ATA. Další informace o řízení přístupu na základě role (RBAC) v ATA najdete v tématu [práce se skupinami rolí ATA](ata-role-groups.md).

## <a name="logging-into-the-ata-console"></a>Přihlášení ke konzole ATA

>[!NOTE]
 > Od verze ATA 1.8 se proces přihlašování ke konzole ATA provádí pomocí jednotného přihlašování.

1. Na serveru ATA Center klikněte na ikonu **konzoly Microsoft ATA** na ploše nebo otevřete prohlížeč a vyhledejte konzolu ATA.

    ![Ikona serveru ATA](media/ata-server-icon.png)

   >[!NOTE]
   > Můžete také otevřít prohlížeč z komponenty ATA Center nebo ATA Gateway a vyhledat IP adresu, kterou jste při instalaci komponenty ATA Center nakonfigurovali pro konzolu ATA.    

2. Pokud počítač, na kterém je nainstalovaná na ATA Center a počítače, ze kterého se pokoušíte získat přístup ke konzole ATA se obě domény připojený, podporuje ATA jednotné přihlašování integrované s ověřováním Windows – Pokud jste již přihlášení k počítači, ATA využívá Tento token pro přihlášení ke konzole ATA. K přihlášení můžete použít také čipovou kartu. Vaše oprávnění v ATA odpovídat vaší [role správce](ata-role-groups.md).

   > [!NOTE]
   > Ujistěte se, že pro přihlášení k počítači, ze kterého chcete získat přístup ke konzole ATA pomocí ATA uživatelské jméno správce a hesla. Alternativně můžete spustit prohlížeč jako jiný uživatel nebo se odhlásit z Windows a přihlásit se jako uživatel s rolí správce ATA. Výzvy konzoly ATA, chcete-li požádat o přihlašovací údaje, přístup ke konzole IP adres zobrazí se výzva k zadání přihlašovacích údajů.

3. K přihlášení pomocí jednotného přihlašování, ujistěte se, že web konzoly ATA je definován jako místní intranetový server v prohlížeči a přístup shortname nebo místním hostiteli.

> [!NOTE]
> Kromě protokolování všech podezřelých aktivit a upozornění na stav se každá změna konfigurace, kterou uděláte v konzole ATA, audituje v protokolu událostí Windows na počítači s komponentou ATA Center, a to v oblasti **Protokoly aplikací a služeb** > **Microsoft ATA**. Stejně tak se audituje každé přihlášení ke konzole ATA.<br></br>  Do protokolu událostí Windows na počítači s komponentou ATA Gateway se protokoluje také konfigurace, která tuto komponentu ovlivňuje. 



## <a name="the-ata-console"></a>Konzola ATA

Konzola ATA poskytuje rychlé zobrazení všech podezřelých aktivit v chronologickém pořadí. Umožňuje přejít k podrobnostem libovolné aktivity a provádět akce založené na těchto aktivitách. Konzola také zobrazuje výstrahy a oznámení, které upozorňují na problémy se sítí ATA na nové aktivity, které se považují za podezřelé.

Toto jsou klíčové prvky konzoly ATA.


### <a name="attack-time-line"></a>Časová osa útoků

Toto je výchozí cílová stránka, která se vám zobrazí po přihlášení ke konzole ATA. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Můžete filtrovat na časové ose útoku a zobrazit všechny, otevřít, zamítnuté nebo Suppressed podezřelých aktivit. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila.

![Obrázek časové osy útoku ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Další informace najdete v tématu [Práce s podezřelými aktivitami](working-with-suspicious-activities.md).

### <a name="notification-bar"></a>Oznamovací pruh

Když se zjistí nové podezřelé aktivity, oznamovací pruh se automaticky otevře na pravé straně. Pokud byly od posledního přihlášení zjištěné nové podezřelé aktivity, oznamovací pruh se otevře hned po vašem úspěšném přihlášení. Oznamovací pruh můžete kdykoli vyvolat kliknutím na šipku napravo.

![Obrázek oznamovacího pruhu ATA](media/notification-bar-1.7.png)

### <a name="whats-new"></a>Co je nového

Po vydání nové verze ATA se **novinky** okno se zobrazí v horní pravé dali vám vědět, co bylo přidáno v nejnovější verzi. Také poskytuje vám s odkazem na stažení verze.

### <a name="filtering-panel"></a>Panel filtrování

Na základě stavu a závažnosti umožňuje filtrovat, které podezřelé aktivity se zobrazí na časové ose útoků nebo na kartě podezřelých aktivit profilu entity.

### <a name="search-bar"></a>Panel hledání

V horní nabídce můžete najít panelu hledání. Můžete vyhledat konkrétního uživatele, počítače nebo skupin v ATA. Pokud si ho chcete vyzkoušet, stačí začít psát.

![Obrázek hledání na konzole ATA](media/ATA-console-search.png)

### <a name="health-center"></a>Health Center

Health Center zobrazuje výstrahy, pokud v nasazení ATA něco nefunguje tak, jak má.

![Obrázek ATA Health Center](media/ATA-Health-Issue.jpg)

Kdykoli váš systém narazí na problém, jako je například Chyba připojení nebo odpojení komponenty ATA Gateway, ikona Health Center vám umožní upozorní zobrazením červené tečky. ![Obrázek červené tečky ATA Health Center](media/ATA-Health-Center-Alert-red-dot.png)

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

Pokud myší najedete myší entity, kdekoli v konzole níž se nachází jedna entita, například uživatele nebo počítač, zobrazí mini profil se automaticky otevře zobrazení následující informace, pokud je k dispozici:

![Obrázek miniprofilu ATA](media/ATA-mini-profile.jpg)

-   Název

-   Obrázek

-   Email

-   Telefon

-   Počet podezřelých aktivit podle závažnosti



## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

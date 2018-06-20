---
title: Principy konzoly Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje způsob přihlášení ke konzole ATA a její komponenty.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2ecffce7d692a9f1ecea8d8c5220ce3b2dbf848e
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009849"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="working-with-the-ata-console"></a>Práce s konzolou ATA

Konzolu ATA použijte k monitorování a reakci na podezřelé aktivity, které detekuje ATA.

Zadáním `?` klíč poskytuje klávesové zkratky pro usnadnění portálu ATA. 

## <a name="enabling-access-to-the-ata-console"></a>Povolení přístupu ke konzole ATA
Chcete-li úspěšně přihlásit ke konzole ATA, budete muset přihlásit jako uživatel, který byl přiřazen správné roli ATA přístup ke konzole ATA. Další informace o řízení přístupu na základě role (RBAC) v ATA najdete v tématu [práce se skupinami role ATA](ata-role-groups.md).

## <a name="logging-into-the-ata-console"></a>Přihlášení ke konzole ATA

>[!NOTE]
 > Od verze ATA 1.8 se proces přihlašování ke konzole ATA provádí pomocí jednotného přihlašování.

1. Na serveru ATA Center klikněte na ikonu **konzoly Microsoft ATA** na ploše nebo otevřete prohlížeč a vyhledejte konzolu ATA.

    ![Ikona serveru ATA](media/ata-server-icon.png)

 >[!NOTE]
 > Můžete také otevřít prohlížeč z komponenty ATA Center nebo ATA Gateway a vyhledat IP adresu, kterou jste při instalaci komponenty ATA Center nakonfigurovali pro konzolu ATA.    

2.  Pokud počítač, na kterém je nainstalován ATA Center a počítači, ze kterého se pokoušíte získat přístup ke konzole ATA jsou obě domény připojený, ATA podporuje jednotné přihlašování v integraci s ověřováním systému Windows – Pokud jste již přihlášeni k počítači, ATA používá Tento token pro přihlášení ke konzole ATA. K přihlášení můžete použít také čipovou kartu. Vaše oprávnění v ATA odpovídají s vaší [role správce](ata-role-groups.md).

 > [!NOTE]
 > Ujistěte se, že jste přihlášení k počítači, ze kterého mají být přístup ke konzole ATA pomocí ATA správce uživatelského jména a hesla. Alternativně můžete spustit prohlížeč jako jiný uživatel nebo se odhlásit z Windows a přihlásit se jako uživatel s rolí správce ATA. K konzoly ATA na požádat o přihlašovací údaje, přístup ke konzole pomocí IP adresy a výzva k zadání přihlašovacích údajů.

3. K přihlášení pomocí jednotného přihlašování, ujistěte se, web konzoly ATA je definován jako web místního intranetu v prohlížeči a přístup pomocí shortname nebo localhost.

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

Když se detekuje nová podezřelá aktivita, oznamovací pruh se automaticky otevře na pravé straně. Pokud byly od posledního přihlášení zjištěné nové podezřelé aktivity, oznamovací pruh se otevře hned po vašem úspěšném přihlášení. Oznamovací pruh můžete kdykoli vyvolat kliknutím na šipku napravo.

![Obrázek oznamovacího pruhu ATA](media/notification-bar-1.7.png)

### <a name="whats-new"></a>Co je nového

Po vydání nové verze ATA, **co je nového** okno se zobrazí v horní pravé umožnit vám vědět, co byl přidán v nejnovější verzi. Je také poskytuje odkaz na stažení verze.

### <a name="filtering-panel"></a>Panel filtrování

Na základě stavu a závažnosti umožňuje filtrovat, které podezřelé aktivity se zobrazí na časové ose útoků nebo na kartě podezřelých aktivit profilu entity.

### <a name="search-bar"></a>Panel hledání

Panel hledání můžete najít v horní nabídce. Můžete hledat konkrétního uživatele, počítače nebo skupiny v ATA. Pokud si ho chcete vyzkoušet, stačí začít psát.

![Obrázek hledání na konzole ATA](media/ATA-console-search.png)

### <a name="health-center"></a>Health Center

Health Center zobrazuje výstrahy, pokud v nasazení ATA něco nefunguje tak, jak má.

![Obrázek ATA Health Center](media/ATA-Health-Issue.jpg)

Kdykoli váš systém narazí na problém, třeba Chyba připojení nebo odpojení komponenty ATA Gateway, ikona Health Center umožňuje upozorní zobrazením červené tečky. ![Obrázek červené tečky ATA Health Center](media/ATA-Health-Center-Alert-red-dot.png)

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

Pokud umístěte ukazatel myši nad entity, kdekoli v konzole níž se nachází prezentuje jedna entita, například uživatele nebo počítač, miniprofil automaticky spustí, pokud je k dispozici zobrazí následující informace:

![Obrázek miniprofilu ATA](media/ATA-mini-profile.jpg)

-   Název

-   Obrázek

-   E-mailu

-   Telefon

-   Počet podezřelých aktivit podle závažnosti



## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

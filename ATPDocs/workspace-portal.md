---
title: Seznámení s portálem rozšířené ochrany před internetovými útoky Azure | Microsoft Docs
description: Popisuje, jak se přihlásit k portálu Azure ATP a k součástem portálu.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 08bab9d934b38859221f7f89df1580b21a8b22a2
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71004894"
---
# <a name="working-with-the-azure-atp-portal"></a>Práce s portálem Azure ATP

> [!NOTE]
> Funkce ATP Azure, které jsou na této stránce popsané, jsou dostupné taky pomocí nového [portálu](https://portal.cloudappsecurity.com).

Pomocí portálu Azure ATP můžete monitorovat podezřelé aktivity zjištěné ATP a reagovat na ně.

`?` Zadání klíče poskytuje klávesové zkratky pro přístupnost portálu Azure atp. 

Portál Azure ATP poskytuje rychlý přehled o všech podezřelých aktivitách v chronologickém pořadí. Umožňuje přejít k podrobnostem libovolné aktivity a provádět akce založené na těchto aktivitách. Portál Azure ATP také zobrazuje výstrahy a oznámení k zdůraznění problémů zjištěných službou Azure ATP nebo novými aktivitami, které se považují za podezřelé.

Tento článek popisuje, jak pracovat s klíčovými prvky portálu Azure ATP.


## <a name="enabling-access-to-the-azure-atp-portal"></a>Povolení přístupu k portálu Azure ATP
Abyste se úspěšně přihlásili k portálu Azure ATP, musíte se přihlásit pomocí uživatele přiřazeného ke skupině zabezpečení Azure Active Directory s přístupem k portálu Azure ATP. Další informace o řízení přístupu na základě role (RBAC) v ochrany ATP v programu Azure najdete v tématu [práce se skupinami rolí služby Azure ATP](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-portal"></a>Přihlášení k portálu Azure ATP

1. Portál Azure ATP můžete zadat buď tak, že se přihlásíte k [https://portal.atp.azure.com](https://portal.atp.azure.com) portálu, vyberete svoji instanci nebo přejdete na adresu URL instance: [https://*InstanceName*. atp.Azure.com](https://*instancename*.atp.azure.com).


2. Azure ATP podporuje jednotné přihlašování integrované s ověřováním Windows – Pokud jste už přihlášení k počítači, Azure ATP pomocí tohoto tokenu přihlašuje k portálu Azure ATP. K přihlášení můžete použít také čipovou kartu. Vaše oprávnění v Azure ATP odpovídají vaší [roli správce](atp-role-groups.md).

   > [!NOTE]
   > Ujistěte se, že se přihlašujete k počítači, ze kterého chcete získat přístup k portálu Azure ATP pomocí uživatelského jména a hesla správce ATP Azure. Případně můžete spustit prohlížeč jako jiný uživatel nebo se odhlásit z Windows a přihlásit se pomocí svého uživatele správce ATP Azure. 


### <a name="attack-time-line"></a>Časová osa útoků

Časová osa útoku je výchozí cílovou stránkou, na kterou jste se přihlásili, když se přihlašujete k portálu Azure ATP. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Časovou čáru útoku můžete filtrovat a zobrazit tak všechny, otevřené, neúspěšné nebo potlačené podezřelé aktivity. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila.

![Obrázek časové osy útoku Azure ATP](media/atp-sa-timeline.png)

Další informace najdete v tématu [práce s výstrahami zabezpečení](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Co je nového

Po vydání nové verze služby Azure ATP se v pravém horním rohu zobrazí okno **co je nového** , které vám umožní zjistit, co se přidalo v nejnovější verzi. Poskytuje taky odkaz na stažení verze.

### <a name="filtering-panel"></a>Panel filtrování

Na základě stavu a závažnosti umožňuje filtrovat, které podezřelé aktivity se zobrazí na časové ose útoků nebo na kartě podezřelých aktivit profilu entity.

### Panel hledání<a name="search-bar"></a>

V horní nabídce můžete najít panel hledání. V Azure ATP můžete vyhledat konkrétního uživatele, počítač nebo skupiny. Pokud si ho chcete vyzkoušet, stačí začít psát. V dolní části panelu hledání je uveden počet nalezených výsledků hledání. 

![Obrázek vyhledávání na portálu Azure ATP](media/atp-workspace-portal-search.png)

Pokud kliknete na číslo, dostanete se na stránku výsledků hledání, ve které můžete filtrovat výsledky podle typu entity pro další šetření.

![Výsledky hledání](media/search-results.png)

### <a name="health-center"></a>Centrum stavů

V centru stavů se zobrazí upozornění, pokud něco v instanci ATP Azure nefunguje správně.

![Obrázek centra stavu ATP Azure ATP](media/atp-health-issue.png)

V případě, že dojde k potížím s vaším systémem, jako je chyba připojení nebo odpojený samostatný senzor Azure ATP, vám ikona stavového centra informuje o zobrazení červené tečky. 

![Obrázek červené tečky v centru stavu ATP Azure ATP](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Citlivé skupiny

Informace o citlivých skupinách v Azure ATP najdete v tématu [práce s citlivými skupinami](sensitive-accounts.md).

### <a name="mini-profile"></a>Miniprofil

Pokud najedete myší na entitu kdekoli na portálu Azure ATP, kde je k dispozici jedna entita, jako je například uživatel nebo počítač, malý profil se automaticky otevře a zobrazí se následující informace, pokud jsou k dispozici a relevantní:

![Obrázek zkráceného profilu Azure ATP](media/atp-mini-profile.png)

- Name
- Název
- Oddělení
- Značky reklamy
- Email
- Office
- Telefonní číslo
- Doména
- Název SAM
- Vytvořeno – při vytvoření entity ve službě Active Directory. Pokud byl vytvořen před spuštěním monitorování Azure ATP, nezobrazí se.
- Poprvé zobrazeno – při prvním výskytu služby Azure ATP byla aktivita z této entity získaná.
- Poslední zjištěná – čas posledního výskytu služby Azure ATP z této entity
- Znak SA-se zobrazí, pokud jsou k této entitě přidruženy podezřelé aktivity.
- Příznakem z nenáročného ATP – zobrazí se v případě, že jsou v programu Windows Defender ATP spojené s touto entitou podezřelé aktivity.
- Označení bočních cest k pohybu – zobrazí se, pokud byly pro tuto entitu v posledních dvou dnech zjištěny cesty bočního pohybu.


## <a name="see-also"></a>Viz také

- [Vytváření instancí Azure ATP](install-atp-step1.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

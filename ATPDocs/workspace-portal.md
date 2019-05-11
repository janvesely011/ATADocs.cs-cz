---
title: Principy rozšířené ochrany před internetovými útoky pro Azure portal | Dokumentace Microsoftu
description: Popisuje, jak se přihlásit na portál ochrany ATP v programu Azure a její komponenty. na portálu
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 12/02/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 130d60b31e97a16fbd1ff372d124d0411ce7b25a
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196532"
---
# <a name="working-with-the-azure-atp-portal"></a>Práce s portálem Azure ATP

Pomocí ochrany ATP v programu Azure portal k monitorování a reakce na podezřelé aktivity detekovaných službou ochrany ATP v programu.

Psát `?` klíč poskytuje klávesové zkratky pro přístupnost portálu ochrany ATP v programu Azure. 

Ochrana ATP v programu Azure portal poskytuje rychlý přehled o všech podezřelých aktivit v chronologickém pořadí. Umožňuje přejít k podrobnostem libovolné aktivity a provádět akce založené na těchto aktivitách. Na portálu ochrany ATP v programu Azure také zobrazuje výstrahy a oznámení, abyste měli na očích problémů zjištěných ochrany ATP v programu Azure nebo nové aktivity, které se považují za podezřelé.

Tento článek popisuje, jak pracovat s klíčové prvky ochrany ATP v programu Azure portal.


## <a name="enabling-access-to-the-azure-atp-portal"></a>Povolení přístupu k portálu služby Azure ATP
Chcete-li úspěšně přihlásit na portál ochrany ATP v programu Azure, budete muset přihlásit jako uživatel, kterým je přiřazená do skupiny zabezpečení služby Azure Active Directory přístup k portálu ochrany ATP v programu Azure. Další informace o řízení přístupu na základě role (RBAC) v ochrany ATP v programu Azure najdete v tématu [práce se skupinami rolí služby Azure ATP](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-portal"></a>Přihlášení k portálu služby Azure ATP

1. Ochrana ATP v programu Azure portal můžete zadat buď po přihlášení k portálu [ https://portal.atp.azure.com ](https://portal.atp.azure.com) a výběr vašeho instance nebo přechodu na adresu URL instance: [https://*instancename*. ATP.Azure.com](https://*instancename*.atp.azure.com).


2. Azure ATP podporuje jednotné přihlašování integrované s ověřováním Windows – Pokud jste již přihlášení k počítači, ochrana ATP v programu Azure používá tento token pro přihlášení na portál ochrany ATP v programu Azure. K přihlášení můžete použít také čipovou kartu. Vaše oprávnění v Azure ATP odpovídají vaše [role správce](atp-role-groups.md).

   > [!NOTE]
   > Ujistěte se, že pro přihlášení k počítači, ze kterého chcete získat přístup k portálu ochrany ATP v programu Azure pomocí služby Azure ATP uživatelské jméno správce a hesla. Alternativně můžete spustit prohlížeč jako jiný uživatel nebo se odhlásit z Windows a protokolu se uživatel s rolí správce vaší služby Azure ATP. 


### <a name="attack-time-line"></a>Časová osa útoků

Na časové ose útoku, toto je výchozí cílová stránka, kterou budete přesměrováni na přihlášení k portálu ochrany ATP v programu Azure. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Můžete filtrovat na časové ose útoku a zobrazit všechny, otevřít, zamítnuté nebo Suppressed podezřelých aktivit. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila.

![Obrázek časové osy útoku Azure ATP](media/atp-sa-timeline.png)

Další informace najdete v tématu [Práce s podezřelými aktivitami](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Co je nového

Po vydání nové verze služby Azure ATP **novinky** okno se zobrazí v horní pravé dali vám vědět, co bylo přidáno v nejnovější verzi. Také poskytuje vám s odkazem na stažení verze.

### <a name="filtering-panel"></a>Panel filtrování

Na základě stavu a závažnosti umožňuje filtrovat, které podezřelé aktivity se zobrazí na časové ose útoků nebo na kartě podezřelých aktivit profilu entity.

### Panel hledání <a name="search-bar"></a>

V horní nabídce můžete najít panelu hledání. Můžete vyhledat konkrétního uživatele, počítače nebo skupiny v Azure ATP. Pokud si ho chcete vyzkoušet, stačí začít psát. V dolní části panelu hledání je označeno počet nalezených výsledků hledání. 

![Vyhledávání v portálu imagí Azure ATP](media/atp-workspace-portal-search.png)

Pokud kliknete číslo, dostanete stránka výsledků hledání, ve kterém můžete filtrovat výsledky podle typu entity pro další zkoumání.

![Výsledky hledání](media/search-results.png)

### <a name="health-center"></a>Health center

Health center zobrazuje výstrahy, pokud něco nefunguje správně ve vaší instanci služby Azure ATP.

![Obrázek health center Azure ATP](media/atp-health-issue.png)

Kdykoli váš systém narazí na problém, jako je například Chyba připojení nebo odpojených ochrany ATP v programu Azure samostatný senzor, ikona Health Center vám umožní upozorní zobrazením červené tečky. 

![Azure obrázek červené tečky health center ochrany ATP v programu](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Citlivé skupiny

Informace o citlivých skupin v Azure ATP, naleznete v tématu [práce s citlivých skupin](sensitive-accounts.md).

### <a name="mini-profile"></a>Miniprofil

Pokud myší najetí myší na entitu, kdekoli na portálu ochrany ATP v programu Azure níž se nachází jedna entita uvedené, například uživatele nebo počítač, mini profil automaticky spustí se zobrazí následující informace, pokud je dostupná a relevantní:

![Obrázek miniprofilu Azure ATP](media/atp-mini-profile.png)

- Název
- Titul
- Oddělení
- Značky AD
- Email
- Office
- Telefonní číslo
- Doména
- Název SAM
- Vytvořit na – kdy byla vytvořena entita ve službě Active Directory. Pokud byl vytvořen před spuštěním ochrany ATP v programu Azure monitoring, se nebudou zobrazovat.
- Poprvé zaznamenáno – první služby Azure ATP, během kterých se zjistí aktivita z této entity.
- Čas posledního kontaktu s – poslední Azure ATP, během kterých se zjistí aktivita z této entity.
- Pokud jsou spojeny s touto entitou podezřelé aktivity, zobrazí se oznámení "BADGE" SA.
- Ochrana ATP v programu WD oznámení "BADGE" se zobrazit, pokud existují podezřelých aktivit v programu Windows Defender ATP spojené s touto entitou.
- Taktiky Lateral Movement, které cesty Odznáček – se zobrazí, pokud byly cesty taktiky Lateral Movement zjištění pro tuto entitu v rámci poslední dva dny.


## <a name="see-also"></a>Viz také

- [Vytváření instancí služby Azure ATP](install-atp-step1.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

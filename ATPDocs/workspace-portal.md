---
title: Principy portálu pracovního prostoru rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje, jak pro přihlášení na portál ochrany ATP v programu Azure pracovní prostor a součásti portálu pracovního prostoru
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0fa8c1e19fde1ec779699b3a2c5411dea0908451
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166286"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="working-with-the-azure-atp-workspace-portal"></a>Práce s portálem pracovní prostor služby Azure ATP

Pomocí portálu Azure ATP pracovního prostoru pro monitorování a reakce na podezřelé aktivity detekovaných službou ochrany ATP v programu.

Psát `?` klíč poskytuje klávesové zkratky pro přístupnost portálu ochrany ATP v programu Azure pracovní prostor. 

Na portálu ochrany ATP v programu Azure pracovní prostor poskytuje rychlý přehled o všech podezřelých aktivit v chronologickém pořadí. Umožňuje přejít k podrobnostem libovolné aktivity a provádět akce založené na těchto aktivitách. Na portálu pracovního prostoru se také zobrazí výstrahy a oznámení, abyste měli na očích problémů zjištěných ochrany ATP v programu Azure nebo nové aktivity, které se považují za podezřelé.

Tento článek popisuje, jak pracovat s klíčové prvky z portálu pracovního prostoru služby Azure ATP.


## <a name="enabling-access-to-the-azure-atp-workspace-portal"></a>Povolení přístupu k portálu pracovního prostoru služby Azure ATP
Úspěšně přihlásit na portál ochrany ATP v programu Azure pracovní prostor, budete muset přihlásit jako uživatel, který byl přiřazen správné skupině zabezpečení Azure Active Directory pro přístup k portálu ochrany ATP v programu Azure pracovní prostor. Další informace o řízení přístupu na základě role (RBAC) v ochrany ATP v programu Azure najdete v tématu [práce se skupinami rolí služby Azure ATP](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-workspace-portal"></a>Přihlášení k portálu pracovního prostoru služby Azure ATP

1. Na portálu pracovního prostoru můžete zadat buď po přihlášení k portálu pro správu pracovního prostoru [ https://portal.atp.azure.com ](https://portal.atp.azure.com) a potom výběrem příslušné pracovní nebo přechodu na adresu URL pracovního prostoru: [https:// *workspacename*. atp.azure.com](https://*workspacename*.atp.azure.com).


2.  Azure ATP podporuje jednotné přihlašování integrované s ověřováním Windows – Pokud jste již přihlášení k počítači, ochrana ATP v programu Azure používá tento token pro přihlášení na portál ochrany ATP v programu Azure pracovní prostor. K přihlášení můžete použít také čipovou kartu. Vaše oprávnění v Azure ATP odpovídají vaše [role správce](atp-role-groups.md).

 > [!NOTE]
 > Ujistěte se, že pro přihlášení k počítači, ze kterého chcete získat přístup k portálu pracovního prostoru ochrana ATP v programu Azure pomocí služby Azure ATP uživatelské jméno správce a hesla. Alternativně můžete spustit prohlížeč jako jiný uživatel nebo se odhlásit z Windows a protokolu se uživatel s rolí správce vaší služby Azure ATP. 


### <a name="attack-time-line"></a>Časová osa útoků

Toto je výchozí cílová stránka, kterou budete přesměrováni na přihlášení k portálu ochrany ATP v programu Azure pracovní prostor. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Můžete filtrovat na časové ose útoku a zobrazit všechny, otevřít, zamítnuté nebo Suppressed podezřelých aktivit. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila.

![Obrázek časové osy útoku Azure ATP](media/atp-sa-timeline.png)

Další informace najdete v tématu [Práce s podezřelými aktivitami](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Co je nového

Po vydání nové verze služby Azure ATP **novinky** okno se zobrazí v horní pravé dali vám vědět, co bylo přidáno v nejnovější verzi. Také poskytuje vám s odkazem na stažení verze.

### <a name="filtering-panel"></a>Panel filtrování

Na základě stavu a závažnosti umožňuje filtrovat, které podezřelé aktivity se zobrazí na časové ose útoků nebo na kartě podezřelých aktivit profilu entity.

### Panel hledání <a name="search-bar"></a>

V horní nabídce můžete najít panelu hledání. Můžete vyhledat konkrétního uživatele, počítače nebo skupiny v Azure ATP. Pokud si ho chcete vyzkoušet, stačí začít psát. V dolní části panelu hledání je označeno počet nalezených výsledků hledání. 

![Azure image vyhledávání v portálu ochrany ATP v programu pracovního prostoru](media/atp-workspace-portal-search.png)

Pokud kliknete číslo, dostanete stránka výsledků hledání, ve kterém můžete filtrovat výsledky podle typu entity pro další zkoumání.

![Výsledky hledání](media/search-results.png)

### <a name="health-center"></a>Health center

Health center zobrazuje výstrahy, pokud něco nefunguje správně ve vašem pracovním prostoru služby Azure ATP.

![Obrázek health center Azure ATP](media/atp-health-issue.png)

Kdykoli váš systém narazí na problém, jako je například Chyba připojení nebo odpojených ochrany ATP v programu Azure samostatný senzor, ikona Health Center vám umožní upozorní zobrazením červené tečky. 

![Azure obrázek červené tečky health center ochrany ATP v programu](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Citlivé skupiny

Informace o citlivých skupin v ochrany ATP v programu, najdete v části [práce s citlivých skupin](sensitive-accounts.md).

### <a name="mini-profile"></a>Miniprofil

Pokud myší najetí myší na entitu, kdekoli na portálu pro pracovní prostor tam, kde je jedna entita uvedené, například uživatele nebo počítač, mini profil automaticky spustí se zobrazí následující informace, je-li k dispozici a jsou relevantní:

![Obrázek miniprofilu Azure ATP](media/atp-mini-profile.png)

- Název
- Název
- Oddělení
- Značky AD
- E-mailu
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

- [Vytváření pracovních prostorů služby Azure ATP](install-atp-step1.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
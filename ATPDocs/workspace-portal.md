---
title: Principy prostoru portálu Azure Advanced Threat Protection | Microsoft Docs
description: Popisuje, jak pro přihlášení k portálu Azure ATP prostoru a součástí portálu pracovního prostoru
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 40e139cc5e7dc6396914b0314d2d698a4782af02
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
ms.locfileid: "34444701"
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="working-with-the-azure-atp-workspace-portal"></a>Práce s portálem Azure ATP pracovního prostoru

Použití portálu Azure ATP prostoru k monitorování a reakci na podezřelé aktivity zjištěný ATP.

Zadáním `?` klíč poskytuje klávesové zkratky pro usnadnění portálu Azure ATP pracovního prostoru. 

Na portálu Azure ATP pracovní prostor poskytuje rychlý přehled o všech podezřelých aktivit v chronologickém pořadí. Umožňuje přejít k podrobnostem libovolné aktivity a provádět akce založené na těchto aktivitách. Na portálu prostoru také zobrazuje výstrahy a oznámení, které upozorňují na problémy, které jsou viditelné Azure ATP nebo nové aktivity, které se považují za podezřelé.

Tento článek popisuje, jak pracovat s klíčové prvky portálu Azure ATP pracovního prostoru.


## <a name="enabling-access-to-the-azure-atp-workspace-portal"></a>Povolení přístupu k portálu Azure ATP pracovního prostoru
Chcete-li úspěšně přihlásit k portálu Azure ATP pracovního prostoru, budete muset přihlásit jako uživatel, který byl přiřazen správné skupiny zabezpečení Azure Active Directory pro přístup k portálu Azure ATP pracovního prostoru. Další informace o řízení přístupu na základě role (RBAC) v Azure ATP najdete v tématu [práce se skupinami role Azure ATP](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-workspace-portal"></a>Protokolování do portálu Azure ATP pracovního prostoru

1. Můžete přejít na portál pro pracovní prostor, buď po přihlášení k portálu pro správu prostoru [ https://portal.atp.azure.com ](https://portal.atp.azure.com) a potom výběrem příslušné prostoru nebo procházení k adrese URL pracovního prostoru: [https:// *workspacename*. atp.azure.com](https://*workspacename*.atp.azure.com).


2.  Azure ATP podporuje jednotné přihlašování v integraci s ověřováním systému Windows – Pokud jste již přihlášeni k počítači, Azure ATP používá tento token pro přihlášení k portálu Azure ATP pracovního prostoru. K přihlášení můžete použít také čipovou kartu. Vaše oprávnění v Azure ATP odpovídají s vaší [role správce](atp-role-groups.md).

 > [!NOTE]
 > Ujistěte se, že jste přihlášení k počítači, ze kterého chcete pro přístup k portálu Azure ATP prostoru pomocí Správce Azure ATP uživatelského jména a hesla. Alternativně můžete spustit prohlížeč jako jiný uživatel nebo protokolu mimo systém Windows a protokolů pomocí svého správce uživatele Azure ATP. 


### <a name="attack-time-line"></a>Časová osa útoků

Toto je výchozí cílová stránka, ke které se otevře při přihlášení k portálu Azure ATP pracovního prostoru. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Můžete filtrovat a zobrazit všechny časové ose útoků otevřít, Suppressed nebo zamítnuté podezřelé aktivity. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila.

![Obrázek časové osy útoku Azure ATP](media/atp-sa-timeline.png)

Další informace najdete v tématu [Práce s podezřelými aktivitami](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Co je nového

Po vydání nové verze Azure ATP, **co je nového** okno se zobrazí v horní pravé umožnit vám vědět, co byl přidán v nejnovější verzi. Je také poskytuje odkaz na stažení verze.

### <a name="filtering-panel"></a>Panel filtrování

Na základě stavu a závažnosti umožňuje filtrovat, které podezřelé aktivity se zobrazí na časové ose útoků nebo na kartě podezřelých aktivit profilu entity.

### Panel hledání <a name="search-bar"></a>

Panel hledání můžete najít v horní nabídce. Můžete hledat konkrétního uživatele, počítače nebo skupiny v Azure ATP. Pokud si ho chcete vyzkoušet, stačí začít psát. V dolní části panelu Hledat počet výsledků hledání najít uvedené. 

![Obrázek hledání portálu Azure ATP pracovního prostoru](media/atp-workspace-portal-search.png)

Pokud kliknete na číslo, dostanete stránky s výsledky hledání ve kterém můžete filtrovat výsledky podle typu entity pro další šetření.

![výsledky hledání](media/search-results.png)

### <a name="health-center"></a>Health center

Health center zobrazuje výstrahy, pokud něco nefunguje správně v pracovním prostoru Azure ATP.

![Azure obrázek ATP health center](media/atp-health-issue.png)

Kdykoli váš systém narazí na problém, třeba Chyba připojení nebo odpojené senzor samostatné Azure ATP, ikona Health Center umožňuje upozorní zobrazením červené tečky. 

![Azure obrázek červené tečky health center ATP](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Citlivé skupiny

Informace o citlivých skupin v ATP najdete v tématu [práce s citlivých skupin](sensitive-accounts.md).

### <a name="mini-profile"></a>Miniprofil

Pokud jste umístěte ukazatel myši nad entity, kdekoli v prostoru portálu níž se nachází prezentuje jedna entita, například uživatele nebo počítač, miniprofil automaticky spustí se zobrazí následující informace, pokud je dostupná a relevantní:

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
- Vytvořit v – Pokud byla vytvořena entita ve službě Active Directory. Pokud byl vytvořen před Azure ATP spuštění monitorování, nebudou zobrazeny.
- Nejprve se seznámili s – poprvé Azure ATP zjištěnými aktivitu z této entity.
- Čas posledního kontaktu s-poslední Azure ATP zjištěnými aktivitu z této entity.
- Pokud jsou podezřelé aktivity, které jsou přidružené k této entitě, zobrazí se oznámení "BADGE" SA.
- WD ATP oznámení "BADGE" se nezobrazí, pokud jsou v systému Windows Defender ATP přidružené k této entitě podezřelé aktivity.
- Laterální pohyb, které cesty oznámení - se zobrazí, pokud byly laterální pohyb cesty pro tuto entitu zjištěn během posledních dvou dnů.


## <a name="see-also"></a>Viz také

- [Vytváření pracovních prostorů Azure ATP](install-atp-step1.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
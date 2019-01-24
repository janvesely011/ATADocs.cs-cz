---
title: Prošetření útoků v cesty laterální pohyb se ATA | Dokumentace Microsoftu
description: Tento článek popisuje, jak detekovat útoky cesty laterální pohyb s Advanced Threat Analytics (ATA).
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b6aaaf1a93fe635f4e159f88e7d55a110bcef0d2
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2019
ms.locfileid: "54840484"
---
# <a name="investigating-lateral-movement-paths-with-ata"></a>Prošetřování laterálních průnikových tras pomocí ATA


*Platí pro: Advanced Threat Analytics verze 1.9*

I v případě, že provedete stačily na ochranu vašich citlivých uživatelů a vaši Správci mají složitých hesel, která se často mění, jsou Posílená jejich počítačů a jejich data jsou bezpečně uložena, útočníci můžou využívat cesty taktiky Lateral Movement k citlivým účty. Útocích taktiky Lateral Movement útočník využívá instance citlivé uživatele po přihlášení na počítač kde kteří nejsou citliví uživatel má místní práva. Útočníci můžou přesuňte následně k laterálnímu, přístup k méně citlivé uživatele a následné přepravy napříč počítači k získání přihlašovacích údajů pro citlivé uživatele. 

## <a name="what-is-a-lateral-movement-path"></a>Co je cesty laterální pohyb?

Laterální pohyb je, když útočník pomocí tohoto počtu účtů pro přístup k citlivým účtům. To lze provést pomocí metod popsaných v[Průvodce prošetřováním podezřelých aktivit](suspicious-activity-guide.md). Pochopit, kdo jsou správci ve vaší síti a které počítače může útočník přístup, útočník využít data na řadiče domény. 

ATA umožňuje využít preemptivní akce ve vaší síti, chcete-li útočníkům zabránit v následných na taktiky Lateral Movement.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Zjišťování rizikové citlivé účty

Ke zjištění, které citlivé účty ve vaší síti byly ohrožené kvůli připojení k méně citlivé účty nebo prostředky v konkrétní časový rámec, postupujte podle těchto kroků. 

1. V nabídce konzoly ATA klikněte na ikonu sestav ![Ikona sestav](./media/ata-report-icon.png).

2. V části **laterální pohyb cesty k citlivým účtům**, pokud nejsou nalezeny žádné cesty taktiky Lateral Movement, je sestava zobrazena šedě. Pokud existují cesty taktiky Lateral Movement, pak data sestavy automaticky vybere první datum, kdy je relevantní data. 

   ![sestavy](./media/reports.png)

3. Klikněte na tlačítko **Stáhnout**.

4. Excelový soubor, který je vytvořen poskytuje podrobnosti o vašich citlivých účtů, které jsou na rizika. **Souhrn** karta obsahuje grafy, které podrobně popisují, počet citlivých účtů, počítačů a průměry za rizikové prostředky. **Podrobnosti** karta obsahuje seznam citlivé účty, které byste měli mít obavy. Všimněte si, že cesty jsou cesty, které dříve existoval a nemusí být k dispozici už dnes.


## <a name="investigate"></a>Prošetření

Teď, když víte, které citlivé účty se riziku, hluboké můžete začít ATA Další informace a přijmout preventivní opatření.

1. V konzole ATA vyhledejte laterální pohyb oznámení "BADGE", který je přidán na profil entity, když je entita v cesty laterální pohyb ![laterální ikonu](./media/lateral-movement-icon.png) nebo ![Ikona cesty](./media/paths-icon.png). Toto je k dispozici, pokud se v poslední dva dny cesty laterální pohyb.

2. Na stránce profilu uživatele, které se otevře, klikněte na tlačítko **laterální pohyb cesty** kartu.

3. Graf, který se zobrazí poskytuje mapování z možných cest pro citlivé uživatele. Graf zobrazuje připojení, které jsme udělali za poslední dva dny.

4. Projděte si grafu chcete zobrazit, co se dozvíte o rizika ohrožení citlivých uživatelských přihlašovacích údajů. Například v této mapy, můžete postupovat podle **přihlašující** šedý šipky zobrazíte, kde Samira přihlášení její privilegovaných přihlašovacích údajů. V tomto případě byly pro Samira citlivé přihlašovací údaje uložené v počítači REDMOND, WA-odch Potom, zjistili, která jiným uživatelům přihlášení na které počítače, které vytvořili nejvíce zviditelnění webu a ohrožení zabezpečení. Tohle je vidět pohledem **správce** černé šipky zjistit, kdo má oprávnění správce na prostředku. V tomto příkladu, všem uživatelům ve skupině **Contoso všechny** umožňuje přístup k přihlašovacím údajům uživatele z tohoto prostředku.  

   ![cesty taktiky Lateral Movement profilu uživatele](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Preventivní osvědčené postupy

- Abyste měli jistotu, že citlivé uživatele pouze při přihlašování posílené počítače pomocí přihlašovacích údajů správce je nejlepším způsobem, jak zabránit taktiky Lateral Movement tam, kde neexistuje žádný uživatel kteří nejsou citliví, který má práva správce na stejném počítači. V příkladu Ujistěte se, že pokud Samira potřebuje přístup k REDMOND, WA-DEV, uživatel přihlásí pomocí uživatelského jména a hesla než její přihlašovací údaje správce, nebo odeberte skupinu všech Contoso z místní skupiny administrators na REDMOND, WA-odch

- Doporučujeme také, že zkontrolujete, že nemá nikdo zbytečné místní oprávnění správce. V tomto příkladu by měl zkontrolovat a zjistěte, jestli všichni ve společnosti Contoso všechny potřebuje oprávnění správce na REDMOND, WA-odch

- Ujistěte se, že lidé mít přístup jenom k potřebné prostředky. V tomto příkladu Oscar Posada výrazně rozšiřuje na Samira vystavení. Je nezbytné, že má být součástí skupiny **Contoso všechny**? Existují podskupiny, které můžete vytvořit a minimalizovat vystavení?

**Tip** – během poslední dva dny se zjistila aktivita, graf se nezobrazí, ale sestava cesty laterální pohyb bude stále k dispozici k poskytování informací o cesty taktiky Lateral Movement za posledních 60 dní.

**Tip** – pokyny o tom, jak nastavit servery ATA k provádění operací SAM-R, které jsou potřebné ke zjišťování cesty laterální pohyb, aby [konfigurace SAM-R](install-ata-step9-samr.md).




## <a name="see-also"></a>Viz také
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

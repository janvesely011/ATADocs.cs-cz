---
title: Prošetřování laterálních průnikových tras pomocí služby Azure ATP | Dokumentace Microsoftu
description: Tento článek popisuje, jak detekovat a prošetřovat potenciální útoky cesty laterální pohyb s Azure Advanced Threat Protection (ATP).
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/3/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9295dc09-ecdb-44c0-906b-cba4c5c8f17c
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4201ccc187b0f06522cc46aefb1518ff22012c86
ms.sourcegitcommit: 1ba4e327784c6267db5a708592c4d81ca23376ba
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/03/2019
ms.locfileid: "53996906"
---
*Platí pro: Azure Advanced Threat Protection*

# <a name="tutorial-use-lateral-movement-paths-lmps"></a>Kurz: Použití cesty taktiky Lateral Movement (LMPs)

Laterální pohyb útoky jsou obvykle provedeno pomocí řadu různých technik. Některé z nejoblíbenějších metod používaných útočníky [krádeže přihlašovacích údajů](suspicious-activity-guide.md#) a [předat lístky](suspicious-activity-guide.md) útoky. V obou metod méně citlivé účty používají útočníci pro laterální přesuny využívajícím počítačů nejsou citliví, které sdílejí uložená pověření přihlášení v účtů, skupin a počítačů s citlivými účty.

V tomto kurzu se naučíte používat LMPs ochrany ATP v programu Azure k [prozkoumat](#investigate) potenciální laterální pohyb cesty a taky výstrahy zabezpečení služby Azure ATP, získat lépe pochopit, co se stalo ve vaší síti a jak. Kromě toho se dozvíte, jak používat [LMP sestavy citlivých účtů](#discover-your-at-risk-sensitive-accounts) zjistit všechny citlivých účtů pomocí potenciální cesty taktiky Lateral Movement, které jsou zjištěny ve vaší síti časové období.

> [!div class="checklist"]
> * Prozkoumat LMPs
> * Zjistit vaše citlivé účty
> * Přístup **laterální cesty Lateral Movement k citlivým účtům** sestavy


## <a name="investigate"></a>Prošetření

Použití a prozkoumat LMPs několika způsoby. Na portálu ochrany ATP v programu Azure vyhledávání entity a pak prozkoumejte cestu nebo aktivity.

1. Na portálu vyhledejte uživatele nebo počítače. Všimněte si, že pokud Odznáček taktiky Lateral Movement byl přidán do profilu entity. Oznámení se zobrazí pouze při zjištění entity v potenciální LMP za posledních 48 hodin.  

   ![laterální ikonu](./media/lateral-movement-icon.png) nebo ![Ikona cesty](./media/paths-icon.png).

2. Na stránce profilu uživatele, které se otevře, klikněte na tlačítko **laterální pohyb cesty** kartu.

   ![Azure kartu ochrany ATP v programu cesty laterální pohyb (LMP)](./media/lateral-movement-path-tab.png)

3. Graf, který se zobrazí poskytuje mapování z možných cest pro citlivé uživatele během 48 hodin časové období. Pokud se zjistila žádná aktivita v posledních dvou dní grafu nezobrazí. Použití **zobrazit jiné datum** možnosti se zobrazí graf pro předchozí detekce cesty laterální pohyb entity.

   ![LMP zobrazit jiné datum](./media/atp-view-different-date.png)

4. Projděte si grafu chcete zobrazit, co se dozvíte o rizika ohrožení citlivých uživatelských přihlašovacích údajů. Například v cestě, postupujte **přihlašující** šedý šipky zobrazíte, kde Nick přihlášení jejich privilegovaných přihlašovacích údajů. V takovém případě citlivé přihlašovací údaje Nick se uložily v počítači SRV služby SHAREPOINT. Nyní, Všimněte si, jaké další uživatelé přihlášení do které počítače, které vytvořili nejvíce zviditelnění webu a ohrožení zabezpečení. Tohle je vidět pohledem **správce** černé šipky zjistit, kdo má oprávnění správce na prostředku. V tomto příkladu všem uživatelům ve skupině helpdesku má schopnost přístup k přihlašovacím údajům uživatele z tohoto prostředku.  

   ![Azure ATP laterální pohyb cestu (LMP)](./media/atp-lmp.png)

## <a name="discover-your-at-risk-sensitive-accounts"></a>Objevte své rizikové citlivé účty

Pokud chcete zjistit všechny citlivé účty ve vaší síti, které jsou vystaveny kvůli připojení k méně citlivé účty, skupin a počítačů v cesty taktiky Lateral Movement, postupujte takto. 

1. V nabídce ochrany ATP v programu Azure portal klikněte na ikonu sestav ![Ikona sestav](./media/atp-report-icon.png).

2. V části **laterální pohyb cesty k citlivým účtům**, pokud neexistují žádné potenciální cesty taktiky Lateral Movement nalezen, je sestava zobrazena šedě. Pokud neexistují potenciální cesty taktiky Lateral Movement, sestavy automaticky provede předvýběr první datum, kdy je relevantní data. Sestava cesty laterální pohyb poskytuje data po dobu 60 dnů.

   ![sestavy](./media/reports.png)

3. Klikněte na tlačítko **Stáhnout**.

4. Excelový soubor se vytvoří, které poskytuje podrobnosti o potenciální cesty taktiky Lateral Movement a ohrožení citlivých účtů pro vybraná data. **Souhrn** karta obsahuje grafy, které podrobně popisují, počet citlivých účtů, počítačů a průměry pro rizikové přístup. **Podrobnosti** karta obsahuje seznam citlivé účty, které byste měli dále prozkoumat.

## <a name="schedule-report"></a>Naplánovat sestavu

Laterální pohyb k citlivým účtům sestavy můžete taky naplánovat pomocí funkce set plánované sestavy.

Všimněte si, že skutečné LMPs podrobné sestavy ke stažení mohou nadále již nebudou dostupné vzhledem k tomu, že jsou v minulosti byly zjištěny a může změnit, změnit nebo oprava, protože byly zjištěny.

Zobrazit historická LMPs, vyberte různá data k dispozici ve výběru kalendáře při vytváření sestav.

## <a name="next-steps"></a>Další postup

V tomto kurzu jste zjistili, jak používat LMPs prozkoumat podezřelé aktivity. Další informace o entitách, které jsou součástí LMPs, pokračujte ke kurzu entity prošetřit.
> [!div class="nextstepaction"]
> [Prošetřování entit](investigate-entity.md)

## <a name="see-also"></a>Viz také

- [Principy Azure ATP laterální pohyb cesty](use-case-lateral-movement-path.md)
- [Konfigurace služby Azure ATP pro vzdálená volání do SAM](install-atp-step8-samr.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
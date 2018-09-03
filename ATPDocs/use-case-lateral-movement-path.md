---
title: Prošetření útoků v cesty laterální pohyb pomocí služby Azure ATP | Dokumentace Microsoftu
description: Tento článek popisuje, jak detekovat útoky cesty laterální pohyb s Azure Advanced Threat Protection (ATP).
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/05/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 270b84c24ef8b52565ee97c2c15374645eb54a2c
ms.sourcegitcommit: 93a133430ac85d6db7afad5f6f2583b3a39c423a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/02/2018
ms.locfileid: "43469647"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Prošetřování laterálních průnikových tras pomocí služby Azure ATP


Laterální pohyb je, když útočník pomocí tohoto počtu účtů pro přístup k citlivým účtům. To lze provést pomocí metod popsaných v [Průvodce prošetřováním podezřelých aktivit](suspicious-activity-guide.md). Laterální pohyb je útočníci k identifikaci a získat přístup k citlivým účtům a počítačů v síti pomocí tohoto počtu účtů, které sdílejí uložená pověření přihlášení v účtů, skupin a počítačů. Jakmile útočník získal přístup, útočník můžete také využít data na řadiče domény.


## <a name="discover-your-at-risk-sensitive-accounts"></a>Objevte své rizikové citlivé účty

Chcete-li zjistit, které citlivé účty ve vaší síti jsou přístupné z důvodu jejich připojení k tohoto počtu účtů, skupin a počítačů, postupujte takto. 

1. V portálu nabídce pracovního prostoru ochrana ATP v programu Azure klikněte na ikonu sestav ![Ikona sestav](./media/atp-report-icon.png).

2. V části **laterální pohyb cesty k citlivým účtům**, pokud neexistují žádné potenciální cesty taktiky Lateral Movement nalezen, je sestava zobrazena šedě. Pokud neexistují potenciální cesty taktiky Lateral Movement, sestavy automaticky provede předvýběr první datum, kdy je relevantní data. Sestava cesty laterální pohyb poskytuje data po dobu 60 dnů.

 ![sestavy](./media/reports.png)

3. Klikněte na tlačítko **Stáhnout**.

4. Excelový soubor se vytvoří, které poskytuje podrobnosti o potenciální cesty taktiky Lateral Movement a ohrožení citlivých účtů pro vybraná data. **Souhrn** karta obsahuje grafy, které podrobně popisují, počet citlivých účtů, počítačů a průměry pro rizikové přístup. **Podrobnosti** karta obsahuje seznam citlivé účty, které byste měli dále prozkoumat. Všimněte si, že cesty podrobné sestavy ke stažení mohou nadále již nebudou dostupné vzhledem k tomu, že parametry zjištěnými za posledních 60 dnů a může mít změnil nebo byl změněn.


## <a name="investigate"></a>Prošetření



1. Na portálu ochrany ATP v programu Azure pracovní prostor vyhledejte laterální pohyb oznámení "BADGE", který je přidán na profil entity, když je entita v cesty laterální pohyb ![laterální ikonu](./media/lateral-movement-icon.png) nebo ![Ikona cesty](./media/paths-icon.png). Všimněte si, že oznámení se zobrazí pouze pokud taktiky Lateral Movement za posledních 48 hodin. 

2. Na stránce profilu uživatele, které se otevře, klikněte na tlačítko **laterální pohyb cesty** kartu. 

3. Graf, který se zobrazí poskytuje mapování z možných cest pro citlivé uživatele. Graf zobrazuje možné připojení zjištěnými v posledních 48 hodin. Pokud se zjistila žádná aktivita v posledních dvou dní grafu nezobrazí. 

4. Projděte si grafu chcete zobrazit, co se dozvíte o rizika ohrožení citlivých uživatelských přihlašovacích údajů. Například v této mapy, můžete postupovat podle **přihlašující** šedý šipky zobrazíte, kde Samira přihlášení jejich privilegovaných přihlašovacích údajů. V tomto případě Samira pro citlivé přihlašovací údaje se uložily v počítači REDMOND, WA-vývoj. Nyní, Všimněte si, jaké další uživatelé přihlášení do které počítače, které vytvořili nejvíce zviditelnění webu a ohrožení zabezpečení. Tohle je vidět pohledem **správce** černé šipky zjistit, kdo má oprávnění správce na prostředku. V tomto příkladu všem uživatelům ve skupině všechny Contoso má schopnost přístup k přihlašovacím údajům uživatele z tohoto prostředku.  

 ![cesty taktiky Lateral Movement profilu uživatele](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Preventivní osvědčené postupy

- Abyste měli jistotu, že citlivé uživatele pouze při přihlašování posílené počítače pomocí přihlašovacích údajů správce je nejlepším způsobem, jak zabránit taktiky Lateral Movement. V příkladu Ujistěte se, že pokud Samira správce potřebuje přístup k REDMOND, WA-vývoj, se přihlašují se pomocí uživatelského jména a hesla, než je jejich přihlašovacích údajů správce.

- Doporučujeme také, že zkontrolujete, že nemá nikdo nepotřebná oprávnění správce. V příkladu měli byste zkontrolovat Pokud všem uživatelům ve společnosti Contoso všechny skutečně vyžaduje práva správce na REDMOND, WA-odch

- Ujistěte se, že lidé mít přístup jenom k potřebné prostředky. V tomto příkladu Oscar Posada výrazně rozšiřuje na Samira vystavení. Je nezbytné, že se tento uživatel ve skupině obsaženy **Contoso všechny**? Existují podskupiny, které by bylo možné vytvořit, chcete-li minimalizovat vystavení?

**Tip** – Pokud se žádná aktivita zjistí během posledních 48 hodin a grafu není k dispozici, sestava cesty laterální pohyb je stále k dispozici a poskytne vám informace o potenciální cesty taktiky Lateral Movement zjištěnými za posledních 60 dní. 

**Tip** – pokyny o tom, jak nastavit vaši klienti a servery pro povolení ochrany ATP v programu Azure k provádění operací SAM-R, které jsou potřebné ke zjišťování cesty laterální pohyb, naleznete v části [konfigurace SAM-R](install-atp-step8-samr.md).


## <a name="see-also"></a>Viz také

- [Konfigurace SAM-R, vyžaduje oprávnění](install-atp-step8-samr.md)
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
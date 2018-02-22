---
title: "Příčin laterální pohyb cesta útoky s Azure ATP | Microsoft Docs"
description: "Tento článek popisuje, jak k detekci laterálního pohybu cesta útoky s Azure Advanced Threat Protection (ATP)."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7deeec2c2ee2c2d964b6495921eba0fa378bd8ee
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection verze 1.9*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Příčin laterální pohyb cesty s Azure ATP

Azure ATP můžete zabránit útokům, které používají laterální pohyb cesty. I v případě, že uděláte vaší nejvhodnější chránit citlivé uživatelé, Správci mají složitá hesla, které se často mění, jsou zesílené zabezpečení svých počítačů a jejich data se ukládají bezpečně, útočníci mohou stále používat laterální pohyb cesty přesunutí ve vaší síti mezi uživateli a počítači, dokud se dosáhl jackpotu virtuální zabezpečení: přihlašovací údaje účtu citlivé správce.

## <a name="what-is-a-lateral-movement-path"></a>Co je laterální pohyb cestu?

Laterální pohyb je, když útočník aktivně používá necitlivých účty pro přístup k citlivým účtům. Mohou použít některou z metod popsaných v [podezřelou aktivitu průvodce](suspicious-activity-guide.md) získat počáteční necitlivých heslo a pak použít nějaký nástroj, jako je Bloodhound, pochopit, kdo jsou správci ve vaší síti a které počítače k nim přistupovat. Poté můžete začít využívat data k dispozici útočníci v řadičích domény vědět, kdo má, které účty a přístup ke které zdroje a soubory a vám můžou ukrást přihlašovací údaje jiných uživatelů (někdy citlivé uživatelů) uložené na počítačích, které mají již získat přístup a následně k laterálnímu přesunout do více uživatelů a prostředků, dokud se bylo možné oprávnění správce ve vaší síti. 

Azure ATP umožňuje preemptivní akce ve vaší síti, chcete-li útočníkům zabránit v laterální pohyb úspěšné.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Zjišťování vaše rizikové citlivé účty

Chcete-li zjistit, které citlivé účty ve vaší síti byly snadno napadnutelný z důvodu jejich připojení na necitlivých účty nebo prostředky, postupujte takto. K zabezpečení sítě před útoky laterální pohyb, ATP v Azure funguje od konce zpětné, což znamená, že Azure ATP vám dává mapu, která se spustí z privilegovaných účtů a poté vám ukáže, kteří uživatelé a zařízení jsou v cestě laterální těchto uživatelů a jejich přihlašovací údaje.

1. Azure ATP nabídce pracovního prostoru portálu klikněte na ikonu sestav ![Ikona sestav](./media/atp-report-icon.png).

2. V části **pomoci odhalit laterální pohybů cesty k citlivým účtům**, pokud nejsou nalezeny žádné cesty laterální pohyb je sestava zobrazena šedě. Pokud existují laterální pohyb cesty, pak kalendářní data sestavy automaticky vybere první datum, kdy je relevantní data. Cesta sestavy laterální pohyb poskytuje data za posledních 60 dní.

 ![sestavy](./media/reports.png)

3. Klikněte na tlačítko **Stáhnout**.

3. Soubor aplikace Excel, která je vytvořena poskytuje podrobnosti o vaše citlivé účty, které jsou v ohrožení. **Souhrn** karta poskytuje grafy, které jsou upřesněny počet citlivé účty počítačů a průměry pro rizikové prostředky. **Podrobnosti** karta obsahuje seznam citlivé účty, které by měly být zajímá.

4. Pokyny k nastavení vaše servery umožňující ATP Azure k provádění operací SAM-R potřebné pro zjišťování cesta laterální pohyb [konfigurace SAM-R](install-atp-step8-samr.md).

## <a name="investigate"></a>Prošetření

Nyní když znáte citlivé účty, které jsou v ohrožení, můžete hloubky podrobné informace ATP Azure získáte další informace a přijmout preventivní opatření.

1. Na portálu Azure ATP pracovního prostoru, podívejte se na uživatele, jehož účet je uveden v zranitelná **pomoci odhalit laterální pohybů cesty k citlivým účtům** sestavy, například Samira Abbasi. Můžete také vyhledat oznámení laterální pohyb, který je přidán do profilu entity, když tato entita je v cestě laterální pohyb ![laterální ikonu](./media/lateral-movement-icon.png) nebo ![cesta ikonu](./media/paths-icon.png). Toto je k dispozici, pokud byl laterální pohyb během posledních dvou dnů. 

2. Na stránce profilu uživatele, které se otevře, klikněte **pomoci odhalit laterální pohyb cesty** kartě. 

3. Diagram, který se zobrazí vám poskytne mapu možných cest pro vaše citlivé uživatele. Graf zobrazuje připojení, které byly provedeny za posledních dvou dní, tak, aby expozici novou. Pokud není zjištěna aktivita za poslední dva dny grafu nezobrazí, ale [pomoci odhalit laterální pohyb cesta sestavy](reports.md) bude stále k dispozici poskytnout informace o způsobech laterální pohyb za posledních 60 dní.

4. Zkontrolujte graf tak, aby najdete, co se dozvíte úniku citlivých uživatelských přihlašovacích údajů. Například v této mapě, můžete postupovat podle Samira Abbasi **přihlášen pomocí** šedý šipky zobrazíte, kde Samira přihlášení jejich Privilegovaná pověření. V takovém případě uložení na Samira citlivé pověření v počítači REDMOND-WA-účelem Potom zjistili, která ostatní uživatelé přihlášení k které počítače, které vytvořili nejvíce zviditelnění webu a ohrožení zabezpečení. Můžete to vidět prohlížením **správce na** začernit dvojice šipek, které chcete zjistit, kdo má oprávnění správce na prostředku. V tomto příkladu všichni členové skupiny všechna Contoso má možnost přístupu k pověřením uživatele z tohoto prostředku.  

 ![cesty laterální pohyb profilu uživatele](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Preventivní osvědčené postupy

- Nejlepší způsob, jak zabránit laterální pohyb je zajistit, že citlivá uživatelé používat přihlašovacích údajů správce jenom v případě, že protokolování do posílené počítače. V příkladu Ujistěte se, že pokud správce Samira potřebuje přístup k REDMOND-WA-Vývojářů, se přihlaste se pomocí uživatelského jména a hesla než jejich přihlašovacích údajů správce.

- Doporučujeme také ověřit, zda, že nemá nikdo nepotřebné oprávnění správce. V příkladu měli zkontrolovat, zda všichni ve společnosti Contoso Všechna práva správce v REDMONDU-WA-účelem opravdu potřebuje

- Vždycky je vhodné Ujistěte se, že lidé pouze mají přístup k potřebné prostředky. Jak vidíte v příkladu, rozsudek Oscar Posada výrazně rozšiřuje Samira na ohrožení. Je nezbytné, uživatel být součástí Contoso všechny? Existují podskupiny, které můžete vytvořit minimalizovat ohrožení?


## <a name="see-also"></a>Viz také

- [Konfigurace SAM-R požadované oprávnění](install-atp-step8-samr.md)
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
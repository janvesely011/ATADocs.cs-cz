---
title: "Příčin laterální pohyb cesta útoky s ATA | Microsoft Docs"
description: "Tento článek popisuje, jak k detekci laterálního pohybu cesta útoky s Advanced Threat Analytics (ATA)."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: dc03cfe1719541dac0f8509c0f8f22987ecb96bb
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/22/2018
---
*Platí pro: Advanced Threat Analytics verze 1.9*

# <a name="investigating-lateral-movement-paths-with-ata"></a>Příčin cesty laterální pohyb se ATA

I v případě, že se vaše nejvhodnější chránit citlivé uživatelé a správci mají složitá hesla, které se často mění, jsou zesílené zabezpečení svých počítačů a jejich dat jsou bezpečně uloženy, útočníci mohou přesto používat laterální pohyb cesty pro přístup k citlivým účty. Při útoku laterální pohyb útočník využívá instancí citlivé uživatele po přihlášení na počítač kde necitlivých uživatel má místní práva. Útočníci můžete pak přesuňte následně k laterálnímu, přístup k méně citlivou uživatele a potom přesunutí mezi počítači k získání přihlašovacích údajů pro citlivé uživatele. 

## <a name="what-is-a-lateral-movement-path"></a>Co je laterální pohyb cestu?

Laterální pohyb je, když útočník aktivně používá necitlivých účty pro přístup k citlivým účtům. Mohou použít některou z metod popsaných v [podezřelou aktivitu průvodce](suspicious-activity-guide.md) získat počáteční necitlivých heslo a pak použít nějaký nástroj, jako je Bloodhound, pochopit, kdo jsou správci ve vaší síti a které počítače k nim přistupovat. Potom přístupem data na řadičích domény a vědět, kdo má účty, které přístup ke které zdroje a soubory, krádež přihlašovací údaje jiných uživatelů (někdy citlivé uživatelů), které jsou uložené na počítačích, které už mají přístup, a potom následně k laterálnímu přesuňte mezi uživateli a prostředky, dokud se bylo možné oprávnění správce ve vaší síti. 

ATA umožňuje preemptivní akce ve vaší síti, chcete-li útočníkům zabránit v laterální pohyb úspěšné.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Zjišťování vaše rizikové citlivé účty

Chcete-li zjistit, které citlivé účty ve vaší síti byly snadno napadnutelný z důvodu jejich připojení na necitlivých účty nebo prostředky, postupujte takto. K zabezpečení sítě před útoky laterální pohyb, funguje ATA od konce zpětné, což znamená, že ATA vám dává mapu, která se spustí z privilegovaných účtů a poté vám ukáže, kteří uživatelé a zařízení jsou v cestě laterální těchto uživatelů a jejich přihlašovacích údajů.

1. V nabídce konzoly ATA klikněte na ikonu sestav ![Ikona sestav](./media/ata-report-icon.png).

2. V části **pomoci odhalit laterální pohybů cesty k citlivým účtům**, pokud nejsou nalezeny žádné cesty laterální pohyb je sestava zobrazena šedě. Pokud existují laterální pohyb cesty, pak kalendářní data sestavy automaticky vybere první datum, kdy je relevantní data. 

 ![sestavy](./media/reports.png)

3. Klikněte na tlačítko **Stáhnout**.

3. Soubor aplikace Excel, která je vytvořena poskytuje podrobnosti o vaše citlivé účty, které jsou v ohrožení. **Souhrn** karta poskytuje grafy, které jsou upřesněny počet citlivé účty počítačů a průměry pro rizikové prostředky. **Podrobnosti** karta obsahuje seznam citlivé účty, které by měly být zajímá.


## <a name="investigate"></a>Prošetření

Nyní když znáte citlivé účty, které jsou v ohrožení, můžete hloubky podrobné informace ATA získáte další informace a přijmout preventivní opatření.

1. V konzole ATA, podívejte se na uživatele, jehož účet je uveden v jako citlivé **pomoci odhalit laterální pohybů cesty k citlivým účtům** sestavy, například Samira Abbasi. Můžete taky vyhledat oznámení laterální pohyb, který je přidán do profilu entity, když tato entita je v cestě laterální pohyb ![laterální ikonu](./media/lateral-movement-icon.png) nebo ![cesta ikonu](./media/paths-icon.png).

2. Na stránce profilu uživatele, které se otevře, klikněte **pomoci odhalit laterální pohyb cesty** kartě.

3. Diagram, který se zobrazí vám poskytne mapu možných cest pro vaše citlivé uživatele. Graf zobrazuje připojení, které byly provedeny za posledních dvou dní, tak, aby expozici novou.

4. Zkontrolujte graf tak, aby najdete, co se dozvíte úniku citlivých uživatelských přihlašovacích údajů. Například v této mapě, můžete postupovat podle Samira Abbasi **přihlášen pomocí** šedý šipky zobrazíte, kde Samira přihlášení svůj Privilegovaná pověření. V takovém případě uložení na Samira citlivé pověření v počítači REDMOND-WA-účelem Potom zjistili, která ostatní uživatelé přihlášení k které počítače, které vytvořili nejvíce zviditelnění webu a ohrožení zabezpečení. Můžete to vidět prohlížením **správce na** začernit dvojice šipek, které chcete zjistit, kdo má oprávnění správce na prostředku. V tomto příkladu všichni členové skupiny všechna Contoso má možnost přístupu k pověřením uživatele z tohoto prostředku.  

 ![cesty laterální pohyb profilu uživatele](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Preventivní osvědčené postupy

- Nejlepší způsob, jak zabránit laterální pohyb je zajistit, že citlivá uživatelé používat přihlašovacích údajů správce jenom v případě, že přihlášením se do počítače posílené tam, kde není necitlivých uživatele, který má práva správce na stejném počítači. V příkladu Ujistěte se, že pokud Samira potřebuje přístup k REDMOND-WA-Vývojářů, uživatel přihlásí pomocí uživatelského jména a hesla než jeho přihlašovací údaje správce, nebo odebrat skupinu všech Contoso z místní skupiny administrators v REDMONDU-WA-účelem

- Doporučujeme také ověřit, zda, že nemá nikdo nepotřebné místní oprávnění správce. V příkladu měli zkontrolovat, zda všichni ve společnosti Contoso Všechna práva správce v REDMONDU-WA-účelem opravdu potřebuje

- Vždycky je vhodné Ujistěte se, že lidé pouze mají přístup k potřebné prostředky. Jak vidíte v příkladu, rozsudek Oscar Posada výrazně rozšiřuje Samira na ohrožení. Je nezbytné, mohl být součástí Contoso všechny? Existují podskupiny, které můžete vytvořit minimalizovat ohrožení?


## <a name="see-also"></a>Viz také
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

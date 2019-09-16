---
title: Pochopení a používání cest po přesunu s využitím Azure ATP | Microsoft Docs
description: Tento článek popisuje možné cesty k okraji (LMPs) Azure Advanced Threat Protection (ATP).
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f7823fee5828df51b336428d810905e2672cc5a4
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71004917"
---
# <a name="azure-atp-lateral-movement-paths-lmps"></a>Cesty k příčnému pohybu Azure ATP (LMPs) 

> [!NOTE]
> Funkce ATP Azure, které jsou na této stránce popsané, jsou dostupné taky pomocí nového [portálu](https://portal.cloudappsecurity.com).

Příčný pohyb je v případě, že útočník používá necitlivé účty k získání přístupu k citlivým účtům v rámci vaší sítě. Boční pohyb používají útočníci k identifikaci a získání přístupu k citlivým účtům a počítačům ve vaší síti, které sdílejí uložené přihlašovací údaje pro přihlášení v účtech, skupinách a počítačích. Jakmile by útočník úspěšně provedl pohyb směrem k vašim klíčovým cílům, mohl by také využít výhod a získat přístup k řadičům domény. Útoky na boční pohyb se provádějí pomocí mnoha metod popsaných v [Průvodci podezřelými aktivitami](suspicious-activity-guide.md).

Klíčovou součástí přehledů zabezpečení služby Azure ATP jsou přepravní cesty nebo LMPs. Azure ATP LMPs jsou vizuální příručky, které vám pomůžou rychle pochopit a identifikovat přesně způsob, jakým se můžou útočníci později přesunout do vaší sítě. Účelem příčného přesunu v rámci přenosného řetězu útoku můžou útočníci získat a ohrozit vaše citlivé účty pomocí necitlivých účtů. Porušení citlivých účtů získá další krok přiblíž k jejich konečnému cíli a dominantnímu postavení v doméně. Pro zajištění úspěchu těchto útoků vám Azure ATP LMPs umožňuje snadno interpretovat, přímé vizuální pokyny na vaše nejohroženější a citlivé účty. LMPs vám pomůže pomoct omezit a zabránit těmto rizikům v budoucnu a před tím, než dostanou dominantní postavení v doméně, zavřít přístup k útočníkovi.

![Cesta k postrannímu pohybu Azure ATP (LMP)](./media/atp-lmp.png)

Útoky na boční pohyb se obvykle dosahují pomocí řady různých technik. Některé z nejoblíbenějších metod používaných útočníky jsou odcizení přihlašovacích údajů a předání lístku. V obou metodách útočníci používají necitlivé účty k bočním pohybům, a zneužívá necitlivých počítačů, které sdílejí uložené přihlašovací údaje pro přihlášení v účtech, skupinách a počítačích s citlivými účty.

## <a name="where-can-i-find-azure-atp-lmps"></a>Kde můžu najít Azure ATP LMPs?

Všechny počítače nebo profily uživatelů zjištěné službou Azure ATP, aby byly na LMP, na kartu **cest pohybu** . Počítače a profily bez karty nebyly nikdy zjištěny v rámci potenciálního LMP. 

![Karta pro cestu k bočnímu pohybu Azure ATP (LMP)](./media/lateral-movement-path-tab.png)

LMP pro každou entitu poskytuje různé informace v závislosti na citlivosti entity: 
- Citliví uživatelé – zobrazí se potenciální LMPy, které by to vedlo k tomuto uživateli.
- Necitliví uživatelé a počítače – potenciální LMPy, se kterými se entita týká, se zobrazuje. <br>

Pokaždé, když se klikne na kartu, Azure ATP zobrazí naposledy zjištěné LMP. Každý potenciální LMP je uložený po dobu 48 hodin po zjištění. Historie LMP je k dispozici. Kliknutím na **Zobrazit jiné datum**Zobrazte starší LMPs zjištěné v minulosti. 

![LMP (zobrazení) – cesta k bočnímu pohybu Azure ATP](./media/atp-lmp-complete.png)

Objevte se, kdy byly zjištěny potenciální LMPs a které související entity jsou potenciálně zapojeny. 

## <a name="lmp-discovery"></a>Zjišťování LMP

Na kartě aktivity se uvede indikace, když se identifikoval nový potenciální LMP:
- Citliví uživatelé – při identifikaci nové cesty pro citlivého uživatele

![Zjistila se LMP citlivá cesta k pohybu Azure ATP.](./media/atp-lmp-activities.png)

- Necitliví uživatelé a počítače – Pokud je tato entita identifikována potenciálním LMP, která vede k citlivým uživatelům.

![Necitlivá cesta k příčnému pohybu Azure ATP (LMP)](./media/atp-lateral-non-sensitive.png)

## <a name="lmp-related-entities"></a>Entity související s LMP
LMP může nyní přímo pomoct s procesem šetření. Seznamy legitimace výstrah zabezpečení Azure ATP poskytují související entity, které se podílejí na každé možné cestě k pohybu. Seznam legitimace přímo pomůže vašemu týmu vaší reakce na zabezpečení zvýšit nebo snížit důležitost výstrahy zabezpečení nebo šetření souvisejících entit. Například když je oznámení o lístku vystaveno, zdrojový počítač, ohrožený uživatel a cílový počítač, ze kterého byl ukradený lístek použit, jsou všechny části potenciálního bočního umístění, které vede na citlivého uživatele. Existence zjištěného LMPu provede šetření výstrahy a ještě důležitějšího sledování podezřelého uživatele, aby se zabránilo tomu, aby se nežádoucí osoba z dalších bočních míst. LMPselné legitimace jsou k dispozici v nástroji, aby bylo snazší a rychlejší, abyste útočníkům zabránili v přesunu vpřed ve vaší síti. 

## <a name="lateral-movement-paths-to-sensitive-accounts-report"></a>Sestava bočních cest k citlivým účtům 
Data LMP jsou také k dispozici v rámci [cest přesunu na citlivé účty](investigate-lateral-movement-path.md). Tato sestava obsahuje seznam citlivých účtů, které jsou zpřístupněny prostřednictvím cest po pohybu, a zahrnuje cesty, které byly vybrány ručně pro konkrétní časové období, nebo zahrnuté do časového období pro plánované sestavy.  Přizpůsobte rozsah dat zahrnutí pomocí výběru kalendáře. 

## <a name="preventative-best-practices"></a>Preventivní osvědčené postupy
Přehledy zabezpečení nejsou nikdy zpožděné, aby se zabránilo dalšímu útoku a napravily škody. Z tohoto důvodu může prozkoumat útok i během fáze dominantního postavení v doméně jiný, ale důležitý příklad. Při zkoumání výstrahy zabezpečení, jako je vzdálené spuštění kódu, se obvykle používá, pokud je výstraha falešně pozitivní, váš řadič domény už může být ohrožen. Ale LMPs informovat, kde útočník získal oprávnění a jaká cesta se k vaší síti použila. Tímto způsobem může LMPs také nabízet klíčové poznatky k nápravě.  

- Nejlepším způsobem, jak zabránit expozici bočního pohybu v rámci vaší organizace, je zajistit, aby citlivé uživatelé používali přihlašovací údaje správce jenom při přihlašování do zesílených počítačů. V příkladu ověřte, zda správce v cestě skutečně potřebuje přístup ke sdílenému počítači. Pokud potřebují přístup, ujistěte se, že se přihlásíte ke sdílenému počítači pomocí uživatelského jména a hesla, které je jiné než přihlašovací údaje správce.

- Ověřte, že uživatelé nemají potřebná oprávnění ke správě. V tomto příkladu zjistíte, jestli všichni ve sdílené skupině skutečně vyžaduje práva správce na vystaveném počítači.

- Ujistěte se, že lidé mají přístup jenom k potřebným prostředkům. V tomto příkladu Ron Harper významně rozšiřuje expozici vážně Cowley. Je nutné, aby do skupiny zahrnoval Ron Harper? Existují podskupiny, které by bylo možné vytvořit pro minimalizaci ozáření bočního pohybu?

**Tip** – Pokud pro entitu v posledních 48 hodinách není zjištěna žádná potenciální aktivita pohybu v cestě k okraji, vyberte, **že chcete zobrazit jiné datum** a vyhledat předchozí možné cesty bočního pohybu. **Sestava LMP to citliví uživatelé** je vždy dostupná, pokud se zjistilo LMPs a poskytuje informace o potenciálních cestách při přesunu citlivých uživatelů. 

**Tip** – pokyny, jak nastavit klienty a servery tak, aby umožňovaly službě Azure ATP provádět operace Sam-R, které jsou potřeba pro detekci cest k příčnému přesunu, najdete v tématu [Konfigurace Sam-r](install-atp-step8-samr.md).


## <a name="investigating-lmps"></a>Prošetření LMPs
Pokyny, jak identifikovat a prozkoumat používání služby Azure ATP po cestách, najdete v tématu [prozkoumání cest po pohybu](investigate-lateral-movement-path.md).


## <a name="see-also"></a>Viz také
- [Zkoumání Azure ATP LMPs](investigate-lateral-movement-path.md)
- [Konfigurace služby Azure ATP pro vzdálená volání do SAM](install-atp-step8-samr.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

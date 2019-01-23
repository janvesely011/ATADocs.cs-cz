---
title: Úvod do cesty taktiky Lateral Movement pomocí ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Tento článek popisuje potenciální Laterálním Průnikovým trasám (LMPs) z Azure Advanced Threat Protection (ATP).
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 88a7d5e23cc6b3f1202f522e40060e71f676397f
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/23/2019
ms.locfileid: "54459069"
---
# <a name="azure-atp-lateral-movement-paths-lmps"></a>Azure ATP laterální pohyb cesty (LMPs) 

Laterální pohyb je, když útočník pomocí tohoto počtu účtů pro přístup k citlivým účtům v celé síti. Laterální pohyb útočníci slouží k identifikaci a získat přístup k citlivým účtům a počítačů v síti, které sdílejí přihlašovací údaje uložené v účtů, skupin a počítačů. Jakmile útočník Díky úspěšné laterální přibližování klíčových cílů, útočník můžete také využít a získat přístup k vašim řadičům domény. Laterální pohyb útoky provádějí pomocí řady metod popsaných v [Průvodce prošetřováním podezřelých aktivit](suspicious-activity-guide.md).

Klíčovou součástí služby Azure ATP přehledy o zabezpečení jsou cesty taktiky Lateral Movement nebo LMPs. Azure LMPs ochrany ATP v programu je vizuální vodítko, které pomáhají rychle zjistit a identifikovat program přesně jak přesunout útočníci následně k laterálnímu uvnitř vaší sítě. Účelem taktiky Lateral Movement v řetězu událostí internetového útoku jsou útočníkům získat a ohrožení vašich citlivých účtů pomocí tohoto počtu účtů. Ohrožení citlivých účtů je získá další krok blíž k jejich konečným cílem dominance v doméně. Pokud chcete zastavit tyto útoky nebudou úspěšné, LMPs ochrany ATP v programu Azure poskytují snadno interpretuje s přímým přístupem visual doprovodné materiály k nejohroženější, citlivé účty. LMPs pomoct pomáhá zmírnit a v budoucnosti zabránilo těchto rizik a zavřete útočník mohl získat přístup před jejich dosažení dominance v doméně.

![Azure ATP laterální pohyb cestu (LMP)](./media/atp-lmp.png)

Laterální pohyb útoky jsou obvykle provedeno pomocí řadu různých technik. Některé z nejoblíbenějších metod používaných útočníky jsou krádeže přihlašovacích údajů a předat-the-Ticket. V obou metod méně citlivé účty používají útočníci pro laterální přesuny využívajícím počítačů nejsou citliví, které sdílejí uložená pověření přihlášení v účtů, skupin a počítačů s citlivými účty.

## <a name="where-can-i-find-azure-atp-lmps"></a>Kde najdu LMPs ochrany ATP v programu Azure?

Každý počítač nebo konkrétního uživatele profil zjištěných ochrany ATP v programu Azure v LMP **laterální pohyb cesty** kartu. Počítače a profily bez kartou nikdy byly zjištěny za potenciální LMP. 

![Azure kartu ochrany ATP v programu cesty laterální pohyb (LMP)](./media/lateral-movement-path-tab.png)

LMP pro každou entitu poskytuje různé informace v závislosti na citlivosti entity: 
- Citliví uživatelé – jsou uvedeny potenciální LMP(s), což vede k tomuto uživateli.
- Uživatelé a počítače – jsou uvedeny potenciální LMP(s) entitou souvisí. <br>

Pokaždé, když dojde ke kliknutí na kartě, zobrazí ochrany ATP v programu Azure nedávno zjištěné LMP. Každý potenciální LMP uložena po dobu 48 hodin po zjišťování. Není k dispozici historie LMP. Zobrazit starší LMPs, které byly zjištěny v minulosti po kliknutí na **zobrazit jiné datum**. 

![Zobrazení Azure ochrany ATP v programu cesty laterální pohyb (LMP)](./media/atp-lmp-complete.png)

Zjistíte, kdy byly zjištěny možné LMPs a potenciálně souvisejících entit, které souvisejí. 

## <a name="lmp-discovery"></a>LMP zjišťování

Na kartě aktivit je přiřazena jako ukazatel toho, když se identifikovat nové potenciální LMP:
- Citliví uživatelé – když novou cestu, kterou jste našli na citlivého uživatele

![Azure identifikovat citlivé na ochrany ATP v programu cesty laterální pohyb (LMP)](./media/atp-lmp-activities.png)


- Uživatelé a počítače – když tuto entitu byl identifikován v potenciální LMP, což vede k citlivé uživatele.

![Azure ochrany ATP v programu cesty laterální pohyb (LMP) nejsou citliví identifikovat](./media/atp-lateral-non-sensitive.png)

## <a name="lmp-related-entities"></a>LMP souvisejících entit
LMP můžete nyní přímo pomáhá při procesu šetření. Azure seznamy výstrah legitimace zabezpečení ochrany ATP v programu poskytují související entity, které jsou součástí každé potenciální cesty laterální pohyb. Seznamy důkazy přímo pomohou vaše odpověď zabezpečení týmu zvýšení nebo snížení závažnost výstrahy zabezpečení a/nebo šetření souvisejících entit. Například při průchodu, je vydána výstraha lístek, zdrojový počítač, dojde k ohrožení bezpečnosti uživatele a cílový počítač odcizených lístků použila, jsou všechny části potenciální cesty laterální pohyb vede na citlivého uživatele. Díky existenci zjištěné LMP vyšetřování upozornění a sledování podezřelého uživatele ještě více důležité, abyste zabránili vaše nežádoucí osoba z dalších laterální přesouvá. Organizovaným důkazy je součástí LMPs umožňují snadněji a rychleji bránící útočníkům v budoucnu ve vaší síti. 

## <a name="lateral-movement-paths-to-sensitive-accounts-report"></a>Laterálním průnikovým trasám sestavy citlivých účtů 
LMP data jsou také k dispozici v [Laterálním Průnikovým trasám sestavy citlivých účtů](investigate-lateral-movement-path.md). Tato sestava uvádí citlivé účty, které jsou zveřejňovány prostřednictvím cesty taktiky Lateral Movement a zahrnuje cesty, které byly ručně vybraných pro určité časové období, nebo součástí časové období pro plánované sestavy.  Upravte rozsah zahrnutých dat pomocí výběru kalendáře. 

## <a name="preventative-best-practices"></a>Preventivní osvědčené postupy
Přehledy o zabezpečení jsou nikdy příliš pozdě. aby se předešlo další útoku a nápravě škod. Z tohoto důvodu vyšetřování útoku i během fáze dominance domény poskytuje příklad jiné, ale důležité. Obvykle při prošetřování výstrahy zabezpečení, jako je vzdálené spuštění kódu, pokud je výstraha o pravdivě pozitivní upozornění řadiči domény může již být ohrožena. Pokud útočník získal oprávnění a co LMPs informuje, ale cesta používají do vaší sítě. Takto použije, může LMPs také nabízejí klíče podrobné informace o způsobu řešení.  

- Abyste měli jistotu, že citlivé uživatele pouze pomocí přihlašovacích údajů správce při přihlašování posílené počítače je nejlepším způsobem, aby se zabránilo ohrožení laterální pohyb v rámci vaší organizace. V příkladu zaškrtněte, pokud správce v cestě ve skutečnosti potřebuje přístup ke sdílené počítače. Pokud potřebují přístup, ujistěte se, že přihlášení pro sdílené počítače pomocí uživatelského jména a hesla, než je jejich přihlašovacích údajů správce.

- Ověřte, že uživatelé nemají nepotřebná oprávnění správce. V příkladu zaškrtněte, pokud všem uživatelům ve skupině sdílené ve skutečnosti vyžaduje oprávnění správce na počítači vystavené.

- Ujistěte se, že lidé mít přístup jenom k potřebné prostředky. V tomto příkladu Ron Harper výrazně rozšiřuje Nick Cowley vystavení. Je nezbytné, Ron Harper být součástí skupiny? Existují podskupiny, které by bylo možné vytvořit, chcete-li minimalizovat vystavení laterální pohyb?

**Tip** – Pokud se rozhodnete žádné potenciál pro entitu za posledních 48 hodin se zjistí aktivita cesty taktiky Lateral Movement **zobrazit jiné datum** a vyhledat předcházející potenciál laterální pohyb cesty. **LMP citlivé uživatele sestavy** je vždy k dispozici je LMPs byly zjištěny a poskytne vám informace o potenciální cesty taktiky Lateral Movement zjistí citlivé uživatele. 

**Tip** – pokyny o tom, jak nastavit vaši klienti a servery pro povolení ochrany ATP v programu Azure k provádění operací SAM-R, které jsou potřebné ke zjišťování cesty laterální pohyb, naleznete v části [konfigurace SAM-R](install-atp-step8-samr.md).


## <a name="investigating-lmps"></a>Zkoumání LMPs
Pokyny o tom, jak identifikovat a prozkoumat pomocí cesty taktiky Lateral Movement ochrany ATP v programu Azure najdete v tématu [prozkoumat cesty taktiky Lateral Movement](investigate-lateral-movement-path.md).


## <a name="see-also"></a>Viz také
- [Zkoumání LMPs ochrany ATP v programu Azure](investigate-lateral-movement-path.md)
- [Konfigurace služby Azure ATP pro vzdálená volání do SAM](install-atp-step8-samr.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
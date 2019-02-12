---
title: Ochrana ATP v programu zabezpečení výstrah kurz pro Azure | Dokumentace Microsoftu
d|Description: This article explains how to use and understand Azure ATP security alerts.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/13/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 671747d5-faed-4352-a871-17b58fdc6574
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1633361f68367dbc82e82e0b18da09227f82206a
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077826"
---
# <a name="tutorial-understanding-security-alerts"></a>Kurz: Principy výstrah zabezpečení

Upozornění zabezpečení v Azure ochrany ATP v programu popisují v vymazat jazyk a grafiku, které podezřelé aktivity, které byly zjištěny ve vaší síti a objekty actor a počítačů, které jsou zahrnuty v něm přítomné hrozby. Výstrahy jsou stupněm závažnost, barevné označení, aby se daly snadno vizuálně filtrovat a uspořádané podle fáze před internetovými útoky. Každé výstraze zajišťuje vám pomůžou rychle porozumět přesně, co se děje ve vaší síti. Upozornění důkazy seznamy obsahovat přímé odkazy na související uživatelé a počítače, abyste se mohli vaše šetření, snadno a s přímým přístupem.

V tomto kurzu se seznámit se se strukturou výstrah zabezpečení služby Azure ATP a jakým způsobem je použít: 

> [!div class="checklist"]
> * Struktura výstrahy zabezpečení
> * Klasifikacích výstrahy zabezpečení
> * Kategorie výstrahy zabezpečení
> * Pokročilé šetření výstrahy zabezpečení
> * Související entity
> * Ochrana ATP v programu Azure a ÚTOKŮ (překlad síťových názvů)


## <a name="security-alert-structure"></a>Struktura výstrahy zabezpečení

Každá výstraha zabezpečení služby Azure ATP zahrnuje:
 
- **Název výstrahy** <br> Oficiální název služby Azure ATP výstrahy.
- **Popis** <br> Stručný popis co se stalo.
- **Důkaz** <br> Další důležité informace a související data o tom, co se stalo s pomoc při procesu šetření.
- **Stažení aplikace Excel** <br> Podrobné Excel stáhnout sestavu pro analýzu

![Azure struktura výstrah zabezpečení ochrany ATP v programu](media/security-alert-structure.png)

## <a name="security-alert-classifications"></a>Klasifikacích výstrahy zabezpečení

Po správném šetření všechny výstrahy zabezpečení služby Azure ATP dají považovat za jednu z následujících typů aktivit:

- **Pravdivě pozitivní upozornění (TP)**: Škodlivá akce zjištěná službou ochrany ATP v programu Azure.

- **Neškodné pravdivě pozitivní upozornění (B-TP)**: Akce zjištěná službou ochrany ATP v Azure, která je skutečná, ale není škodlivá, třeba test průniku nebo známé aktivity generovaných schválených aplikací.

- **Falešně pozitivní (FP)**: Upozornění hodnotu false, to znamená aktivity neměli dojít.

### <a name="is-the-security-alert-a-tp-b-tp-or-fp"></a>Výstraha zabezpečení, je zpracování transakcí, B-TP nebo FP

Pro každou výstrahu odpovědět na tyto otázky k určení výstrah klasifikace a pomáhá v rozhodování, jak postupovat dál:

1. Jak běžná je tato výstraha zabezpečení ve vašem prostředí?
2. Aktivovalo upozornění stejné typy počítačů nebo uživatelů?
   Například servery se stejným role nebo uživatelé ze stejné skupiny/oddělení? Kdyby podobné počítače nebo uživatele, můžete rozhodnout vyloučit, abyste se vyhnuli dalším další budoucí FP výstrahy.

Poznámka: Zvýšení výstrah přesně stejný typ obvykle snižuje podezřelé/význam úroveň výstrahy. Pro opakující se výstrahy zkontrolujte konfigurace a používat výstrahy zabezpečení, že definice pochopit, co se přesně děje a podrobnosti o aktivaci opakování. 

## <a name="security-alert-categories"></a>Kategorie výstrahy zabezpečení

Upozornění zabezpečení v Azure ochrany ATP v programu jsou rozdělené do následujících kategorií nebo fází, jako je fáze v řetězu událostí typické internetového útoku. Další informace o jednotlivých fází a výstrahy, které jsou navržené k detekování každého útoku, pomocí následujících odkazů:

- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před taktikou lateral movement](atp-lateral-movement-alerts.md)
- [Výstrahy před dominancí v doméně](atp-domain-dominance-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)

## <a name="advanced-security-alert-investigation"></a>Výstrahy vyšetřování pokročilé zabezpečení

Abyste získali více podrobností na výstrahu zabezpečení, stáhněte si podrobnou zprávu upozornění aplikace Excel.

1. Klikněte na tlačítko tří teček v pravém horním rohu jakékoli upozornění, vyberte *podrobnosti o stahování*.
 
Každého stažení služby Azure ATP výstrah Excel obsahuje následující informace:   
- Souhrn – první karta obsahuje stručný přehled výstrahy 
  - Titul 
  - Popis 
  - Počáteční čas (UTC) 
  - Koncový čas (UTC) 
  - Závažnost – nízké/střední/vysoké
  - Stav – otevřený/uzavřený
  - Čas aktualizace stavu (UTC)
  - Zobrazit v prohlížeči
- Všechny používané entity (účty počítačů a prostředků) jsou uvedeny, oddělené jejich role. 
    - Zdroj, cíl, nebo, v závislosti na upozornění. 
- Většina karty z nich zahrnuje následující data pro jednotlivé entity: 
  - Název
  - Podrobnosti 
  - Type 
  - SamName  
  - Zdrojový počítač
  - Zdrojový uživatel (Pokud je k dispozici)
  - Domain Controllers
  - Využívaných prostředků: Čas, počítače, název, podrobností, typ, služby.
  - Další záložky k výstraze: 
      - V napadených účtů při použití podezřelý útok hrubou silou.
      - V systému DNS (Domain Name) serverů, když podezřelý napadených zahrnuté síťové mapování rekognoskace (DNS).
  - Související entity: ID, typ, název, Json jedinečné Entity jedinečné Entity profilu Json
- Vše nezpracované aktivity zachycené senzory ochrany ATP v programu Azure související s včetně upozornění (sítě nebo událostí aktivit):
  - Síťové aktivity
  - Události aktivity

![Souvisejícími entitami](media/involved-entities.png)

### <a name="related-entities"></a>Související entity

Každé upozornění obsahuje poslední zarážky **související entity**. Související entity jsou všechny entity účastnící se podezřelé aktivity, bez oddělení "role" se přehrávají v upozornění. Každá entita má dva soubory Json, jedinečné Entity Json a Json profil jedinečné Entity. Další informace o entitě a který vám pomůže prozkoumat upozornění, použijte tyto dva soubory Json. 
 
**Unique Entity Json**
 
Obsahuje data, která ochrany ATP v programu Azure vytvořeným ze služby Active Directory o účtu. To zahrnuje všechny atributy jako *rozlišující název*, *SID*, <em>LockoutTime, a * PasswordExpiryTime</em>. Pro uživatelské účty, obsahuje data *oddělení*, *e-mailu*, a *PhoneNumber*. Pro účty počítačů obsahuje data *OperatingSystem*, <em>IsDomainController, a * DnsName</em>.

**Json profil jedinečné Entity**

Zahrnuje všechna data v entitě profilované služby Azure ATP. Ochrana ATP v programu Azure používá síť a událostí aktivit zachytit Další informace o uživatelích a počítačích prostředí. Ochrana ATP v programu Azure profily relevantní informace na entitu. Tyto informace přispívá možnosti identifikace hrozeb služby Azure ATP.

![Související entity](media/related-entities.png)
 
### <a name="how-can-i-use-azure-atp-information-in-an-investigation"></a>Jak můžete použít informace služby Azure ATP v šetření? 

Vyšetřování může být uvedené podle potřeby. Tady je několik nápadů, jak prozkoumat používání dat poskytované služby Azure ATP.

- Zaškrtněte, pokud všechny související uživatelé patří do stejné skupiny nebo oddělení?
- Související uživatelé sdílí prostředky, aplikace nebo počítače?
- Je účet aktivní, i v případě, že jeho PasswordExpiryTime o už uplynulé?

## <a name="azure-atp-and-nnr-network-name-resolution"></a>Ochrana ATP v programu Azure a ÚTOKŮ (překlad síťových názvů)

Funkce detekce ve službě Azure ATP spoléhají na aktivní síťové název řešení ÚTOKŮ přeložit IP adresy na počítačích ve vaší organizaci. Použití ÚTOKŮ, ochrana ATP v programu Azure je možnost provést korelaci mezi nezpracovaná aktivity (který obsahuje IP adresy) a relevantní počítačů zahrnutých v každé aktivity. Ochrana ATP v programu Azure založené na aktivitách nezpracovaná, profily entit, včetně počítačů a generuje výstrahy.

NNR dat je zásadní pro zjišťování následující výstrahy:
- Krádež identity podezřelého softwaru (pass-the-ticket) 
- Podezřelý útok DCSync (replikace adresářových služeb)
- Mapování sondování sítě (DNS)

Použijte NNR informace uvedené v **síťové aktivity** kartu upozornění stahování sestavy, a zjistit, jestli výstrahu **FP**. V případě **FP** výstrahy, je běžné mít výsledkem jistoty NNR uvedeným s nízkou spolehlivostí.

Stáhněte sestavu, která data se vyskytují ve dvou sloupcích: 
- **Zdrojový/cílový počítač** 

    - *Jistota* – s nízkým rozlišením jistoty může znamenat nesprávné překlad.
- **Zdrojový/cílový počítač**
    - *Metoda překladu* – poskytuje metody NNR používá k překladu IP adresu na počítačích v organizaci.

![Síťové aktivity](media/network-activities.png)

Další informace o tom, jak pracovat s výstrahami zabezpečení služby Azure ATP najdete v tématu [práce s výstrahami zabezpečení](working-with-suspicious-activities.md).

## <a name="see-also"></a>Viz také

- [Prošetřování uživatelů](investigate-a-user.md)
- [Prošetřování počítačů](investigate-a-computer.md)
- [Práce s cesty taktiky Lateral Movement](use-case-lateral-movement-path.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
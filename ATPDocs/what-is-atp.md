---
title: Co je Azure Advanced Threat Protection (ATP)? | Dokumenty Microsoft
description: Vysvětluje, co je Azure Advanced Threat Protection (ATP) a jaké druhy podezřelých aktivit může zjistit
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c889fc070ffaf79a89c072d83edf6cc6f1cd0413
ms.sourcegitcommit: 121c49d559e71741136db1626455b065e8624ff9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2018
ms.locfileid: "41734773"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="what-is-azure-advanced-threat-protection"></a>Co je Azure Advanced Threat Protection?
Azure Advanced Threat Protection (ATP) je cloudová služba, která pomáhá chránit podniková hybridní prostředí před různými typy pokročilých cílených kybernetických útoků a ohrožením zevnitř.

## <a name="how-azure-atp-works"></a>Jak funguje Azure ATP

Ochrana ATP v programu Azure využívá speciální síťový parsovací modul k zachycení a parsování síťového provozu různých protokolů (například Kerberos, DNS, RPC, NTLM a další) pro ověřování, autorizaci a shromažďování informací. Ochrana ATP v programu Azure tyto informace shromažďuje prostřednictvím:

-   Nasazení služby Azure ATP senzorů přímo na řadiče domény
-   Zrcadlení portů z řadičů domény a serverů DNS do samostatného senzoru služby Azure ATP

Ochrana ATP v programu Azure přebírá informace z různých zdrojů dat, jako jsou protokoly a události v síti, chování uživatelů a dalších entit v organizaci a vytvářet o nich profil chování.
Ochrana ATP v programu Azure může přijímat události a protokoly z:

-   Integrace se SIEM
-   Předávání událostí systému Windows (WEF)
-   Přímo z protokolu událostí Windows (pro senzor)
-   Monitorování účtů ze sítí VPN pomocí protokolu RADIUS


Další informace o architektuře služby Azure ATP, naleznete v tématu [Architektura ochrany ATP v programu Azure](atp-architecture.md).

## <a name="what-does-azure-atp-do"></a>Co dělá ochrany ATP v programu Azure?

Technologie ochrany ATP v programu Azure detekuje různé podezřelé aktivity, zaměřuje se na několik fází v řetězci kill internetového útoku včetně:

-   Rekognoskace, během které útočníci shromáždit informace o tom, jak je sestavená prostředí, jaké různé formáty jsou a entit, které neexistuje. Se připravují si plán pro další fáze útoku.
-   Cyklus laterálního pohybu, během kterého útočník investuje čas a úsilí do rozšíření prostoru pro útoky uvnitř vaší sítě.
-   Dominance domény (trvalost), během které útočník zachycuje informace, které mu umožňují pokračovat v kampani pomocí různých sad vstupních bodů, přihlašovacích údajů a technik. 

Tyto fáze internetového útoku jsou podobné a předvídatelné bez ohledu na typ napadené společnosti nebo typ informací, o které se usiluje.
Ochrana ATP v programu Azure hledá tří hlavní typy útoků: škodlivé útoky, neobvyklé chování a problémy a rizika zabezpečení.

**Útoky se zlými úmysly** zjištění nedeterministicky stejně jako prostřednictvím analýzy neobvyklé chování. Úplný seznam známých typů útoků zahrnují:

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   Forged PAC (MS14-068)
-   Zlatý lístek
    -   čas anomoly
    -   neexistující účet – nové
-   Škodlivá replikace
-   Vytváření výčtu adresářových služeb
-   Výčet relací SMB
-   Rekognoskace DNS
-   Horizontální útoky hrubou silou 
-   Vertikální útoky hrubou silou
-   Skeleton Key
-   Neobvyklý protokol
-   Oslabení šifrování
-   Vzdálené spuštění
-   Vytvoření škodlivé služby
-   Povýšení řadiče domény podezřelé (možný útok DCShadow) – nové
-   Podezřelá replikace požadavku (možný útok DCShadow) – nové
-   Síť VPN 


Ochrana ATP v programu Azure detekuje tyto podezřelé aktivity a zobrazí příslušné informace na portálu ochrany ATP v programu Azure pracovní prostor, včetně jasného zobrazení kdo, co, kdy a jak. Jak vidíte, při sledování tohoto jednoduchého a uživatelsky vstřícného řídicího panelu budete upozorněni, že ochrana ATP v programu Azure, že útok typu Pass-the-Ticket se má podezření na útok počítačům klient 1 a 2 ve vaší síti.

 ![ukázky služby Azure ATP obrazovky pass-the-ticket](media/pass-the-ticket-sa.png)


Ochrana ATP v programu Azure také detekuje **problémy a rizika zabezpečení**, včetně:

-   Slabé protokoly
-   Známá slabá místa protokolů
-   [Cesty taktiky Lateral Movement k citlivým účtům](use-case-lateral-movement-path.md)

# <a name="what-threats-does-azure-atp-look-for"></a>Jaké hrozby ochrany ATP v programu Azure vyhledejte?

Ochrana ATP v programu Azure zajišťuje detekci pro následující fáze pokročilých útoků: rekognoskace, zneužití přihlašovacích údajů, laterální pohyb, zvýšení úrovně oprávnění, dominance v doméně a další. Tyto detekce jsou zaměřené na zjišťování pokročilých útoků a vnitřních hrozeb ještě předtím, než mohou ve vaší organizaci způsobit škody.

Výsledkem detekce v jednotlivých fázích je několik podezřelých aktivit relevantních pro danou fázi. Každá podezřelá aktivita je v korelaci s různými charakteristikami možných útoků.
Na následujícím obrázku jsou zvýrazněné fáze v řetězci úkonů útočníka, kde ochrany ATP v programu Azure aktuálně poskytuje detekci:

![Ochrana ATP v programu Azure zaměřit se na postranní aktivity v řetězci úkonů útočníka](media/attack-kill-chain-small.jpg)


Další informace najdete v tématu [práce s podezřelými aktivitami](working-with-suspicious-activities.md) a [Průvodce prošetřováním podezřelých aktivit ochrany ATP v programu Azure](suspicious-activity-guide.md).

## <a name="whats-next"></a>Co dál?

-   Další informace o způsobu ochrany ATP v programu Azure zapadá do vaší sítě: [architektura služby Azure ATP](atp-architecture.md)

-   Abyste mohli začít nasazením ochrany ATP v programu: [ochrany ATP v programu nainstalovat](install-atp-step1.md)


## <a name="see-also"></a>Viz také
- [Nejčastější dotazy k Azure ATP](atp-technical-faq.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
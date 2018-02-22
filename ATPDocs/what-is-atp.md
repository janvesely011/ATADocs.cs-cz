---
title: Co je Azure Advanced Threat Protection (ATP)? | Dokumentace Microsoftu
description: "Vysvětluje, co je Azure Advanced Threat Protection (ATP) a jaké druhy podezřelých aktivit může zjistit."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5ccac90a171c895ee8b4d5336a125ccd7fa66239
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="what-is-azure-advanced-threat-protection"></a>Co je Azure Advanced Threat Protection?
Azure ochrany rozšířené hrozba (ATP) je Cloudová služba, která pomáhá chránit vaše organizace hybridní prostředí z více typů pokročilé cílové internetovými útoky i vnitřními hrozbami.

## <a name="how-azure-atp-works"></a>Jak funguje Azure ATP

Azure ATP využívá proprietární sítě, analýza modul k zaznamenání a analyzovat síťový provoz více protokolů (například protokolu Kerberos, DNS, RPC, protokol NTLM a dalších) pro ověřování, autorizaci a shromažďování informací. Tyto informace jsou shromažďovány pomocí Azure ATP prostřednictvím buď:

-   Nasazení Azure ATP senzorů přímo na řadiče domény
-   Port zrcadlení ze serverů řadiče domény a DNS na samostatné senzoru Azure ATP

Azure ATP trvá informace z více-zdrojů dat, jako jsou protokoly a události v síti, k informace chování uživatelů a ostatní entity v organizaci a vytvoření profilu chování o nich.
Azure ATP může přijímat události a protokoly:

-   Integrace se SIEM
-   Předávání událostí systému Windows (WEF)
-   Přímo z sběru událostí systému Windows (pro senzoru)
-   Monitorování účtů ze sítě VPN RADIUS


Další informace o architektuře Azure ATP najdete v tématu [architektura ATP Azure](atp-architecture.md).

## <a name="what-does-azure-atp-do"></a>Jakým způsobem Azure ATP?

Azure technologie ATP zjištění několik podezřelých aktivit, zaměřené na několik fází internetový útoku kill řetězu včetně:

-   Rekognoskace, během které útočníci shromažďovat informace o tom, jak je integrovaná prostředí, jaké jiné prostředky jsou a entit, které neexistuje. Obecně se vytváření jejich plán pro další fáze útoku.
-   Cyklus laterálního pohybu, během kterého útočník investuje čas a úsilí do rozšíření prostoru pro útoky uvnitř vaší sítě.
-   Dominance v doméně (trvalost), během které útočník zachytává informace, což jim umožní obnovit jejich kampaň použití různých sad vstupních bodů, přihlašovací údaje a techniky. 

Tyto fáze internetového útoku jsou podobné a předvídatelné bez ohledu na typ napadené společnosti nebo typ informací, o které se usiluje.
Azure ATP hledá tři hlavní typy útoků: útoky se zlými úmysly, neobvyklé chování a problémy se zabezpečením a rizika.

**Útoky se zlými úmysly** zjištění deterministicky a také prostřednictvím analýzy neobvyklé chování. Úplný seznam typů známé útoky zahrnuje:

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   Forged PAC (MS14-068)
-   Zlatý lístek
-   Škodlivou replikaci
-   Vytváření výčtu adresářových služeb
-   Výčet relací SMB
-   Rekognoskace DNS
-   Vodorovné hrubou silou 
-   Svislé hrubou silou
-   Skeleton Key
-   Neobvyklé protokolu
-   Přechod na starší verzi šifrování
-   Vzdálené spuštění
-   Vytvoření škodlivý služby


Azure ATP zjištění těchto podezřelých aktivit a zobrazí informace, na portálu Azure ATP prostoru včetně zrušte zobrazení, kdo, kdy a jak. Jak je vidět, sledováním tento jednoduchý uživatelsky přívětivý řídicí panel, se zobrazí výstraha, že Azure ATP má podezření, že útoku Pass-the-Ticket došlo k pokusu o klienta 1 a 2 klientských počítačů ve vaší síti.

 ![Ukázka Azure ATP obrazovky pass-the-ticket](media/pass-the-ticket-sa.png)


Navíc rozpozná Azure ATP **problémy se zabezpečením a rizika**, včetně:

-   Slabé protokoly
-   Známá slabá místa protokolů
-   [Laterální pohyb cestu k citlivé účty](use-case-lateral-movement-path.md)

# <a name="what-threats-does-azure-atp-look-for"></a>Jaké hrozby Azure ATP Hledat?

Azure ATP zajišťuje detekci pro následující fáze pokročilých útoků: rekognoskace, zneužití přihlašovacích údajů, laterální pohyb, zvýšení úrovně oprávnění, dominance v doméně a další. Tyto detekce jsou zaměřené na zjišťování pokročilých útoků a vnitřních hrozeb ještě předtím, než mohou ve vaší organizaci způsobit škody.

Výsledkem detekce v jednotlivých fázích je několik podezřelých aktivit relevantních pro danou fázi. Každá podezřelá aktivita je v korelaci s různými charakteristikami možných útoků.
Tato fáze v řetězu událostí, kde Azure ATP aktuálně poskytuje detekce jsou vyznačené na následujícím obrázku:

![Azure ATP zaměřit se na laterální aktivity v útoku ukončit řetězec](media/attack-kill-chain-small.jpg)


Další informace najdete v tématu [práce s podezřelými aktivitami](working-with-suspicious-activities.md) a [Azure ATP podezřelou aktivitu průvodce](suspicious-activity-guide.md).

## <a name="whats-next"></a>Co dál?

-   Další informace o tom, jak Azure ATP zapadá do vaší sítě: [architektura Azure ATP](atp-architecture.md)

-   Zahájení nasazení ATP: [nainstalovat ATP](install-atp-step1.md)


## <a name="see-also"></a>Viz také
- [Nejčastější dotazy k Azure ATP](atp-technical-faq.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
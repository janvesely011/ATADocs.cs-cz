---
title: Co je Microsoft Advanced Threat Analytics (ATA)? | Microsoft ATA
description: "Popisuje řešení Microsoft Advanced Threat Analytics (ATA) a jaké druhy podezřelých aktivit může zjistit."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: c2f8d642f5ab0927448730453873a5b6271b3d2b


---

*Platí pro: Advanced Threat Analytics verze 1.7*


## Co je Advanced Threat Analytics?
Řešení ATA (Advanced Threat Analytics) je místní platforma, která chrání podnik před různými typy pokročilých cílových útoků z kyberprostoru a před vnitřními hrozbami.

## Popis fungování řešení ATA
ATA přebírá informace z různých zdrojů dat, z protokolů a událostí v síti a zkoumá chování uživatelů a entit v organizaci. Potom na základě toho vytváří profily jejich chování.
ATA může přijímat události a protokoly z následujících zdrojů:

-   Integrace se SIEM
-   Předávání událostí systému Windows (WEF)

Kromě toho ATA využívá analytický modul vlastní sítě k zachycení a analýze síťového provozu různých protokolů (například Kerberos, DNS, RPC, NTLM a dalších) pro ověřování a autorizaci a shromažďování informací. ATA tyto informace shromažďuje prostřednictvím následujícího:

-   zrcadlení portů z řadičů domény a serverů DNS do ATA Gateway,
-   nasazení ATA Lightweight Gateway (LGW) přímo na řadičích domény.

Další informace o architektuře ATA najdete v článku [Architektura ATA](/advanced-threat-analytics/plan-design/ata-architecture).

Podívejte se na úvodní video o řešení ATA.
<iframe width="560" height="315" src="https://www.youtube.com/embed/0nA9FeTRZFw" frameborder="0" allowfullscreen></iframe>

## Co ATA dělá?

Technologie ATA detekuje různé podezřelé aktivity a zaměřuje se na několik fází v řetězci internetového útoku, včetně následujícího:

-   Rekognoskace, během které útočníci shromažďují informace o konstrukci prostředí, o různých assetech a entitách a připravují si plán pro další fáze útoku.
-   Cyklus laterálního pohybu, během kterého útočník investuje čas a úsilí do rozšíření prostoru pro útoky uvnitř vaší sítě.
-   Dominance domény (trvalost), během které útočník zachycuje informace, které mu umožňují pokračovat v kampani pomocí různých sad vstupních bodů, přihlašovacích údajů a technik. 

Tyto fáze internetového útoku jsou podobné a předvídatelné bez ohledu na typ napadené společnosti nebo typ informací, o které se usiluje.
ATA hledá tří hlavní typy útoků: Škodlivé útoky, nestandardní chování a bezpečnostní problémy a rizika.

**Škodlivé útoky** se detekují deterministicky vyhledáváním úplného seznamu známých typů útoků, včetně následujících:

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   Forged PAC (MS14-068)
-   Zlatý lístek
-   Škodlivé replikace
-   Rekognoskace
-   Hrubá síla
-   Vzdálené spuštění

Úplný seznam detekcí a jejich popisu najdete v článku [Jaké podezřelé aktivity může ATA detekovat?](ata-threats.md)
ATA detekuje tyto podezřelé aktivity a zobrazí příslušné informace v konzole ATA včetně jasného zobrazení kdo, co, kdy a jak. Jak sami vidíte, při sledování tohoto jednoduchého a uživatelsky vstřícného řídicího panelu budete upozorněni, že ATA má podezření na útok typu Pass-the-Hash proti počítačům Klient 1 a 2 ve vaší síti.

 ![ukázková obrazovka ATA s útokem typu pass-the-hash](media/sample screen pth.png)

ATA detekuje **neobvyklé chování** pomocí analýzy chování a využitím strojového učení. Díky tomu odhalí sporné aktivity a neobvyklé chování uživatelů a zařízení ve vaší síti, včetně následujícího:

-   Neobvyklá přihlášení
-   Neznámé hrozby
-   Sdílení hesla
-   Laterální pohyb


Podezřelé aktivity tohoto typu můžete zobrazit na řídicím panelu ATA. V následujícím příkladu vás ATA upozorní, když uživatel získá přístup ke čtyřem počítačům, které obvykle nepoužívá, což může být důvod pro poplach.

 ![ukázková obrazovka řešení ATA s neobvyklým chováním](media/sample screen abnormal behavior.png) 

ATA také detekuje **problémy a rizika zabezpečení**, včetně následujícího:

-   Porušení vztahu důvěryhodnosti
-   Slabé protokoly
-   Známá slabá místa protokolů

Podezřelé aktivity tohoto typu můžete zobrazit na řídicím panelu ATA. V následujícím příkladu vás ATA informuje o porušení vztahu důvěryhodnosti mezi počítačem ve vaší síti a doménou.

  ![ukázková obrazovka ATA s porušeným vztahem důvěryhodnosti](media/sample screen broken trust.png)


## Co dál?

-   Další informace o zapojení řešení ATA do vaší sítě najdete v tématu [Architektura ATA](/advanced-threat-analytics/plan-design/ata-architecture).

-   Pokud chcete začít s nasazením ATA, přečtěte si téma [Instalace ATA](/advanced-threat-analytics/deploy-use/install-ata).

## Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->



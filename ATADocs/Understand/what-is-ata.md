---
title: Co je Microsoft Advanced Threat Analytics (ATA)? | Dokumentace Microsoftu
description: "Popisuje řešení Microsoft Advanced Threat Analytics (ATA) a jaké druhy podezřelých aktivit může zjistit."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 09/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: 70d66bccfda484722afa63a7f85dc8f85013f54f


---

*Platí pro: Advanced Threat Analytics verze 1.7*


# <a name="what-is-advanced-threat-analytics"></a>Co je Advanced Threat Analytics?
Řešení ATA (Advanced Threat Analytics) je místní platforma, která chrání podnik před různými typy pokročilých cílových útoků z kyberprostoru a před vnitřními hrozbami.

## <a name="how-ata-works"></a>Popis fungování řešení ATA
ATA přebírá informace z různých zdrojů dat, z protokolů a událostí v síti a zkoumá chování uživatelů a entit v organizaci. Potom na základě toho vytváří profily jejich chování.
ATA může přijímat události a protokoly z následujících zdrojů:

-   Integrace se SIEM
-   Předávání událostí systému Windows (WEF)

Kromě toho ATA využívá analytický modul vlastní sítě k zachycení a analýze síťového provozu různých protokolů (například Kerberos, DNS, RPC, NTLM a dalších) pro ověřování a autorizaci a shromažďování informací. ATA tyto informace shromažďuje prostřednictvím následujícího:

-   zrcadlení portů z řadičů domény a serverů DNS do ATA Gateway,
-   nasazení ATA Lightweight Gateway (LGW) přímo na řadičích domény.

Další informace o architektuře ATA najdete v článku [Architektura ATA](/advanced-threat-analytics/plan-design/ata-architecture).

## <a name="what-does-ata-do"></a>Co ATA dělá?

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


## <a name="whats-next"></a>Co dál?

-   Další informace o zapojení řešení ATA do vaší sítě najdete v tématu [Architektura ATA](/advanced-threat-analytics/plan-design/ata-architecture).

-   Pokud chcete začít s nasazením ATA, přečtěte si téma [Instalace ATA](/advanced-threat-analytics/deploy-use/install-ata).

## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jan17_HO1-->



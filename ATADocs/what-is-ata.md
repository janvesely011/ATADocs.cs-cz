---
title: Co je Microsoft Advanced Threat Analytics (ATA)? | Dokumentace Microsoftu
description: "Popisuje řešení Microsoft Advanced Threat Analytics (ATA) a jaké druhy podezřelých aktivit může zjistit."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/20/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: db2133e05fb7d2390f4b7e05dd219be71bf4e157
ms.sourcegitcommit: 129bee06ff89b72d21b64f9aa0d1a29f66bf9153
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*


# <a name="what-is-advanced-threat-analytics"></a>Co je Advanced Threat Analytics?
Řešení ATA (Advanced Threat Analytics) je místní platforma, která chrání podnik před různými typy pokročilých cílových útoků z kyberprostoru a před vnitřními hrozbami.

## <a name="how-ata-works"></a>Popis fungování řešení ATA

ATA využívá proprietární modul pro parsování sítě k zachycení a parsování síťového provozu přes různé protokoly (například Kerberos, DNS, RPC, NTLM a další) za účelem ověřování, autorizaci a shromažďování informací. ATA tyto informace shromažďuje prostřednictvím:

-   zrcadlení portů z řadičů domény a serverů DNS na ATA Gateway a/nebo
-   nasazení ATA Lightweight Gateway (LGW) přímo na řadičích domény.

ATA přebírá informace z různých zdrojů dat, jako jsou protokoly a události v síti, a poznává tak chování uživatelů a jiných entit v organizaci. Potom na základě toho vytváří profily jejich chování.
ATA může přijímat události a protokoly z následujících zdrojů:

-   Integrace se SIEM
-   Předávání událostí systému Windows (WEF)
-   Přímo z protokolu událostí Windows (komponenta Lightweight Gateway)


Další informace o architektuře ATA najdete v článku [Architektura ATA](ata-architecture.md).

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
ATA detekuje tyto podezřelé aktivity a zobrazí příslušné informace v konzole ATA včetně jasného zobrazení kdo, co, kdy a jak. Jak vidíte, při sledování tohoto jednoduchého a uživatelsky vstřícného řídicího panelu budete upozorněni, že ATA má podezření na útok typu Pass-the-Ticket proti počítačům Klient 1 a 2 ve vaší síti.

 ![Ukázková obrazovka ATA s útokem typu Pass-the-Ticket](media/pass_the_ticket_sa.png)

ATA detekuje **neobvyklé chování** pomocí analýzy chování a využitím strojového učení. Díky tomu odhalí sporné aktivity a neobvyklé chování uživatelů a zařízení ve vaší síti, včetně následujícího:

-   Neobvyklá přihlášení
-   Neznámé hrozby
-   Sdílení hesla
-   Laterální pohyb
-   Úprava citlivých skupin


Podezřelé aktivity tohoto typu můžete zobrazit na řídicím panelu ATA. V následujícím příkladu vás ATA upozorní, když uživatel získá přístup ke čtyřem počítačům, které obvykle nepoužívá, což může být důvod pro poplach.

 ![ukázková obrazovka řešení ATA s neobvyklým chováním](media/abnormal-behavior-sa.png) 

ATA také detekuje **problémy a rizika zabezpečení**, včetně následujícího:

-   Porušení vztahu důvěryhodnosti
-   Slabé protokoly
-   Známá slabá místa protokolů

Podezřelé aktivity tohoto typu můžete zobrazit na řídicím panelu ATA. V následujícím příkladu vás ATA informuje o porušení vztahu důvěryhodnosti mezi počítačem ve vaší síti a doménou.

  ![ukázková obrazovka ATA s porušeným vztahem důvěryhodnosti](media/broken-trust-sa.png)


## <a name="known-issues"></a>Známé problémy

- Pokud aktualizujete na ATA 1.7 a hned potom na ATA 1.8, aniž nejprve aktualizujete komponenty ATA Gateway, nebudete moct migrovat na ATA 1.8. Před aktualizací komponenty ATA Center na verzi 1.8 je nezbytné nejprve aktualizovat všechny brány na verzi 1.7.1 nebo 1.7.2.

- Pokud vyberete možnost provedení úplné migrace, může to v závislosti na velikosti databáze trvat velmi dlouho. Při výběru možností migrace se zobrazuje odhadovaný čas. Než se rozhodnete, kterou možnost vyberete, věnujte prosím tomuto údaji pozornost. 


## <a name="whats-next"></a>Co dál?

-   Další informace o zapojení řešení ATA do vaší sítě najdete v tématu [Architektura ATA](ata-architecture.md).

-   Pokud chcete začít s nasazením ATA, přečtěte si téma [Instalace ATA](install-ata-step1.md).

## <a name="related-videos"></a>Související videa
- [Připojení k zabezpečení komunitě](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Viz také
[Playbook podezřelé aktivity ATA](http://aka.ms/ataplaybook)
[podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

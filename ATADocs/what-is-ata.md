---
title: Co je Microsoft Advanced Threat Analytics (ATA)? | Dokumenty Microsoft
description: Popisuje řešení Microsoft Advanced Threat Analytics (ATA) a jaké druhy podezřelých aktivit může zjistit.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/24/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ab2b6fa569f0c639b63ceb0317ecf0ae7a53411d
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2019
ms.locfileid: "54840909"
---
# <a name="what-is-advanced-threat-analytics"></a>Co je Advanced Threat Analytics?

*Platí pro: Advanced Threat Analytics verze 1.9*

Řešení ATA (Advanced Threat Analytics) je místní platforma, která chrání podnik před různými typy pokročilých cílových útoků z kyberprostoru a před vnitřními hrozbami.

## <a name="how-ata-works"></a>Popis fungování řešení ATA

ATA využívá speciální síťový parsovací modul k zachycení a parsování síťového provozu různých protokolů (například Kerberos, DNS, RPC, NTLM a další) pro ověřování, autorizaci a shromažďování informací. ATA tyto informace shromažďuje prostřednictvím následujícího:

-   zrcadlení portů z řadičů domény a serverů DNS na ATA Gateway a/nebo
-   nasazení ATA Lightweight Gateway (LGW) přímo na řadičích domény.

ATA přebírá informace z různých zdrojů dat, jako jsou protokoly a události v síti, další chování uživatelů a dalších entit v organizaci a o nich profil chování sestavení.
ATA může přijímat události a protokoly z následujících zdrojů:

-   Integrace se SIEM
-   Předávání událostí systému Windows (WEF)
-   Přímo z protokolu událostí Windows (komponenta Lightweight Gateway)


Další informace o architektuře ATA najdete v tématu [architektura ATA](ata-architecture.md).

## <a name="what-does-ata-do"></a>Co ATA dělá?

Technologie ATA detekuje různé podezřelé aktivity a zaměřuje se na několik fází v řetězci internetového útoku, včetně následujícího:

-   Rekognoskace, během které útočníci shromáždit informace o tom, jak je sestavená prostředí, jaké různé formáty jsou a entit, které neexistuje. Obvykle se jedná, kde útočníci sestavit plány pro své další fáze útoku.
-   Cyklus laterálního pohybu, během kterého útočník investuje čas a úsilí do rozšíření prostoru pro útoky uvnitř vaší sítě.
-   Dominance domény (trvalost), během které útočník zachycuje informace, které umožňuje pokračovat v kampani pomocí různých sad vstupních bodů, přihlašovacích údajů a technik. 

Tyto fáze internetového útoku jsou podobné a předvídatelné bez ohledu na typ napadené společnosti nebo typ informací, o které se usiluje.
ATA hledá tří hlavní typy útoků: Útoky se zlými úmysly, neobvyklé chování a problémy se zabezpečením a rizika.

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

Úplný seznam detekcí a jejich popis najdete v části [co podezřelé aktivity může ATA detekovat?](ata-threats.md). 

ATA detekuje tyto podezřelé aktivity a zobrazí příslušné informace v konzole ATA včetně jasného zobrazení kdo, co, kdy a jak. Jak vidíte, při sledování tohoto jednoduchého a uživatelsky vstřícného řídicího panelu budete upozorněni, že ATA má podezření, že došlo k pokusu o útok typu Pass-the-Ticket na počítačům klient 1 a 2 ve vaší síti.

 ![Ukázková obrazovka ATA s útokem typu Pass-the-Ticket](media/pass_the_ticket_sa.png)

ATA detekuje **neobvyklé chování** pomocí analýzy chování a využitím strojového učení. Díky tomu odhalí sporné aktivity a neobvyklé chování uživatelů a zařízení ve vaší síti, včetně následujícího:

-   Neobvyklá přihlášení
-   Neznámé hrozby
-   Sdílení hesla
-   Laterální pohyb
-   Úprava citlivých skupin


Podezřelé aktivity tohoto typu můžete zobrazit na řídicím panelu ATA. V následujícím příkladu ATA vás upozorní, když uživatel přistupuje k čtyři počítače, které se obvykle nepoužívají tímto uživatelem, který může být důvod pro poplach.

 ![ukázková obrazovka řešení ATA s neobvyklým chováním](media/abnormal-behavior-sa.png) 

ATA také detekuje **problémy a rizika zabezpečení**, včetně následujícího:

-   Porušení vztahu důvěryhodnosti
-   Slabé protokoly
-   Známá slabá místa protokolů

Podezřelé aktivity tohoto typu můžete zobrazit na řídicím panelu ATA. V následujícím příkladu vás ATA informuje o porušení vztahu důvěryhodnosti mezi počítačem ve vaší síti a doménou.

  ![ukázková obrazovka ATA s porušeným vztahem důvěryhodnosti](media/broken-trust-sa.png)


## <a name="known-issues"></a>Známé problémy

- Při aktualizaci na ATA 1.7 a hned potom na ATA 1.8, aniž nejprve aktualizujete komponenty ATA Gateway, nelze migrovat na ATA 1.8. Před aktualizací komponenty ATA Center na verzi 1.8 je nezbytné nejprve aktualizovat všechny brány na verzi 1.7.1 nebo 1.7.2.

- Pokud vyberete možnost provedení úplné migrace, může to v závislosti na velikosti databáze trvat velmi dlouho. Při výběru možností migrace se zobrazí odhadovaná doba – Poznačte si to předtím, než se rozhodnete, kterou možnost vyberete. 


## <a name="whats-next"></a>Co dále?

-   Další informace o zapojení řešení ATA do vaší sítě: [Architektura ATA](ata-architecture.md)

-   Abyste mohli začít nasazením ATA: [Instalace ATA](install-ata-step1.md)

## <a name="related-videos"></a>Související videa
- [Připojení k zabezpečení komunitě](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)


## <a name="see-also"></a>Viz také
[Playbook podezřelých aktivit ATA](http://aka.ms/ataplaybook)
[podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

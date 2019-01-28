---
title: Monitorování řadičů domény a nainstalované senzory nainstalován na řadiče domény pomocí rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje monitorování služby Azure ATP senzory a pokrytí ze senzorů pomocí služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/27/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 92decce8-b3ae-4d32-8407-a95314a66863
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6dd6574250819bd8c60da00c7f1547bb34845f75
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085544"
---
# <a name="monitoring-your-domain-controller-coverage"></a>Monitorování pokrytí řadiče domény

Jakmile vaše první senzor ochrany ATP v programu Azure je nainstalovaný a nakonfigurovaný na všech řadičích domény v síti, ochrany ATP v programu Azure zahájí monitorování vašeho prostředí pro řadiče domény. 

Během instalace doporučujeme vybrat alespoň jeden řadič domény senzoru služby Azure ATP jako kandidát na synchronizátora domény na doménu. Jedna z úloh senzor synchronizátor domény je zajistit této domény, které řadiče aktivně se vyhledávají pro tento konkrétní senzoru. Řadiče domény můžete přepnout do a z stav Release candidate synchronizátor domény po počáteční konfiguraci. Zobrazit [Konfigurace senzoru služby Azure ATP](install-atp-step5.md) Další informace o konfiguraci Azure ze senzorů a nastavíte ho jako **kandidát na synchronizátora domény**. 

Jakmile senzoru služby Azure ATP nainstalovaná a nakonfigurovaná na řadiči domény v síti, senzor komunikuje se službou ochrana ATP v programu Azure na základě konstantní odesílání informací o stavu, stavu a verze senzor a shromažďují události služby Active Directory a změny.  

### <a name="domain-controller-status"></a>Stav řadiče domény

Ochrana ATP v programu Azure nepřetržitě monitoruje prostředí pro řadiče domény nemonitorované prostředí a sestavy na nich vám pomůžou při správě úplné pokrytí vašeho prostředí. 

1. Pokud chcete zkontrolovat stav vaší zjištěné monitorované a nemonitorované řadiče domény a jejich stav, přejděte na **konfigurace** oblast služby Azure ATP portálu v části **systému** vyberte **Senzorů**.
   
     ![Monitorování stavu senzoru s Azure ATP](media/atp-sensors-status-monitoring.png)

2. Řadiče domény aktuálně monitorované a nemonitorované se zobrazují v horní části obrazovky. Pokud chcete stáhnout podrobnosti o monitorování stavu řadičů domény, vyberte **podrobnosti o stahování**. 

Stažení aplikace Excel pokrytí řadič domény obsahuje následující informace pro všechny zjištěné řadiče domény ve vaší organizaci:

|Titul|Popis|
|----|----|
|Název hostitele|Název počítače|
|Název domény|Název domény|
|Monitorovat|Azure ochrany ATP v programu Sledování stavu|
|typ snímače|Azure ochrany ATP v programu nebo samostatného senzoru služby Azure ATP|
|Organizační jednotka|Umístění v rámci služby Active Directory |
|Verze operačního systému| Verze operačního systému se zjistil|
|IP adresa|Zjištěná IP adresa| 


> [!NOTE]
> Azure stránky konfigurace portálu ochrany ATP v programu můžete změnit jenom správci služby Azure ATP.


## <a name="see-also"></a>Viz také

- [Architektura služby Azure ATP](atp-architecture.md)
- [Konfigurace ochrany ATP v programu Azure senzorů](install-atp-step5.md)
- [Podpora více doménovými strukturami](atp-multi-forest.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
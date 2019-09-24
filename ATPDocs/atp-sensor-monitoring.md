---
title: Monitorování řadičů domény a nainstalovaných senzorů nainstalovaných na řadičích domény pomocí rozšířené ochrany před internetovými útoky Azure | Microsoft Docs
description: Popisuje, jak monitorovat senzory ATP Azure a pokrytí senzorů pomocí Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 92decce8-b3ae-4d32-8407-a95314a66863
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6970908b95fe31ecd24b4cdc1005180e39495913
ms.sourcegitcommit: 15f882cf45776877fdaca8367a7a0fe7f06a7917
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/23/2019
ms.locfileid: "71185599"
---
# <a name="monitoring-your-domain-controller-coverage"></a>Monitorování pokrytí řadiče domény

Po instalaci a konfiguraci prvního senzoru ATP Azure na jakémkoli řadiči domény ve vaší síti začne Azure ATP monitorovat vaše prostředí pro řadiče domény. 

Během instalace se doporučuje vybrat aspoň jeden řadič domény se senzorem Azure ATP jako kandidáta na synchronizátor domény v každé doméně. Jednou z úloh senzoru synchronizátoru domény je zajistit, aby řadiče domény byly aktivně vyhledány konkrétním senzorem. Řadiče domény se dají po počáteční konfiguraci přepnout do stavu kandidáta na synchronizátor domény a. Pokud jako kandidáta na synchronizátor domény není vybraný žádný řadič domény, dojde jenom k pasivnímu monitorování síťové aktivity na řadičích domény. Další informace o konfiguraci snímače Azure a jeho nastavení jako **kandidáta na synchronizátor domény**najdete v tématu [Konfigurace senzorů Azure ATP](install-atp-step5.md) . 

Po instalaci a konfiguraci senzoru ATP Azure na řadiči domény ve vaší síti senzor komunikuje se službou Azure ATP na konstantním základu odesílání stavu senzorů, stavu a informací o verzi a shromažďování událostí služby Active Directory a provedeny.  

### <a name="domain-controller-status"></a>Stav řadiče domény

Azure ATP nepřetržitě monitoruje vaše prostředí pro nemonitorované řadiče domény zavedené do vašeho prostředí a oznamuje jim, které vám pomůžou se správou plného pokrytí vašeho prostředí. 

1. Pokud chcete zjistit stav zjištěných monitorovaných a nemonitorovaných řadičů domény a jejich stav, vraťte se do oblasti **Konfigurace** na portálu Azure ATP v části **systém** vyberte **senzory**.
   
    ![Monitorování stavu senzoru ATP Azure](media/atp-sensors-status-monitoring.png)

2. V horní části obrazovky se zobrazí aktuálně monitorované a nemonitorované řadiče domény. Chcete-li stáhnout podrobnosti o stavu monitorování řadičů domény, vyberte možnost **Stáhnout podrobnosti**. 

Stažení v aplikaci Excel v pokrytí řadiče domény poskytuje následující informace pro všechny zjištěné řadiče domény ve vaší organizaci:

|Titul|Popis|
|----|----|
|Název hostitele|Název počítače|
|Název domény|Název domény|
|Monitor|Stav monitorování ATP Azure|
|Typ senzoru|Senzor Azure ATP nebo samostatný senzor Azure ATP|
|Organizační jednotka|Umístění v rámci služby Active Directory |
|Verze operačního systému| Zjistila se verze operačního systému.|
|IP adresa|Zjištěná IP adresa| 

### <a name="search-domain-controllers"></a>Hledat řadiče domény

Správa loďstva senzorů a řadičů domény může být náročná. Pro snazší vyhledání a identifikaci řadičů domény se dají prohledávat pomocí funkce hledání v seznamu senzorů Azure ATP. 

1. Pokud chcete vyhledat řadiče domény, v části **systém** klikněte na oblast **Konfigurace** portálu Azure ATP a vyberte **senzory**.
1. Vyberte možnost filtr ve sloupci **řadič domény** v seznamu tabulka řadiče domény. 
1. Zadejte název, který chcete vyhledat. V poli hledání se aktuálně nepodporují zástupné znaky. 

    ![Řadič domény vyhledávání Azure ATP](media/search-sensor.png)

> [!NOTE]
> Konfigurační stránky portálu Azure ATP můžou upravovat jenom správci ATP Azure.


## <a name="see-also"></a>Viz také

- [Architektura ATP Azure](atp-architecture.md)
- [Konfigurace senzorů Azure ATP](install-atp-step5.md)
- [Podpora více doménových struktur](atp-multi-forest.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

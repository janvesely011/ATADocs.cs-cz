---
title: Plánování nasazení Advanced Threat Analytics | Dokumentace Microsoftu
description: Pomůže vám naplánovat nasazení a určit, kolik serverů ATA bude potřeba k podpoře vaší sítě.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 08/05/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 1b5b24ff-0df8-4660-b4f8-64d68cc72f65
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3f5e493993acfb6bbb440691f11053d46bf5e1ba
ms.sourcegitcommit: 8df26fb312472b8df1da70e581517223d26de8c2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/05/2019
ms.locfileid: "68781825"
---
# <a name="ata-capacity-planning"></a>Plánování kapacity ATA

*Platí pro: Advanced Threat Analytics verze 1,9*

Tento článek vám pomůže určit, kolik serverů ATA je potřeba k monitorování vaší sítě. Pomůže vám zjistit, kolik komponent ATA Gateway a/nebo ATA Lightweight Gateway potřebujete, a kapacitu serveru pro komponenty ATA Center a komponenty ATA Gateway.

> [!NOTE] 
> ATA Center se dá nasadit na libovolného dodavatele IaaS, pokud jsou splněné požadavky na výkon popsané v tomto článku.

## <a name="using-the-sizing-tool"></a>Použití nástroje pro změnu velikosti
Doporučený a nejjednodušší způsob, jak určit kapacitu pro vaše nasazení ATA, je použití [nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool). Spusťte nástroj pro změnu velikosti ATA a z výsledků v excelovém souboru pomocí následujících polí určete potřebnou kapacitu ATA:

- PROCESOR a paměť pro ATA Center: Porovnává pole počet **zaneprázdněných paketů/s** v souboru výsledků tabulky ATA Center do pole **pakety za sekundu** v [tabulce ATA Center](#ata-center-sizing).

- Úložiště ATA Center: Porovnává pole počet **paketů/s** v souboru výsledků tabulky ATA Center s polem **pakety za sekundu** v [tabulce ATA Center](#ata-center-sizing).
- ATA Gateway: V závislosti na [zvoleném typu brány](#choosing-the-right-gateway-type-for-your-deployment)se porovnává pole počet **zaneprázdněných paketů/s** v tabulce ATA Gateway v souboru výsledků až do pole **pakety za sekundu** v [tabulce ATA Gateway](#ata-gateway-sizing) nebo v [tabulce ATA Lightweight Gateway](#ata-lightweight-gateway-sizing).


![Ukázkový nástroj plánování kapacity](media/capacity-tool.png)


> [!NOTE]
> Vzhledem k tomu, že různá prostředí se liší a mají více speciálních a neočekávaných vlastností síťového provozu, po počátečním nasazení ATA a spuštění nástroje pro změnu velikosti může být nutné upravit a vyladit nasazení pro kapacitu.


Pokud z nějakého důvodu nemůžete použít nástroj pro změnu velikosti ATA, ručně shromažďujte údaje čítače paketů za sekundu ze všech řadičů domény po dobu 24 hodin s nízkým intervalem sběru hodnot (přibližně 5 sekund). Pak u každého řadiče domény musíte vypočítat denní průměr a průměr za nejvytíženější období (15 minut).
Následující části uvádějí pokyny, jak shromáždit čítač paketů za sekundu z jednoho řadiče domény.


> [!NOTE]
> Vzhledem k tomu, že různá prostředí se liší a mají více speciálních a neočekávaných vlastností síťového provozu, po počátečním nasazení ATA a spuštění nástroje pro změnu velikosti může být nutné upravit a vyladit nasazení pro kapacitu.


### <a name="ata-center-sizing"></a>Nastavení velikosti ATA Center
Pro vypracování analýzy chování uživatelů vyžaduje ATA Center data za nejméně 30 dnů.
 

|Paketů za sekundu ze všech řadičů domény|Procesor (jádra&#42;)|Paměť (GB)|Úložiště databáze za den (GB)|Úložiště databáze za měsíc (GB)|IOPS&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1 000|2|32|0.3|9|30 (100)
|40,000|4|48|12|360|500 (750)
|200 000|8|64|60|1 800|1 000 (1 500)
|400 000|12|96|120|3 600|2 000 (2 500)
|750 000|24|112|225|6 750|2 500 (3 000)
|1 000 000|40|128|300|9 000|4 000 (5 000)

&#42;To zahrnuje fyzická jádra, ne jádra typu Hyper.

&#42;&#42;Průměrné počty (počty ve špičce)
> [!NOTE]
> - ATA Center dokáže zpracovat agregované maximum 1 milion paketů za sekundu ze všech monitorovaných řadičů domény. V některých prostředích může stejné ATA Center zpracovávat celkový provoz, který je vyšší než 1M. Pokud potřebujete s takovými prostředími pomoct, obraťte se na adresu askcesec@microsoft.com.
> - Pokud velikost volného místa dosáhne minimální hodnoty buď 20%, nebo 200 GB, nejstarší kolekce dat se odstraní. Pokud není možné úspěšně omezit shromažďování dat na tuto úroveň, bude zaznamenána výstraha.  ATA bude dál fungovat, dokud nebude dosaženo prahové hodnoty 5% nebo 50 GB volného místa.  V tomto okamžiku ATA zastaví naplnění databáze a vydá se další výstraha.
> - ATA Center je možné nasadit na libovolného dodavatele IaaS, pokud jsou splněné požadavky na výkon popsané v tomto článku.
> - Latence úložiště pro čtení a zápisu aktivit musí být menší než 10 ms.
> - Poměr mezi čtením a zápisem aktivit je přibližně 1:3 při méně než 100 000 paketů za sekundu a 1:6 při více než 100 000 paketů za sekundu.
> - Když centrum spouštíte jako virtuální počítač (VM), vyžaduje to, aby se k VIRTUÁLNÍmu počítači přidělila veškerá paměť. Další informace o spuštění ATA Center jako virtuálního počítače najdete v tématu [požadavky na ATA Center](https://docs.microsoft.com/advanced-threat-analytics/ata-prerequisites#dynamic-memory) .
> - K zajištění optimálního výkonu nastavte **možnost napájení** pro ATA Center na hodnotu **Vysoký výkon**.<br>
> - Při práci na fyzickém serveru databáze ATA vyžaduje, abyste v systému BIOS **zakázali** neuniformní přístup k paměti (NUMA). Ve vašem systému se NUMA může označovat také jako prokládání uzlů. V takovém případě bude potřeba prokládání uzlů **povolit**, abyste NUMA zakázali. Další informace najdete v dokumentaci k systému BIOS. Tento postup není relevantní, pokud ATA Center běží na virtuálním serveru.


## <a name="choosing-the-right-gateway-type-for-your-deployment"></a>Výběr vhodného typu brány pro vaše nasazení
V nasazení ATA se podporuje libovolná kombinace typů ATA Gateway:

- Jen komponenty ATA Gateway
- Jen komponenty ATA Lightweight Gateway
- Kombinace obojího

Při určování typu nasazení brány vezměte do úvahy následující výhody:

|Typ brány|Výhody|Náklady|Topologie nasazení|Použití řadiče domény|
|----|----|----|----|-----|
|ATA Gateway|Nasazení mimo IP síť znesnadňuje útočníkům rozpoznání přítomnosti ATA.|Vyšší|Instaluje se ve spojení s řadičem domény (mimo IP síť).|Podporuje až 50 000 paketů za sekundu.|
|ATA Lightweight Gateway|Nevyžaduje vyhrazený server a konfiguraci zrcadlení portů.|Nižší|Instaluje se na řadiči domény.|Podporuje až 10 000 paketů za sekundu.|

Dál jsou uvedené příklady situací, kdy by řadiče domény měly být pokryté komponentami ATA Lightweight Gateway:


- Pobočky

- Virtuální řadiče domény nasazené v cloudu (IaaS)


Dál jsou uvedené příklady situací, kdy by řadiče domény měly být pokryté komponentami ATA Gateway:


- Datová centra ústředí (řadiče domén s více než 10 000 pakety za sekundu)


### <a name="ata-lightweight-gateway-sizing"></a>Velikosti pro ATA Lightweight Gateway

ATA Lightweight Gateway může podporovat monitorování jednoho řadiče domény na základě objemu síťového provozu, který tento řadič generuje. 


|Pakety za sekundu&#42;|Procesor (jádra&#42;&#42;)|Paměť (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1 000|2|6|
|5,000|6|16|
    |10 000|10|24|

&#42;Celkový počet paketů za sekundu na řadiči domény, který sleduje tato konkrétní komponenta ATA Lightweight Gateway.

&#42;&#42;Celkový počet jader bez hyperthreadingu, která má tento řadič domény nainstalovaná.<br>Přestože je hyperthreading pro ATA Lightweight Gateway přijatelný, při plánování kapacity byste měli počítat skutečná jádra, nikoli jádra s hyperthreadingem.

&#42;&#42;&#42;Celkový objem paměti, kterou má tento řadič domény nainstalovanou.

> [!NOTE]   
> -   Pokud řadič domény nemá prostředky, které ATA Lightweight Gateway vyžaduje, výkon řadiče domény to neovlivní, ale ATA Lightweight Gateway nemusí fungovat podle očekávání.
> -   Když centrum spouštíte jako virtuální počítač (VM), vyžaduje to, aby se k VIRTUÁLNÍmu počítači přidělila veškerá paměť. Další informace o spuštění ATA Center jako virtuálního počítače najdete v tématu [požadavky na ATA Center](https://docs.microsoft.com/advanced-threat-analytics/ata-prerequisites#dynamic-memory).)
> -   K zajištění optimálního výkonu nastavte **možnost napájení** pro ATA Lightweight Gateway na hodnotu **Vysoký výkon**.
> -   Vyžaduje se minimálně 5 GB místa a doporučuje se 10 GB, včetně místa potřebného pro binární soubory ATA, [protokoly ATA](troubleshooting-ata-using-logs.md)a [protokoly výkonu](troubleshooting-ata-using-perf-counters.md).


### <a name="ata-gateway-sizing"></a>Nastavení velikosti ATA Gateway

Při rozhodování o tom, kolik komponent ATA Gateway nasadíte, zvažte následující problémy.

-   **Doménové struktury a domény služby Active Directory**<br>
    ATA může monitorovat provoz z několika domén z jedné doménové struktury služby Active Directory. Monitorování několika doménových struktur služby Active Directory vyžaduje samostatná nasazení řešení ATA. Nekonfigurujte jedno nasazení ATA pro monitorování síťového provozu řadičů domény patřících do různých doménových struktur.

-   **Zrcadlení portů**<br>
Aspekty zrcadlení portů můžou vyžadovat, abyste pro datové centrum nebo pobočku nasadili několik komponent ATA Gateway.

-   **Kapacita**<br>
    ATA Gateway může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů monitorovaných řadičů domény. 
<br>



|Pakety za sekundu&#42;|Procesor (jádra&#42;&#42;)|Paměť (GB)|
|---------------------------|-------------------------|---------------|
|1 000|1|6|
|5,000|2|10|
|10,000|3|12|
|20,000|6|24|
|50 000|16|48|

&#42;Celkový průměrný počet paketů za sekundu ze všech řadičů domény, které sleduje tato konkrétní ATA Gateway za nejvytíženější hodinu.

&#42;Celkové množství provozu řadiče domény na zrcadleném portu nesmí překročit kapacitu síťové karty pro zachytávání na ATA Gateway.

&#42;&#42;Technologie Hyper-Threading musí být zakázaná.

> [!NOTE] 
> -   Když centrum spouštíte jako virtuální počítač (VM), vyžaduje to, aby se k VIRTUÁLNÍmu počítači přidělila veškerá paměť. Další informace o spuštění ATA Center jako virtuálního počítače najdete v tématu [požadavky na ATA Center](https://docs.microsoft.com/advanced-threat-analytics/ata-prerequisites#dynamic-memory) .
> -   K zajištění optimálního výkonu nastavte **možnost napájení** pro ATA Gateway na hodnotu **Vysoký výkon**.
> -   Vyžaduje se minimálně 5 GB místa a doporučuje se 10 GB, včetně místa potřebného pro binární soubory ATA, [protokoly ATA](troubleshooting-ata-using-logs.md)a [protokoly výkonu](troubleshooting-ata-using-perf-counters.md).



## <a name="related-videos"></a>Související videa
- [Výběr správného typu ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Nástroj pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Požadavky ATA](ata-prerequisites.md)
- [Architektura ATA](ata-architecture.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

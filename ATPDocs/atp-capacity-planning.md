---
title: Plánování nasazení rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Pomůže vám naplánovat nasazení a rozhodnout, kolik serverů ochrany ATP v programu Azure bude potřeba k podpoře vaší sítě.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.service: azure-advanced-threat-protection
ms.prod: ''
ms.assetid: da0ee438-35f8-4097-b3a1-1354ad59eb32
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 51ce0ca62d29c58475f8f426ee715515cf106193
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/23/2019
ms.locfileid: "54459086"
---
# <a name="azure-atp-capacity-planning"></a>Plánování kapacity v Azure ATP
Tento článek pomůže určit, kolik ochrany ATP v programu Azure senzory a samostatné senzory, které potřebujete.

## <a name="using-the-sizing-tool"></a>Použití nástroje pro změnu velikosti
Doporučený a nejjednodušší způsob, jak určit kapacitu pro vaše nasazení služby Azure ATP, je použít [nástroje pro změnu velikosti ochrany ATP v programu Azure](http://aka.ms/aatpsizingtool). Spusťte nástroj pro změnu velikosti ochrany ATP v programu Azure a z výsledků v Excelovém souboru, použijte následující pole k určení paměti a procesoru, který používá senzor:

> [!NOTE] 
> Nástroj pro změnu velikosti má dvě tabulky – jeden pro ochrany ATP v programu Azure a jeden pro ATA. Ujistěte se, že používáte správné list.

- Senzor ochrany ATP v programu Azure: Shoda **zaneprázdněný Packets/sec** v tabulce senzoru služby Azure ATP v souboru výsledků s **PAKETŮ za SEKUNDU** pole [tabulky senzoru služby Azure ATP](#azure-atp-standalone-sensor-sizing) nebo [Ochrany ATP v programu azure samostatný senzor tabulky](#azure-atp-sensor-sizing), v závislosti na [zvoleného typu senzor](#choosing-the-right-sensor-type-for-your-deployment).


![Ukázkový nástroj plánování kapacity](media/capacity-tool.png)


Pokud z nějakého důvodu nemůžete použít nástroj pro změnu velikosti ochrany ATP v programu Azure, ručně shromažďujte údaje čítače paketů za sekundu ze všech řadičů domény po dobu 24 hodin s malým intervalem sběru hodnot (přibližně 5 sekund). U každého řadiče domény, musí pak, vypočítat denní průměr a průměr za nejvytíženější období (15 minut).
Následující části uvádějí pokyny, jak shromáždit čítač paketů za sekundu z jednoho řadiče domény.

## Výběr správné senzor typu nasazení<a name="choosing-the-right-sensor-type-for-your-deployment"></a>
V nasazení služby Azure ATP libovolnou kombinaci typů senzoru služby Azure ATP podporované:

- Jenom ochrana ATP v programu Azure senzorů
- Pouze senzorů samostatné služby Azure ATP
- Kombinace obojího

Při určování typu nasazení ze senzorů, vezměte v úvahu následující výhody:

|typ snímače|Výhody|Náklady|Topologie nasazení|Použití řadiče domény|
|----|----|----|----|-----|
|Senzoru služby Azure ATP|Nevyžaduje vyhrazený server a konfiguraci zrcadlení portů.|Nižší|Instaluje se na řadiči domény.|Podporuje až 100 000 paketů za sekundu|
|Azure ATP samostatný senzor|Nasazení mimo IP síť znesnadňuje útočníkům že ochrany ATP v programu Azure je k dispozici|Vyšší|Instaluje se ve spojení s řadičem domény (mimo IP síť).|Podporuje až 100 000 paketů za sekundu|


Zvažte následující skutečnosti při rozhodování o tom, kolik senzorů samostatné ochrany ATP v programu Azure k nasazení.

-   **Doménové struktury a domény služby Active Directory**<br>
    Ochrana ATP v programu Azure může monitorovat provoz z několika domén v rámci více doménových struktur služby Active Directory pro každou instanci, kterou jste vytvořili. 

-   **Zrcadlení portů**<br>
    Úvahy o zrcadlení portů může vyžadovat nasazení více senzorů samostatné ochrany ATP v programu Azure na datové centrum nebo pobočku Web.

-   **Kapacita**<br>
    Samostatný senzor ochrany ATP v programu Azure může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů monitorovaných řadičů domény. 


## Azure senzor ochrany ATP v programu a velikosti samostatný senzor <a name="sizing"></a>

Senzoru služby Azure ATP může podporovat monitorování jednoho řadiče domény na základě objemu síťového provozu, který tento řadič generuje. V následující tabulce je odhad, finální částku, která analyzuje senzor je závislá na dobu provozu a distribuci provozu. 
> [!NOTE]
> Následující kapacitu procesoru a paměti odkazuje na senzoru vlastní spotřeba – ne kapacity řadiče domény.

|Paketů za sekundu *|Procesor (jádra)|Paměť (GB)|
|----|----|-----|
|0-1k|0.25|2.50|
|1k-5k|0.75|6.00|
|5-10 tis.|1.00|6.50|
|10k-20k|2.00|9.00|
|20 – 50 tis.|3.50|9.50|
|50k-75k |3.50|9.50|
|75 100 tis.|3.50 |9.50|

> [!NOTE]
> - Celkový počet jader, která bude používat služba sensor.<br>Doporučuje se, že nechcete pracovat jádra typu hyper.
> - Celkové množství paměti, která bude používat služba sensor.
> -   Pokud řadič domény nemá prostředky, které senzoru služby Azure ATP vyžaduje, výkon řadiče domény nemá vliv, ale senzoru služby Azure ATP nemusí fungovat podle očekávání.
> -   Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.
> -   Pro zajištění optimálního výkonu nastavte **možnost vypnutí** senzoru služby Azure ATP k **vysoký výkon**.
> -   Je vyžadováno nejméně 2 jádra a 6 GB místa a doporučuje 10 GB včetně místa potřebného pro binární soubory ochrany ATP v programu Azure a protokoly.


## <a name="domain-controller-traffic-estimation"></a>Odhad provozu řadiče domény

Existují různé nástroje, které můžete použít ke zjištění průměrného počtu paketů za sekundu vašich řadičů domény. Pokud nemáte žádné nástroje, které sledují tento čítač, můžete k získání požadovaných informací použít nástroj Sledování výkonu.

Pokud chcete určit počet paketů za sekundu, proveďte na každém řadiči domény následující postup:

1.  Otevřete nástroj Sledování výkonu.

    ![Obrázek nástroje Sledování výkonu](media/atp-traffic-estimation-1.png)

2.  Rozbalte položku **Sady kolekcí dat**.

    ![Obrázek sad kolekcí dat](media/atp-traffic-estimation-2.png)

3.  Klikněte pravým tlačítkem na **Definované uživatelem** a vyberte **Nová položka** &gt; **Sada kolekcí dat**.

    ![Obrázek nové sady kolekcí dat](media/atp-traffic-estimation-3.png)

4.  Zadejte název pro sadu kolekcí a vyberte **Vytvořit ručně (Upřesnit)**.

5.  V části **Jaký typ dat chcete zahrnout?** vyberte **Protokoly vytváření dat a Čítač výkonu**.

    ![Obrázek typu dat pro novou sadu kolekcí dat](media/atp-traffic-estimation-5.png)

6.  V části **Které čítače výkonu chcete protokolovat?** klikněte na **Přidat**.

7.  Rozbalte položku **Síťový adaptér**, vyberte **Pakety/s** a vyberte vhodnou instanci. Pokud si nejste jisti, můžete vybrat **&lt;Všechny instance&gt;** a kliknout na **Přidat** a **OK**.

    > [!NOTE]
    > Pokud chcete tuto operaci provést na příkazovém řádku, spuštěním příkazu `ipconfig /all` zobrazte název adaptéru a konfiguraci.

    ![Obrázek přidání čítačů výkonu](media/atp-traffic-estimation-7.png)

8.  Změnit **interval vzorkování** k **pět sekund**.

9. Nastavte umístění, kam chcete data uložit.

10. V části **vytvořit sadu kolekcí dat**vyberte **spustit tuto sadu kolekcí dat**a klikněte na tlačítko **Dokončit**.

    Nyní byste měli vidět vytvořenou sadu kolekcí dat se zeleným trojúhelníkem, který označuje, že je funkční.

11. Po 24 hodinách sadu kolekcí dat zastavte kliknutím pravým tlačítkem na sadu kolekcí dat a výběrem **Zastavit**.

    ![Obrázek zastavení sady kolekcí dat](media/atp-traffic-estimation-12.png)

12. V Průzkumníku souborů přejděte do složky, kam byl uložen soubor .blg, a dvojím kliknutím ho otevřete v nástroji Sledování výkonu.

13. Vyberte čítač Pakety/s a poznamenejte si průměrnou a maximální hodnotu.

    ![Obrázek čítače Pakety/s](media/atp-traffic-estimation-14.png)



## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Architektura služby Azure ATP](atp-architecture.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

---
title: "Plánování nasazení Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Pomůže vám naplánovat nasazení a určit, kolik serverů ATA bude potřeba k podpoře vaší sítě."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/5/2017
ms.topic: get-started-article
ms.service: advanced-threat-analytics
ms.prod: 
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ce017adf26e30a5fde3c89a30c33f87d71716a4c
ms.sourcegitcommit: 998e8aed5835b228e907aab78845723a02521741
translationtype: HT
---
*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="ata-capacity-planning"></a>Plánování kapacity ATA
Toto téma vám pomůže určit, kolik serverů ATA bude potřeba k monitorování vaší sítě, kolik komponent ATA Gateway nebo ATA Lightweight Gateway potřebujete a jakou kapacitu serveru vyžadují ATA Center a komponenty ATA Gateway.

> [!NOTE] 
> ATA Center se dá nasadit na libovolného dodavatele IaaS, pokud jsou splněné požadavky na výkon popsané v tomto článku.

##<a name="using-the-sizing-tool"></a>Použití nástroje pro změnu velikosti
Doporučený a nejjednodušší způsob, jak určit kapacitu pro vaše nasazení ATA, je použití [nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool). Spusťte nástroj pro změnu velikosti ATA a z výsledků v excelovém souboru pomocí následujících polí určete potřebnou kapacitu ATA:

- CPU a paměť pro ATA Center: Porovnejte pole **Busy Packets/sec** (Počet paketů za sekundu při vytížení) v tabulce pro ATA Center v souboru výsledků s polem **PACKETS PER SECOND** (Počet paketů za sekundu) v [tabulce pro ATA Center](#ata-center-sizing).

- Úložiště pro ATA Center: Porovnejte pole **Avg Packets/sec** (Průměrný počet paketů za sekundu) v tabulce pro ATA Center v souboru výsledků s polem **PACKETS PER SECOND** (Počet paketů za sekundu) v [tabulce pro ATA Center](#ata-center-sizing).
- ATA Gateway: Porovnejte pole **Busy Packets/sec** (Počet paketů za sekundu při vytížení) v tabulce pro ATA Gateway v souboru výsledků s polem **PACKETS PER SECOND** (Počet paketů za sekundu) v [tabulce pro ATA Gateway](#ata-gateway-sizing) nebo v [tabulce pro ATA Lightweight Gateway](#ata-lightweight-gateway-sizing) podle [zvoleného typu brány](#choosing-the-right-gateway-type-for-your-deployment).


![Ukázkový nástroj plánování kapacity](media/capacity tool.png)



Pokud z nějakého důvodu nemůžete použít nástroj pro změnu velikosti ATA, budete muset ručně shromáždit informace z čítače paketů za sekundu ze všech řadičů domény po dobu 24 hodin s velmi malým intervalem sběru hodnot (přibližně 5 sekund). Pak u každého řadiče domény musíte vypočítat denní průměr a průměr za nejvytíženější období (15 minut).
Následující části uvádějí pokyny, jak shromáždit čítač paketů za sekundu z jednoho řadiče domény.



### <a name="ata-center-sizing"></a>Nastavení velikosti ATA Center
Pro vypracování analýzy chování uživatelů vyžaduje ATA Center data za nejméně 30 dnů.
 

|Paketů za sekundu ze všech řadičů domény|Procesor (jádra&#42;)|Paměť (GB)|Úložiště databáze za den (GB)|Úložiště databáze za měsíc (GB)|IOPS&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1 000|2|32|0.3|9|30 (100)
|10 000|4|48|3|90|200 (300)
|40 000|8|64|12|360|500 (1 000)
|100 000|12|96|30|900|1 000 (1 500)
|400 000|40|128|120|3&600;|4&000; (5&000;)

&#42;To zahrnuje fyzická jádra, ne jádra typu Hyper.

&#42;&#42;Průměrné počty (počty ve špičce)
> [!NOTE]
> -   ATA Center může zpracovávat agregované maximum 400 000 snímků za sekundu (FPS) ze všech monitorovaných řadičů domény. V některých prostředích může stejné ATA Center zpracovávat celkový provoz, který je vyšší než 400 000. Pokud potřebujete s takovými prostředími pomoct, pište na adresu askcesec@microsoft.com.
> -   Uvedené velikosti úložišť jsou čisté hodnoty, ale vy byste měli vždy počítat s růstem do budoucna a zajisti, aby na disku, kde je umístěná databáze, bylo vždycky aspoň 20 % volného místa.
> -   Pokud velikost volného místa dosáhne minimální hodnoty buď 20 %, nebo 100 GB, nejstarší kolekce dat se odstraní. To bude pokračovat, dokud nezůstane jen 5 % nebo 50 GB volného místa. Pak se shromažďování dat zastaví.
> - ATA Center je možné nasadit na libovolného dodavatele IaaS, pokud jsou splněné požadavky na výkon popsané v tomto článku.
> -   Latence úložiště pro čtení a zápisu aktivit musí být menší než 10 ms.
> -   Poměr mezi čtením a zápisem aktivit je přibližně 1:3 při méně než 100 000 paketů za sekundu a 1:6 při více než 100 000 paketů za sekundu.
> -   Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.
> -   K zajištění optimálního výkonu nastavte **možnost napájení ** pro ATA Center na hodnotu **Vysoký výkon**.<br>
> -   Při práci na fyzickém serveru databáze ATA vyžaduje, abyste v systému BIOS **zakázali** neuniformní přístup k paměti (NUMA). Ve vašem systému se NUMA může označovat také jako prokládání uzlů. V takovém případě bude potřeba prokládání uzlů **povolit**, abyste NUMA zakázali. Další informace najdete v dokumentaci k systému BIOS. Pokud ATA Center běží na virtuálním serveru, není tento text relevantní.


## <a name="choosing-the-right-gateway-type-for-your-deployment"></a>Výběr vhodného typu brány pro vaše nasazení
V nasazení ATA se podporuje libovolná kombinace typů ATA Gateway:

- Jenom komponenty ATA Gateway
- Jenom komponenty ATA Lightweight Gateway
- Kombinace obojího

Při určování typu nasazení brány vezměte v úvahu:

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
|1 000|2|6|
|5,000|6|16|
    |10 000|10|24|

&#42;Celkový počet paketů za sekundu na řadiči domény, který sleduje tato konkrétní komponenta ATA Lightweight Gateway.

&#42;&#42;Celkový počet jader bez vláken typu Hyper, která má tento řadič domény nainstalovaná.<br>Přestože je hyperthreading pro ATA Lightweight Gateway přijatelný, při plánování kapacity byste měli počítat skutečná jádra, a nikoli jádra s vlákny typu Hyper.

&#42;&#42;&#42;Celkový objem paměti, kterou má tento řadič domény nainstalovanou.

> [!NOTE]    
> -   Pokud řadič domény nemá nezbytný objem prostředků, které ATA Lightweight Gateway vyžaduje, výkon řadiče domény to neovlivní, ale ATA Lightweight Gateway nemusí fungovat podle očekávání.
> -   Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.
> -   K zajištění optimálního výkonu nastavte **možnost napájení ** pro ATA Lightweight Gateway na hodnotu **Vysoký výkon**.
> -   Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. Zahrnuje to prostor potřebný pro binární soubory ATA, [protokoly ATA](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-logs) a [protokoly výkonu](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-perf-counters).


### <a name="ata-gateway-sizing"></a>Nastavení velikosti ATA Gateway

Při rozhodování o tom, kolik komponent ATA Gateway nasadíte, zvažte následující:

-    **Doménové struktury a domény služby Active Directory**<br>
    ATA může monitorovat provoz z několika domén z jedné doménové struktury služby Active Directory. Monitorování několika doménových struktur služby Active Directory vyžaduje samostatná nasazení řešení ATA. Jedno nasazení ATA by nemělo být nakonfigurované pro monitorování síťového provozu řadičů domény patřících do různých doménových struktur.

-    **Zrcadlení portů**<br>
Aspekty zrcadlení portů můžou vyžadovat, abyste pro datové centrum nebo pobočku nasadili několik komponent ATA Gateway.

-    **Kapacita**<br>
    ATA Gateway může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů monitorovaných řadičů domény. 
<br>



|Pakety za sekundu&#42;|Procesor (jádra&#42;&#42;)|Paměť (GB)|
|---------------------------|-------------------------|---------------|
|1 000|1|6|
|5,000|2|10|
|10 000|3|12|
|20 000|6|24|
|50 000|16|48|
&#42;Celkový průměrný počet paketů za sekundu ze všech řadičů domény, které sleduje tato konkrétní ATA Gateway za nejvytíženější hodinu.

&#42;Celkové množství provozu řadiče domény na zrcadleném portu nesmí překročit kapacitu síťové karty pro zachytávání na ATA Gateway.

&#42;&#42;Technologie Hyper-Threading musí být zakázaná.

> [!NOTE] 
> -   Dynamická paměť se nepodporuje.
> -   K zajištění optimálního výkonu nastavte **možnost napájení ** pro ATA Gateway na hodnotu **Vysoký výkon**.
> -   Vyžaduje se minimálně 5 GB volného místa, doporučuje se 10 GB. Zahrnuje to prostor potřebný pro binární soubory ATA, [protokoly ATA](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-logs) a [protokoly výkonu](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-perf-counters).


## <a name="domain-controller-traffic-estimation"></a>Odhad provozu řadiče domény
Existují různé nástroje, které můžete použít ke zjištění průměrného počtu paketů za sekundu vašich řadičů domény. Pokud nemáte žádné nástroje, které sledují tento čítač, můžete k získání požadovaných informací použít nástroj Sledování výkonu.

Pokud chcete určit počet paketů za sekundu, proveďte na každém řadiči domény následující postup:

1.  Otevřete nástroj Sledování výkonu.

    ![Obrázek nástroje Sledování výkonu](media/ATA-traffic-estimation-1.png)

2.  Rozbalte položku **Sady kolekcí dat**.

    ![Obrázek sad kolekcí dat](media/ATA-traffic-estimation-2.png)

3.  Klikněte pravým tlačítkem na **Vlastní** a vyberte **Nový** &gt; **Sada kolekcí dat**.

    ![Obrázek nové sady kolekcí dat](media/ATA-traffic-estimation-3.png)

4.  Zadejte název pro sadu kolekcí a vyberte **Vytvořit ručně (Upřesnit)**.

5.  V části **Jaký typ dat chcete zahrnout?** vyberte **Protokoly vytváření dat a Čítač výkonu**.

    ![Obrázek typu dat pro novou sadu kolekcí dat](media/ATA-traffic-estimation-5.png)

6.  V části **Které čítače výkonu chcete protokolovat?** klikněte na **Přidat**.

7.  Rozbalte položku **Síťový adaptér**, vyberte **Pakety/s** a vyberte vhodnou instanci. Pokud si nejste jisti, můžete vybrat **&lt;Všechny instance&gt;** a kliknout na **Přidat** a **OK**.

    > [!NOTE]
    > Chcete-li to provést, v příkazovém řádku spusťte příkaz `ipconfig /all`, který zobrazí název adaptéru a konfiguraci.

    ![Obrázek přidání čítačů výkonu](media/ATA-traffic-estimation-7.png)

8.  Změňte **Interval vzorku** na **1 sekunda**.

9. Nastavte umístění, kam chcete data uložit.

10. V části **Vytvořit sadu kolekcí dat** vyberte **Spustit tuto sadu kolekcí dat** a klikněte na **Dokončit**

    Měli byste nyní vidět sadu kolekcí dat, kterou jste právě vytvořili, se zeleným trojúhelníkem označujícím, že je funkční.

11. Po 24 hodinách sadu kolekcí dat zastavte kliknutím pravým tlačítkem na sadu kolekcí dat a výběrem **Zastavit**.

    ![Obrázek zastavení sady kolekcí dat](media/ATA-traffic-estimation-12.png)

12. V Průzkumníku souborů přejděte do složky, kam byl uložen soubor .blg, a dvojím kliknutím ho otevřete v nástroji Sledování výkonu.

13. Vyberte čítač Pakety/s a poznamenejte si průměrnou a maximální hodnotu.

    ![Obrázek čítače Pakety/s](media/ATA-traffic-estimation-14.png)

## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Architektura ATA](ata-architecture.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

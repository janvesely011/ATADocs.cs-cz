---
title: "Plánování nasazení ATA | Microsoft Advanced Threat Analytics"
description: "Pomůže vám naplánovat nasazení a určit, kolik serverů ATA bude potřeba k podpoře vaší sítě."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: ff8eb5361d3dfeaa3715d325ed91c0ad422211ed


---

# Plánování kapacity ATA
Toto téma vám pomůže určit, kolik serverů ATA bude potřeba k podpoře vaší sítě, kolik komponent ATA Gateway a ATA Lightweight Gateway potřebujete a jako kapacitu serveru vyžadují ATA Center a komponenty ATA Gateway.

## Nastavení velikosti ATA Center
Pro vypracování analýzy chování uživatelů vyžaduje ATA Center data za nejméně 30 dnů. Požadované místo na disku pro databázi ATA na každý řadič domény je definováno níže. Pokud máte víc řadičů domény, sečtěte požadovaná místa na disku pro jednotlivé řadiče domény, abyste vypočítali celkovou velikost požadovaného místa pro databázi ATA.
> [!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

|Pakety za sekundu&#42;|Procesor (jádra&#42;&#42;)|Paměť (GB)|Úložiště databáze za den (GB)|Úložiště databáze za měsíc (GB)|IOPS&#42;&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1 000|2|32|0.3|9|30 (100)
|10 000|4|48|3|90|200 (300)
|40 000|8|64|12|360|500 (1 000)
|100 000|12|96|30|900|1 000 (1 500)
|400 000|40|128|120|1 800|2 000 (2 500)
&#42;Průměrný denní celkový počet paketů za sekundu ze všech řadičů domény, které sledují všechny komponenty ATA Gateway.

&#42;&#42;To zahrnuje fyzická jádra, ne jádra typu Hyper.

&#42;&#42;&#42;Průměrné počty (počty ve špičce)
> [!NOTE]
> -   ATA Center může zpracovávat agregované maximum 400 000 snímků za sekundu (FPS) ze všech monitorovaných řadičů domény.
> -   Uvedené velikosti úložišť jsou čisté hodnoty, ale vy byste měli vždy počítat s růstem do budoucna a zajisti, aby na disku, kde je umístěná databáze, bylo vždycky aspoň 20 % volného místa.
> -   Pokud velikost volného místa dosáhne minimální hodnoty buď 20 %, nebo 100 GB, nejstarší kolekce dat se odstraní. To bude pokračovat, dokud nezůstanou buď jen 2 dny dat, nebo 5 % nebo 50 GB volného místa, a v takovém okamžiku se shromažďování dat zastaví.
> -  Latence úložiště pro čtení a zápisu aktivit musí být menší než 10 ms.
> -  Poměr mezi čtením a zápisem aktivit je přibližně 1:3 při méně než 100 000 paketů za sekundu a 1:6 při více než 100 000 paketů za sekundu.

## Výběr vhodného typu brány pro vaše nasazení
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


## Velikosti pro ATA Lightweight Gateway

ATA Lightweight Gateway může podporovat monitorování jednoho řadiče domény na základě objemu síťového provozu, který tento řadič generuje. 
> [!NOTE] 
> Pokud se spustí jako dynamická paměť virtuálního počítače nebo libovolná jiná paměť, funkce rozšiřování rozsahů stránek se nepodporuje.

|Pakety za sekundu&#42;|Procesor (jádra&#42;&#42;)|Paměť (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1 000|2|6|
|5,000|6|16|
    |10 000|10|24|

&#42;Celkový počet paketů za sekundu na řadiči domény, který sleduje tato konkrétní komponenta ATA Lightweight Gateway.

&#42;&#42;Celkový počet jader bez vláken typu Hyper, která má tento řadič domény nainstalovaná.<br>Přestože je hyperthreading pro ATA Lightweight Gateway přijatelný, při plánování kapacity byste měli počítat skutečná jádra, a nikoli jádra s vlákny typu Hyper.

&#42;&#42;&#42;Celkový objem paměti, kterou má tento řadič domény nainstalovanou.
> [!NOTE]   
> Pokud řadič domény nemá nezbytný objem prostředků, které ATA Lightweight Gateway vyžaduje, výkon řadiče domény to neovlivní, ale ATA Lightweight Gateway nemusí fungovat podle očekávání.


## Nastavení velikosti ATA Gateway

Při rozhodování o tom, kolik komponent ATA Gateway nasadíte, zvažte následující:

-   **Doménové struktury a domény služby Active Directory**<br>
    ATA může monitorovat provoz z několika domén z jedné doménové struktury služby Active Directory. Monitorování několika doménových struktur služby Active Directory vyžaduje samostatná nasazení řešení ATA. Jedno nasazení ATA by nemělo být nakonfigurované pro monitorování síťového provozu řadičů domény patřících do různých doménových struktur.

-   **Zrcadlení portů**<br>
Aspekty zrcadlení portů můžou vyžadovat, abyste pro datové centrum nebo pobočku nasadili několik komponent ATA Gateway.

-   **Kapacita**<br>
    ATA Gateway může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů monitorovaných řadičů domény. 
<br>

> [!NOTE] 
> Dynamická paměť se nepodporuje.

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



## Odhad provozu řadiče domény
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

## Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Architektura ATA](ata-architecture.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->



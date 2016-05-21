---
# required metadata

title: Plánování kapacity ATA | Microsoft Advanced Threat Analytics
description: Pomůže vám určit, kolik serverů ATA bude potřeba k podpoře vaší sítě.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Plánování kapacity ATA
Toto téma vám pomůže určit, kolik serverů ATA bude potřeba k podpoře vaší sítě.

## Nastavení velikosti ATA Center
Pro vypracování analýzy chování uživatelů vyžaduje ATA Center data za nejméně 30 dnů. Požadované místo na disku pro databázi ATA na každý řadič domény je definováno níže. Pokud máte víc řadičů domény, sečtěte požadovaná místa na disku pro jednotlivé řadiče domény, abyste vypočítali celkovou velikost požadovaného místa pro databázi ATA.

|Pakety za sekundu&#42;|Procesor (jádra&#42;&#42;)|Paměť (GB)|Úložiště operačního systému (GB)|Úložiště databáze za den (GB)|Úložiště databáze za měsíc (GB)|IOPS&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1 000|4|48|200|1.5|45|30 (100)
|10 000|4|48|200|15|450|200 (300)
|40 000|8|64|200|60|1 800|500 (1 000)
|100 000|12|96|200|150|4 500|1 000 (1 500)
|200 000|16|128|200|300|9 000|2 000 (2 500)
&#42;Průměrný denní celkový počet paketů za sekundu ze všech řadičů domény, které sledují všechny komponenty ATA Gateway.

&#42;&#42;To zahrnuje fyzická jádra, ne jádra typu Hyper.

&#42;&#42;&#42;Průměrné počty (počty ve špičce)
> [!NOTE]
> -   ATA Center může zpracovávat agregované maximum 200 000 snímků za sekundu (FPS) ze všech monitorovaných řadičů domény.
> -   U velkých nasazeních (počínaje přibližně u 100 000 paketů za sekundu) vyžadujeme, aby byl deník databáze umístěn na jiném disku než databáze.
> -   Uvedené velikosti úložišť jsou čisté hodnoty, ale vy byste měli vždy počítat s růstem do budoucna a zajisti, aby na disku, kde je umístěná databáze, bylo vždycky aspoň 20 % volného místa.
> -   Pokud velikost volného místa dosáhne minimální hodnoty buď 20 %, nebo 100 GB, odstraní se nejstarších 24 hodin dat. To bude pokračovat, dokud nezůstanou buď jen 2 dny dat, nebo 5 % nebo 50 GB volného místa, a v takovém okamžiku se shromažďování dat zastaví.
> -  Latence úložiště pro čtení a zápisu aktivit musí být menší než 10 ms.
> -  Poměr mezi čtením a zápisem aktivit je přibližně 1:3 při méně než 100 000 paketů za sekundu a 1:6 při více než 100 000 paketů za sekundu.

## Nastavení velikosti ATA Gateway
ATA Gateway může podporovat monitorování několika řadičů domény, v závislosti na objemu síťových přenosů monitorovaných řadičů domény.

|Pakety za sekundu&#42;|Procesor (jádra&#42;&#42;)|Paměť (GB)|Úložiště operačního systému (GB)|
|---------------------------|-------------------------|---------------|-------------------|
|10 000|4|12|80|
|20 000|8|24|100|
|40 000|16|64|200|
&#42;Celkový počet paketů za sekundu ze všech řadičů domény, které sleduje tato konkrétní ATA Gateway.

&#42;Celkové množství provozu řadiče domény na zrcadleném portu nesmí překročit kapacitu síťové karty pro zachytávání na ATA Gateway.

&#42;&#42;Technologie Hyper-Threading musí být zakázaná.

## Odhad provozu řadiče domény
Existují různé nástroje, které můžete použít ke zjištění průměrného počtu paketů za sekundu vašich řadičů domény. Pokud nemáte žádné nástroje, které sledují tento čítač, můžete k získání požadovaných informací použít nástroj Sledování výkonu.

Pokud chcete určit počet paketů za sekundu, proveďte na každém řadiči domény následující postup:

1.  Otevřete nástroj Sledování výkonu.

    ![Obrázek nástroje Sledování výkonu](media/ATA-traffic-estimation-1.png)

2.  Rozbalte položku **Sady kolekcí dat**..

    ![Obrázek sad kolekcí dat](media/ATA-traffic-estimation-2.png)

3.  Klikněte pravým tlačítkem na **Vlastní** a vyberte **Nový** &gt; **Sada kolekcí dat**..

    ![Obrázek nové sady kolekcí dat](media/ATA-traffic-estimation-3.png)

4.  Zadejte název pro sadu kolekcí a vyberte **Vytvořit ručně (Upřesnit)**..

5.  V části **Jaký typ dat chcete zahrnout?** vyberte **Protokoly vytváření dat a Čítač výkonu**..

    ![Obrázek typu dat pro novou sadu kolekcí dat](media/ATA-traffic-estimation-5.png)

6.  V části **Které čítače výkonu chcete protokolovat?** klikněte na **Přidat**..

7.  Rozbalte položku **Síťový adaptér**, vyberte **Pakety/s** a vyberte vhodnou instanci. Pokud si nejste jisti, můžete vybrat **&lt;Všechny instance&gt;** a kliknout na **Přidat** a **OK**..

    > [!NOTE]
    > Chcete-li to provést, v příkazovém řádku spusťte příkaz `ipconfig /all`, který zobrazí název adaptéru a konfiguraci.

    ![Obrázek přidání čítačů výkonu](media/ATA-traffic-estimation-7.png)

8.  Změňte **Intervalu vzorku** na **1 sekunda**..

9. Nastavte umístění, kam chcete data uložit.

10. V části **Vytvořit sadu kolekcí dat** vyberte **Spustit tuto sadu kolekcí dat** a klikněte na **Dokončit**.

    Měli byste nyní vidět sadu kolekcí dat, kterou jste právě vytvořili, se zeleným trojúhelníkem označujícím, že je funkční.

11. Po 24 hodinách zastavte sadu kolekcí dat kliknutím pravým tlačítkem na sadu kolekcí dat a výběrem **Zastavit**.

    ![Obrázek zastavení sady kolekcí dat](media/ATA-traffic-estimation-12.png)

12. V Průzkumníku souborů přejděte do složky, kam byl uložen soubor .blg, a dvojím kliknutím ho otevřete v nástroji Sledování výkonu.

13. Vyberte čítač Pakety/s a poznamenejte si průměrnou a maximální hodnotu.

    ![Obrázek čítače Pakety/s](media/ATA-traffic-estimation-14.png)

## Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Architektura ATA](/advanced-threat-analytics/understand-explore/ata-architecture)
- [Podporu získáte na našem fóru!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO4-->



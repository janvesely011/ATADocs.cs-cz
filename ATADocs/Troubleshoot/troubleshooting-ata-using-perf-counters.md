---
# required metadata

title: Řešení potíží s ATA pomocí čítačů výkonu | Microsoft Advanced Threat Analytics
description: Popisuje, jak se čítače výkonu dají použít k řešení potíží s ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: df162a62-f273-4465-9887-94271f5000d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Řešení potíží s ATA pomocí čítačů výkonu
Čítače výkonu ATA poskytují přehled o tom, jak dobře jednotlivé komponenty ATA fungují. Komponenty ATA zpracovávají data sekvenčně. To znamená, že případný problém vyvolá řetězovou reakci, která způsobí zhoršení provozu. Pokud chcete problém vyřešit, musíte zjistit, která komponenta selhává, a pak problém vyřešit na samém začátku řetězce.
    Pokud chcete lépe pochopit tok interních komponent ATA, přečtěte si článek [Architektura ATA](/advanced-threat-analytics/understand-explore/ata-architecture).

**Proces komponent ATA**:

1.  Když komponenta dosáhne své maximální velikosti, zablokuje odesílání dalších entit z předchozí komponenty.

2.  Tímto způsobem se začne zvětšovat **vlastní** velikost předchozí komponenty, až zablokuje odesílání dalších entit z komponenty před ní.

3.  To samé se děje s dalšími komponentami až k počáteční komponentě NetworkListener, která omezí síťový provoz, když už nebude moct přesměrovávat entity.

4. Data uvedená v čítačích výkonu vám pomůžou pochopit, jak jednotlivé komponenty fungují.

## Čítače výkonu ATA Gateway
Přidáním čítačů výkonu ATA Gateway můžete sledovat výkon komponenty ATA Gateway v reálném čase.
Stačí otevřít Sledování výkonu a přidat všechny čítače pro ATA Gateway. Název příslušného objektu čítače výkonu je Microsoft ATA Gateway.

![Obrázek přidání čítačů výkonu](media/ATA-performance-counters.png)

Tady je seznam hlavních čítačů výkonu komponenty ATA Gateway, kterým je potřeba věnovat pozornost:

|Čítač|Popis|Prahová hodnota|Odstraňování potíží|
|-----------|---------------|-------------|-------------------|
|NetworkListener Captured Parser Messages/Sec (Zachycené zprávy analyzované komponentou NetworkListener/s)|Objem provozu, který ATA Gateway zpracovává za sekundu|Žádná prahová hodnota|Pomáhá zjistit objem provozu, který ATA Gateway analyzuje.|
|NetworkListener Captured Dropped Messages/Sec (Zachycené zprávy vynechané komponentou NetworkListener/s)|Objem provozu, který ATA Gateway vynechává za sekundu|Tato hodnota by měla být stále nulová (výjimečná krátká zhoršení jsou přijatelná).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
|NetworkListener Captured Dropped ETW Real Time Buffers/Sec (Zachycené vyrovnávací paměti ETW v reálném čase vynechané komponentou NetworkListener/s)|Objem provozu, který ATA Gateway vynechává za sekundu|Tato hodnota by měla být stále nulová (výjimečná krátká zhoršení jsou přijatelná).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
|NetworkListener Captured Dropped ETW Log Buffers/Sec (Zachycené vyrovnávací paměti ETW protokolů vynechané komponentou NetworkListener/s)|Objem provozu, který ATA Gateway vynechává za sekundu|Tato hodnota by měla být stále nulová (výjimečná krátká zhoršení jsou přijatelná).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
|NetworkListener Captured Dropped ETW Events/Sec (Zachycené události ETW vynechané komponentou NetworkListener/s)|Objem provozu, který ATA Gateway vynechává za sekundu|Tato hodnota by měla být stále nulová (výjimečná krátká zhoršení jsou přijatelná).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
|NetworkActivityTranslator Message Data # Block Size (Velikost bloku dat zpráv komponenty NetworkActivityTranslator)|Objem provozu zařazený do fronty pro překlad na síťové aktivity (NA)|Hodnota by měla být menší než maximum-1 (výchozí maximum je 100000).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
|EntityResolver Activity Block Size (Velikost bloku aktivit komponenty EntityResolver)|Objem síťových aktivit (NA) zařazených do fronty pro překlad|Hodnota by měla být menší než maximum-1 (výchozí maximum je 10000).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
|EntitySender Entity Batch Block Size (Velikost bloku dávky entit komponenty EntitySender)|Objem síťových aktivit (NA) zařazených do fronty pro odeslání na ATA Center|Hodnota by měla být menší než maximum-1 (výchozí maximum je 1000000).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
|EntitySender Batch Send Time (Čas odeslání dávky komponenty EntitySender)|Doba, kterou trvalo odeslání poslední dávky|Po většinu času by měla být menší než 1000 milisekund.|Zkontrolujte, jestli mezi komponentami ATA Gateway a ATA Center nejsou nějaké síťové potíže.|

> [!NOTE]
> -   Hodnoty čítačů jsou v milisekundách.
> -   Někdy je vhodnější monitorovat všechny čítače pomocí typu grafu Sestava (příklad: monitorování všech čítačů v reálném čase).

## Čítače výkonu ATA Center
Přidáním čítačů výkonu ATA Center můžete sledovat výkon softwaru ATA Center v reálném čase.

Stačí otevřít Sledování výkonu a přidat všechny čítače pro ATA Center. Název příslušného objektu čítače výkonu je Microsoft ATA Center.

![Přidání čítačů výkonu ATA Center](media/ATA-Gateway-perf-counters.png)

Tady je seznam hlavních čítačů výkonu komponenty ATA Center, kterým je potřeba věnovat pozornost:

|Čítač|Popis|Prahová hodnota|Odstraňování potíží|
|-----------|---------------|-------------|-------------------|
|EntityReceiver Entity Batch Block Size (Velikost bloku dávky entit komponenty EntityReceiver)|Počet dávek entit, které komponenta ATA Center zařadila do fronty|Hodnota by měla být menší než maximum-1 (výchozí maximum je 100).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener.  Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
|NetworkActivityProcessor Network Activity Block Size (Velikost bloku síťových aktivit komponenty NetworkActivityProcessor)|Počet síťových aktivit (NA) zařazených do fronty pro zpracování|Hodnota by měla být menší než maximum-1 (výchozí maximum je 10000).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
|EntityProfiler Network Activity Block Size (Velikost bloku síťových aktivit komponenty EntityProfiler)|Počet síťových aktivit (NA) zařazených do fronty pro profilování|Hodnota by měla být menší než maximum-1 (výchozí maximum je 10000).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
|CenterDatabaseClient &#42; Block Size (CenterDatabaseClient &#42; velikost bloku)|Počet síťových aktivit konkrétního typu zařazených do fronty pro zápis do databáze|Hodnota by měla být menší než maximum-1 (výchozí maximum je 50000).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
|Čas detekce komponenty DetectionEngine|Celková doba, kterou trval poslední úplný cyklus deterministických detekcí|Hodnota by měla být menší než 900000 (15 minut).|Zkontrolujte, jestli nejsou potíže s procesorem, pamětí nebo úložištěm.|

> [!NOTE]
> -   Hodnoty čítačů jsou v milisekundách.
> -   Někdy je vhodnější monitorovat všechny čítače pomocí typu grafu Sestava (příklad: monitorování všech čítačů v reálném čase).

## Čítače operačního systému
Následuje seznam hlavních čítačů operačního systému, kterým je potřeba věnovat pozornost:

|Čítač|Popis|Prahová hodnota|Odstraňování potíží|
|-----------|---------------|-------------|-------------------|
|Procesor(_celkem)\% času procesoru|Procentuální hodnota uplynulého času, kdy procesor zpracovával vlákno, které není nečinné|V průměru méně než 80 %|Zkontrolujte, jestli některý z procesů nespotřebovává více procesorového času, než by měl.<br /><br />Přidejte víc procesorů.<br /><br />Snižte objem provozu na server.<br /><br />Čítač Procesor(_celkem)\% času procesoru může být u virtuálních serverů méně přesný. V takovém případě je přesnější měřit nedostatek výkonu procesoru pomocí čítače Systém\Délka fronty procesoru.|
|Systém\Přepnutí kontextu/s|Celková rychlost přepínání procesorů mezi jednotlivými vlákny|Méně než 5000&#42;jader (fyzických jader)|Zkontrolujte, jestli některý z procesů nespotřebovává více procesorového času, než by měl.<br /><br />Přidejte víc procesorů.<br /><br />Snižte objem provozu na server.<br /><br />Čítač Procesor(_celkem)\% času procesoru může být u virtuálních serverů méně přesný. V takovém případě je přesnější měřit nedostatek výkonu procesoru pomocí čítače Systém\Délka fronty procesoru.|
|Systém\Délka fronty procesoru|Počet vláken, které jsou připravené ke spuštění a čekají na naplánování|Méně než 5&#42;jader (fyzických jader)|Zkontrolujte, jestli některý z procesů nespotřebovává více procesorového času, než by měl.<br /><br />Přidejte víc procesorů.<br /><br />Snižte objem provozu na server.<br /><br />Čítač Procesor(_celkem)\% času procesoru může být u virtuálních serverů méně přesný. V takovém případě je přesnější měřit nedostatek výkonu procesoru pomocí čítače Systém\Délka fronty procesoru.|
|Paměť\Počet MB k dispozici|Velikost fyzické paměti (RAM), která je k dispozici pro přidělení|Hodnota by měla být vyšší než 512.|Zkontrolujte, jestli některý z procesů nespotřebovává více fyzické paměti, než by měl.<br /><br />Zvětšete velikost fyzické paměti.<br /><br />Snižte objem provozu na server.|
|Logický disk(&#42;)\Střední doba disku/čtení|Průměrná latence pro čtení dat z disku (jako instanci byste měli zvolit databázovou jednotku).|Hodnota by měla být menší než 10 milisekund.|Zkontrolujte, jestli některý z procesů nevyužívá databázovou jednotku víc, než by měl.<br /><br />Poraďte se s dodavatelem nebo týmem pro úložiště, jestli tato jednotka dokáže zvládat aktuální zatížení a mít přitom latenci menší než 10 ms. Aktuální zatížení se dá určit pomocí čítačů využití disku.|
|Logický disk(&#42;)\Střední doba disku/zápis|Průměrná latence pro zápis dat na disk (jako instanci byste měli zvolit databázovou jednotku).|Hodnota by měla být menší než 10 milisekund.|Zkontrolujte, jestli některý z procesů nevyužívá databázovou jednotku víc, než by měl.<br /><br />Poraďte se s dodavatelem nebo týmem pro úložiště, jestli tato jednotka dokáže zvládat aktuální zatížení a mít přitom latenci menší než 10 ms. Aktuální zatížení se dá určit pomocí čítačů využití disku.|
|\Logický disk(&#42;)\Čtení z disku/s|Rychlost provádění operací čtení z disku|Žádná prahová hodnota|Čítače využití disku mohou pomoci při řešení potíží s latencí úložiště.|
|\Logický disk(&#42;)\Bajty čtení z disku/s|Počet bajtů, které se za sekundu načtou z disku|Žádná prahová hodnota|Čítače využití disku mohou pomoci při řešení potíží s latencí úložiště.|
|\Logický disk(&#42;)\Zápisy na disk/s|Rychlost provádění operací zápisu na disk|Žádná prahová hodnota|Čítače využití disku (mohou pomoci při řešení potíží s latencí úložiště)|
|\Logický disk(&#42;)\Bajty zápisu na disk/s|Počet bajtů, které se za sekundu zapíší na disk|Žádná prahová hodnota|Čítače využití disku mohou pomoci při řešení potíží s latencí úložiště.|


<!--HONumber=Apr16_HO4-->



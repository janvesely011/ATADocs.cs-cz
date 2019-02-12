---
title: Řešení potíží s Advanced Threat Analytics pomocí čítačů výkonu | Dokumentace Microsoftu
description: Popisuje, jak se čítače výkonu dají použít k řešení potíží s ATA.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 9/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: df162a62-f273-4465-9887-94271f5000d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f5eac97c2c3da5294f5fa42b00792cafe456b35e
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56078013"
---
# <a name="troubleshooting-ata-using-the-performance-counters"></a>Řešení potíží s ATA pomocí čítačů výkonu

*Platí pro: Advanced Threat Analytics verze 1.9*

Čítače výkonu ATA poskytují přehled o tom, jak dobře jednotlivé komponenty ATA fungují. Komponenty ATA zpracovávají data sekvenčně. To znamená, že případný problém může na některém místě řetězce komponent způsobit částečné zhoršení provozu. Pokud chcete problém vyřešit, musíte zjistit, která komponenta selhává, a pak problém vyřešit na samém začátku řetězce. Data uvedená v čítačích výkonu vám pomůžou pochopit, jak jednotlivé komponenty fungují.
Pokud chcete lépe pochopit tok interních komponent ATA, přečtěte si článek [Architektura ATA](ata-architecture.md).

**Proces komponent ATA**:

1.  Když komponenta dosáhne své maximální velikosti, zablokuje odesílání dalších entit z předchozí komponenty.

2.  Tímto způsobem se začne zvětšovat **vlastní** velikost předchozí komponenty, až zablokuje odesílání dalších entit z komponenty před ní.

3.  To se děje s komponentami až ke komponentě NetworkListener, která omezí síťový provoz, když už nebude moct přesměrovávat entity.


## <a name="retrieving-performance-monitor-files-for-troubleshooting"></a>Načítání souborů sledování výkonu kvůli řešení problémů

Pokud chcete načíst soubory sledování výkonu (BLG) z různých komponent ATA, postupujte takto:
1.  Otevřete Perfmon.
2.  Zastavte sadu kolekcí dat: **Microsoft ATA Gateway** nebo **Microsoft ATA Center**.
3.  Přejděte do složky sady kolekcí dat (ve výchozím nastavení je to složka C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs\DataCollectorSets nebo C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs\DataCollectorSets.
4.  Zkopírujte naposledy změněný soubor BLG.
5.  Restartujte sadu kolekcí dat: **Microsoft ATA Gateway** nebo **Microsoft ATA Center**.


## <a name="ata-gateway-performance-counters"></a>Čítače výkonu ATA Gateway

V této části všechny odkazy na ATA Gateway platí také pro ATA Lightweight Gateway.

Přidáním čítačů výkonu ATA Gateway můžete sledovat stav v reálném čase výkon komponenty ATA Gateway.
To se provádí tak, že otevřete **sledování výkonu** a přidat všechny čítače pro ATA Gateway. Název příslušného objektu čítače výkonu je: **Microsoft ATA Gateway**.

Tady je seznam hlavních čítačů výkonu komponenty ATA Gateway, kterým je potřeba věnovat pozornost:

> [!div class="mx-tableFixed"]
> 
> |Čítač|Popis|Prahová hodnota|Řešení potíží|
> |-----------|---------------|-------------|-------------------|
> |Microsoft ATA Gateway\NetworkListener PEF Parsed Messages\Sec (Zprávy analyzované komponentou Microsoft ATA Gateway\PEF NetworkListener/s)|Objem provozu, který ATA Gateway zpracovává za sekundu|Žádná prahová hodnota|Pomáhá zjistit objem provozu, který ATA Gateway analyzuje.|
> |NetworkListener PEF Dropped Events/Sec (Události vynechané komponentou PEF NetworkListener/s)|Objem provozu, který ATA Gateway vynechává za sekundu|Tato hodnota by měla být stále nulová (výjimečná krátká zhoršení jsou přijatelná).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
> |Microsoft ATA Gateway\NetworkListener ETW Dropped Events\Sec (Microsoft ATA Gateway\Události vynechané komponentou ETW NetworkListener/s)|Objem provozu, který ATA Gateway vynechává za sekundu|Tato hodnota by měla být stále nulová (výjimečná krátká zhoršení jsou přijatelná).|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
> |Microsoft ATA Gateway\NetworkActivityTranslator Message Data # Block Size (Microsoft ATA Gateway\Velikost bloku dat zpráv komponenty NetworkActivityTranslator)|Objem provozu zařazený do fronty pro překlad na síťové aktivity (NA)|Musí být menší než maximum-1 (výchozí maximum: 100,000)|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
> |Microsoft ATA Gateway\EntityResolver Activity Block Size (Microsoft ATA Gateway\Velikost bloku aktivity komponenty EntityResolver)|Počet síťových aktivit (na) zařazených do fronty pro překlad.|Musí být menší než maximum-1 (výchozí maximum: 10,000)|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
> |Microsoft ATA Gateway\EntitySender Entity Batch Block Size (Microsoft ATA Gateway\Velikost bloku dávky entit komponenty EntitySender)|Objem síťových aktivit (NA) zařazených do fronty pro odeslání na ATA Center|Musí být menší než maximum-1 (výchozí maximum: 1,000,000)|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Další informace najdete v části **Proces komponent ATA** uvedené výš.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
> |Microsoft ATA Gateway\EntitySender Batch Send Time (Microsoft ATA Gateway\Čas odeslání dávky komponenty EntitySender)|Doba, kterou trvalo odeslání poslední dávky|Po většinu času by měla být menší než 1000 milisekund.|Zkontrolujte, jestli mezi komponentami ATA Gateway a ATA Center nejsou nějaké síťové potíže.|
> 
> [!NOTE]
> -   Hodnoty čítačů jsou v milisekundách.
> -   Někdy je vhodnější monitorovat úplný seznam čítačů výkonu pomocí **sestavy** typ rozhraní graph (Příklad: monitorování všech čítačů v reálném čase)

## <a name="ata-lightweight-gateway-performance-counters"></a>Čítače výkonu ATA Lightweight Gateway
Čítače výkonu můžete použít ke správě kvóty v Lightweight Gateway, abyste se ujistili, že ATA nespotřebovává příliš mnoho prostředků z řadičů domény, ve kterých není nainstalovaná.
Pokud chcete změřit omezení prostředků, které ATA na Lightweight Gateway vynucuje, přidejte tyto čítače.

To se provádí tak, že otevřete **sledování výkonu** a přidat všechny čítače pro ATA Lightweight Gateway. Názvy objektů čítače výkonu jsou: **Microsoft ATA Gateway** a **Microsoft ATA Gateway Updater**.

> [!div class="mx-tableFixed"]
> 
> |Čítač|Popis|Prahová hodnota|Řešení potíží|
> |-----------|---------------|-------------|-------------------|
> |Max. procento času procesoru Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager|Maximální množství času procesoru (v procentech), které může proces Lightweight Gateway spotřebovat. |Žádná prahová hodnota. | Toto je omezení, které chrání prostředky řadiče domény, aby je nespotřebovala ATA Lightweight Gateway. Pokud si všimnete, že proces v určitém časovém intervalu často dosahuje maximálního limitu (proces dosáhne limitu a potom začne zahazovat provoz), znamená to, bude třeba přidat další prostředky na server s řadičem domény.|
> |Max. velikost potvrzené paměti Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager|Maximální velikost potvrzené paměti (v bajtech), kterou může proces Lightweight Gateway spotřebovat.|Žádná prahová hodnota. | Toto je omezení, které chrání prostředky řadiče domény, aby je nespotřebovala ATA Lightweight Gateway. Pokud si všimnete, že proces v určitém časovém intervalu často dosahuje maximálního limitu (proces dosáhne limitu a potom začne zahazovat provoz), znamená to, bude třeba přidat další prostředky na server s řadičem domény.| 
> |Omezení velikosti pracovní sady Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager|Maximální velikost fyzické paměti (v bajtech), kterou může proces Lightweight Gateway spotřebovat.|Žádná prahová hodnota. | Toto je omezení, které chrání prostředky řadiče domény, aby je nespotřebovala ATA Lightweight Gateway. Pokud si všimnete, že proces v určitém časovém intervalu často dosahuje maximálního limitu (proces dosáhne limitu a potom začne zahazovat provoz), znamená to, bude třeba přidat další prostředky na server s řadičem domény.|



Pokud chcete zobrazit skutečnou spotřebou, podívejte se na následující čítače:


> [!div class="mx-tableFixed"]
> 
> |Čítač|Popis|Prahová hodnota|Řešení potíží|
> |-----------|---------------|-------------|-------------------|
> |Process(Microsoft.Tri.Gateway)\%Čas procesoru|Množství času procesoru (v procentech), které proces Lightweight Gateway skutečně spotřebovává. |Žádná prahová hodnota. | Porovnejte výsledky tohoto čítače s limitem Max. procento času procesoru GatewayUpdaterResourceManager. Pokud si všimnete, že proces v určitém časovém intervalu často dosahuje maximálního limitu (proces dosáhne limitu a potom začne odpojovat provoz), znamená to, budete muset vyhradit další prostředky pro součást Lightweight Gateway.|
> |Process(Microsoft.Tri.Gateway)\Soukromé bajty|Velikost potvrzené paměti (v bajtech), kterou proces Lightweight Gateway skutečně spotřebovává.|Žádná prahová hodnota. | Porovnejte výsledky tohoto čítače s limitem Max. velikost potvrzené paměti GatewayUpdaterResourceManager. Pokud si všimnete, že proces v určitém časovém intervalu často dosahuje maximálního limitu (proces dosáhne limitu a potom začne zahazovat provoz), znamená to, bude třeba vyhradit další prostředky pro Lightweight Gateway.| 
> |Process(Microsoft.Tri.Gateway)\Pracovní sada|Velikost fyzické paměti (v bajtech), kterou proces Lightweight Gateway skutečně spotřebovává.|Žádná prahová hodnota. |Porovnejte výsledky tohoto čítače s limitem Max. velikost potvrzené paměti GatewayUpdaterResourceManager. Pokud si všimnete, že proces v určitém časovém intervalu často dosahuje maximálního limitu (proces dosáhne limitu a potom začne odpojovat provoz), znamená to, budete muset vyhradit další prostředky pro součást Lightweight Gateway.|

## <a name="ata-center-performance-counters"></a>Čítače výkonu ATA Center
Přidáním čítačů výkonu ATA Center můžete sledovat výkon softwaru ATA Center v reálném čase.

To se provádí tak, že otevřete **sledování výkonu** a přidat všechny čítače pro ATA Center. Název příslušného objektu čítače výkonu je: **Microsoft ATA Center**.

Tady je seznam hlavních čítačů výkonu komponenty ATA Center, kterým je potřeba věnovat pozornost:

> [!div class="mx-tableFixed"]
> 
> |Čítač|Popis|Prahová hodnota|Řešení potíží|
> |-----------|---------------|-------------|-------------------|
> |Velikost bloku dávky entit Microsoft ATA Center\EntityReceiver|Počet dávek entit, které komponenta ATA Center zařadila do fronty|Musí být menší než maximum-1 (výchozí maximum: 10,000)|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener.  Odkazovat na předchozí **proces komponent ATA**.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
> |Velikost bloku síťových aktivit Microsoft ATA Center\NetworkActivityProcessor|Počet síťových aktivit (NA) zařazených do fronty pro zpracování|Musí být menší než maximum-1 (výchozí maximum: 50,000)|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Odkazovat na předchozí **proces komponent ATA**.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
> |Velikost bloku síťových aktivit Microsoft ATA Center\EntityProfiler|Počet síťových aktivit (NA) zařazených do fronty pro profilování|Musí být menší než maximum-1 (výchozí maximum: 100,000)|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Odkazovat na předchozí **proces komponent ATA**.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
> |Microsoft ATA Center\Database &#42; velikost bloku|Počet síťových aktivit konkrétního typu zařazených do fronty pro zápis do databáze|Musí být menší než maximum-1 (výchozí maximum: 50,000)|Zkontrolujte, jestli některá komponenta nedosáhla své maximální velikosti a neblokuje předchozí komponenty až ke komponentě NetworkListener. Odkazovat na předchozí **proces komponent ATA**.<br /><br />Zkontrolujte, jestli nejsou potíže s procesorem nebo pamětí.|
> 
> 
> [!NOTE]
> -   Hodnoty čítačů jsou v milisekundách.
> -   Někdy je vhodnější monitorovat úplný seznam čítače pomocí typu grafu sestava (Příklad: monitorování všech čítačů v reálném čase).

## <a name="operating-system-counters"></a>Čítače operačního systému
V následující tabulce jsou uvedeny hlavních čítačů operačního systému je potřeba věnovat pozornost:

> [!div class="mx-tableFixed"]
> 
> |Čítač|Popis|Prahová hodnota|Řešení potíží|
> |-----------|---------------|-------------|-------------------|
> |Procesor(_celkem)\% času procesoru|Procentuální hodnota uplynulého času, kdy procesor zpracovával vlákno, které není nečinné|V průměru méně než 80 %|Zkontrolujte, jestli některý z procesů nespotřebovává více procesorového času, než by měl.<br /><br />Přidejte víc procesorů.<br /><br />Snižte objem provozu na server.<br /><br />Čítač Procesor(_celkem)\%% času procesoru může být u virtuálních serverů méně přesný. V takovém případě je přesnější měřit nedostatek výkonu procesoru pomocí čítače Systém\Délka fronty procesoru.|
> |Systém\Přepnutí kontextu/s|Celková rychlost přepínání procesorů mezi jednotlivými vlákny|Méně než 5000&#42;jader (fyzických jader)|Zkontrolujte, jestli některý z procesů nespotřebovává více procesorového času, než by měl.<br /><br />Přidejte víc procesorů.<br /><br />Snižte objem provozu na server.<br /><br />Čítač Procesor(_celkem)\%% času procesoru může být u virtuálních serverů méně přesný. V takovém případě je přesnější měřit nedostatek výkonu procesoru pomocí čítače Systém\Délka fronty procesoru.|
> |Systém\Délka fronty procesoru|Počet vláken, které jsou připravené ke spuštění a čekají na naplánování|Méně než pět&#42;jader (fyzických jader)|Zkontrolujte, jestli některý z procesů nespotřebovává více procesorového času, než by měl.<br /><br />Přidejte víc procesorů.<br /><br />Snižte objem provozu na server.<br /><br />Čítač Procesor(_celkem)\%% času procesoru může být u virtuálních serverů méně přesný. V takovém případě je přesnější měřit nedostatek výkonu procesoru pomocí čítače Systém\Délka fronty procesoru.|
> |Paměť\Počet MB k dispozici|Velikost fyzické paměti (RAM), která je k dispozici pro přidělení|By měla být větší než 512|Zkontrolujte, jestli některý z procesů nespotřebovává více fyzické paměti, než by měl.<br /><br />Zvětšete velikost fyzické paměti.<br /><br />Snižte objem provozu na server.|
> |Logický disk(&#42;)\Střední Doba disku/čtení|Průměrná latence pro čtení dat z disku (jako instanci byste měli zvolit databázovou jednotku).|Hodnota by měla být menší než 10 milisekund.|Zkontrolujte, jestli některý z procesů nevyužívá databázovou jednotku víc, než by měl.<br /><br />Poraďte se s týmu nebo dodavatele úložiště, jestli tato jednotka dokáže zvládat aktuální zatížení přitom má latenci menší než 10 ms. Aktuální zatížení se dá určit pomocí čítačů využití disku.|
> |Logický disk(&#42;)\Střední Doba disku/zápis|Průměrná latence pro zápis dat na disk (jako instanci byste měli zvolit databázovou jednotku).|Hodnota by měla být menší než 10 milisekund.|Zkontrolujte, jestli některý z procesů nevyužívá databázovou jednotku víc, než by měl.<br /><br />Poraďte se s nebo týmem pro úložiště, jestli tato jednotka dokáže zvládat aktuální zatížení přitom má latenci menší než 10 ms. Aktuální zatížení se dá určit pomocí čítačů využití disku.|
> |\Logický disk(&#42;)\Čtení z disku/s|Rychlost provádění operací čtení z disku|Žádná prahová hodnota|Čítače využití disku mohou pomoci při řešení potíží s latencí úložiště.|
> |\Logický disk(&#42;)\Bajty čtení z disku/s|Počet bajtů, které se za sekundu načtou z disku|Žádná prahová hodnota|Čítače využití disku mohou pomoci při řešení potíží s latencí úložiště.|
> |\Logický disk&#42;\Zápisy na disk/s|Rychlost provádění operací zápisu na disk|Žádná prahová hodnota|Čítače využití disku (mohou pomoci při řešení potíží s latencí úložiště)|
> |\Logický disk(&#42;)\Bajty zápisu na disk/s|Počet bajtů, které se za sekundu zapíší na disk|Žádná prahová hodnota|Čítače využití disku mohou pomoci při řešení potíží s latencí úložiště.|

## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

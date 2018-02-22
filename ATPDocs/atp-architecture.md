---
title: Architektura Azure Advanced Threat Protection | Microsoft Docs
description: Popisuje architekturu z Azure Advanced Threat Analytics (ATP)
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 09f82fa21bbaf61573b39fbe7a051db5c5e3b92a
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="azure-atp-architecture"></a>Azure ATP Architecture
Architektura Azure Advanced Threat Protection je znázorněna v tomto obrázku:

![Diagram topologie architektury služby Azure ATP](media/atp-architecture-topology.png)

Azure ATP monitoruje síťového provozu řadiče domény s využitím zrcadlení portů na senzor samostatné služby Azure ATP pomocí fyzických nebo virtuálních přepínačů. Pokud nasadíte senzoru Azure ATP přímo na řadiče domény, eliminuje požadavek pro zrcadlení portů. Kromě toho Azure ATP můžete využívat události systému Windows (předávaných přímo z řadičů domény nebo serveru SIEM) a analyzovat data související s útoky a hrozbami. Azure ATP přijímá analyzovaný provoz z Azure ATP samostatné senzor a senzor Azure ATP. Pomocí profilace, deterministické detekce, strojového učení a behaviorálních algoritmů pak poznává vaši síť, umožňuje detekovat anomálie a upozorňuje vás na podezřelé aktivity.

Tato část popisuje tok zaznamenávání událostí a síťových a prochází k podrobnému popisu funkce základních komponent ATP: senzor samostatné Azure ATP, Azure ATP senzor (což je stejné základní funkce jako samostatný senzoru Azure ATP), a cloudové služby Azure ATP. 

## <a name="azure-atp-components"></a>Azure ATP součásti
Azure ATP se skládá z následujících součástí:

-   **Azure portálu pro správu prostoru ATP** <br>
Portálu pro správu prostoru Azure ATP vám umožní vytvořit pracovních prostorů a umožňuje integraci s jinými službami Microsoftu.

> [!NOTE]
> Do jednoho pracovního prostoru může připojit pouze snímače z jedné doménové struktury služby Active Directory.

-   **Portál Azure prostoru ATP** <br>
Na portálu Azure ATP prostoru přijímá data z ATP senzory a senzory samostatné. Monitoruje, spravuje a prověří hrozeb ve vašem prostředí.

-   **Azure senzor ATP**<br>
Senzor Azure ATP se instaluje přímo na řadiče domény a monitoruje jejich provoz přímo, bez nutnosti využívat vyhrazený server nebo konfigurovat zrcadlení portů. 

-   Azure senzor samostatné ATP<br>
Senzor samostatné Azure ATP je nainstalován na vyhrazený server, který monitoruje provoz z řadičů domény pomocí zrcadlení portů nebo síťového ODPOSLOUCHÁVÁNÍ. Jde o alternativu k Azure ATP senzoru.

## <a name="deployment-options"></a>Možnosti nasazení
Můžete nasadit pomocí následující kombinace senzorů ATP Azure:

-   **Použití pouze Azure ATP senzorů**<br>
Nasazení Azure ATP může obsahovat pouze Azure ATP snímače: senzorů ATP Azure jsou nasazené na každém řadiči domény a žádné další servery nebo konfigurací zrcadlení portů je nezbytné.

-   **Použití pouze samostatné senzorů Azure ATP** <br>
Nasazení Azure ATP může obsahovat pouze senzorů Azure ATP samostatné, bez jakékoli Azure ATP snímače: všechny řadiče domény musí být nakonfigurované povolit zrcadlení portů pro služby Azure ATP samostatné senzor nebo síťové odposlouchávání musí být na místě.

-   **Pomocí Azure ATP samostatné senzory a Azure ATP senzorů**<br>
Nasazení Azure ATP zahrnuje Azure ATP samostatné senzory a snímače Azure ATP. Azure ATP snímače jsou nainstalovány na některém z řadičů domény (například všech řadičů v pobočkách). Ve stejnou dobu jsou ostatní řadiče domény monitorovat Azure ATP samostatné snímače (třeba větší řadiče domén ve vašich hlavních datových centrech).


### <a name="azure-atp-workspace-management-portal"></a>Azure portálu pro správu prostoru ATP

Portálu pro správu prostoru Azure ATP umožňuje:

-   Vytvoření a správa pracovních prostorů Azure ATP

-   Integrace s jinými službami zabezpečení Microsoftu

Nastavení pracovního prostoru hlavní jako **primární**. Pouze jednoho pracovního prostoru můžete nastavit jako primární. Nastavení pracovního prostoru jako primární účinky integrace - lze pouze integrovat Azure ATP s Windows Defender ATP vašeho primární pracovního prostoru. Můžete změnit, které pracovní prostor je primární později, ale aby bylo možné provést, budete muset odebrat všechny integrace pro aktuální primární pracovní prostor již nastaven.

### <a name="azure-atp-workspace-portal"></a>Portál Azure prostoru ATP

Pracovní prostor Azure ATP umožňuje spravovat následující funkce Azure ATP:

-   Správa nastavení konfigurace senzor Azure ATP pro senzor a samostatné

-   Zobrazení dat přijatých ze senzorů samostatné Azure ATP a Azure ATP snímače 

-   Monitorování zjistil podezřelých aktivit na základě behaviorální strojové učení algoritmy pro detekci neobvyklého chování a deterministické algoritmy pro detekci pokročilých útoků na základě v řetězu událostí útoku.

-   Volitelné: na portálu pro správu prostoru můžete nakonfigurovat na odesílání e-mailů a událostí při zjištění podezřelé aktivity nebo události stavu.


|||
|-|-|
|Příjem entit|Tato funkce přijímá dávky entit ze všech Azure ATP senzory a snímače samostatné Azure ATP.|
|Procesor síťové aktivity|Zpracovává všechny síťové aktivity v rámci každé přijaté dávky. Například přiřazování mezi různými kroky ověřování Kerberos prováděnými z potenciálně různých počítačů.|
|Profilování entit|Profiluje všechny jedinečné entity podle událostí a provozu. Například Azure ATP aktualizuje seznam přihlášených počítačů pro každý uživatelský profil.|
|Azure portálu pro správu prostoru ATP|Umožňuje spravovat pracovní prostory Azure ATP.|
|Portál Azure prostoru ATP|Prostoru Azure ATP slouží ke konfiguraci Azure ATP a monitorování podezřelých aktivit zjištěný Azure ATP ve vaší síti. Pracovní prostor Azure ATP není závislá na senzoru Azure ATP a spustí i v případě, že je služba Azure ATP senzor zastavená. |
|Detektory|Detektory pomocí algoritmů machine learningu a deterministických pravidel vyhledávají podezřelé aktivity a nestandardní chování uživatelů ve vaší síti.|

Při rozhodování o tom, kolik pracovních prostorů Azure ATP nasadit ve vaší síti, zvažte následující kritéria:

-   Jednoho pracovního prostoru Azure ATP můžete monitorovat jednu doménovou strukturu služby Active Directory. Pokud máte více než jedné doménové struktuře služby Active Directory, potřebujete minimálně jeden cloudové služby Azure ATP pro každou doménovou strukturu služby Active Directory.


## <a name="azure-atp-sensor-and-azure-atp-standalone-sensor"></a>Azure senzor ATP a senzor samostatné Azure ATP

**Azure ATP senzor** a **Azure ATP senzor** mají stejné základní funkce:

-   Zachytávají a prošetřují síťový provoz na řadiči domény. Toto je provoz prostřednictvím zrcadlení portů pro samostatné senzorů Azure ATP a místní provoz řadiče domény v Azure ATP senzorů. 

-   Přijímají události systému Windows přímo z řadičů domény (pro senzorů ATP) nebo ze serverů SIEM nebo Syslog (pro samostatnou senzorů ATP)

-  Zobrazí informace o monitorování účtů protokolu RADIUS od poskytovatele sítě VPN

-   Získávají data o uživatelích a počítačích z domény Active Directory.

-   Provádějí rozpoznání síťových entit (uživatelů, skupin a počítačů).

-   Přenášejí relevantní data do cloudové služby Azure ATP

-   Monitorování několika řadičů domény z jedné samostatné senzoru Azure ATP nebo monitorování jeden řadič domény pro senzor Azure ATP.

Senzor samostatné Azure ATP přijímá síťový provoz a události systému Windows ze sítě a zpracovává je v následujících hlavních komponentách:

|||
|-|-|
|Network Listener|Komponenta Network Listener zaznamená síťový provoz a analyzuje provoz. Toto je úloha procesoru náročné, takže je velmi důležité zkontrolovat [Azure ATP požadavky](atp-prerequisites.md) při plánování senzor Azure ATP nebo Azure ATP samostatné senzor.|
|Event Listener|Komponenta Event Listener shromažďuje a analyzuje události systému Windows předávaných ze serveru SIEM ve vaší síti.|
|Windows Event Log Reader|Windows Event Log Reader přečte a analyzuje události systému Windows předávaných do protokolu událostí Windows senzor samostatné Azure ATP z řadičů domény.|
|Network Activity Translator | Převádí analyzovaný síťový provoz na logickou reprezentaci provozu používanou v rámci Azure ATP (NetworkActivity).
|Entity Resolver|Komponenta Entity Resolver přebírá analyzovaná data (ze síťového provozu a z událostí) a přiřazuje jim data o účtech a identitách ze služby Active Directory. Výsledky jsou přiřazeny IP adresám nalezeným v analyzovaných datech. Entity Resolver efektivně kontroluje hlavičky paketů a umožňuje analýzou ověřovacích paketů získat názvy počítačů, vlastnosti a identity. Entity Resolver kombinuje analyzované ověřovací pakety s daty ve skutečných paketech.|
|Entity Sender|Komponenta Entity Sender odešle analyzovaných a přiřazených dat do cloudové služby Azure ATP.|

## <a name="azure-atp-sensor-features"></a>Funkce Azure senzor ATP

Následující funkce pracují různě v závislosti na tom, jestli používáte senzor samostatné Azure ATP nebo senzor Azure ATP.

-   Senzor Azure ATP může číst události místně, aniž by bylo nutné konfigurovat předávání událostí.

-   **Kandidát na synchronizátora domény**<br>
Kandidát na synchronizátora domény zodpovídá za proaktivní synchronizaci všech entity z konkrétní domény služby Active Directory (podobně jako tento mechanismus sami řadiče domén replikace). Jeden senzor se náhodně vybere ze seznamu kandidátů, která bude sloužit jako synchronizátor domény. <br><br>
Pokud je synchronizátor více než 30 minut offline, vybere se jiný kandidát. Pokud není k dispozici pro konkrétní doménu žádný synchronizátor domény, je Azure ATP proaktivně synchronizovat entity a jejich změny, ale Azure ATP načte nové entity, jako jsou zjištěna v monitorovaném provozu. 
<br>Pokud není dostupný žádný synchronizátor domény, a vyhledejte entita, která nemá žádnou komunikaci s ním souvisejí, se nezobrazí žádné výsledky hledání.<br><br>
Ve výchozím nastavení jsou všechny samostatné senzorů Azure ATP kandidáty na synchronizátora zařazené.<br><br>
Azure senzorů ATP nejsou kandidáty na synchronizátora zařazené ve výchozím nastavení.


-   **Omezení prostředků**<br>
Senzor Azure ATP zahrnuje monitorovací komponentu, která vyhodnotí dostupný paměťovou a výpočetní kapacitu na řadiči domény, na kterém je spuštěn. Proces monitorování spouští každých 10 sekund a dynamicky aktualizuje kvóty využití procesoru a paměti na procesu senzor Azure ATP, abyste měli jistotu, že v libovolném časovém okamžiku v čase, má řadič domény alespoň 15 % volných výpočetních a paměťových prostředků.<br><br>
Tento proces vždycky uvolní prostředky bez ohledu na to, co se na řadiči domény děje, aby se zajistilo jeho základní fungování.<br><br>
Pokud to způsobí, že Azure ATP senzoru dojdou prostředky, se monitoruje provoz jenom částečně a monitorování výstrahy "vyřazen provoz prostřednictvím zrcadlení portů sítě" se zobrazí na stránce stavu.

V následující tabulce je uvedený příklad řadiče domény s dostatečným objemem dostupných výpočetních prostředků pro povolení vyšší kvóty, než je aktuálně potřeba, takže se monitoruje veškerý provoz:

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Azure ATP senzor (Microsoft.Tri.sensor.exe)|Různé (ostatní procesy) |Azure ATP senzor kvóty|Zahazuje senzor provozu?|
|30%|20%|10%|45%|Ne|

Služby Active Directory potřebuje výpočetní výkon, sníží kvótu vyžaduje Azure ATP senzoru. V následujícím příkladu senzor ATP Azure potřebuje víc, než je přidělená kvóta a omezí některý provoz (monitoruje provoz jenom částečně):

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Azure ATP senzor (Microsoft.Tri.sensor.exe)|Různé (ostatní procesy) |Azure ATP senzor kvóty|Zahazuje senzor provozu?|
|60%|15%|10%|15%|Ano|


## <a name="your-network-components"></a>Komponenty vaší sítě
Chcete-li pracovat s Azure ATP, nezapomeňte zaškrtnout nastavit následující součásti.

### <a name="port-mirroring"></a>Zrcadlení portů
Pokud používáte Azure ATP samostatné senzorů, budete muset nastavit port zrcadlení pro řadiče domény, které se monitorují a nastavte senzoru samostatné Azure ATP jako cíl pomocí fyzických nebo virtuálních přepínačů. Další možností je použít síťové odposlouchávání. Azure ATP funguje v případě některých, ale ne všechny řadiče domény jsou monitorovány, ale detekce budou méně účinné.

Při zrcadlení portů zrcadlí všechny síťového provozu řadiče domény do Azure ATP samostatné senzoru, jen malá část tohoto objemu je pak pošle komprimován, do Azure ATP Cloudová služba pro analýzu.

Řadiče domény a senzory samostatné Azure ATP může být fyzické nebo virtuální. Další informace najdete v tématu [konfigurace zrcadlení portů](configure-port-mirroring.md).


### <a name="events"></a>Události
Pro zlepšení detekce Azure ATP Pass-the-Hash, útoků hrubou silou, změny citlivých skupin, vytváření služby podezřelé, úpravy, aby se pod těmito, Azure ATP vyžaduje následující události systému Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 a 7045. Tyto může buď přečíst automaticky senzoru Azure ATP nebo v případě, že Azure ATP senzoru není nasazený, můžete přesměrovávají na samostatné senzoru Azure ATP v jednom ze dvou způsobů, tím nakonfigurujete senzoru samostatné Azure ATP tak, aby naslouchala událostem SIEM nebo [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md).

-   Konfigurace senzoru samostatné Azure ATP tak, aby naslouchala událostem SIEM <br>Nakonfigurujte SIEM pro předávání určitých událostí systému Windows ATP. Azure ATP podporuje několik poskytovatelů SIEM. Další informace najdete v tématu [konfigurace předávání událostí](configure-event-forwarding.md).

-   Konfigurace předávání událostí systému Windows<br>Jiným způsobem, jak Azure ATP můžete získávat události, je konfigurace řadičů domény k předávání událostí systému Windows 4776, 4732, 4733, 4728, 4729, 4756, 4757 a 7045 na vaší samostatné senzor Azure ATP. To je obzvláště užitečné, pokud nemáte server SIEM, nebo pokud ATP není aktuálně podporovaná vašeho systému SIEM. Další informace o předávání událostí systému Windows v ATP najdete v tématu [předávání událostí systému Windows konfigurace](configure-event-forwarding.md). To platí jenom pro fyzické samostatný senzorů Azure ATP - nechcete senzoru Azure ATP.


## <a name="see-also"></a>Viz také
- [Požadavky Azure ATP](atp-prerequisites.md)
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/trisizingtool)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)

- - [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)

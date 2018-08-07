---
title: Architektura služby Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Popisuje architekturu z Azure Advanced Threat Analytics (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/05/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8264799f3aad2fb27287f56513458f34a3a7b0c6
ms.sourcegitcommit: 14c05a210ae92d35100c984ff8c6d171db7c3856
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2018
ms.locfileid: "39567640"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="azure-atp-architecture"></a>Architektura služby Azure ATP
Architektura služby Azure Advanced Threat Protection:

![Diagram topologie architektury Azure ATP](media/atp-architecture-topology.png)

Ochrana ATP v programu Azure monitoruje síťový provoz řadičů domény pomocí zrcadlení portů pro Azure ATP samostatný senzor pomocí fyzických nebo virtuálních přepínačů. Pokud provádíte nasazení senzoru služby Azure ATP přímo na řadiče domény, vyhnete se nutnosti zrcadlení portů. Ochrana ATP v programu Azure můžete navíc využít událostí Windows (předávaných přímo z řadičů domény nebo serveru SIEM) a analyzovat data útoky a hrozbami. Ochrana ATP v programu Azure přijímá analyzovaný provoz z ochrany ATP v programu Azure samostatný senzor a senzoru služby Azure ATP. Pomocí profilace, deterministické detekce, strojového učení a behaviorálních algoritmů pak poznává vaši síť, umožňuje detekovat anomálie a upozorňuje vás na podezřelé aktivity.

Tato část popisuje tok sítě a zaznamenávání událostí a operací k podrobnému popisu funkce základních komponent ochrany ATP v programu: ochrana ATP v programu Azure samostatný senzor, senzoru služby Azure ATP (který má stejné základní funkce jako samostatného senzoru služby Azure ATP), a cloudové službě ochrana ATP v programu Azure. 

Při instalaci přímo na řadiče domény, přistupuje k senzor požadované protokoly událostí přímo z řadiče domény. Po senzor mají být tyto protokoly a síťový provoz, ochrana ATP v programu Azure odesílá pouze tyto analyzované informace ke službě ochrana ATP v programu Azure (ne všechny protokoly).

## <a name="azure-atp-components"></a>Komponenty služby Azure ATP
Ochrana ATP v programu Azure se skládá z následujících součástí:

-   **Azure portálu pro správu pracovního prostoru ochrana ATP v programu** <br>
Na portálu pro správu pracovního prostoru ochrana ATP v programu Azure umožňuje vytvářet pracovní prostory a umožňuje integraci s jinými službami Microsoftu.

> [!NOTE]
> Do jednoho pracovního prostoru můžete připojit pouze senzorů z jedné doménové struktury služby Active Directory.

-   **Azure portal pracovní prostor ochrany ATP v programu** <br>
Na portálu ochrany ATP v programu Azure pracovní prostor přijímá data ze senzorů ochrany ATP v programu a samostatné senzorů. Monitoruje, spravuje a prověří hrozby ve vašem prostředí.

-   **Senzoru služby Azure ATP**<br>
Senzoru služby Azure ATP se instaluje přímo na řadičích domény a monitoruje jejich provoz přímo, bez nutnosti vyhrazený server nebo konfigurovat zrcadlení portů. 

-   **Azure ATP samostatný senzor**<br>
Ochrana ATP v programu Azure samostatný senzor je nainstalovaný na vyhrazený server, který monitoruje provoz z řadičů domény pomocí zrcadlení portů nebo síťového ODPOSLOUCHÁVÁNÍ. Jedná se o alternativu k senzoru služby Azure ATP.

## <a name="deployment-options"></a>Možnosti nasazení
Nasazením služby Azure ATP pomocí následující kombinace senzory:

-   **Použití pouze ochrany ATP v programu Azure senzorů**<br>
Nasazení služby Azure ATP může obsahovat pouze ochrany ATP v programu Azure senzory: senzorů The ochrany ATP v programu Azure jsou nasazené na každém řadiči domény a žádné další servery nebo je nutné konfiguraci zrcadlení portů.

-   **Použití pouze ochrany ATP v programu Azure samostatné senzorů** <br>
Nasazení služby Azure ATP může obsahovat pouze senzorů ochrany ATP v programu Azure samostatné, bez jakékoli služby Azure ATP senzory: všechny řadiče domény musí být nakonfigurované tak, aby povolovaly zrcadlení portů na Azure ATP samostatný senzor nebo síťové odposlouchávání musí být splněné.

-   **Pomocí ochrany ATP v programu Azure samostatné senzory a senzory ochrany ATP v programu Azure**<br>
Vaše nasazení služby Azure ATP obsahuje ochrany ATP v programu Azure samostatné senzory a senzory ochrany ATP v programu Azure. Ochrana ATP v programu Azure senzorů jsou nainstalované na některých řadičích domény (například všech řadičů v pobočkách). Ve stejnou dobu ostatní řadiče domény jsou monitorovaná senzorů samostatné ochrany ATP v programu Azure (třeba větší řadiče domény v hlavních datových centrech).


### <a name="azure-atp-workspace-management-portal"></a>Azure portálu pro správu pracovního prostoru ochrana ATP v programu

Na portálu pro správu pracovního prostoru ochrana ATP v programu Azure vám umožní:

-   Vytvoření a správa pracovních prostorů služby Azure ATP

-   Integrace s jinými službami zabezpečení Microsoftu

Nastavit jako váš hlavní pracovní prostor **primární**. Nastavení pracovního prostoru jako primární účinky integrace - můžete pouze integrovat služby Azure ATP ochrany ATP v programu Windows Defender pro vaši primární pracovní prostor. 

> [!NOTE]
> - Ochrana ATP v programu Azure aktuálně podporuje vytvoření jen jednoho pracovního prostoru. Po odstranění pracovního prostoru, budete kontaktovat podporu a znovu aktivujte ji. Může mít maximálně tři odstraněný pracovní prostory. Pokud chcete zvýšit počet pracovních prostorů uložené, odstraněné, obraťte se na podporu služby Azure ATP.
> - Pokud žádný senzor je nainstalovaný ve svém pracovním prostoru během 60 dnů, může dojít k odstranění pracovního prostoru a budete muset znovu vytvořit.



### <a name="azure-atp-workspace-portal"></a>Azure portal pracovní prostor ochrany ATP v programu

Pracovní prostor ochrany ATP v programu Azure umožňuje spravovat následující funkce ochrany ATP v programu Azure:

-   Spravovat nastavení konfigurace senzoru služby Azure ATP pro ze senzorů a samostatné

-   Zobrazení data přijatá ze senzorů samostatné ochrany ATP v programu Azure a služby Azure ATP senzorů 

-   Monitorování zjistila podezřelé aktivity na základě algoritmů behaviorální strojové učení a detekuje neobvyklé chování a deterministické algoritmy pro detekci pokročilých útoků podle řetězu událostí útoku.

-   Volitelné: na portálu pro správu pracovního prostoru můžete nakonfigurovat na odesílání e-mailů a událostí při zjištění podezřelé aktivity nebo události týkající se stavu.


|||
|-|-|
|Příjem entit|Tato funkce přijímá dávky entit ze všech ochrany ATP v programu Azure senzory a senzory samostatné ochrany ATP v programu Azure.|
|Procesor síťové aktivity|Zpracovává všechny síťové aktivity v rámci každé přijaté dávky. Například přiřazování mezi různými kroky ověřování Kerberos prováděnými z potenciálně různých počítačů.|
|Profilování entit|Profiluje všechny jedinečné entity podle událostí a provozu. Ochrana ATP v programu Azure například aktualizuje seznam přihlášených počítačů pro každý uživatelský profil.|
|Azure portálu pro správu pracovního prostoru ochrana ATP v programu|Slouží ke správě pracovních prostorů služby Azure ATP.|
|Azure portal pracovní prostor ochrany ATP v programu|Pracovní prostor ochrany ATP v programu Azure slouží ke konfiguraci ochrany ATP v programu Azure a monitorování podezřelých aktivit ve vaší síti zjištěno službou ochrany ATP v programu Azure. Pracovní prostor ochrany ATP v programu Azure není závislá na senzoru služby Azure ATP a běží i v případě, že je zastavena služba sensor ochrany ATP v programu Azure. |
|Detektory|Detektory pomocí algoritmů machine learningu a deterministických pravidel vyhledávají podezřelé aktivity a nestandardní chování uživatelů ve vaší síti.|

Při rozhodování o tom, kolik pracovních prostorů služby Azure ATP nasadit ve vaší síti, zvažte následující kritéria:

-   Jeden pracovní prostor služby Azure ATP můžete monitorovat jednu doménovou strukturu služby Active Directory. Pokud máte více než jednu doménovou strukturu služby Active Directory, budete potřebovat minimálně jedna Cloudová služba ochrany ATP v programu Azure pro každou doménovou strukturu služby Active Directory.


## <a name="azure-atp-sensor-and-azure-atp-standalone-sensor"></a>Azure senzor ochrany ATP v programu a samostatného senzoru služby Azure ATP

**Senzoru služby Azure ATP** a **samostatného senzoru služby Azure ATP** mají stejné základní funkce:

-   Zachytávají a prošetřují síťový provoz na řadiči domény. Toto je provoz prostřednictvím zrcadlení portů pro služby Azure ATP samostatné senzory a místní provoz řadiče domény v Azure ATP senzory. 

-   Příjem událostí Windows přímo z řadičů domény (pro senzory ochrany ATP v programu) nebo ze serverů SIEM nebo Syslog (pro samostatný senzory ochrany ATP v programu)

-   Zobrazí informace o monitorování účtů protokolu RADIUS od poskytovatele připojení VPN

-   Získávají data o uživatelích a počítačích z domény Active Directory.

-   Provádějí rozpoznání síťových entit (uživatelů, skupin a počítačů).

-   Přenášejí relevantní data do cloudové služby Azure ATP

-   Monitorování několika řadičů domény z jedné služby Azure ATP samostatný senzor, nebo monitorovat jeden řadič domény pro senzoru služby Azure ATP.

Ve výchozím nastavení ochrany ATP v programu Azure podporuje až 100 senzorů. Pokud chcete nainstalovat více, kontaktujte podporu služby Azure ATP.

Samostatný senzor ochrany ATP v programu Azure přijímá síťový provoz a události Windows ze sítě a zpracovává je v následujících hlavních komponentách:

|||
|-|-|
|Network Listener|Komponenta Network Listener zachytává síťový provoz a analyzuje provoz. Toto je úloha náročná na výkon procesoru, takže je velmi důležité zkontrolovat [požadavky ochrany ATP v programu Azure](atp-prerequisites.md) při plánování vaší ochrany ATP v programu Azure nebo samostatného senzoru služby Azure ATP.|
|Event Listener|Komponenta Event Listener zachytává a Parsuje události Windows, které jsou předávány ze serveru SIEM ve vaší síti.|
|Windows Event Log Reader|Windows Event Log Reader čte a Parsuje události Windows předávaných do protokolu událostí Windows samostatný senzor ochrany ATP v programu Azure z řadičů domény.|
|Network Activity Translator | Převádí analyzovaný síťový provoz na logickou reprezentaci provozu používanou v Azure ATP (NetworkActivity).
|Entity Resolver|Komponenta Entity Resolver přebírá analyzovaná data (ze síťového provozu a z událostí) a přiřazuje jim data o účtech a identitách ze služby Active Directory. Výsledky jsou přiřazeny IP adresám nalezeným v analyzovaných datech. Entity Resolver efektivně kontroluje hlavičky paketů a umožňuje analýzou ověřovacích paketů získat názvy počítačů, vlastnosti a identity. Entity Resolver kombinuje analyzované ověřovací pakety s daty ve skutečných paketech.|
|Entity Sender|Komponenta Entity Sender odesílá parsovaná a spárovaná data do cloudové služby Azure ATP.|

## <a name="azure-atp-sensor-features"></a>Funkce Azure senzor ochrany ATP v programu

Následující funkce pracují různě v závislosti na tom, jestli používáte Azure ATP samostatný senzor nebo senzoru služby Azure ATP.

-   Senzoru služby Azure ATP můžete číst události místně bez nutnosti konfigurace předávání událostí.

-   **Kandidát na synchronizátora domény**<br>
Kandidát na synchronizátora domény zodpovídá za proaktivní synchronizaci všech entity z konkrétní domény služby Active Directory (podobně jako mechanismu, který používá sami řadiče domény pro replikaci). Jeden senzor se náhodně vybere ze seznamu kandidátů, která bude sloužit jako synchronizátor domény. <br><br>
Pokud je synchronizátor více než 30 minut offline, vybere se jiný kandidát. Pokud není k dispozici pro konkrétní doménu žádný synchronizátor domény, je ochrana ATP v programu Azure nemůže proaktivně synchronizovat entity a jejich změny, ale ochrany ATP v programu Azure načte nové entity, jako jsou zjištěna v monitorovaném provozu. 
<br>Pokud není dostupný žádný synchronizátor domény a hledáte entitu, která nemá žádný provoz s ní spojené, se nezobrazí žádné výsledky hledání.<br><br>
Ve výchozím nastavení jsou kandidátem na synchronizátora všechny senzory samostatné ochrany ATP v programu Azure.<br><br>
Azure senzorů ochrany ATP v programu nejsou kandidáti na synchronizátora ve výchozím nastavení.


-   **Omezení prostředků**<br>
Senzoru služby Azure ATP zahrnuje monitorovací komponentu, která vyhodnotí dostupnou kapacitu výpočetní a paměťové prostředky na řadiči domény, na kterém je spuštěný. Proces monitorování spouští každých 10 sekund a dynamicky aktualizuje kvóty využití procesoru a paměti v procesu ochrany ATP v programu Azure ze senzorů a ujistěte se, že v libovolném časovém okamžiku v čase, obsahuje řadič domény alespoň 15 % volných výpočetních a paměťových prostředků.<br><br>
Tento proces vždycky uvolní prostředky bez ohledu na to, co se na řadiči domény děje, aby se zajistilo jeho základní fungování.<br><br>
Pokud to způsobí, že se senzoru služby Azure ATP dojdou prostředky, se monitoruje provoz jenom částečně a monitorování výstrahy "zrušenou provoz prostřednictvím zrcadlení portů sítě" se zobrazí na stránce stavu.

V následující tabulce je uvedený příklad řadiče domény s dostatečným objemem dostupných výpočetních prostředků pro povolení vyšší kvóty, než je aktuálně potřeba, takže se monitoruje veškerý provoz:

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Senzor ochrany ATP v programu Azure (Microsoft.Tri.sensor.exe)|Různé (ostatní procesy) |Azure senzor kvóta ochrany ATP v programu|Senzor zahazuje provozu?|
|30%|20%|10%|45%|Ne|

Pokud služby Active Directory potřebuje další výpočetní výkon, kvóta vyžadovaná komponentou senzoru služby Azure ATP se snižuje. V následujícím příkladu senzoru služby Azure ATP potřebuje víc, než je přidělená kvóta a omezí některý provoz (monitoruje provoz jenom částečně):

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Senzor ochrany ATP v programu Azure (Microsoft.Tri.sensor.exe)|Různé (ostatní procesy) |Azure senzor kvóta ochrany ATP v programu|Senzor zahazuje provozu?|
|60%|15%|10%|15%|Ano|


## <a name="your-network-components"></a>Komponenty vaší sítě
Ověřte, že následující komponenty jsou nastavena, chcete-li pracovat s Azure ATP.

### <a name="port-mirroring"></a>Zrcadlení portů
Pokud použijete samostatný senzorů ochrany ATP v programu Azure, budete muset nastavit port zrcadlení pro řadiče domény, které se monitorují a nastavit samostatný senzor ochrany ATP v programu Azure jako cíle pomocí fyzických nebo virtuálních přepínačů. Další možností je použít síťové odposlouchávání. Ochrana ATP v programu Azure funguje v případě některých, ale ne všechny řadiče domény jsou monitorované, ale detekce budou méně účinné.

Při zrcadlení portů odráží všechny sítě provozu na řadiči domény do služby Azure ATP samostatný senzor, jenom malá část tohoto objemu je pak odeslat, v komprimovaném tvaru do služby Azure ATP Cloudová služba pro analýzy.

Řadiče domény a senzory samostatné ochrany ATP v programu Azure můžou být fyzické nebo virtuální. Další informace najdete v tématu [konfigurace zrcadlení portů](configure-port-mirroring.md).


### <a name="events"></a>Události
Pro zlepšení detekce ochrany ATP v programu Azure Pass-the-Hash, útoky hrubou silou, úpravy citlivých skupin, vytváření podezřelé služeb, změny Honeytokenů, ochrana ATP v programu Azure potřebuje následující události Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 a 7045. Ty můžete buď automaticky číst senzoru služby Azure ATP nebo v případě, že není nasazený senzoru služby Azure ATP, může být přeposílán do samostatného senzoru služby Azure ATP v jednom ze dvou způsobů, tím nakonfigurujete samostatný senzor ochrany ATP v programu Azure tak, aby naslouchala událostem SIEM nebo [Konfigurace předávání událostí Windows](configure-event-forwarding.md).

-   Konfigurace ochrany ATP v programu Azure samostatný senzor tak, aby naslouchala událostem SIEM <br>Nakonfigurujte svou správu SIEM pro předávání určitých událostí Windows ochrany ATP v programu. Ochrana ATP v programu Azure podporuje několik poskytovatelů siem. Další informace najdete v tématu [konfigurace předávání událostí](configure-event-forwarding.md).

-   Konfigurace předávání událostí systému Windows<br>Jiným způsobem, jak služby Azure ATP můžete získávat události, je konfigurace řadičů domén tak, aby předával události Windows 4776, 4732, 4733, 4728, 4729, 4756, 4757 a 7045 na váš samostatný senzor ochrany ATP v programu Azure. To je zvlášť užitečné, pokud nemáte server SIEM nebo systému SIEM se aktuálně nepodporují ochrany ATP v programu. Další informace o předávání událostí Windows v ochrany ATP v programu najdete v tématu [předávání událostí Windows konfigurace](configure-event-forwarding.md). Platí jen pro fyzické samostatný senzorů ochrany ATP v programu Azure - nechcete senzoru služby Azure ATP.


## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/trisizingtool)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)

- - [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)

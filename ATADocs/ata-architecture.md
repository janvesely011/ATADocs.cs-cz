---
title: Architektura Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisu architektury Microsoft Advanced Threat Analytics (ATA)
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 8/26/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f4ab67f48eded7a612dfea4cefefdfe8529800d0
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077809"
---
# <a name="ata-architecture"></a>Architektura ATA

*Platí pro: Advanced Threat Analytics verze 1.9*

Architektura Microsoft Advanced Threat Analytics je znázorněna v tomto obrázku:

![Diagram topologie architektury ATA](media/ATA-architecture-topology.jpg)

ATA monitoruje síťový provoz řadičů domény pomocí zrcadlení portů na komponentě ATA Gateway s využitím fyzických nebo virtuálních přepínačů. Pokud přímo na řadiče domény nasadíte ATA Lightweight Gateway, vyhnete se nutnosti zrcadlení portů. ATA navíc dokáže využívat události systému Windows (předávané přímo z řadičů domény nebo serveru SIEM) a analyzovat data související s útoky a hrozbami.
Tato část popisuje tok zaznamenávání událostí a síťových operací a zaměřuje se na funkčnost základních komponent ATA: ATA Gateway, ATA Lightweight Gateway (má stejné základní funkce jako ATA Gateway) a ATA Center.


![Diagram toku dat v architektuře ATA](media/ATA-traffic-flow.jpg)

## <a name="ata-components"></a>Komponenty ATA
Součástí ATA jsou následující komponenty:

-   **ATA Center** <br>
ATA Center přijímá data ze všech komponent ATA Gateway a ATA Lightweight Gateway, které nasadíte.
-   **ATA Gateway**<br>
ATA Gateway se instaluje na vyhrazený server, který monitoruje provoz z řadičů domény pomocí zrcadlení portů nebo síťového odposlouchávání.
-   **ATA Lightweight Gateway**<br>
ATA Lightweight Gateway se instaluje přímo na řadiče domény a monitoruje jejich provoz přímo, bez nutnosti využívat vyhrazený server nebo konfigurovat zrcadlení portů. Představuje alternativu k ATA Gateway.

Nasazení ATA se může skládat z jediné komponenty ATA Center připojené ke všem komponentám ATA Gateway, všem komponentám ATA Lightweight Gateway nebo ke kombinaci komponent ATA Gateway a ATA Lightweight Gateway.


## <a name="deployment-options"></a>Možnosti nasazení
ATA můžete nasadit s využitím následující kombinace bran:

-   **Jenom komponenty ATA Gateway** <br>
Nasazení ATA může obsahovat jen komponenty ATA Gateway, bez jakékoli komponenty ATA Lightweight Gateway: Všechny řadiče domény musí být nakonfigurované tak, aby povolovaly zrcadlení portů na ATA Gateway nebo síťové odposlouchávání musí být splněné.
-   **Jenom komponenty ATA Lightweight Gateway**<br>
Nasazení ATA může obsahovat jen komponenty ATA Lightweight Gateway: ATA Lightweight Gateway jsou nasazené na každém řadiči domény a žádné další servery nebo je nutné konfiguraci zrcadlení portů.
-   **Komponenty ATA Gateway i ATA Lightweight**<br>
Nasazení ATA obsahuje jak komponenty ATA Gateway, tak ATA Lightweight Gateway. Komponenty ATA Lightweight Gateway jsou nainstalované na některých řadičích domény (například na všech řadičích domény v pobočkách). Jiné řadiče domény jsou zároveň monitorované komponentami ATA Gateway (například větší řadiče domény v hlavních datových centrech).

Ve všech těchto scénářích odesílají všechny brány data do ATA Center.




## <a name="ata-center"></a>ATA Center
**ATA Center** zajišťuje následující funkce:

-   Spravuje konfiguraci komponent ATA Gateway a ATA Lightweight Gateway.

-   Přijímá data od komponent ATA Gateway a ATA Lightweight Gateway. 

-   Detekuje podezřelé aktivity.

-   Spouští algoritmy ATA pro behaviorální machine learning a detekuje neobvyklé chování.

-   Spouští různé deterministické algoritmy pro detekci pokročilých útoků na základě řetězu událostí útoku.

-   Spouští konzolu ATA.

-   Volitelné: Komponenty ATA Center můžete nakonfigurovat na odesílání e-mailů a událostí, když zjistí podezřelou aktivitu.

ATA Center přijímá parsovaný provoz z komponent ATA Gateway a ATA Lightweight Gateway. Pomocí profilace, deterministické detekce, strojového učení a behaviorálních algoritmů pak poznává vaši síť, umožňuje detekovat anomálie a upozorňuje vás na podezřelé aktivity.

|||
|-|-|
|Příjem entit|Přijímá dávky entit ze všech komponent ATA Gateway a ATA Lightweight Gateway.|
|Procesor síťové aktivity|Zpracovává všechny síťové aktivity v rámci každé přijaté dávky. Například přiřazování mezi různými kroky ověřování Kerberos prováděnými z potenciálně různých počítačů.|
|Profilování entit|Profiluje všechny jedinečné entity podle událostí a provozu. ATA například aktualizuje seznam přihlášených počítačů pro každý uživatelský profil.|
|Databáze komponenty Center|Spravuje proces zápisu síťových aktivit a událostí do databáze. |
|Databáze|ATA využívá pro ukládání všech dat databázi MongoDB:<br /><br />-   Síťové aktivity<br />-   Aktivity událostí<br />-   Jedinečné entity<br />-   Podezřelé aktivity<br />-   Konfigurace ATA|
|Detektory|Detektory pomocí algoritmů machine learningu a deterministických pravidel vyhledávají podezřelé aktivity a nestandardní chování uživatelů ve vaší síti.|
|Konzola ATA|Konzola ATA slouží ke konfiguraci řešení ATA a monitorování podezřelých aktivit, které ATA detekuje ve vaší síti. Konzola ATA není závislá na službě ATA Center a běží i v případě, že je tato služba zastavená, dokud může komunikovat s databází.|

Při úvahách o tom, kolik komponent ATA Center nasadit ve vaší síti, zvažte následující kritéria:

-   Jedna komponenta ATA Center může monitorovat jednu doménovou strukturu služby Active Directory. Pokud máte více než jednu doménovou strukturu služby Active Directory, potřebujete minimálně jednu komponentu ATA Center na každou doménovou strukturu.

-    V rozsáhlých nasazeních služby Active Directory nemusí být jedna komponenta ATA Center schopná zpracovat veškerý síťový provoz na řadičích domény. V takovém případě se vyžaduje několik komponent ATA Center. Počet komponent ATA Center závisí na [plánování kapacity ATA](ata-capacity-planning.md).

## <a name="ata-gateway-and-ata-lightweight-gateway"></a>ATA Gateway a ATA Lightweight Gateway

### <a name="gateway-core-functionality"></a>Základní funkce brány
**ATA Gateway** a **ATA Lightweight Gateway** mají stejné základní funkce:

-   Zachytávají a prošetřují síťový provoz na řadiči domény. Jedná se o provoz komponent ATA Gateway zrcadlený na portech a místní provoz řadiče domény na komponentách ATA Lightweight Gateway. 

-   Přijímají události systému Windows ze serverů SIEM nebo syslog, případně z řadičů domény prostřednictvím předávání událostí systému Windows.

-   Získávají data o uživatelích a počítačích z domény Active Directory.

-   Provádějí rozpoznání síťových entit (uživatelů, skupin a počítačů).

-   Přenášejí relevantní data do komponenty ATA Center.

-   Monitorují několik řadičů domény z jedné komponenty ATA Gateway nebo jeden řadič domény (ATA Lightweight Gateway).

Komponenta ATA Gateway přijímá síťový provoz a události systému Windows ze sítě a zpracovává je v následujících hlavních komponentách:

|||
|-|-|
|Network Listener|Network Listener zachytává a parsuje síťový provoz. Tato úloha je náročná na výkon procesoru. Proto je při plánování nasazení komponenty ATA Gateway nebo ATA Lightweight Gateway velmi důležité zkontrolovat [požadavky ATA](ata-prerequisites.md).|
|Event Listener|Event Listener zachytává a parsuje události Windows, které server SIEM předává do vaší sítě.|
|Windows Event Log Reader|Windows Event Log Reader čte a parsuje události Windows, které řadiče domény předávají protokolu událostí Windows komponenty ATA Gateway.|
|Network Activity Translator | Převádí analyzovaný síťový provoz na logickou reprezentaci provozu používanou v rámci ATA (NetworkActivity).
|Entity Resolver|Komponenta Entity Resolver přebírá analyzovaná data (ze síťového provozu a z událostí) a přiřazuje jim data o účtech a identitách ze služby Active Directory. Výsledky jsou přiřazeny IP adresám nalezeným v analyzovaných datech. Entity Resolver efektivně kontroluje hlavičky paketů a umožňuje analýzou ověřovacích paketů získat názvy počítačů, vlastnosti a identity. Entity Resolver kombinuje analyzované ověřovací pakety s daty ve skutečných paketech.|
|Entity Sender|Entity Sender odesílá parsovaná a spárovaná data do ATA Center.|

## <a name="ata-lightweight-gateway-features"></a>Funkce komponenty ATA Lightweight Gateway

Následující funkce pracují různě v závislosti na tom, jestli používáte ATA Gateway nebo ATA Lightweight Gateway.

-   ATA Lightweight Gateway dokáže číst události místně bez nutnosti konfigurace předávání událostí.

-   **Kandidát na synchronizátora domény**<br>
Brána synchronizátora domény zodpovídá za proaktivní synchronizaci všech entity z konkrétní domény služby Active Directory (je obdobou mechanismu, který samotné domény využívají k replikaci). Ze seznamu kandidátů se náhodně vybere jedna brána, která bude sloužit jako synchronizátor domény. <br><br>
Pokud je synchronizátor více než 30 minut offline, vybere se jiný kandidát. Pokud není k dispozici pro konkrétní doménu žádný synchronizátor domény, je ATA nemůže proaktivně synchronizovat entity a jejich změny, ale ATA bude reaktivně načítat nové entity, jako jsou zjištěna v monitorovaném provozu. 
<br>Pokud není dostupný žádný synchronizátor domény a hledáte entitu, která nemá žádný provoz s ní spojené, se nezobrazí žádné výsledky hledání.<br><br>
Ve výchozím nastavení jsou kandidátem na synchronizátora všechny komponenty ATA Gateway.<br><br>
Protože komponenty ATA Lightweight Gateway se nejčastěji nasazují na pobočkách a malých řadičích domén, nejsou ve výchozím nastavení mezi kandidáty na synchronizátora zařazené.


-   **Omezení prostředků**<br>
ATA Lightweight Gateway zahrnuje monitorovací komponentu, která vyhodnotí dostupnou kapacitu výpočetní a paměťové prostředky na řadiči domény, na kterém je spuštěný. Tento monitorovací proces se spouští každých 10 sekund a dynamicky aktualizuje kvóty využití procesoru a paměti v procesu ATA Lightweight Gateway. Cílem je zajistit, aby v libovolném časovém okamžiku měl řadič domény alespoň 15 % volných výpočetních a paměťových prostředků.<br><br>
Tento proces vždycky uvolní prostředky bez ohledu na to, co se na řadiči domény děje, aby se zajistilo jeho základní fungování.<br><br>
Pokud to způsobí, že ATA Lightweight Gateway dojdou prostředky, se monitoruje provoz jenom částečně a monitorování výstrahy "zrušenou provoz prostřednictvím zrcadlení portů sítě" se zobrazí na stránce stavu.

V následující tabulce je uvedený příklad řadiče domény s dostatečným objemem dostupných výpočetních prostředků pro povolení vyšší kvóty, než je aktuálně potřeba, takže se monitoruje veškerý provoz:

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA Lightweight Gateway (Microsoft.Tri.Gateway.exe)|Různé (ostatní procesy) |Kvóta pro ATA Lightweight Gateway|Omezení brány|
|30%|20%|10%|45%|Ne|

Pokud Active Directory potřebuje víc výpočetních prostředků, kvóta vyžadovaná komponentou ATA Lightweight Gateway se sníží. V následujícím příkladu ATA Lightweight Gateway potřebuje víc, než je přidělená kvóta, a omezí některý provoz (monitoruje provoz jenom částečně):

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA Lightweight Gateway (Microsoft.Tri.Gateway.exe)|Různé (ostatní procesy) |Kvóta pro ATA Lightweight Gateway|Omezení brány|
|60%|15%|10%|15%|Ano|


## <a name="your-network-components"></a>Komponenty vaší sítě
Aby bylo možné pracovat se službou ATA, ujistěte se, že chcete zkontrolovat, že následující komponenty jsou nastaveny.

### <a name="port-mirroring"></a>Zrcadlení portů
Pokud používáte komponenty ATA Gateway, musíte nastavit zrcadlení portů pro řadiče domény, které se monitorují a jako cíl pomocí fyzických nebo virtuálních přepínačů nastavit ATA Gateway. Další možností je použít síťové odposlouchávání. ATA funguje v případě některých, ale ne všechny řadiče domény jsou monitorované, ale detekce budou méně účinné.

Při zrcadlení portů zrcadlí veškerý síťový provoz řadičů domény do komponenty ATA Gateway, jenom malá část tohoto objemu je pak odešlou, v komprimovaném tvaru komponentě ATA Center k analýze.

Řadiče domény a komponenty ATA Gateway můžou být fyzické i virtuální. Další informace najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md).


### <a name="events"></a>Události
K vylepšení detekce útoků typu Pass-the-Hash, útoky hrubou silou, úpravy citlivých skupin a Honeytokenů potřebuje ATA následující události Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757. Tyto události buď může automaticky číst ATA Lightweight Gateway, nebo mohou být jedním ze dvou způsobů předávány komponentě ATA Gateway (v případě, že komponenta ATA Lightweight Gateway není nasazená), a to konfigurací komponenty ATA Gateway pro naslouchání událostem SIEM, nebo [konfigurací předávání událostí Windows](configure-event-collection.md).

-   Konfigurace komponenty ATA Gateway pro naslouchání událostem SIEM <br>Nakonfigurujte SIEM pro předávání určitých událostí systému Windows bráně ATA Gateway. ATA podporuje několik poskytovatelů SIEM. Další informace najdete v tématu [Konfigurace sběru událostí](configure-event-collection.md).

-   Konfigurace předávání událostí systému Windows<br>Jiným způsobem, jak může ATA získávat události, je konfigurace řadičů domén tak, aby předával události Windows 4776, 4732, 4733, 4728, 4729, 4756 a 4757 komponentě ATA Gateway. To je obzvláště užitečné, pokud nemáte server SIEM nebo pokud ATA váš server SIEM v současnosti nepodporuje. K dokončení vaší konfigurace předávání událostí Windows v ATA najdete v článku [předávání událostí Windows konfigurace](configure-event-collection.md). Platí jen pro fyzické komponenty ATA Gateway, nikoli pro ATA Lightweight Gateway.

## <a name="related-videos"></a>Související videa
- [Volba správného typu komponenty ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)


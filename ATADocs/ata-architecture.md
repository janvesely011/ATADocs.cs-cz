---
title: Architektura Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisu architektury Microsoft Advanced Threat Analytics (ATA)
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/08/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 9579108bd0bb2fa91e2e196ab90284f396025db1
ms.sourcegitcommit: e4f108aec3cbfd88562217e36195b5d1250a1bbd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2019
ms.locfileid: "70803105"
---
# <a name="ata-architecture"></a>Architektura ATA

*Platí pro: Advanced Threat Analytics verze 1,9*

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
Nasazení ATA může obsahovat jenom komponenty ATA Gateway bez komponent ATA Lightweight Gateway: Všechny řadiče domény musí být nakonfigurované tak, aby umožňovaly zrcadlení portů na ATA Gateway, nebo musí být nastavené síťové kohouty.
-   **Jenom komponenty ATA Lightweight Gateway**<br>
Nasazení ATA může obsahovat jenom komponenty ATA Lightweight Gateway: Komponenty ATA Lightweight Gateway jsou nasazené na každém řadiči domény a nejsou potřeba žádné další servery ani konfigurace zrcadlení portů.
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

-   Volitelné: ATA Center se dá nakonfigurovat tak, aby odesílala e-maily a události při zjištění podezřelé aktivity.

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

-    V rozsáhlých nasazeních služby Active Directory nemusí být jedna komponenta ATA Center schopná zpracovat veškerý provoz všech řadičů domény. V takovém případě se vyžaduje několik komponent ATA Center. Počet komponent ATA Center závisí na [plánování kapacity ATA](ata-capacity-planning.md).

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
Pokud je synchronizátor více než 30 minut offline, vybere se jiný kandidát. Pokud není k dispozici žádný kandidát na synchronizátor domény pro konkrétní doménu, ATA proaktivně synchronizuje entity a jejich změny, ale ATA znovu aktivuje nové entity, když se zjistí v monitorovaném provozu. 
<br>Pokud není k dispozici žádný synchronizátor domény, bude hledání entity bez provozu, který je s ním spojený, zobrazovat žádné výsledky.<br><br>
Ve výchozím nastavení jsou všechny komponenty ATA Gateway kandidáty na synchronizátory domén.<br><br>
Protože komponenty ATA Lightweight Gateway se nejčastěji nasazují na pobočkách a malých řadičích domén, nejsou ve výchozím nastavení mezi kandidáty na synchronizátora zařazené. <br><br>V prostředí jenom s odlehčenými branami se doporučuje přiřadit dvě brány jako kandidáti na synchronizátor, kde jedna odlehčená brána je výchozím kandidátem pro synchronizátor a druhá je záloha pro případ, že výchozí hodnota je offline déle než 30. minuty. 


-   **Omezení prostředků**<br>
ATA Lightweight Gateway obsahuje monitorovací součást, která vyhodnocuje dostupnou výpočetní a paměťovou kapacitu na řadiči domény, na kterém běží. Tento monitorovací proces se spouští každých 10 sekund a dynamicky aktualizuje kvóty využití procesoru a paměti v procesu ATA Lightweight Gateway. Cílem je zajistit, aby v libovolném časovém okamžiku měl řadič domény alespoň 15 % volných výpočetních a paměťových prostředků.<br><br>
Tento proces vždycky uvolní prostředky bez ohledu na to, co se na řadiči domény děje, aby se zajistilo jeho základní fungování.<br><br>
Pokud to způsobí, že ATA Lightweight Gateway vyčerpá prostředky, monitoruje se jenom částečný provoz a na stránce stav se zobrazí výstraha monitorování "vynechané síťové přenosy se zrcadlením portů".

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
Aby bylo možné pracovat s ATA, zkontrolujte, zda jsou nastaveny následující komponenty.

### <a name="port-mirroring"></a>Zrcadlení portů
Pokud používáte komponenty ATA Gateway, musíte nastavit zrcadlení portů pro řadiče domény, které jsou monitorované, a nastavit ATA Gateway jako cíl pomocí fyzických nebo virtuálních přepínačů. Další možností je použít síťové odposlouchávání. ATA funguje, pokud se monitorují některé, ale ne všechny řadiče domény, ale detekce jsou méně efektivní.

Přestože zrcadlení portů odráží všechny síťové přenosy řadiče domény do komponenty ATA Gateway, pošle se do komponenty ATA Center za účelem analýzy jenom malé procento tohoto přenosu dat, které se pak komprimuje.

Řadiče domény a komponenty ATA Gateway můžou být fyzické i virtuální. Další informace najdete v tématu [Konfigurace zrcadlení portů](configure-port-mirroring.md).


### <a name="events"></a>Duration
K vylepšení detekce ATA-the-hash, hrubou silou, úpravám citlivých skupin a tokenů medu potřebuje ATA následující události systému Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757. Tyto události buď může automaticky číst ATA Lightweight Gateway, nebo mohou být jedním ze dvou způsobů předávány komponentě ATA Gateway (v případě, že komponenta ATA Lightweight Gateway není nasazená), a to konfigurací komponenty ATA Gateway pro naslouchání událostem SIEM, nebo [konfigurací předávání událostí Windows](configure-event-collection.md).

-   Konfigurace komponenty ATA Gateway pro naslouchání událostem SIEM <br>Nakonfigurujte SIEM pro předávání určitých událostí systému Windows bráně ATA Gateway. ATA podporuje několik poskytovatelů SIEM. Další informace najdete v tématu [Konfigurace sběru událostí](configure-event-collection.md).

-   Konfigurace předávání událostí systému Windows<br>Další způsob, jakým může ATA získat vaše události, je konfigurace řadičů domény pro přeposílání událostí Windows 4776, 4732, 4733, 4728, 4729, 4756 a 4757 do komponenty ATA Gateway. To je obzvláště užitečné, pokud nemáte server SIEM nebo pokud ATA váš server SIEM v současnosti nepodporuje. Postup dokončení konfigurace předávání událostí systému Windows v ATA najdete v tématu [konfigurace předávání událostí systému Windows](configure-event-collection.md). To platí jenom pro fyzické komponenty ATA Gateway – ne pro ATA Lightweight Gateway.

## <a name="related-videos"></a>Související videa
- [Výběr správného typu ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Nástroj pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)


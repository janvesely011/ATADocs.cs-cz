---
# required metadata

title: Architektura ATA | Microsoft Advanced Threat Analytics
description: Popisu architektury Microsoft Advanced Threat Analytics (ATA)
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Architektura ATA
Architektura Microsoft Advanced Threat Analytics je znázorněna v tomto obrázku:

![Diagram topologie architektury ATA](media/ATA-architecture-topology.jpg)

ATA monitoruje síťový provoz na řadičích domény. Využívá přitom zrcadlení portů na ATA Gateway pomocí fyzických nebo virtuálních přepínačů, nebo nasazení ATA Lightweight Gateway přímo na řadiče domény (v takovém případě není zrcadlení portů potřeba). ATA navíc dokáže využívat události systému Windows (předávané přímo z řadičů domény nebo serveru SIEM) a analyzovat data související s útoky a hrozbami.
Tato část popisuje tok zaznamenávání událostí a síťových operací a prochází k podrobnému popisu funkce základních komponent řešení ATA: ATA Gateway, ATA Lightweight Gateway (má stejné základní funkce jako ATA Gateway) a ATA Center.


![Diagram toku dat v architektuře ATA](media/ATA-traffic-flow.jpg)

## Komponenty ATA
ATA se skládá z následujících komponent:

-   **ATA Center** <br>
ATA Center přijímá data ze všech komponent ATA Gateway a ATA Lightweight Gateway, které nasadíte.
-   **ATA Gateway**<br>
ATA Gateway se instaluje na vyhrazený server, který monitoruje provoz z řadičů domény pomocí zrcadlení portů nebo síťového odposlouchávání.
-   **ATA Lightweight Gateway**<br>
ATA Lightweight Gateway se instaluje přímo na řadiče domény a monitoruje jejich provoz přímo, bez nutnosti využívat vyhrazený server nebo konfigurovat zrcadlení portů. Představuje alternativu k ATA Gateway.

Nasazení ATA se může skládat z jedné komponenty ATA Center připojené ke všem komponentám ATA Gateway, všem komponentám ATA Lightweight Gateway nebo ke kombinaci komponent ATA Gateway a ATA Lightweight Gateway.


## Možnosti nasazení
ATA můžete nasadit s využitím následující kombinace bran:

-   **Jenom komponenty ATA Gateway** <br>
Pokud nasazení ATA obsahuje jenom komponenty ATA Gateway (a žádné komponenty ATA Lightweight Gateway), musí být všechny řadiče domény nakonfigurované tak, aby povolovaly zrcadlení portů na ATA Gateway, nebo musí být nastavené síťové odposlouchávání.
-   **Jenom komponenty ATA Lightweight Gateway**<br>
Pokud nasazení ATA obsahuje jenom komponenty ATA Lightweight Gateway, jsou nasazené na každém řadiči domény a nejsou potřeba žádné další servery ani konfigurace zrcadlení portů.
-   **Komponenty ATA Gateway i ATA Lightweight**<br>
Pokud nasazení ATA obsahuje komponenty ATA Gateway i ATA Lightweight Gateway, komponenta ATA Lightweight Gateway je nainstalovaná na některých řadičích domény (třeba na všech řadičích domény na pobočkách), zatímco ostatní řadiče domény jsou monitorované prostřednictvím komponent ATA Gateway (třeba větší řadiče domén ve vašich hlavních datových centrech).

Ve všech třech scénářích všechny brány odesílají data do ATA Center.




## ATA Center
**ATA Center** zajišťuje následující funkce:

-   Spravuje konfiguraci komponent ATA Gateway a ATA Lightweight Gateway.

-   Přijímá data od komponent ATA Gateway a ATA Lightweight Gateway. 

-   Detekuje podezřelé aktivity.

-   Spouští algoritmy ATA pro behaviorální machine learning a detekuje neobvyklé chování.

-   Spouští různé deterministické algoritmy pro detekci pokročilých útoků na základě řetězu událostí útoku.

-   Spouští konzolu ATA.

-   Volitelné: ATA Center můžete nakonfigurovat pro odesílání e-mailů a událostí při zjištění podezřelé aktivity.

ATA Center přijímá analyzovaný provoz z komponent ATA Gateway a ATA Lightweight Gateway, provádí profilování, spouští deterministickou detekci, machine learning a behaviorální algoritmy s cílem zjistit informace o vaší síti a umožnit tak detekci anomálií a varovat před podezřelými aktivitami.

|||
|-|-|
|Příjem entit|Tato funkce přijímá dávky entit ze všech komponent ATA Gateway a ATA Lightweight Gateway.|
|Procesor síťové aktivity|Zpracovává všechny síťové aktivity v rámci každé přijaté dávky. Například přiřazování mezi různými kroky ověřování Kerberos prováděnými z potenciálně různých počítačů.|
|Profilování entit|Profiluje všechny jedinečné entity podle událostí a provozu. Zde například ATA aktualizuje seznam přihlášených počítačů pro každý uživatelský profil.|
|Databáze komponenty Center|Spravuje proces zápisu síťových aktivit a událostí do databáze. |
|Databáze|ATA využívá pro ukládání všech dat databázi MongoDB:<br /><br />-   Síťové aktivity<br />-   Aktivity událostí<br />-   Jedinečné entity<br />-   Podezřelé aktivity<br />-   Konfigurace ATA|
|Detektory|Detektory pomocí algoritmů machine learningu a deterministických pravidel vyhledávají podezřelé aktivity a nestandardní chování uživatelů ve vaší síti.|
|Konzola ATA|Konzola ATA slouží ke konfiguraci řešení ATA a monitorování podezřelých aktivit, které ATA detekuje ve vaší síti. Konzola ATA není závislá na komponentě ATA Center a poběží i v případě, že je služba zastavená. Jedinou podmínkou je možnost komunikace s databází.|
Při úvahách o tom, kolik komponent ATA Center nasadit ve vaší síti, zvažte následující:

-   Jedna komponenta ATA Center může monitorovat jednu doménovou strukturu služby Active Directory. Pokud máte více než jednu doménovou strukturu služby Active Directory, budete potřebovat minimálně jednu komponentu ATA Center na každou doménovou strukturu.

-    Ve velmi rozsáhlých nasazeních služby Active Directory nemusí být jedna komponenta ATA Center schopná zpracovat veškerý síťový provoz na řadičích domény. V takovém případě je potřeba použít několik komponent ATA Center. Počet komponent ATA Center závisí na [plánování kapacity ATA](ata-capacity-planning.md).

## ATA Gateway a ATA Lightweight Gateway

### Základní funkce brány
**ATA Gateway** a **ATA Lightweight Gateway** mají stejné základní funkce:

-   Zachytávají a kontrolují síťový provoz na řadiči domény (v případě ATA Gateway provoz prostřednictvím zrcadlení portů a v případě ATA Lightweight Gateway místní provoz na řadiči domény). 

-   Přijímají události systému Windows ze serverů SIEM nebo syslog, případně z řadičů domény prostřednictvím předávání událostí systému Windows.

-   Získávají data o uživatelích a počítačích z domény Active Directory.

-   Provádějí překlad síťových entit (uživatelů, skupin a počítačů).

-   Přenášejí relevantní data do komponenty ATA Center.

-   Monitorují několik řadičů domény z jedné komponenty ATA Gateway nebo jeden řadič domény (ATA Lightweight Gateway).

Komponenta ATA Gateway přijímá síťový provoz a události systému Windows ze sítě a zpracovává je v následujících hlavních komponentách:

|||
|-|-|
|Network Listener|Komponenta Network Listener je odpovědná za zachytávání síťového provozu a jeho analýzu. Tato úloha je náročná na výkon procesoru. Proto je při plánování nasazení komponenty ATA Gateway nebo ATA Lightweight Gateway velmi důležité zkontrolovat [požadavky ATA](ata-prerequisites.md).|
|Event Listener|Komponenta Event Listener je odpovědná za zaznamenávání a analýzu událostí systému Windows předávaných ze serveru SIEM ve vaší síti.|
|Windows Event Log Reader|Komponenta Windows Event Log Reader odpovídá za čtení a analýzu událostí systému Windows předávaných do protokolu událostí komponenty ATA Gateway z řadičů domény.|
|Network Activity Translator | Převádí analyzovaný síťový provoz na logickou reprezentaci provozu používanou v rámci ATA (NetworkActivity).
|Entity Resolver|Komponenta Entity Resolver přebírá analyzovaná data (ze síťového provozu a z událostí) a přiřazuje jim data o účtech a identitách ze služby Active Directory. Výsledky jsou přiřazeny IP adresám nalezeným v analyzovaných datech. Entity Resolver efektivně kontroluje hlavičky paketů a umožňuje analýzou ověřovacích paketů získat názvy počítačů, vlastnosti a identity. Entity Resolver kombinuje analyzované ověřovací pakety s daty ve skutečných paketech.|
|Entity Sender|Komponenta Entity Sender je odpovědná za zasílání analyzovaných a přiřazených dat do komponenty ATA Center.|

## Funkce komponenty ATA Lightweight Gateway

Následující funkce pracují různě v závislosti na tom, jestli používáte ATA Gateway nebo ATA Lightweight Gateway.

-   **Kandidát na synchronizátora domény**<br>
Brána synchronizátora domény zodpovídá za proaktivní synchronizaci všech entity z konkrétní domény služby Active Directory (je obdobou mechanismu, který samotné domény využívají k replikaci). Ze seznamu kandidátů se náhodně vybere jedna brána, která bude sloužit jako synchronizátor domény. <br><br>
Pokud je synchronizátor více než 30 minut offline, vybere se jiný kandidát. Pokud pro konkrétní doménu není dostupný žádný synchronizátor domény, ATA nemůže proaktivně synchronizovat entity a jejich změny, bude ale reaktivně načítat nové entity, když se v monitorovaném provozu detekují. 
<br>Pokud není dostupný žádný synchronizátor domény a hledáte entitu, se kterou nesouvisí žádný provoz, nezobrazí se žádné výsledky hledání.<br><br>
Ve výchozím nastavení jsou kandidátem na synchronizátora všechny komponenty ATA Gateway.<br><br>
Protože komponenty ATA Lightweight Gateway se nejčastěji nasazují na pobočkách a malých řadičích domén, nejsou ve výchozím nastavení mezi kandidáty na synchronizátora zařazené.


-   **Omezení prostředků**<br>
ATA Lightweight Gateway zahrnuje monitorovací komponentu, která vyhodnotí dostupnou paměťovou a výpočetní kapacitu na řadiči domény, na kterém je spuštěná. Tento monitorovací proces se spouští každých 10 sekund a dynamicky aktualizuje kvóty využití procesoru a paměti v procesu ATA Lightweight Gateway. Cílem je zajistit, aby v libovolném časovém okamžiku měl řadič domény alespoň 15 % volných výpočetních a paměťových prostředků.<br><br>
Tento proces vždycky uvolní prostředky bez ohledu na to, co se na řadiči domény děje, aby se zajistilo jeho základní fungování.<br><br>
Pokud následkem toho komponentě ATA Lightweight Gateway dojdou prostředky, provoz se monitoruje jenom částečně a na stavové stránce se zobrazí monitorovací výstraha typu Omezení síťového provozu se zrcadlením portů.

V následující tabulce je uvedený příklad řadiče domény s dostatečným objemem dostupných výpočetních prostředků pro povolení vyšší kvóty, než je aktuálně potřeba, takže se monitoruje veškerý provoz:

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA Lightweight Gateway (Microsoft.Tri.Gateway.exe)|Různé (ostatní procesy) |Kvóta pro ATA Lightweight Gateway|Omezení brány|
|30 %|20 %|10 %|45 %|Ne|

Pokud Active Directory potřebuje víc výpočetních prostředků, kvóta vyžadovaná komponentou ATA Lightweight Gateway se sníží. V následujícím příkladu ATA Lightweight Gateway potřebuje víc, než je přidělená kvóta, a omezí některý provoz (monitoruje provoz jenom částečně):

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA Lightweight Gateway (Microsoft.Tri.Gateway.exe)|Různé (ostatní procesy) |Kvóta pro ATA Lightweight Gateway|Omezení brány|
|60 %|15 %|10 %|15 %|Ano|



## Komponenty vaší sítě
Před použitím řešení ATA zkontrolujte následující skutečnosti:

### Zrcadlení portů
Pokud používáte komponenty ATA Gateway, musíte nastavit zrcadlení portů pro řadiče domén, které se budou monitorovat, a pomocí fyzických nebo virtuálních přepínačů nastavit ATA Gateway jako cíl. Další možností je použít síťové odposlouchávání. Pokud se monitorují jenom některé řadiče domény (ale ne všechny), ATA bude fungovat, ale detekce budou méně účinné.

Při zrcadlení portů sice řadič domény zrcadlí veškerý síťový provoz na komponentu ATA Gateway, ale jen velmi malá část tohoto objemu je pak v komprimovaném tvaru odeslána komponentě ATA Center k analýze.

Řadiče domény a komponenty ATA Gateway můžou být fyzické i virtuální. Další informace najdete v tématu [Konfigurace zrcadlení portů](/advanced-threat-analytics/deploy-use/configure-port-mirroring).


### Události
Pro zlepšení detekce útoků typu pass-the-hash, útoků hrubou silou a účtů ve funkci návnady (honeytoken) ATA potřebuje získávat události systému Windows s ID 4776. Ten může být přeposílán komponentě ATA Gateway jedním ze dvou způsobů, buď konfigurací komponenty ATA Gateway tak, aby naslouchala událostem SIEM, nebo pomocí předávání událostí systému Windows.

-   Konfigurace komponenty ATA Gateway pro naslouchání událostem SIEM <br>Nakonfigurujte SIEM pro předávání určitých událostí systému Windows bráně ATA Gateway. ATA podporuje několik poskytovatelů SIEM. Další informace najdete v tématu [Konfigurace sběru událostí](/advanced-threat-analytics/deploy-use/configure-event-collection).

-   Konfigurace předávání událostí systému Windows<br>Jiným způsobem, jak může ATA získávat události, je konfigurace řadičů domén tak, aby předávaly událost systému Windows s ID 4776 komponentě ATA Gateway. To je obzvláště užitečné, pokud nemáte server SIEM nebo pokud ATA váš server SIEM v současnosti nepodporuje. Další informace o předávání událostí systému Windows v ATA najdete v tématu [Konfigurace předávání událostí systému Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding).

## Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace sběru událostí](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurace předávání událostí systému Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=Jun16_HO1-->



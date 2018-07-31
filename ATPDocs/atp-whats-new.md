---
title: Co je nového v ochraně ATP v Azure | Dokumentace Microsoftu
description: Popisuje nejnovější verze ochrany ATP v programu Azure a poskytuje informace o novinkách v jednotlivých verzích.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/29/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ebdae7617dd550631186ab87cba922758649fd45
ms.sourcegitcommit: 759e99f670c42c2dd60d07b2200d3de01ddf6055
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/30/2018
ms.locfileid: "39335975"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="whats-new-in-azure-atp"></a>Co je nového v Azure ATP 

## <a name="azure-atp-release-242"></a>Verze ochrany ATP v programu Azure 2,42

Vydáno 29. července 2018

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 


## <a name="azure-atp-release-241"></a>Verze ochrany ATP v programu Azure 2.41

Vydáno 22. července 2018

- **Podpora více doménovými strukturami Azure ochrany ATP v programu je postupně zavádí (preview)** <br> Ochrana ATP v programu Azure teď můžete podpořit organizace s víc doménovými strukturami, které poskytuje možnost monitorování aktivity a profily uživatelů napříč doménovými strukturami. Tato nová funkce umožňuje:

  - Zobrazení a prošetřování aktivity prováděné uživateli napříč více doménovými strukturami z podokně ze skla.
  - Zlepšuje detekci a omezuje počet falešně pozitivních výsledků tím, že poskytuje pokročilé integrace služby Active Directory a účet řešení.
  - Získejte lepší výstrah monitorování a vytváření sestav pro pokrytí napříč organizací.


-   **Nové detekce: DCShadow**<br>Dvě nové detekce byly přidány k ochraně před útoky stínové (DCShadow) řadiče domény:

    -   Povýšení řadiče domény podezřelé (možný útok DCShadow) – tato detekce pomáhá detekovat útoky, ve kterých zosobnit počítače s řadičem domény a pak se pokusí použít replikační změny do ostatních řadičů domény ve vaší doméně.

    -   Podezřelá žádost o replikaci (možný útok DCShadow) – tato detekce, které pomáhá chránit proti útokům, které se pokusil o provedení povýšení řadiče domény z počítačů, které nejsou řadiče domény chcete-li změnit adresářových objektů.

-   **Vylepšené informace oslabení šifrování**<br>Šifrování downgrade detekce nyní poskytuje další informace týkající se konkrétního typu útoku zjistil: overpass-the-hash, zlatý lístek a typu skeleton key. Tyto výstrahy navíc mají byl agregován umožňující snadnější šetření.
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 



## <a name="azure-atp-release-240"></a>Verze ochrany ATP v programu Azure 2,40

Vydáno 15. července 2018

- Detekce pass-the-ticket nyní obsahuje oddíl důkazy na stránce podrobností výstrahy. To poskytuje další informace k prošetření upozornění.

- Příznaky ovládacích prvků přístup uživatele, které najdete v profilu uživatele v adresáři data, nyní obsahují legendu, takže můžete líp pochopit, které atributy jsou a které jsou vypnuté.  

## <a name="azure-atp-release-239"></a>Verze ochrany ATP v programu Azure 2.39

Vydané 5. července 2018
-   **Přidat nové detekce: Kerberos golden ticket - neexistující účet** (preview)<br>Toto nové zjišťování pomáhá chránit vaši organizaci před útoky, ve kterých je vytvořen zlatý lístek Kerberos účtu, který neexistuje ve vaší doméně. Další informace najdete v tématu [Průvodce prošetřováním podezřelých aktivit rozšířené ochrany před internetovými útoky pro Azure](suspicious-activity-guide.md#golden-ticket)

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 


## <a name="azure-atp-release-238"></a>Verze ochrany ATP v programu Azure 2,38

Vydáno 1. července 2018

- Tato verze obsahuje opravy a vylepšení pro více problémů a také vylepšení ochrany ATP v programu Azure portal.

## <a name="azure-atp-release-237"></a>Verze ochrany ATP v programu Azure 2.37

Vydáno 24. června 2018

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 

## <a name="azure-atp-release-236"></a>Verze ochrany ATP v programu Azure hodnotu 2,36

Vydáno 17. června 2018

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 


## <a name="azure-atp-release-235"></a>Verze ochrany ATP v programu Azure 2.35

Vydáno 10. června 2018
 
- **Nové ve verzi preview detekce**<br></br>Z nichž lze dodat nové funkce v nyní, bude ochrana ATP v programu Azure využít výhod skutečnost, že je Cloudová služba – rychlá cykly – a poskytneme vám nové detekce nejkratší možné době. Tyto nové detekce byla označená jako "preview" při prvním vydání. Obvykle nové detekce se přesune z verze preview pro obecnou dostupnost během pár týdnů. Ve výchozím nastavení se zobrazí náhled detekcí. Informace o vyjádří svůj nesouhlas najdete v tématu [ve verzi preview detekce](working-with-suspicious-activities.md#preview-detections).
 
- **Podezřelé zjišťování sítě VPN**<br></br>Tato verze přináší předběžnou verzi detekce podezřelých VPN. Ochrana ATP v programu Azure učí chování uživatele sítě VPN, včetně počítačů, uživatelů přihlášených k a umístění, které uživatelé připojit z a vás upozorní, když je odchylky od očekávané chování. Další informace najdete v tématu [detekce podezřelých VPN](suspicious-activity-guide.md#suspicious-vpn-detection).

- **Zpožděné aktualizace**<br></br>Teď máte možnost nastavit ochrana ATP v programu Azure snímačů a aktualizovat později pokaždé, když aktualizace ochrany ATP v programu Azure. Teď můžete nastavit každou senzoru služby Azure ATP **zpožděné aktualizace** tak, aby se aktualizuje po 24 hodinách od aktualizace ochrany ATP v programu Azure cloud service. Tato funkce umožňuje otestovat aktualizaci na konkrétní testovací senzorů a aktualizovat vaše produkční senzorů pouze později. Pokud během první cyklu aktualizací zjistíte problém, otevřete lístek podpory. Další informace najdete v části [ochrany ATP v programu Azure aktualizace senzorů](sensor-update.md).

- **Implementace zjišťování aktualizované neobvyklý protokol**<br></br>Neobvyklý protokol implementace detekce nyní poskytuje další informace. Můžete teď najdete v tématu, které potenciál útoku podezření nástroj ochrany ATP v programu Azure je v práci v síti. Další informace najdete v tématu [Průvodce prošetřováním podezřelých aktivit](suspicious-activity-guide.md).
 
- **Výstraha zastaralé senzor**<br></br>Ochrana ATP v programu Azure zahrnuje nové monitorování výstrahy dali vám vědět, pokud je senzoru více než tři verze zastaralé. Pokud se zobrazí toto upozornění, by měl aktualizovat senzoru nebo prozkoumat, proč se senzor neaktualizují automaticky. Pokud výstrahy se opakuje, odinstalujte a znovu nainstalujte senzoru.

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 

## <a name="azure-atp-release-234"></a>Verze ochrany ATP v programu Azure 2.34

Vydáno 3. června 2018
 
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 

 
## <a name="azure-atp-release-233"></a>Verze ochrany ATP v programu Azure 2,33

Vydáno 27. května 2018

- Funkce ve verzi Preview: ochrana ATP v programu Azure teď podporuje nové jazyky a 13 nové národní prostředí:
    - Čeština
    - Maďarština
    - Italština
    - Korejština
    - Holandština
    - Polština
    - Portugalština (Brazílie)
    - Portugalština (Portugalsko)
    - Rusko
    - Švédština
    - Turečtina
    - Čínština (Čína)
    - Čínština (Tchaj-wan)



## <a name="azure-atp-release-232"></a>Verze ochrany ATP v programu Azure 2.32

Vydáno 13. května 2018
 
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 

## <a name="azure-atp-release-231"></a>Verze ochrany ATP v programu Azure 2.31

Vydáno 6. května 2018
 
- Byly vylepšeny překlad názvů. V rámci tohoto úsilí, kromě aktivního řešení RPC a NetBIOS senzor vydat paket TLS klienta Hello na koncový bod protokolu RDP (3389) portu. 
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 

## <a name="azure-atp-release-230"></a>Verze ochrany ATP v programu Azure 2,30

Vydáno 29. dubna 2018
 
- Podezřelé aktivity oslabení šifrování teď obsahují důkazy oddílu, který popisuje příznaky detekovaných službou ochrany ATP v programu Azure, které ji podezření, že, k čemu aktivita oslabení šifrování. 
-   Ochrana ATP v programu Azure nyní používá Azure Email Orchestrator pro všechny e-mailů z ochrany ATP v programu Azure, včetně podezřelých aktivit monitorování výstrah a sestav. Uvidíte, že tato e-mailová oznámení teď řídí konzistentní formát pro snadné použití a Excelové soubory se propojí s e-mailu ke stažení z konzoly.
 
 

## <a name="azure-atp-release-229"></a>Verze ochrany ATP v programu Azure 2.29

Vydáno 22. dubna 2018
 
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 
 
 
## <a name="azure-atp-release-228"></a>Verze ochrany ATP v programu Azure 2.28

Vydáno 15. dubna 2018
 
-   Uživatelé, kteří jsou členy skupin rolí uživatelů ochrany ATP v programu Azure a prohlížeče ochrany ATP v programu Azure teď mají oprávnění k zobrazení výstrah monitorování.
- Tato verze obsahuje opravy a vylepšení pro několik problémů. 


## <a name="azure-atp-release-227"></a>Verze ochrany ATP v programu Azure 2,27

Vydáno 8. dubna 2018

- Nyní máte možnost k poskytnutí zpětné vazby uživatelů v horním navigačním panelu. Kliknutím na ikonu veselého obličeje v panelu nabídky vám umožní odesílat e-mailu týmu rozšířené ochrany před internetovými útoky pro Azure s vaším názorem.

- Tato verze obsahuje opravy a vylepšení pro několik problémů. 
 

## <a name="azure-atp-release-226"></a>Verze ochrany ATP v programu Azure 2.26

Vydáno 25. března 2018

- Až ochrany ATP v programu Azure upozorňuje vás na podezřelé aktivity, které identifikují jako neškodné pozitivní (legitimní akci, která není podezřelé aktivity), budete mít možnost vyloučit počítače a IP adresy pro další způsoby detekce, včetně: oslabení šifrování, LDAP Útok hrubou silou, podobě zfalšovaných certifikátů PAC, útoky hrubou silou a Pass-the-hash.
-   Byl vylepšen výkon senzoru služby Azure ATP.
-   Nové oblasti pro nasazení pracovního prostoru, přidala se teď můžete nasadit pracovní prostor v Asii. 


## <a name="azure-atp-release-225"></a>Verze ochrany ATP v programu Azure 2.25

Vydáno 18. března 2018

- Vícefaktorové ověřování (MFA) je nyní podporována v ochrany ATP v programu Azure. Tenanty používající MFA nyní můžete zadat na portálu ochrany ATP v programu Azure.
- Ochrana ATP v programu Azure teď má [ **stav systému** ](https://health.atp.azure.com/) stránku, kde přinášejí informace o tom, zda na portálu pro správu pracovního prostoru je aplikace bude aktivní, pokud dojde k problémům s detekcí a senzor je možné odeslat přenosy dat do cloudu. Můžete přistupovat **stav systému** z řádku nabídek služby Azure ATP.


## <a name="azure-atp-release-224"></a>Verze ochrany ATP v programu Azure 2,24

Vydáno 11. března 2018

**Nové a aktualizované detekce**
  - Podezřelé vytvoření služby – útočníci se pokusí spustit podezřelé služby ve vaší síti. Ochrana ATP v programu Azure nyní vydá výstrahu, když zjistí, že někdo v určitém počítači běží novou službu, která se zdá podezřelá. Tato detekce se zakládá na událostech (ne přenosy v síti) a je na všech řadičích domény v síti, které je předávání událostí 7045 do služby Azure ATP. Další informace najdete v článku [Průvodce prošetřováním podezřelých aktivit](suspicious-activity-guide.md).

**Vylepšené šetření**
  - Ochrana ATP v programu Azure zahrnuje bohatších možností [profil entity](entity-profiles.md). Profil entity poskytuje platformu, která je navržená pro podrobné informace o zkoumání aktivity uživatelů, jedná se o prostředky, které k nim přistupovat, počítače, které jsou přihlášeni a mnoho dalších. Profil entity také poskytuje data adresáře a umožní vám identifikovat potenciální cesty taktiky Lateral Movement do nebo z entity, můžete získat další informace o potenciálním porušením ve vaší organizaci.

  - Ochrana ATP v programu můžete ručně značka entity jako *citlivé* k vylepšení detekce a sledování. Toto značení ovlivňuje mnoho detekce ochrany ATP v programu Azure, jako je například detekci úprav citlivých skupin a [cesty laterální pohyb](use-case-lateral-movement-path.md), které využívají entity, které se považují za citlivé.

**Nové sestavy, které pomáhají s prošetřením**
  - [Hesla přístupný ve formátu prostého textu sestavy](reports.md) umožňuje rozpoznat, kdy se služby odeslat přihlašovací údaje k účtu se odesílají v prostém textu. To umožňuje prozkoumat služby a zvýšit úroveň zabezpečení sítě. Tato sestava nahradí výstrahy podezřelá aktivita ve formě prostého textu.
  - [Laterální cesty Lateral Movement k citlivým účtům sestavě](reports.md) obsahuje citlivé účty, které jsou zveřejňovány prostřednictvím cesty taktiky Lateral Movement. To umožňuje zmírnit tyto cesty a posilovat jejich zabezpečení sítě s cílem minimalizovat riziko útoku povrchu. To vám umožňuje zabránit taktiky Lateral Movement tak, aby útočníci nelze přesouvat mezi vaší sítě mezi uživatelé a počítače služby, dokud se přístupů v loterii zabezpečení virtuálních: přihlašovací údaje účtu správce citlivé.

- Můžete teď snadno poskytnout přístup k dokumentaci z odkazu v rámci upozornění na podezřelou aktivitu Chcete-li zobrazit [šetření kroky, které můžete provést](suspicious-activity-guide.md). 

**Vylepšení výkonu**
 -  Senzor infrastruktury služby Azure ATP byla vylepšena z hlediska výkonu: agregovaná zobrazení provozu povolí optimalizaci CPU a paketů kanálu a opětovně používá sockets k řadičům domény, chcete-li minimalizovat relace protokolu SSL řadiči domény.

## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
---
# required metadata

title: Co je Microsoft Advanced Threat Analytics (ATA)? | Microsoft Advanced Threat Analytics
description: Popisuje řešení Microsoft Advanced Threat Analytics (ATA) a jaké druhy podezřelých aktivit může zjistit.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


## Co je ATA?
Microsoft Advanced Threat Analytics (ATA) je špičkové řešení analýz EUBA (User and Entity Behavioral Analytics), které si klade za cíl pomáhat IT specialistům na zabezpečení při ochraně organizací před pokročilými cílenými útoky (APT) i vnitřními hrozbami. ATA pomocí pokročilé technologie machine learningu automaticky analyzuje a rozpoznává běžné a neobvyklé chování entit (uživatelů, zařízení a prostředků) a učí se. Díky tomu pomáhá rozpoznat známé nebezpečné útoky a techniky, problémy zabezpečení a rizika. S použitím znalostí a zkušeností v oblasti bezpečnosti na světové úrovni se tato inovativní technologie zaměřuje na odhalování bezpečnostních hrozeb dřív, než způsobí nějaké škody.

## Co ATA dělá?
ATA detekuje:

  - Pokročilé trvalé hrozby (APT), a to na samém počátku procesu, kdy ještě nemohou způsobit škody

  - Vnitřní hrozby

ATA pomáhá rozpoznat skutečně podezřelé aktivity a zaměřit se na to, co je opravdu důležité.

Detekční modul ATA využívá machine learning, důkladnou kontrolu paketů na základě kontextu jednotlivých entit, analýzy protokolů a informace ze služby Active Directory (AD) k analýze chování uživatelů a dalších entit.

ATA do hloubky analyzuje síťový provoz ve vaší organizaci a pomocí machine learningu vytváří mapu normálních aktivit, provozu a používání prostředků ve vaší organizaci. Poté ATA všechno jen tiše sleduje a upozorní vás, když se objeví něco nestandardního. To všechno je možné díky technologii hloubkové kontroly paketů společnosti Microsoft (DPI), která díky znalosti kontextu jednotlivých entit umožňuje analyzovat síťový provoz do větší hloubky a poskytuje řešení ATA možnost analyzovat všechny úrovně síťového prostředí.

ATA shromažďuje také informace o relevantních událostech ze systémů SIEM a z řadičů domény. Po dokončení analýzy ATA vytvoří dynamické a průběžně aktualizované zobrazení všech osob, zařízení a prostředků v organizaci. Pomocí tohoto komplexního zobrazení dokáže ATA detekovat známé nebezpečné útoky, například typu pass-the hash, pass-the-ticket, rekognoskace a další, a taky hledat abnormality v chování entit ve vaší síti.

Jakmile se detekuje podezřelá aktivita, ATA vydá výstrahu. Pomocí pokročilých algoritmů pro agregaci a kontextové ověřování současně minimalizuje počet falešně pozitivních výstrah.



## Jaké hrozby ATA vyhledává?

ATA zajišťuje detekci pro následující fáze pokročilých útoků: rekognoskace, únik přihlašovacích údajů, laterální pohyb, zvýšení úrovně oprávnění, dominance v doméně a další. Tyto detekce jsou zaměřené na zjišťování pokročilých útoků a vnitřních hrozeb ještě předtím, než mohou ve vaší organizaci způsobit škody.

Výsledkem detekce v jednotlivých fázích je několik podezřelých aktivit relevantních pro danou fázi. Každá podezřelá aktivita je v korelaci s různými charakteristikami možných útoků.

### Rekognoskace
ATA poskytuje několik způsobů detekce rekognoskace. Mezi tyto detekce patří:

-   **Rekognoskace pomocí zjišťování účtů**<br>Upozorní na pokusy útočníků použít protokol Kerberos ke zjištění existence určitých uživatelů, a to i v případě, že se tato aktivita neobjeví v protokolech na řadiči domény.
-   **Výčet síťových relací**<br>
V rámci fáze rekognoskace se útočníci mohou dotazovat řadiče domény na všechny aktivní relace SMB na serveru, což jim umožní získat přístup ke všem IP adresám a uživatelům, kteří jsou k těmto relacím SMB přidružení. Výčet relací SMB potom útočníci mohou využít k cílení na citlivé účty a následně k laterálnímu pohybu napříč sítí.
-   **Rekognoskace pomocí DNS**<br>
Informace DNS v cílové síti jsou pro rekognoskaci často velmi užitečné. Informace DNS obsahují seznam všech serverů a často i všech klientů a mapování na příslušné IP adresy. Zobrazení informací DNS může útočníkům poskytnout podrobný přehled o těchto entitách ve vašem prostředí, což jim umožní zaměřit úsilí na entity, které jsou pro jejich kampaň relevantní.

### Prozrazené přihlašovací údaje

K detekci prozrazených přihlašovacích údajů ATA využívá analýzu chování na základě machine learningu a také rozpoznání známých útoků a technik.

Pomocí analýzy chování a machine learningu ATA dokáže detekovat podezřelé aktivity, jako jsou neobvyklá přihlášení, nestandardní přístup k prostředkům a přístup mimo běžnou pracovní dobu, což by mohlo ukazovat na únik přihlašovacích údajů.
Pro ochranu proti zneužití přihlašovacích údajů rozpoznává ATA následující známé útoky a techniky:

 - **:** <br>Hrubá síla Při útoku hrubou silou se útočníci snaží uhodnout přihlašovací údaje uživatelů zkoušením kombinací běžných jmen a hesel.

- **Útočníci často používají složité algoritmy nebo slovníky, aby vyzkoušeli tolik kombinací, kolik jim systém dovolí.**<br>
Zpřístupnění citlivých účtů v prostém textu

- **Pokud se přihlašovací údaje k účtům s vysokými oprávněními odešlou v prostém textu, ATA vám doporučí aktualizovat konfiguraci počítače.** <br>
Služba zpřístupňující účty v prostém textu

- **Pokud služba na počítači odesílá přihlašovací údaje k několika účtům v prostém textu, ATA vám doporučí aktualizovat konfiguraci této služby.**<br>
Podezřelé aktivity účtu sloužícího jako návnada (honeytoken) Účty ve funkci návnady (honeytoken) jsou fiktivní účty nastavené tak, aby přitahovaly, identifikovaly a sledovaly podezřelé aktivity, které se je pokusí využít.
-   **ATA vás upozorní na jakékoli činnosti probíhající pod těmito účty.**<br>
Neobvyklá implementace protokolu Požadavky na ověření (Kerberos nebo NTLM) se obvykle zpracovávají pomocí normální sady metod a protokolů. K zajištění úspěšného ověření ale stačí, aby požadavek splňoval konkrétní sadu požadavků. Útočníci mohou implementovat tyto protokoly s malými odchylkami od normální implementace v daném prostředí.
-   **Tyto odchylky mohou signalizovat přítomnost útočníka, který se pokouší využít nebo už úspěšně využívá prozrazené přihlašovací údaje.**<br>
Škodlivý požadavek na soukromé informace přes Data Protection Data Protection API (DPAPI) je služba ochrany dat založená na heslech. Tuto službu ochrany používají různé aplikace, které ukládají tajné údaje uživatelů, jako jsou hesla k webům a přihlašovací údaje ke sdíleným složkám. Při ztrátě hesla mohou uživatelé dešifrovat chráněná data pomocí obnovovacího klíče, který nezahrnuje jejich heslo.
-   **V doménovém prostředí útočníci mohou vzdáleně ukrást obnovovací klíč a použít ho k dešifrování chráněných dat ve všech počítačích připojených k doméně.**<br>
Neobvyklé chování V případě vnitřních hrozeb a pokročilých útoků se často k podvodnému získání přihlašovacích údajů k účtům využívají techniky sociálního inženýrství nebo zcela nové a dosud neznámé metody a techniky.

### Díky tomu, že ATA analyzuje chování entit, detekuje případné abnormality v operacích, které tyto entity provádějí, a upozorňuje na ně, dokáže tyto typy ohrožení detekovat.
Laterální pohyb

K detekci laterálního pohybu, při němž uživatelé zneužijí přihlašovací údaje k získání přístupu k prostředkům, ke kterým přístup mít nemají, ATA využívá analýzy chování využívající machine learning a také rozpoznání známých škodlivých útoků a technik.

Pomocí analýzy chování a machine learningu ATA dokáže detekovat nestandardní přístup k prostředkům, nestandardní využití zařízení a další indikátory, které by mohly ukazovat na únik přihlašovacích údajů.

- **Kromě toho ATA k rozpoznání laterálního pohybu využívá detekci technik, které při laterálním pohybu používají útočníci, například:** <br>
Pass-the-ticket
- **Při útoku typu pass-the-ticket útočník získá lístek Kerberos z jednoho počítače a použije ho k získání přístupu k jinému počítači tak, že předstírá identitu některé entity v síti.** <br>
Pass-the-hash
- **Při útoku typu pass-the-hash útočník odcizí hodnotu hash NTML entity a použije ji k ověření prostřednictvím NTLM, k předstírání identity dané entity a k přístupu k prostředkům v síti.**<br>
Over-pass-the-hash
-   **Útoky over-pass-the-hash spočívají v použití odcizené hodnoty hash NTLM k ověření prostřednictvím protokolu Kerberos a k získání platného lístku TGT Kerberos. Tento lístek se pak použije k ověření uživatele jako platného a k získání přístupu k prostředkům v síti.**<br>
Neobvyklé chování Laterální pohyb je technika, kterou útočníci často používají k pohybu mezi zařízeními a oblastmi v napadené síti a získání přístupu k privilegovaným přihlašovacím údajům nebo citlivým informacím, které je zajímají.

### ATA dokáže rozpoznat laterální pohyb analýzou chování uživatelů a zařízení a jejich vztahů uvnitř podnikové sítě a detekcí neobvyklých přístupových vzorců, které mohou indikovat laterální pohyb ze strany útočníka.
Zvýšení oprávnění 

ATA detekuje úspěšné i neúspěšné pokusy o útoky metodou zvýšení oprávnění, kdy se útočník pokouší o zvýšení stávajících oprávnění, a to i opakovaně, dokud nezíská plnou kontrolu nad napadeným prostředím.

- **K detekci zvýšení oprávnění ATA využívá kombinaci analýz chování (detekce neobvyklého chování privilegovaných účtů) a detekci známých nebezpečných útoků a technik, které se často využívají pro zvýšení oprávnění, jako například:**<br>
Zneužití MS14-068 (Forged PAC) Při útoku typu falešný certifikát PAC útočník vloží do svého platného lístku TGT autorizační data ve formě podvržené autorizační hlavičky. To mu zaručuje další oprávnění, která mu ale organizace neudělila.
- **V tomto scénáři útočník využívá dříve odcizené přihlašovací údaje nebo údaje získaných technikou laterálního pohybu.**<br>
Zneužití MS11-013 (Silver PAC) Útoky zneužitím MS11-013 využívají chybu zabezpečení privilegií v protokolu Kerberos, která umožňuje falšování konkrétních aspektů lístků služby Kerberos. Kyberzločinec nebo útočník, který tuto chybu zabezpečení úspěšně zneužil, může získat token se zvýšenými oprávněními na řadiči domény.

### V tomto scénáři útočník využívá dříve odcizené přihlašovací údaje nebo údaje získaných technikou laterálního pohybu.
Dominance v doméně

- **ATA detekuje úspěšné i neúspěšné pokusy o získání celkové kontroly a dominance v napadaném prostředí. Využívá přitom detekci známých technik, které útočníci využívají. Patří mezi ně:**<br>
Malware typu Skeleton key
- **Při útoku typu Skeleton key se do řadiče domény nainstaluje malware, který útočníkům umožňuje, aby se ověřili jako jakýkoli uživatel, ale oprávněným uživatelům nebrání v normálním přihlašování.**<br>
Zlatý lístek V tomto případě útočník odcizí přihlašovací údaje KBTGT, tj. zlatý lístek protokolu Kerberos.
- **Tento lístek umožňuje offline vytvoření platného lístku TGT, se kterým je možné získat přístup k prostředkům v síti.**<br>
Vzdálené spuštění
-   Útočníci se mohou pokusit o ovládnutí sítě vzdáleným spouštěním kódu na vašem řadiči domény. Požadavky na škodlivou replikaci

## V prostředí Active Directory (AD) dochází k pravidelné replikaci mezi řadiči domény.

-   Útočník může zfalšovat požadavek na replikaci AD (někdy zosobněním řadiče domény). To mu umožní načíst dat uložená ve službě AD, včetně hodnot hash hesel, aniž by musel využívat rušivější techniky, jako je třeba služba Stínová kopie svazku.

-   Co dál?

## Další informace o zapojení řešení ATA do vaší sítě najdete v tématu [Architektura ATA](/advanced-threat-analytics/plan-design/ata-architecture).
[Pokud chcete začít s nasazením ATA, přečtěte si téma [Instalace ATA](/advanced-threat-analytics/deploy-use/install-ata).](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Jun16_HO1-->



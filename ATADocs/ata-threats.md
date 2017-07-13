---
title: "Jaké hrozby Advanced Threat Analytics detekuje? | Dokumentace Microsoftu"
description: "Uvádí hrozby, které ATA detekuje"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 630bb2b74dafcf9ab9b3469c2afbf8abc59c2dbf
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/03/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*

# Jaké hrozby ATA vyhledává?
<a id="what-threats-does-ata-look-for" class="xliff"></a>

ATA zajišťuje detekci pro následující fáze pokročilých útoků: rekognoskace, únik přihlašovacích údajů, laterální pohyb, zvýšení úrovně oprávnění, dominance v doméně a další. Tyto detekce jsou zaměřené na zjišťování pokročilých útoků a vnitřních hrozeb ještě předtím, než mohou ve vaší organizaci způsobit škody.
Výsledkem detekce v jednotlivých fázích je několik podezřelých aktivit relevantních pro danou fázi. Každá podezřelá aktivita je v korelaci s různými charakteristikami možných útoků.
Na následujícím obrázku jsou zvýrazněné fáze v řetězci úkonů útočníka (kill-chain), kde ATA aktuálně poskytuje detekci.

![Zaměření řešení ATA na postranní aktivity v řetězci úkonů útočníka](media/attack-kill-chain-small.jpg)


### Rekognoskace
<a id="reconnaissance" class="xliff"></a>

ATA poskytuje několik způsobů detekce rekognoskace. Mezi tyto detekce patří:

-   **Rekognoskace pomocí výčtu účtů**<br></br>Upozorní na pokusy útočníků použít protokol Kerberos ke zjištění existence určitých uživatelů, a to i v případě, že se tato aktivita neobjeví v protokolech na řadiči domény.

-   **Výčet síťových relací**<br></br>V rámci fáze rekognoskace se útočníci mohou dotazovat řadiče domény na všechny aktivní relace SMB na serveru, což jim umožní získat přístup ke všem IP adresám a uživatelům, kteří jsou k těmto relacím SMB přidružení. Výčet relací SMB potom útočníci mohou využít k cílení na citlivé účty a následně k laterálnímu pohybu napříč sítí.

-   **Rekognoskace pomocí DNS**<br></br>Informace DNS v cílové síti jsou pro rekognoskaci často velmi užitečné. Informace DNS obsahují seznam všech serverů a často i všech klientů a mapování na příslušné IP adresy. Zobrazení informací DNS může útočníkům poskytnout podrobný přehled o těchto entitách ve vašem prostředí, což jim umožní zaměřit úsilí na entity, které jsou pro jejich kampaň relevantní.

-   **Rekognoskace pomocí výčtu adresářových služeb**<br></br>Detekce rekognoskace entit (uživatelů, skupin atd.) prováděná pomocí protokolu SAM-remote ke spouštění dotazů vůči řadičům domény. Tato metoda rekognoskace převládá v mnoha typech malwaru, které můžeme vidět ve scénářích skutečných útoků. 


### Prozrazené přihlašovací údaje
<a id="compromised-credentials" class="xliff"></a>

K detekci prozrazených přihlašovacích údajů ATA využívá analýzu chování na základě machine learningu a také rozpoznání známých útoků a technik.
Pomocí analýzy chování a machine learningu ATA dokáže detekovat podezřelé aktivity, jako jsou neobvyklá přihlášení, nestandardní přístup k prostředkům a přístup mimo běžnou pracovní dobu, což by mohlo ukazovat na únik přihlašovacích údajů. Pro ochranu proti zneužití přihlašovacích údajů rozpoznává ATA následující známé útoky a techniky:

-   **Hrubá síla**<br></br>Při útoku hrubou silou se útočníci snaží uhodnout přihlašovací údaje uživatelů zkoušením kombinací běžných jmen a hesel. Útočníci často používají složité algoritmy nebo slovníky, aby vyzkoušeli tolik kombinací, kolik jim systém dovolí.

- **Podezřelé chyby ověřování** (behaviorální hrubá síla) <br></br> Útočníci se pokoušejí prolomit účty hrubou silou s využitím přihlašovacích údajů. ATA při detekci neobvyklého chování při neúspěšném ověření zobrazí upozornění.

-   **Zveřejnění citlivých účtů při ověřování pomocí prostého textu**<br></br>Pokud se přihlašovací údaje k účtům s vysokými oprávněními odešlou v prostém textu, ATA vám doporučí aktualizovat konfiguraci počítače.

-   **Služba zveřejňující účty při ověřování pomocí prostého textu** <br></br>Pokud služba na počítači odesílá přihlašovací údaje k několika účtům v prostém textu, ATA vám doporučí aktualizovat konfiguraci této služby.

-   **Podezřelé aktivity účtu sloužícího jako návnada (honeytoken)**<br></br>Účty ve funkci návnady (honeytoken) jsou fiktivní účty nastavené tak, aby přitahovaly, identifikovaly a sledovaly podezřelé aktivity, které se je pokusí využít. ATA vás upozorní na jakékoli činnosti probíhající pod těmito účty.

-   **Neobvyklá implementace protokolu**<br></br>Požadavky na ověření (Kerberos nebo NTLM) se obvykle zpracovávají pomocí normální sady metod a protokolů. K zajištění úspěšného ověření ale stačí, aby požadavek splňoval konkrétní sadu požadavků. Útočníci mohou implementovat tyto protokoly s malými odchylkami od normální implementace v daném prostředí. Tyto odchylky mohou signalizovat přítomnost útočníka, který se pokouší využít nebo už úspěšně využívá prozrazené přihlašovací údaje.

-   **Škodlivá žádost o soukromé informace přes Data Protection**<br></br>Data Protection API (DPAPI) je služba ochrany dat založená na heslech. Tuto službu ochrany používají různé aplikace, které ukládají tajné údaje uživatelů, jako jsou hesla k webům a přihlašovací údaje ke sdíleným složkám. Při ztrátě hesla mohou uživatelé dešifrovat chráněná data pomocí obnovovacího klíče, který nezahrnuje jejich heslo. V doménovém prostředí útočníci mohou vzdáleně ukrást obnovovací klíč a použít ho k dešifrování chráněných dat ve všech počítačích připojených k doméně.

-   **Neobvyklé chování**<br></br>V případě vnitřních hrozeb a pokročilých útoků se často k podvodnému získání přihlašovacích údajů k účtům využívají techniky sociálního inženýrství nebo zcela nové a dosud neznámé metody a techniky. Díky tomu, že ATA analyzuje chování entit, detekuje případné abnormality v operacích, které tyto entity provádějí, a upozorňuje na ně, dokáže tyto typy ohrožení detekovat.

### Laterální pohyb
<a id="lateral-movement" class="xliff"></a>

K detekci laterálního pohybu, při němž uživatelé zneužijí přihlašovací údaje k získání přístupu k prostředkům, ke kterým přístup mít nemají, ATA využívá analýzy chování využívající machine learning a také rozpoznání známých škodlivých útoků a technik.
Pomocí analýzy chování a machine learningu ATA dokáže detekovat nestandardní přístup k prostředkům, nestandardní využití zařízení a další indikátory, které by mohly ukazovat na únik přihlašovacích údajů.
Kromě toho ATA k rozpoznání laterálního pohybu využívá detekci technik, které při laterálním pohybu používají útočníci, například:

-   **Předání lístku (Pass-the-Ticket)** <br></br>Při útoku typu pass-the-ticket útočník získá lístek Kerberos z jednoho počítače a použije ho k získání přístupu k jinému počítači tak, že předstírá identitu některé entity v síti.

-   **Předání hodnoty hash (Pass-the-Hash)** <br></br>Při útoku typu pass-the-hash útočník odcizí hodnotu hash NTML entity a použije ji k ověření prostřednictvím NTLM, k předstírání identity dané entity a k přístupu k prostředkům v síti.

-   **Vynechání hodnoty hash (Over-pass-the-Hash)**<br></br>Útoky over-pass-the-hash spočívají v použití odcizené hodnoty hash NTLM k ověření prostřednictvím protokolu Kerberos a k získání platného lístku TGT Kerberos. Tento lístek se pak použije k ověření uživatele jako platného a k získání přístupu k prostředkům v síti.

-   **Neobvyklé chování**<br></br>Laterální pohyb je technika, kterou útočníci často používají k pohybu mezi zařízeními a oblastmi v napadené síti a získání přístupu k privilegovaným přihlašovacím údajům nebo citlivým informacím, které je zajímají. ATA dokáže rozpoznat laterální pohyb analýzou chování uživatelů a zařízení a jejich vztahů uvnitř podnikové sítě a detekcí neobvyklých přístupových vzorců, které mohou indikovat laterální pohyb ze strany útočníka.

### Zvýšení oprávnění
<a id="privilege-escalation" class="xliff"></a>

ATA detekuje úspěšné i neúspěšné pokusy o útoky metodou zvýšení oprávnění, kdy se útočník pokouší o zvýšení stávajících oprávnění, a to i opakovaně, dokud nezíská plnou kontrolu nad napadeným prostředím.
K detekci zvýšení oprávnění ATA využívá kombinaci analýz chování (detekce neobvyklého chování privilegovaných účtů) a detekci známých nebezpečných útoků a technik, které se často využívají pro zvýšení oprávnění, jako například:

-   **Zneužití MS14-068 (zfalšovaný certifikát PAC)**<br></br>Při útoku typu falešný certifikát PAC útočník vloží do svého platného lístku TGT autorizační data ve formě podvržené autorizační hlavičky. To mu zaručuje další oprávnění, která mu ale organizace neudělila. V tomto scénáři útočník využívá dříve odcizené přihlašovací údaje nebo údaje získaných technikou laterálního pohybu.

-   **Zneužití MS11-013 (stříbrný certifikát PAC)**<br></br>Útoky zneužitím MS11-013 využívají chybu zabezpečení privilegií v protokolu Kerberos, která umožňuje falšování konkrétních aspektů lístků služby Kerberos. Kyberzločinec nebo útočník, který tuto chybu zabezpečení úspěšně zneužil, může získat token se zvýšenými oprávněními na řadiči domény. V tomto scénáři útočník využívá dříve odcizené přihlašovací údaje nebo údaje získaných technikou laterálního pohybu.

-   **Neobvyklá úprava citlivých skupin**  <br></br>Jako součást fáze eskalace oprávnění upravují útočníci skupiny s vysokými oprávněními, aby získali přístup k citlivým prostředkům. ATA teď detekuje, pokud dojde u skupiny se zvýšenými oprávněními k neobvyklé změně.

### Dominance v doméně
<a id="domain-dominance" class="xliff"></a>

ATA detekuje úspěšné i neúspěšné pokusy o získání celkové kontroly a dominance v napadaném prostředí. Využívá přitom detekci známých technik, které útočníci využívají. Patří mezi ně:

-   **Malware Skeleton key**<br></br>Při útoku typu Skeleton key se do řadiče domény nainstaluje malware, který útočníkům umožňuje, aby se ověřili jako jakýkoli uživatel, ale oprávněným uživatelům nebrání v normálním přihlašování.

-   **Zlatý lístek**<br></br>V tomto případě útočník odcizí přihlašovací údaje KBTGT, tj. zlatý lístek protokolu Kerberos. Tento lístek umožňuje offline vytvoření platného lístku TGT, se kterým je možné získat přístup k prostředkům v síti.

-   **Vzdálené spuštění**<br></br>Útočníci se mohou pokusit o ovládnutí sítě vzdáleným spouštěním kódu na vašem řadiči domény.

- **Pokus o vzdálené spuštění – WMI exec**<br></br>Útočníci se mohou pokusit o ovládnutí sítě vzdáleným spouštěním kódu na vašem řadiči domény. ATA detekuje vzdálené spuštění využívající metody WMI ke vzdálenému spouštění kódu.

-   **Škodlivé žádosti o replikaci** <br></br>V prostředí Active Directory (AD) dochází k pravidelné replikaci mezi řadiči domény. Útočník může zfalšovat požadavek na replikaci AD (někdy zosobněním řadiče domény). To mu umožní načíst dat uložená ve službě AD, včetně hodnot hash hesel, aniž by musel využívat rušivější techniky, jako je třeba služba Stínová kopie svazku.


## Co dál?
<a id="whats-next" class="xliff"></a>

-   Další informace o zapojení řešení ATA do vaší sítě najdete v tématu [Architektura ATA](ata-architecture.md).

-   Pokud chcete začít s nasazením ATA, přečtěte si téma [Instalace ATA](install-ata-step1.md).

## Viz také
<a id="see-also" class="xliff"></a>
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

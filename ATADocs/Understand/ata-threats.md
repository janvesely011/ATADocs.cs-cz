---
title: "Jaké hrozby Advanced Threat Analytics detekuje? | Dokumentace Microsoftu"
description: "Uvádí hrozby, které ATA detekuje"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7cef61d8bb4db140b966d9d38698e78c7b8aff8c
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Platí pro: Advanced Threat Analytics verze 1.7*

# <a name="what-threats-does-ata-look-for"></a>Jaké hrozby ATA vyhledává?

ATA zajišťuje detekci pro následující fáze pokročilých útoků: rekognoskace, únik přihlašovacích údajů, laterální pohyb, zvýšení úrovně oprávnění, dominance v doméně a další. Tyto detekce jsou zaměřené na zjišťování pokročilých útoků a vnitřních hrozeb ještě předtím, než mohou ve vaší organizaci způsobit škody.
Výsledkem detekce v jednotlivých fázích je několik podezřelých aktivit relevantních pro danou fázi. Každá podezřelá aktivita je v korelaci s různými charakteristikami možných útoků.
Na následujícím obrázku jsou zvýrazněné fáze v řetězci úkonů útočníka (kill-chain), kde ATA aktuálně poskytuje detekci.

![Zaměření řešení ATA na postranní aktivity v řetězci úkonů útočníka](media/attack-kill-chain-small.jpg)


### <a name="reconnaissance"></a>Rekognoskace
ATA poskytuje několik způsobů detekce rekognoskace. Mezi tyto detekce patří:
-    **Rekognoskace pomocí výčtu účtů** Detekuje pokusy útočníků použít protokol Kerberos ke zjištění existence určitých uživatelů, a to i v případě, že se tato aktivita neobjeví v protokolech na řadiči domény.
-    **Výčet síťové relace** V rámci fáze rekognoskace se útočníci mohou dotazovat řadiče domény na všechny aktivní relace SMB na serveru, což jim umožní získat přístup ke všem IP adresám a uživatelům, kteří jsou k těmto relacím SMB přidružení. Výčet relací SMB potom útočníci mohou využít k cílení na citlivé účty a následně k laterálnímu pohybu napříč sítí.
-    **Rekognoskace pomocí DNS** Informace DNS v cílové síti jsou pro rekognoskaci často velmi užitečné. Informace DNS obsahují seznam všech serverů a často i všech klientů a mapování na příslušné IP adresy. Zobrazení informací DNS může útočníkům poskytnout podrobný přehled o těchto entitách ve vašem prostředí, což jim umožní zaměřit úsilí na entity, které jsou pro jejich kampaň relevantní.
-   **Rekognoskace pomocí výčtu adresářových služeb** Detekce rekognoskace entit (uživatelů, skupin atd.) prováděná pomocí protokolu vzdáleného SAM za účelem spouštění dotazů na řadiče domény. Tato metoda rekognoskace převládá v mnoha typech malwaru, které můžeme vidět ve scénářích skutečných útoků. 


### <a name="compromised-credentials"></a>Prozrazené přihlašovací údaje
K detekci prozrazených přihlašovacích údajů ATA využívá analýzu chování na základě machine learningu a také rozpoznání známých útoků a technik.
Pomocí analýzy chování a machine learningu ATA dokáže detekovat podezřelé aktivity, jako jsou neobvyklá přihlášení, nestandardní přístup k prostředkům a přístup mimo běžnou pracovní dobu, což by mohlo ukazovat na únik přihlašovacích údajů. Pro ochranu proti zneužití přihlašovacích údajů rozpoznává ATA následující známé útoky a techniky:
-    **Hrubá síla** Při útoku hrubou silou se útočníci snaží uhodnout přihlašovací údaje uživatelů zkoušením kombinací běžných jmen a hesel. Útočníci často používají složité algoritmy nebo slovníky, aby vyzkoušeli tolik kombinací, kolik jim systém dovolí.
-    **Přihlašování k citlivým účtům v otevřeném textu** Pokud se přihlašovací údaje k účtům s vysokými oprávněními odesílají v prostém textu, ATA vám doporučí aktualizovat konfiguraci počítače.
-    **Služba přihlašující se k citlivým účtům v otevřeném textu** Pokud služba na počítači přihlašuje k účtu s vysokými oprávněními v prostém textu, ATA vám doporučí aktualizovat konfiguraci služby.
-    **Podezřelá aktivita v účtu sloužícím jako návnada** Účty ve funkci návnady (Honey Token) jsou fiktivní účty nastavené tak, aby přitahovaly, identifikovaly a sledovaly podezřelé aktivity, které se je pokusí využít. ATA vás upozorní na jakékoli činnosti probíhající pod těmito účty.
-    **Neobvyklá implementace protokolu**Požadavky na ověření (Kerberos nebo NTLM) se obvykle zpracovávají pomocí normální sady metod a protokolů. K zajištění úspěšného ověření ale stačí, aby požadavek splňoval konkrétní sadu požadavků. Útočníci mohou implementovat tyto protokoly s malými odchylkami od normální implementace v daném prostředí. Tyto odchylky mohou signalizovat přítomnost útočníka, který se pokouší využít nebo už úspěšně využívá prozrazené přihlašovací údaje.
-    **Škodlivý požadavek na soukromé informace přes Data Protection** Data Protection API (DPAPI) je služba ochrany dat založená na heslech. Tuto službu ochrany používají různé aplikace, které ukládají tajné údaje uživatelů, jako jsou hesla k webům a přihlašovací údaje ke sdíleným složkám. Při ztrátě hesla mohou uživatelé dešifrovat chráněná data pomocí obnovovacího klíče, který nezahrnuje jejich heslo. V doménovém prostředí útočníci mohou vzdáleně ukrást obnovovací klíč a použít ho k dešifrování chráněných dat ve všech počítačích připojených k doméně.
-    **Neobvyklé chování** V případě vnitřních hrozeb a pokročilých útoků se často k podvodnému získání přihlašovacích údajů k účtům využívají techniky sociálního inženýrství nebo zcela nové a dosud neznámé metody a techniky. Díky tomu, že ATA analyzuje chování entit, detekuje případné abnormality v operacích, které tyto entity provádějí, a upozorňuje na ně, dokáže tyto typy ohrožení detekovat.

### <a name="lateral-movement"></a>Laterální pohyb
K detekci laterálního pohybu, při němž uživatelé zneužijí přihlašovací údaje k získání přístupu k prostředkům, ke kterým přístup mít nemají, ATA využívá analýzy chování využívající machine learning a také rozpoznání známých škodlivých útoků a technik.
Pomocí analýzy chování a machine learningu ATA dokáže detekovat nestandardní přístup k prostředkům, nestandardní využití zařízení a další indikátory, které by mohly ukazovat na únik přihlašovacích údajů.
Kromě toho ATA k rozpoznání laterálního pohybu využívá detekci technik, které při laterálním pohybu používají útočníci, například:
-    **Pass-the-ticket** Při útoku tohoto typu útočník získá lístek Kerberos z jednoho počítače a použije ho k získání přístupu k jinému počítači předstíráním entity v síti.
-    **Pass-the-hash** Při tomto typu útočník získá hodnotu hash entity v kontextu protokolu NTLM a použije ji k ověření prostřednictvím NTLM, k předstírání identity dané entity a k přístupu k prostředkům v síti.
-    **Over-pass-the-hash** Tyto útoky spočívají v použití odcizené hodnoty hash NTLM k ověření prostřednictvím protokolu Kerberos, k získání platného lístku TGT Kerberos a následně k ověření jako platného uživatele a k získání přístupu k prostředkům v síti.
-    **Neobvyklé chování** Laterální pohyb je technika, kterou útočníci často používají k pohybu mezi zařízeními a oblastmi v napadené síti a získání přístupu k privilegovaným přihlašovacím údajům nebo citlivým informacím, které je zajímají. ATA dokáže rozpoznat laterální pohyb analýzou chování uživatelů a zařízení a jejich vztahů uvnitř podnikové sítě a detekcí neobvyklých přístupových vzorců, které mohou indikovat laterální pohyb ze strany útočníka.

### <a name="privilege-escalation"></a>Zvýšení oprávnění
ATA detekuje úspěšné i neúspěšné pokusy o útoky metodou zvýšení oprávnění, kdy se útočník pokouší o zvýšení stávajících oprávnění, a to i opakovaně, dokud nezíská plnou kontrolu nad napadeným prostředím.
K detekci zvýšení oprávnění ATA využívá kombinaci analýz chování (detekce neobvyklého chování privilegovaných účtů) a detekci známých nebezpečných útoků a technik, které se často využívají pro zvýšení oprávnění, jako například:
-    **Zneužití MS14-068 (Forged PAC)** Při útoku typu falešný certifikát PAC útočník vloží do svého platného lístku TGT autorizační data ve formě podvržené autorizační hlavičky. To mu zaručuje další oprávnění, která mu ale organizace neudělila. V tomto scénáři útočník využívá dříve odcizené přihlašovací údaje nebo údaje získaných technikou laterálního pohybu.
-    **Zneužití MS11-013 (Silver PAC)** Útoky zneužitím MS11-013 využívají chybu zabezpečení privilegií v protokolu Kerberos, která umožňuje falšování konkrétních aspektů lístků služby Kerberos. Kyberzločinec nebo útočník, který tuto chybu zabezpečení úspěšně zneužil, může získat token se zvýšenými oprávněními na řadiči domény. V tomto scénáři útočník využívá dříve odcizené přihlašovací údaje nebo údaje získaných technikou laterálního pohybu.

### <a name="domain-dominance"></a>Dominance v doméně
ATA detekuje úspěšné i neúspěšné pokusy o získání celkové kontroly a dominance v napadaném prostředí. Využívá přitom detekci známých technik, které útočníci využívají. Patří mezi ně:
-    **Malware typu Skeleton key** Při útoku typu skeleton key se do řadiče domény nainstaluje malware, který útočníkům umožňuje ověření jako jakýkoli uživatel, ale oprávněným uživatelům nebrání v normálním přihlašování.
-    **Zlatý lístek** V tomto případě útočník odcizí přihlašovací údaje KBTGT, tj. zlatý lístek protokolu Kerberos. Tento lístek umožňuje offline vytvoření platného lístku TGT, se kterým je možné získat přístup k prostředkům v síti.
-    **Vzdálené spuštění** Útočníci se mohou pokusit o ovládnutí sítě vzdáleným spouštěním kódu na vašem řadiči domény.
-    **Požadavky na škodlivou replikaci** V prostředí Active Directory (AD) dochází k pravidelné replikaci mezi řadiči domény. Útočník může zfalšovat požadavek na replikaci AD (někdy zosobněním řadiče domény). To mu umožní načíst dat uložená ve službě AD, včetně hodnot hash hesel, aniž by musel využívat rušivější techniky, jako je třeba služba Stínová kopie svazku.


## <a name="whats-next"></a>Co dál?

-   Další informace o zapojení řešení ATA do vaší sítě najdete v tématu [Architektura ATA](/advanced-threat-analytics/plan-design/ata-architecture).

-   Pokud chcete začít s nasazením ATA, přečtěte si téma [Instalace ATA](/advanced-threat-analytics/deploy-use/install-ata).

## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

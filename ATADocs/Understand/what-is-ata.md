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
Microsoft Advanced Threat Analytics (ATA) je řešení zabezpečení, které pomáhá IT profesionálům chránit jejich organizace před pokročilými cílenými útoky i vnitřními hrozbami. ATA automaticky analyzuje, učí se a identifikuje normální a nenormální chování entit (uživatelů, zařízení a prostředků) a identifikuje různá rizika, například známé nebezpečné útoky nebo problémy se zabezpečením. S použitím znalostí a zkušeností v oblasti bezpečnosti na světové úrovni se tato inovativní technologie zaměřuje na odhalování bezpečnostních hrozeb dřív, než způsobí nějaké škody.

## Co ATA dělá?
ATA detekuje:

  - Pokročilé trvalé hrozby (APT), a to na samém počátku procesu, kdy ještě nemohou způsobit škody

  - Vnitřní hrozby

  ATA také umožní oddělit signál od šumu a soustředit se tak na to, co je důležité.

ATA má detekční modul, který využívá strojové učení, hloubkovou kontrolu paketů s kontextem entit, analýzy protokolů a informace ze služby Active Directory (AD) k analýze chování uživatelů a dalších entit.
Tento detekční modul provádí hloubkovou analýzu síťového provozu a využívá strojové učení k vytvoření mapy normálních aktivit, provozu a používání prostředků ve vaší organizaci. Poté ATA všechno jen tiše sleduje a upozorní vás, když se objeví něco nestandardního. Tohoto výsledku se dosahuje využitím technologie hloubkové kontroly paketů společnosti Microsoft (DPI). Tato technologie umožňuje díky znalosti kontextu jednotlivých entit analyzovat síťový provoz do větší hloubky a poskytuje řešení ATA možnost analyzovat všechny úrovně síťového prostředí. ATA shromažďuje také informace o relevantních událostech ze systémů SIEM a z řadičů domény. 

Po dokončení analýzy vytvoří ATA dynamické a průběžně aktualizované zobrazení všech osob, zařízení a prostředků v organizaci. Pomocí tohoto komplexního obrazu dokáže ATA detekovat známé nebezpečné útoky, například typu pass-the hash, pass-the-ticket a rekognoskace. ATA také vyhledává jakékoli anomálie v chování entit v síti.  

Jakmile je detekována podezřelá aktivita, ATA vydá výstrahu. Pomocí pokročilých algoritmů pro agregaci a kontextové ověřování současně minimalizuje počet falešně pozitivních výstrah.


## Jaké hrozby ATA vyhledává?

ATA zajišťuje detekci pro následující fáze pokročilých útoků: rekognoskace, zneužití přihlašovacích údajů, laterální pohyb, zvýšení úrovně oprávnění, dominance v doméně a další. Tyto detekce jsou zaměřené na zjišťování pokročilých útoků a vnitřních hrozeb ještě předtím, než mohou vaši organizaci poškodit.

Detekce v každé fázi hledá několik typů podezřelých aktivit relevantních pro danou fázi. Každá podezřelá aktivita koreluje s různými charakteristikami možných útoků.


### Rekognoskace
ATA poskytuje několik způsobů detekce rekognoskace. Například podezřelá aktivita **Reconnaissance using account enumeration** (Rekognoskace pomocí zjišťování účtů) upozorní na pokusy útočníků použít protokol Kerberos ke zjištění existence určitých uživatelů, a to i v případě, že se tato aktivita neobjeví v protokolech na řadiči domény.

### Zneužití přihlašovacích údajů

ATA detekuje zneužití přihlašovacích údajů díky analýze chování využívající strojové učení, jakož rozpoznání známých útoků a technik.  

ATA dokáže rozpoznat podezřelé aktivity, například neobvyklá přihlášení, nestandardní přístup k prostředkům a přístup mimo běžnou pracovní dobu. Kterákoli z těchto podezřelých aktivit může znamenat potenciální zneužití nebo prozrazení přihlašovacích údajů.

Pro ochranu proti zneužití přihlašovacích údajů rozpoznává ATA následující známé útoky a techniky:

 - **Hrubá síla** – při útoku hrubou silou se útočníci snaží uhodnout přihlašovací údaje uživatelů zkoušením kombinací běžných jmen a hesel. Útočníci často používají složité algoritmy nebo slovníky, aby vyzkoušeli tolik kombinací, kolik jim systém dovolí.

- **Přihlašování k citlivým účtům v otevřeném textu** – pokud se přihlašovací údaje k účtům s vysokými oprávněními odesílají v prostém textu, ATA vám doporučí aktualizovat konfiguraci počítače.

- **Služba přihlašující se k citlivým účtům v otevřeném textu** – pokud služba na počítači přihlašuje k účtu s vysokými oprávněními v prostém textu, ATA vám doporučí aktualizovat konfiguraci služby.

- **Podezřelá aktivita v účtu sloužícím jako návnada** – účty ve funkci návnady (Honey Token) jsou fiktivní účty nastavené tak, aby přitahovaly, identifikovaly a sledovaly podezřelé aktivity, které se je pokusí využít. ATA vás upozorní na jakékoli činnosti probíhající pod těmito účty.

### Laterální pohyb
Jako laterální pohyb se označuje situace, kdy uživatelé využívají přihlašovací údaje k určitým prostředkům pro přístup k jiným prostředkům, ke kterým by neměli mít oprávnění. ATA takový laterální pohyb detekuje díky analýze chování využívající strojové učení, jakož i rozpoznáním známých útoků a technik.  

ATA zjišťuje nestandardního přístupy k prostředkům, časy jejich používání a další indikátory, které by mohly pomoci odhalit laterální pohyb. Kromě toho ATA k rozpoznání laterálního pohybu využívá detekci technik, které při laterálním pohybu používají útočníci, například:
- **Pass-the-ticket** – při útoku tohoto typu útočník získá lístek Kerberos z jednoho počítače a použije ho k získání přístupu k jinému počítači předstíráním entity v síti.
- **Pass-the-hash** – při tomto typu útočník získá hodnotu hash entity v kontextu protokolu NTLM a použije ji k ověření prostřednictvím NTLM, k předstírání identity dané entity a k přístupu k prostředkům v síti.
- **Over-pass-the-hash** – tyto útoky spočívají v použití odcizené hodnoty hash NTLM k ověření prostřednictvím protokolu Kerberos, k získání platného lístku TGT Kerberos a následně k ověření jako platného uživatele a k získání přístupu k prostředkům v síti.

### Zvýšení oprávnění
Útok metodou zvýšení oprávnění se pokouší o zvýšení stávajících oprávnění, a to i opakovaně, dokud útočník nezíská plnou kontrolu nad prostředím napadeného počítače. ATA detekuje jak úspěšné, tak i neúspěšné pokusy o zvýšení oprávnění. ATA využívá analýzu chování k detekci neobvyklého používání privilegovaných účtů. ATA také detekuje známé nebezpečné útoky a techniky, které se často používají pro zvýšení oprávnění, jako například:
- **MS14-068 exploit (Forged PAC)** – při útoku typu Forged PAC útočník vloží autorizační data do svého platného lístku TGT ve formě podvržené autorizační hlavičky. S touto technikou útočník získá oprávnění, která mu jeho organizace nepřidělila.
- Použití dříve odcizených přihlašovacích údajů nebo údajů získaných technikou laterálního pohybu.

### Dominance v doméně
Dominance v doméně znamená, že se útočníci pokusí (neúspěšně nebo úspěšně) o získání úplné kontroly nad napadeným prostředím. ATA rozpoznává tyto pokusy vyhledáváním známých technik používaných útočníky, které zahrnují:
- **Malware typu Skeleton key** – při útoku typu skeleton key se do řadiče domény nainstaluje malware, který útočníkům umožňuje ověření jako jakýkoli uživatel, ale oprávněným uživatelům nebrání v normálním přihlašování.
- **Zlatý lístek** – v tomto případě útočník odcizí přihlašovací údaje KBTGT, tj. zlatý lístek protokolu Kerberos. Tento lístek umožňuje offline vytvoření platného lístku TGT, se kterým je možné získat přístup k prostředkům v síti.
- **Vzdálené spuštění** – útočníci se mohou pokusit o ovládnutí sítě vzdáleným spouštěním kódu na vašem řadiči domény.


## Co dál?

-   Další informace o zapojení řešení ATA do vaší sítě najdete v tématu [Architektura ATA](ata-architecture.md).

-   Zahájení nasazení ATA: [Instalace ATA](/advanced-threat-analytics/deploy-useinstall-ata)

## Viz také
[Podporu pro řešení ATA získáte na našem fóru!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO4-->



---
title: Novinky Advanced Threat Analytics verze 1.6 | Dokumentace Microsoftu
description: Uvádí novinky ATA verze 1.6 spolu se známými problémy.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 27b139e5-12b9-4953-8f53-eb58e8ce0038
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7b615f3f6e0fd3a7402a0c87a5df118431d566f3
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56078030"
---
# <a name="whats-new-in-ata-version-16"></a>Novinky ATA verze 1.6
Tyto poznámky k verzi obsahují informace o známých problémech v této verzi Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-16-update"></a>Co je nového v aktualizaci ATA 1.6?
Aktualizace ATA na verzi 1.6 přináší vylepšení v následujících oblastech:

-   Nové detekce

-   Vylepšení stávajících detekcí

-   ATA Lightweight Gateway

-   Automatické aktualizace

-   Vylepšený výkon komponenty ATA Center

-   Menší požadavky na úložiště

-   Podpora IBM QRadar

### <a name="new-detections"></a>Nové detekce


- **Škodlivý požadavek na soukromé informace přes Data Protection** Data Protection API (DPAPI) je služba ochrany dat založená na heslech. Tuto službu ochrany používají různé aplikace, které ukládají tajné údaje uživatelů, jako jsou hesla k webům a přihlašovací údaje ke sdíleným složkám. Za účelem podpory při ztrátě hesla mohou uživatelé dešifrovat chráněná data pomocí obnovovacího klíče, který nezahrnuje jejich heslo. V doménovém prostředí útočníci mohou vzdáleně ukrást obnovovací klíč a použít ho k dešifrování chráněných dat ve všech počítačích připojených k doméně.


- **Výčet síťových relací** Rekognoskace je klíčovou fází v rámci rozšířeného řetězu událostí útoku. Řadiče domén (DC) fungují pro účely distribuce objektů zásad skupiny jako souborové servery. Využívají přitom protokol SMB (Server Message Block). V rámci fáze rekognoskace se útočníci mohou dotazovat řadiče domény na všechny aktivní relace SMB na serveru. To mu umožní získat přístup ke všem uživatelům a IP adresy přidružené k těmto relacím SMB přidružení. Výčet relací SMB potom útočníci mohou využít k cílení na citlivé účty a následně k laterálnímu pohybu napříč sítí.


- **Požadavky na škodlivou replikaci** V prostředí Active Directory dochází k pravidelné replikaci mezi řadiči domény. Útočník může zfalšovat požadavek replikace služby Active Directory (někdy zosobněním řadiče domény). Tato falešného umožňuje umožní načíst dat uložená ve službě Active Directory, včetně hodnot hash hesel, aniž by musel využívat rušivější techniky, jako je stínová kopie svazku.


- **Detekce chyby zabezpečení MS11-013**  
Je zvýšení privilegií v protokolu Kerberos, který umožňuje konkrétních aspektů lístků služby Kerberos zfalšovat. Kyberzločinec nebo útočník, který tuto chybu zabezpečení úspěšně zneužije, může získat token se zvýšenými oprávněními na řadiči domény.


- **Neobvyklá implementace protokolu**Požadavky na ověření (Kerberos nebo NTLM) se obvykle zpracovávají pomocí standardní sady metod a protokolů. K zajištění úspěšného ověření ale stačí, aby požadavek splňoval konkrétní sadu požadavků. Útočníci mohou implementovat tyto protokoly s malými odchylkami od standardní implementace v daném prostředí. Tyto odchylky mohou signalizovat přítomnost útočníka pokusu o provedení útoku, třeba technikou Pass-The-Hash, útoky hrubou silou a další.


### <a name="improvements-to-existing-detections"></a>Vylepšení stávajících detekcí
ATA 1.6 zahrnuje vylepšenou detekční logiku, která omezuje falešně pozitivní i falešně negativní scénáře pro již existující detekce, jako je zlatý lístek, Honeytoken, útok hrubou silou a vzdálené spuštění.

### <a name="the-ata-lightweight-gateway"></a>ATA Lightweight Gateway
Tato verze ATA zavádí nové možnosti nasazení pro ATA Gateway, které umožňují instalovat tuto komponentu přímo na řadič domény. Tato možnost nasazení odebere méně důležité funkce ATA Gateway a na základě prostředků dostupných na řadiči domény zavede dynamickou správu prostředků, která zajistí, že stávající operace řadiče domény nebudou ovlivněny. ATA Lightweight Gateway snižuje náklady na nasazení ATA. Ve stejnou dobu, usnadňuje nasazení v pobočkách, ve kterých je omezenou kapacitu hardwarových prostředků nebo nemohou nastavit podporu pro zrcadlení portů nahoru.
Další informace o ATA Lightweight Gateway najdete v tématu [Architektura ATA](ata-architecture.md#ata-gateway-and-ata-lightweight-gateway).

Další informace o aspektech nasazení a volbě vhodného typu brány najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment).


### <a name="automatic-updates"></a>Automatické aktualizace
Počínaje verzí 1.6 je možné ATA Center aktualizovat pomocí služby Microsoft Update. Komponenty ATA Gateway se teď navíc dají automaticky aktualizovat pomocí standardních kanálů pro komunikaci s komponentou ATA Center.
### <a name="improved-ata-center-performance"></a>Vylepšený výkon komponenty ATA Center
Nižší databázové zatížení a efektivnější způsob spouštění detekcí v této verzi umožňuje monitorovat pomocí jedné komponenty ATA Center mnohem víc řadičů domén.

### <a name="lower-storage-requirements"></a>Menší požadavky na úložiště
ATA 1.6 potřebuje ke spuštění databáze ATA výrazně menší prostor úložiště. V současnosti vyžaduje jenom 20 % prostoru úložiště v porovnání s předchozími verzemi.

### <a name="support-for-ibm-qradar"></a>Podpora IBM QRadar
ATA může přijímat události z řešení QRadar SIEM společnosti IBM, kromě dříve podporovaných řešení SIEM.

## <a name="known-issues"></a>Známé problémy
V této verzi existují následující známé problémy.

### <a name="failure-to-recognize-new-path-in-manually-moved-databases"></a>Nerozpoznání nových cest u ručně přesunutých databází

V nasazeních ATA, ve kterých je cesta k databázi ručně přesunutá, se pro aktualizaci nepoužije nová cesta k databázi. Přesunout ručně, že cesta k databázi, může způsobit následující problémy:


- ATA může využít veškeré volné místo na systémové jednotce komponenty ATA Center, bez pravidelného odstraňování starých síťových aktivit.


- Aktualizace ATA na verzi 1.6 může způsobit, že selžou kontroly připravenosti spouštěné před aktualizací, jak ukazuje následující obrázek.
    ![Selhání kontroly připravenosti](media/ata_failed_readinesschecks.png)
    
    > [!IMPORTANT]
    > Před aktualizací ATA na verzi 1.6 aktualizujte následující klíč registru správnou cestu k databázi: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath`
    
### <a name="migration-failure-when-updating-from-ata-15"></a>Selhání migrace při aktualizaci z ATA 1.5
Při aktualizaci na ATA 1.6 může proces aktualizace selhat s následujícím kódem chyby:

![Aktualizace ATA na verzi 1.6 chyba](http://i.imgur.com/QrLSApr.png) Pokud se zobrazí tato chyba, zkontrolujte protokol nasazení v: **C:\Users\<uživatele > \AppData\Local\Temp**a hledejte následující výjimku:

    System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> MongoDB.Driver.MongoWriteException: A write operation resulted in an error. E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : "<guid>" } ---> MongoDB.Driver.MongoBulkWriteException`1: A bulk write operation resulted in one or more errors.  E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : " <guid> " }

Tato chyba může také zobrazit: System.ArgumentNullException: Hodnota nemůže být null.
    
Pokud se zobrazí některá z těchto chyb, spusťte následující alternativní řešení:

**Alternativní řešení:** 

1.  Přesuňte složku data_old do dočasné složky (obvykle umístěné v adresáři %ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin).
2.  Odinstalujte ATA Center v1.5 a odstraňte všechna databázová data.
![Odinstalace ATA 1.5](http://i.imgur.com/x4nJycx.png)
3.  Znovu nainstalujte ATA Center v1.5. Zkontrolujte, že používáte stejnou konfiguraci jako předchozí instalace ATA 1.5 (certifikáty, IP adresy, cesta k databázi atd.).
4.  Zastavte následující služby v uvedeném pořadí:
    1.  Microsoft Advanced Threat Analytics Center
    2.  MongoDB
5.  Databázové soubory MongoDB nahraďte soubory ve složce data_old.
6.  Spusťte následující služby v uvedeném pořadí:
    1.  MongoDB
    2.  Microsoft Advanced Threat Analytics Center
7.  Zkontrolujte protokoly a ověřte, že produkt běží bez chyb.
8.  [Stažení](http://aka.ms/ataremoveduplicateprofiles "Stáhněte") nástroj RemoveDuplicateProfiles.exe a zkopírujte ho do hlavní instalační cesty (%ProgramFiles%\Microsoft Advanced Threat Analytics\Center).
9.  Z příkazového řádku se zvýšenými oprávněními spusťte `RemoveDuplicateProfiles.exe` a počkejte, dokud nebude úplně zrušená.
10. Odsud: ...\Microsoft Advanced Threat Analytics\Center\MongoDB\bin adresáře: **Mongo ATA**, zadejte následující příkaz:

          db.SuspiciousActivities.remove({ "_t" : "RemoteExecutionSuspiciousActivity", "DetailsRecords" : { "$elemMatch" : { "ReturnCode" : null } } }, { "_id" : 1 });

![Alternativní řešení aktualizace](http://i.imgur.com/Nj99X2f.png)

Měla by se vrátit `WriteResult({ "nRemoved" : XX })` kde "XX" je počet podezřelých aktivit, které byly odstraněny. Pokud je toto číslo větší než 0, ukončete příkazový řádek a pokračujte v procesu aktualizace.


### <a name="net-framework-461-requires-restarting-the-server"></a>Net Framework 4.6.1 vyžaduje restartování serveru

![Restartování rozhraní .Net Framework](media/ata-net-framework-restart.png)

### <a name="historical-network-activities-no-longer-migrated"></a>Historické síťové aktivity se už nemigrují
Tato verze ATA poskytuje vylepšený detekční modul, který zajišťuje přesnější detekci a omezuje řadu falešně pozitivních scénářů, hlavně pro útoky typu pass-the-hash.
Nový a vylepšený detekční modul využívá vloženou detekční technologii, která umožňuje detekci bez přístupu k historickým síťovým aktivitám, výrazně zvýšit výkon komponenty ATA Center. Zároveň to znamená, že je potřeba migrovat historické síťové aktivity během procesu aktualizace.
ATA při aktualizaci vyexportuje tato data do složky `<Center Installation Path>\Migration` jako soubor JSON pro případ, že byste je v budoucnu potřebovali.

## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizace ATA na verzi 1.6 – průvodce migrací](ata-update-1.6-migration-guide.md)

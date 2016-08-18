---
title: "Řešení potíží s ATA pomocí databáze ATA | Microsoft ATA"
description: "Popisuje, jak můžete databázi ATA použít k řešení potíží."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: c86b6dc880238e262f696e88c54bc1bc7e01a1db


---

# Řešení potíží s ATA pomocí databáze ATA
ATA používá jako svou databázi MongoDB.
Můžete pracovat s databází pomocí výchozího příkazového řádku nebo nástroje uživatelského rozhraní a provádět pokročilé úlohy a řešení potíží.

## Interakce s databází
Výchozí a nejzákladnější možnost pro dotazování databáze je použití prostředí Mongo:

1.  Otevřete okno příkazového řádku a změňte cestu ke složce bin MongoDB. Výchozí cesta je **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Spusťte `mongo.exe ATA`. Ujistěte se, že jste text ATA zadali velkými písmeny.

|Postupy|Syntaxe|Poznámky|
|-------------|----------|---------|
|Kontrola kolekcí v databázi|`show collections`|Užitečné jako koncový test ke zjištění, že se provoz zapisuje do databáze a že ATA přijímá událost 4776.|
|Získání podrobností o uživateli/počítači/skupině (UniqueEntity), jako je ID uživatele|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|Vyhledání provozu ověřování Kerberos pocházejícího z určitého počítače v určitý den|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Chcete-li získat &lt;ID zdrojového počítače&gt;, můžete dát dotaz na kolekce UniqueEntity, jak ukazuje příklad.<br /><br />Každý typ síťové aktivity, jako je například ověřování Kerberos, má svou vlastní kolekci pro datum UTC.|
|Vyhledání provozu NTLM pocházejícího z určitého počítače vztahujícího se k určitému účtu v určitý den|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|Chcete-li získat &lt;ID zdrojového počítače&gt; a &lt;ID účtu&gt;, můžete dát dotaz na kolekce UniqueEntity, jak ukazuje příklad.<br /><br />Každý typ síťové aktivity, jako je například ověřování NTLM, má svou vlastní kolekci pro datum UTC.|
|Hledání rozšířených vlastností, jako jsou například aktivní data účtu |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|Chcete-li získat &lt;ID účtu&gt;, můžete dát dotaz na kolekce UniqueEntity, jak ukazuje příklad.<br>Název vlastnosti, která zobrazuje data, ve kterých byl účet aktivní, se nazývá ActiveDates. <br>
Například můžete chtít vědět, jestli má účet alespoň 21 dnů aktivity, aby bylo možné pro něj spustit algoritmus strojového učení abnormálního chování.|
|Proveďte pokročilé změny konfigurace. V tomto příkladu změníme velikost fronty odesílání pro všechny komponenty ATA Gateway na 10000.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

Následující příklad uvádí ukázku kódu pomocí syntaxe uvedené výše. Pokud zkoumáte podezřelou aktivitu, ke které došlo 20. října 2015, a chcete se dozvědět víc o aktivitách NTLM, které v daný den provedl uživatel John Doe:<br /><br />Nejdříve vyhledejte ID uživatele John Doe.

`db.UniqueEntity.find({Name: "John Doe"})`<br>Poznamenejte si jeho ID, které je uvedené hodnotou `_id`. Pro náš příklad předpokládejme, že toto ID je `123bdd24-b269-h6e1-9c72-7737as875351`.<br>Potom vyhledejte kolekci s nejbližším datum, které je před hledaným datem, v našem příkladu 20. říjnem 2015.<br>Poté vyhledejte aktivity NTLM účtu uživatele John Doe: 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`
## Konfigurační soubor ATA
Konfigurace ATA je uložená v databázi v kolekci SystemProfile.
Tato kolekce se zálohuje každou hodinu službou ATA Center do souboru s názvem SystemProfile.json. Je umístěný v podsložce s názvem Backup. Ve výchozím umístění instalace ATA se nachází tady: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile.json**. 

**Poznámka:** Doporučujeme, abyste si tento soubor někam zazálohovali, pokud v ATA provádíte velké změny.

Je možné obnovit všechna nastavení spuštěním následujícího příkazu:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## Viz také
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurace sběru událostí](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurace předávání událostí systému Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->



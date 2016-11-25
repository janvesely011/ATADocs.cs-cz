---
title: "Řešení potíží s ATA pomocí databáze ATA | Dokumentace Microsoftu"
description: "Popisuje, jak můžete databázi ATA použít k řešení potíží."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fca7f1b2b8260cad6e0ce32aad1c9e1b53fc0ad5
ms.openlocfilehash: bff3224736981f38616172a6b1717d7d125c3c0a


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="troubleshooting-ata-using-the-ata-database"></a>Řešení potíží s ATA pomocí databáze ATA
ATA používá jako svou databázi MongoDB.
Můžete pracovat s databází pomocí výchozího příkazového řádku nebo nástroje uživatelského rozhraní a provádět pokročilé úlohy a řešení potíží.

## <a name="interacting-with-the-database"></a>Interakce s databází
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

## <a name="see-also"></a>Viz také
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurace shromažďování událostí](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurace předávání událostí systému Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Nov16_HO3-->



---
title: Řešení potíží s Advanced Threat Analytics pomocí databáze | Dokumentace Microsoftu
description: Popisuje, jak můžete databázi ATA použít k řešení potíží.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 54c8ce78952a9e7a4dd072c5dc91e87dc44f0071
ms.sourcegitcommit: b11433f7d454231a62f64c9d9bfa1355ecf91075
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/18/2019
ms.locfileid: "54403678"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="troubleshooting-ata-using-the-ata-database"></a>Řešení potíží s ATA pomocí databáze ATA
ATA používá jako svou databázi MongoDB.
Můžete pracovat s databází pomocí výchozího příkazového řádku nebo nástroje uživatelského rozhraní a provádět pokročilé úlohy a řešení potíží.

## <a name="interacting-with-the-database"></a>Interakce s databází
Výchozí a nejzákladnější možnost pro dotazování databáze je použití prostředí Mongo:

1.  Otevřete okno příkazového řádku a změňte cestu ke složce bin MongoDB. Výchozí cesta je: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Spusťte `mongo.exe ATA`. Ujistěte se, že jste text ATA zadali velkými písmeny.

> [!div class="mx-tableFixed"]
|Postupy|Syntaxe|Poznámky|
|-------------|----------|---------|
|Kontrola kolekcí v databázi|`show collections`|Užitečné jako koncový test ke zjištění, že se provoz zapisuje do databáze a že ATA přijímá událost 4776.|
|Získání podrobností o uživateli/počítači/skupině (UniqueEntity), jako je ID uživatele|`db.UniqueEntity.find({CompleteSearchNames: "<name of entity in lower case>"})`||
|Vyhledání provozu ověřování Kerberos pocházejícího z určitého počítače v určitý den|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Chcete-li získat &lt;ID zdrojového počítače&gt;, můžete dát dotaz na kolekce UniqueEntity, jak ukazuje příklad.<br /><br />Každý typ síťové aktivity, jako je například ověřování Kerberos, má svou vlastní kolekci pro datum UTC.|
|Proveďte pokročilé změny konfigurace. V tomto příkladu změňte velikost fronty odesílání pro všechny komponenty ATA Gateway na 10000.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

Následující příklad uvádí ukázku kódu pomocí syntaxe uvedené výše. Pokud zkoumáte podezřelou aktivitu, ke které došlo 20. října 2015, a chcete se dozvědět víc o aktivitách NTLM, které v daný den provedl uživatel John Doe:<br /><br />Nejdříve vyhledejte ID uživatele John Doe.

`db.UniqueEntity.find({Name: "John Doe"})`<br>Poznamenejte si ID označené hodnotou `_id` například předpokládat, že je ID `123bdd24-b269-h6e1-9c72-7737as875351`<br>Vyhledejte kolekci s nejbližším datum, který je před datem, které hledáte, v příkladu 20/10/2015.<br>Poté vyhledejte aktivity NTLM účtu uživatele John Doe: 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

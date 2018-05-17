---
title: Advanced Threat Analytics dodržování předpisů, vztah důvěryhodnosti, zabezpečení dat a ochrany osobních údajů | Microsoft Docs
description: Poskytuje seznam ATA prostředků, videa, Začínáme, nasazení a odkazy plán připravenosti.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/16/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: dee55446c18ee9bc560045c94f9421840fc28fc2
ms.sourcegitcommit: 714a01edc9006b38d1163d03852dafc2a5fddb5f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
*Platí pro: Advanced Threat Analytics verze 1.9*

# <a name="ata-compliance-trust-data-security-and-privacy"></a>Dodržování předpisů ATA, vztah důvěryhodnosti, zabezpečení dat a ochrany osobních údajů 

Informace o vztahu důvěryhodnosti ATA a dodržování předpisů najdete v tématu [vztah důvěryhodnosti služby portálu](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) a [Microsoft 365 Enterprise GDPR kompatibility lokality](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).

## <a name="searching-for-and-identifying-personal-data"></a>Hledání a identifikaci osobní data 

Všechna data v ATA, která má vztah k entity je odvozen z Active Directory (AD) a replikují do ATA z ní. Při hledání osobní údaje, je nejdřív byste měli zvážit hledání AD. 

Z komponenty ATA Center použijte panelu Hledat zobrazíte identifikovatelné osobní data, která je uložená v databázi. Uživatelé můžete vyhledávat konkrétní uživatele nebo zařízení. Kliknutím na entity se otevře stránka profilu zařízení nebo uživatele. Profil poskytuje komplexní podrobnosti o entitu, jeho historie a související síťové aktivity, které jsou odvozené ze služby Active Directory. 

## <a name="updating-personal-data"></a>Aktualizace osobních dat 

Osobní data o uživatelích a entity v ATA je odvozený od uživatele AD je objekt ve vaší organizaci. Z toho důvodu se projeví jakékoli změny provedené v profilu uživatele ve službě AD v ATA. 

## <a name="deleting-personal-data"></a>Odstranění osobní data 

I když se data v ATA se replikují a vždy aktualizovat ze služby Active Directory, když je odstraněn entity ve službě AD, data entity v ATA se udržuje pro účely zabezpečení šetření. 

Pokud chcete trvale odstranit uživatelská data z databáze ATA, postupujte takto: 

1. [Stáhněte si](https://aka.ms/ata-gdpr-script) skript MongoDB (gdpr.js).  

2. Zkopírujte skript do počítače ATA Center a spusťte následující příkaz z počítače ATA Center: 

Použijte ATA GDPR databázového skriptu k odstranění entity a odstranit data aktivity entity, jak je popsáno v následujících částech.

### <a name="delete-entities"></a>Odstranění entity

Tato akce trvale odstraní entitu z databáze ATA. Pokud chcete spustit tento příkaz, zadejte název příkazu `deleteAccount`a `SamName`, `UpnName` nebo `GUID` počítače nebo uživatelské jméno, které chcete odstranit. Příklad: 

`C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval “var params= deleteAccount,admin1@contoso.com;” GDPR.js `

Spuštění to úplně odebere entita s hlavní název uživatele admin1@contoso.com z databáze spolu s aktivitami a výstrahy zabezpečení, které jsou přidružené k entitě. 

### <a name="delete-entity-activity-data"></a>Odstranit data entity aktivit

Tato akce trvale odstraní entity aktivity data z databáze ATA. Budou všechny entity jsou stejné, ale jsou odstraněny aktivity a výstrahy zabezpečení související s je pro zadaný časový rámec. 

Pokud chcete spustit tento příkaz, zadejte název příkazu `deleteOldData`a počet dnů dat, které chcete zachovat v databázi. 

Příklad: 

`C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval “var params= deleteOldData,30;” GDPR.js`

Tento skript odeberete všechna data pro všechny entity aktivit a výstrahy zabezpečení z databáze, které jsou starší než 30 dní. Zachovají dat pouze posledních 30 dnů.

## <a name="exporting-personal-data"></a>Export osobní data 

Vzhledem k tomu, že data související s entitami ATA je odvozena ze služby Active Directory, je pouze podmnožinu dat uložené v databázi ATA. Z tohoto důvodu je třeba exportovat data související s entity ze služby Active Directory. 

ATA můžete exportovat do Excelu všechny informace týkající se zabezpečení, která by mohla obsahovat osobní data. 

 
## <a name="opt-out-of-telemetry"></a>Výslovný nesouhlas s telemetrie 

ATA shromažďuje anonymních telemetrická o každé nasazení a odesílá tato data přes HTTPS k serverům Microsoftu. Tato data Microsoft používá k vylepšení budoucích verzích ATA. 

Další informace najdete v tématu [Správa nastavení telemetrie](manage-telemetry-settings.md).

Postup při zakázání shromažďování dat:

1. Přihlaste se ke konzole ATA, na panelu nástrojů klikněte na tlačítko se třemi tečkami a vyberte **O aplikaci**. 
2. Zrušte zaškrtnutí políčka **Send us usage information to help improve your customer experience in the future** (Posílat nám informace o použití k vylepšení zkušeností uživatelů v budoucnosti). 

 

 

 

## <a name="additional-resources"></a>Další materiály a zdroje informací

[Stránka Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Zdroje informací a materiály z komunity

[ATA blog](https://aka.ms/ATABlog)
[ATA komunity](https://aka.ms/ATACommunity)
[svůj názor na ATA](https://aka.ms/ATAUserVoice)

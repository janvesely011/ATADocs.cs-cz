---
title: Advanced Threat Analytics osobních údajů zásad | Dokumentace Microsoftu
description: Obsahuje odkazy na informace o tom, jak odstranit soukromé informace a osobní dat z ATA.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 9/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 46f38285f2822e80744d3aa89b6eb820dd660367
ms.sourcegitcommit: 62b631f64a639f5df04bf805755f26c69b40e8e4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638979"
---
# <a name="ata-data-security-and-privacy"></a>Ochrana osobních údajů a zabezpečení dat ATA

*Platí pro: Advanced Threat Analytics verze 1.9*

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="searching-for-and-identifying-personal-data"></a>Hledání a identifikovat osobní údaje 

Všechna data v ATA, která má vztah k entity je odvozen ze služby Active Directory (AD) a replikují do ATA z něj. Při hledání osobní údaje, je první místo, kde byste měli zvážit hledání AD. 

Z komponenty ATA Center pomocí panelu hledání zobrazíte identifikovatelné osobní údaje uložené v databázi. Uživatele můžete vyhledat konkrétního uživatele nebo zařízení. Kliknutím na entitu se otevře, uživatele nebo na stránce profilu zařízení. Profil, který vám poskytne komplexní informace o entitě, jeho historie a související síťové aktivity odvozené ze služby AD. 

## <a name="updating-personal-data"></a>Aktualizace osobních údajů 

Osobní údaje týkající se uživatelů a entit v ATA je odvozen od uživatele objektu ve vaší organizaci uživatele AD. Z toho důvodu se projeví všechny změny provedené v profilu uživatele ve službě AD v ATA. 

## <a name="deleting-personal-data"></a>Odstraňování osobních údajů 

I když se data v ATA jsou replikována a vždy aktualizovat ze služby AD, kdy odstranění entity ve službě AD, data entity v ATA se udržuje pro účely vyšetřování zabezpečení. 

Pokud budete pro trvalé odstranění uživatelská data z databáze ATA, postupujte takto: 

1. [Stáhněte si](https://aka.ms/ata-gdpr-script) skript MongoDB (gdpr.js).  

2. Zkopírujte skript do složky ATA (umístěný ve `"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB` a spuštěním následujícího příkazu z počítače ATA Center: 

Pomocí skriptu databáze ATA GDPR odstranění entit a odstraňování dat entity aktivity, jak je popsáno v následujících částech.

### <a name="delete-entities"></a>Odstranění entit

Tato akce trvale odstraní entitu z databáze ATA. Ke spuštění tohoto příkazu, zadejte název příkazu `deleteAccount`a `SamName`, `UpnName` nebo `GUID` počítače nebo uživatelské jméno, které chcete odstranit. Příklad: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteAccount,admin1@contoso.com';" GDPR.js`

Spuštěnou úplně odebere entita s hlavní název uživatele admin1@contoso.com z databáze spolu s všech aktivit a výstrahy zabezpečení přidružené k entitě. 

### <a name="delete-entity-activity-data"></a>Odstranit data entity aktivity

Tato akce trvale odstraní entity aktivity data z databáze ATA. Všechny entity jsou beze změny, ale jsou odstraněny aktivit a výstrahy zabezpečení s nimi spojeny pro zadaný časový rámec. 

Ke spuštění tohoto příkazu, zadejte název příkazu `deleteOldData`a počet dnů od data, která chcete zachovat v databázi. 

Příklad: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteOldData,30';" GDPR.js`

Tento skript odebere všechna data pro všechny entity aktivit a výstrahy zabezpečení z databáze, která jsou starší než 30 dní. Zachová pouze data posledních 30 dní.

## <a name="exporting-personal-data"></a>Exportování osobních údajů 

Vzhledem k tomu, že data související s entitami v ATA jsou odvozena ze služby AD, se ukládají pouze podmnožinu těchto dat v databázi ATA. Z tohoto důvodu je třeba exportovat data související entity ze služby AD. 

ATA umožňuje exportovat do Excelu, všechny informace související se zabezpečením, která by mohla obsahovat osobní údaje. 

 
## <a name="opt-out-of-system-generated-logs"></a>Výslovný nesouhlas s systémem generovaných protokolů 

ATA shromažďuje anonymních systémem generované protokoly o každé nasazení a tato data přenáší přes protokol HTTPS na servery Microsoftu. Tato data Microsoft používá k vylepšení budoucích verzích ATA. 

Další informace najdete v tématu [spravovat systémem generované protokoly](manage-telemetry-settings.md).

Chcete-li zakázat shromažďování dat:

1. Přihlaste se ke konzole ATA, na panelu nástrojů klikněte na tlačítko se třemi tečkami a vyberte **O aplikaci**. 
2. Zrušte zaškrtnutí políčka **Send us usage information to help improve your customer experience in the future** (Posílat nám informace o použití k vylepšení zkušeností uživatelů v budoucnosti). 

## <a name="additional-resources"></a>Další zdroje

- Informace o ATA zabezpečení a dodržování předpisů, najdete v článku [portálu důvěryhodnosti služeb](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) a [dodržování předpisů GDPR pro Microsoft 365 Enterprise lokality](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).

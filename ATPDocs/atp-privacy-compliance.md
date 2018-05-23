---
title: Azure Advanced Threat Protection osobní data zásad | Microsoft Docs
description: Obsahuje odkazy na informace o tom, jak odstranit soukromé informace a osobní data z Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 1e890491b44bcf97a7f0f19d825155072ac1a2f4
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
---
*Platí pro: Azure Advanced Threat Protection*

# <a name="azure-atp-data-security-and-privacy"></a>Azure ATP data zabezpečení a ochrana osobních údajů

> [!NOTE]
> Pokud vás zajímá zobrazení nebo odstranění osobních údajů, přečtěte si pokyny společnosti Microsoft v [správce dodržování předpisů Microsoft](https://servicetrust.microsoft.com/ComplianceManager) a v [GDPR části webu Microsoft 365 Enterprise dodržování předpisů](https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr). Pokud hledáte obecné informace o GDPR, přečtěte si téma [GDPR části portálu služby důvěřovat](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## <a name="search-for-and-identify-personal-data"></a>Vyhledat a identifikovat osobní data 

V Azure Advanced Threat Protection můžete zobrazit identifikovatelné osobní údaje z [prostoru portálu](workspace-portal.md) pomocí [panelu Hledat](workspace-portal.md#search-bar). 

Můžete vyhledat konkrétní uživatele nebo počítač, a kliknutím na entity přejdete na uživatele nebo počítače [stránky profil](entity-profiles.md). Profil poskytuje komplexní podrobnosti o entitě ze služby Active Directory, včetně síťové aktivity související s dané entity a jeho historie.

Azure ATP osobních údajů je získané ze služby Active Directory pomocí senzoru Azure ATP a uloženy v databázi back-end.

## <a name="update-personal-data"></a>Aktualizovat osobní data 

Vzhledem k tomu, že osobní údaje uživatele Azure ATP je odvozený z objektu uživatele ve službě Active Directory organizace, všechny změny provedené v profilu uživatele ve službě AD se projeví v Azure ATP.


## <a name="delete-personal-data"></a>Odstranit osobní data 

Po odstranění uživatele ze služby Active Directory organizace Azure ATP automaticky odstraní uživatelský profil a všechny související síťové aktivity v roce. Můžete také [odstranit](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) všechny výstrahy zabezpečení, které obsahují osobní údaje. 

## <a name="export-personal-data"></a>Exportovat osobní údaje 

V Azure ATP máte možnost [export]((working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) výstrahy informace zabezpečení do aplikace Excel. To bude také exportovat osobní data. 
 
## <a name="audit-personal-data"></a>Osobní data auditu

 
Azure ATP implementuje auditování změn osobní data, včetně odstranění a export záznamů osobní data. Doba uchování záznamu pro audit je 90 dní. V Azure ATP auditování je funkce back-end a není k dispozici pro zákazníky.
 

 

## <a name="additional-resources"></a>Další materiály a zdroje informací

- Informace o vztahu důvěryhodnosti Azure ATP a dodržování předpisů najdete v tématu [vztah důvěryhodnosti služby portálu](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) a [Microsoft 365 Enterprise GDPR kompatibility lokality](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).

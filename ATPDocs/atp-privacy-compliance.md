---
title: Zásady osobních údajů rozšířené ochrany před internetovými útoky v Azure | Microsoft Docs
description: Obsahuje odkazy na informace o tom, jak odstranit soukromé informace a osobní údaje z Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 08/11/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: af8481be19535903ca1e992a62a813acb473fcf0
ms.sourcegitcommit: e185d6cf13ef0c40206a5d1980e3953ef8834a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2019
ms.locfileid: "68951259"
---
# <a name="azure-atp-data-security-and-privacy"></a>Zabezpečení dat a ochrana osobních údajů v Azure ATP

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Hledání a identifikace osobních údajů 

Rozšířená ochrana před internetovými útoky v Azure vám umožní zobrazit identifikovatelné osobní údaje z [portálu Azure ATP](workspace-portal.md) pomocí [panelu hledání](workspace-portal.md#search-bar). 

Vyhledejte konkrétního uživatele nebo počítač a kliknutím na entitu se přepněte na [stránku profil](entity-profiles.md)uživatele nebo počítače. Profil poskytuje podrobné informace o entitě ze služby Active Directory, včetně síťové aktivity spojené s touto entitou a její historií.

Osobní údaje z Azure ATP se shromažďují ze služby Active Directory prostřednictvím snímače ATP Azure a ukládají se do back-endu databáze.

## <a name="update-personal-data"></a>Aktualizace osobních údajů 

Data osobního uživatele v Azure ATP jsou odvozená od objektu uživatele ve službě Active Directory organizace. Změny provedené v profilu uživatele v organizačním prostředí se proto projeví ve službě Azure ATP.


## <a name="delete-personal-data"></a>Odstranit osobní údaje 

- Po odstranění uživatele ze služby Active Directory organizace Azure ATP automaticky odstraní profil uživatele a všechny související síťové aktivity v roce. Můžete také [Odstranit](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) všechny výstrahy zabezpečení, které obsahují osobní údaje. 

- Doporučuje se oprávnění **jen pro čtení** na kontejneru odstraněných **objektů** . Další informace o tom, jak se ve službě Azure ATP používá oprávnění kontejneru odstraněné objekty * *, najdete v tématu doporučení kontejneru odstraněných objektů v tématu [požadavky Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/atp-prerequisites#before-you-start).

## <a name="export-personal-data"></a>Export osobních dat 

V Azure ATP máte možnost [exportovat](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) informace o výstrahách zabezpečení do Excelu. Tato funkce také exportuje osobní údaje. 
 
## <a name="audit-personal-data"></a>Audit osobních dat

Azure ATP implementuje Audit změn osobních údajů, včetně odstranění a exportu osobních záznamů. Doba uchovávání záznamu auditu je 90 dní. Auditování v Azure ATP je back-endové funkce a není pro ně přístupná pro zákazníky.
 
## <a name="additional-resources"></a>Další zdroje

- Informace o důvěryhodnosti a dodržování předpisů v Azure ATP najdete na [portálu Trust Service](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) a na [webu dodržování předpisů Microsoft 365 Enterprise GDPR](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).

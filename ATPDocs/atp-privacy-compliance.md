---
title: Azure osobní údaje zásady rozšířené ochrany před internetovými útoky | Dokumentace Microsoftu
description: Obsahuje odkazy na informace o tom, jak odstranit soukromé informace a osobní data ze služby Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/26/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: d64cc0d40acc31e2187305c38a625924a91db06b
ms.sourcegitcommit: 7d025a2518ce63f38ce609dc21d8c3bacdd6a8e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/26/2018
ms.locfileid: "36948927"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*

# <a name="azure-atp-data-security-and-privacy"></a>Zabezpečení dat ve službě Azure ATP a ochrana osobních údajů

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Vyhledat a identifikovat osobní údaje 

V rozšířené ochrany před internetovými útoky pro Azure můžete zobrazit identifikovatelné osobní údaje [portálu pracovního prostoru](workspace-portal.md) pomocí [vyhledávacího](workspace-portal.md#search-bar). 

Můžete vyhledat konkrétního uživatele nebo počítače a kliknete na entitu vás přivedou k uživateli nebo počítači [stránku profilu](entity-profiles.md). Profil, který vám poskytne komplexní podrobnosti o entitě ze služby Active Directory, včetně síťové aktivity související s touto entitou a jeho historie.

Azure ATP osobních údajů je získané ze služby Active Directory pomocí senzoru služby Azure ATP a uloženy v databázi back-endu.

## <a name="update-personal-data"></a>Aktualizovat osobní údaje 

Protože osobní údaje uživatelů ochrany ATP v programu Azure je odvozen z objektu uživatele ve službě Active Directory organizace, všechny změny provedené v profilu uživatele v AD se projeví v ochrany ATP v programu Azure.


## <a name="delete-personal-data"></a>Odstranění osobních údajů 

Po odstranění uživatele ze služby Active Directory organizace ochrany ATP v programu Azure automaticky odstraní profil uživatele a všechny související síťové aktivity v roce. Můžete také [odstranit](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) všechny výstrahy zabezpečení, které obsahují osobní údaje. 

## <a name="export-personal-data"></a>Export osobních údajů 

V ochraně ATP v Azure máte možnost [exportovat](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) informace o výstrahách zabezpečení do aplikace Excel. To se také exportovat osobní údaje. 
 
## <a name="audit-personal-data"></a>Osobní data auditu

Ochrana ATP v programu Azure implementuje auditu změn osobní údaje, včetně, odstraňování a export záznamů osobní údaje. Doba uchování záznamu pro audit je 90 dní. Auditování v ochrany ATP v programu Azure je funkce back-end a není k dispozici zákazníkům.
 
## <a name="additional-resources"></a>Další materiály a zdroje informací

- Informace o důvěryhodnosti ochrany ATP v programu Azure a dodržování předpisů, najdete v článku [portálu důvěryhodnosti služeb](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) a [dodržování předpisů GDPR pro Microsoft 365 Enterprise lokality](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).

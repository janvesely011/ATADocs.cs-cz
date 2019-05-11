---
title: Azure osobní údaje zásady rozšířené ochrany před internetovými útoky | Dokumentace Microsoftu
description: Obsahuje odkazy na informace o tom, jak odstranit soukromé informace a osobní data ze služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 10/04/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 6758527b61e2b1ab440898ed23aa7d507d8f3b3c
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196798"
---
# <a name="azure-atp-data-security-and-privacy"></a>Zabezpečení dat ve službě Azure ATP a ochrana osobních údajů

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Vyhledat a identifikovat osobní údaje 

V rozšířené ochrany před internetovými útoky pro Azure můžete zobrazit identifikovatelné osobní údaje [ochrany ATP v programu Azure portal](workspace-portal.md) pomocí [vyhledávacího](workspace-portal.md#search-bar). 

Vyhledat konkrétního uživatele nebo počítače a klikněte na některou entitu, aby vám uživatele nebo počítače [stránku profilu](entity-profiles.md). Profil, který vám poskytne komplexní podrobnosti o entitě ze služby Active Directory, včetně síťové aktivity související s touto entitou a jeho historie.

Azure ATP osobních údajů je získané ze služby Active Directory pomocí senzoru služby Azure ATP a uloženy v databázi back-endu.

## <a name="update-personal-data"></a>Aktualizovat osobní údaje 

Azure ATP osobní uživatelské data jsou odvozena z objektu uživatele ve službě Active Directory organizace. Proto se projeví změny provedené v profilu uživatele v organizaci AD v ochrany ATP v programu Azure.


## <a name="delete-personal-data"></a>Odstranění osobních údajů 

Po odstranění uživatele ze služby Active Directory organizace ochrany ATP v programu Azure automaticky odstraní profil uživatele a všechny související síťové aktivity v roce. Můžete také [odstranit](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) všechny výstrahy zabezpečení, které obsahují osobní údaje. 

## <a name="export-personal-data"></a>Export osobních dat 

V ochraně ATP v Azure máte možnost [exportovat](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) informace o výstrahách zabezpečení do aplikace Excel. Tato funkce zároveň exportuje osobní údaje. 
 
## <a name="audit-personal-data"></a>Audit osobních dat

Ochrana ATP v programu Azure implementuje auditu změn osobní údaje, včetně, odstraňování a export záznamů osobní údaje. Doba uchování záznamu pro audit je 90 dní. Auditování v ochrany ATP v programu Azure je funkce back-end a není k dispozici zákazníkům.
 
## <a name="additional-resources"></a>Další zdroje

- Informace o důvěryhodnosti ochrany ATP v programu Azure a dodržování předpisů, najdete v článku [portálu důvěryhodnosti služeb](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) a [dodržování předpisů GDPR pro Microsoft 365 Enterprise lokality](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).

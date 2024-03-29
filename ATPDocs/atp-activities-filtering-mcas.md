---
title: Azure Advanced Threat Protection aktivity filtrování a zásadami v Microsoft Cloud App Security | Dokumentace Microsoftu
description: Přehled služby Azure ATP aktivity filtrování a zásad pomocí Microsoft Cloud App Security.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 397e5a77-2bc7-454c-9fe5-649ebaab16b3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1508cb558f16adf54f80cec0c13631059dbf45bf
ms.sourcegitcommit: f60835d655e68ffaa8ed8c43bd9fa20233d7e495
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506540"
---
# <a name="use-activity-filters-and-create-action-policies-with-azure-atp-in-microsoft-cloud-app-security"></a>Použít filtry aktivity a pomocí služby Azure ATP v Microsoft Cloud App Security vytvořit zásady 

Tento článek slouží k vám pomohou pochopit, jak filtrovat a vytvářet zásady ochrany ATP v programu Azure aktivity pomocí Microsoft Cloud App Security. 

Další informace o tom, jak provést integraci, naleznete v tématu [integrace Azure ochrany ATP v programu Cloud App Security](https://docs.microsoft.com/cloud-app-security/aatp-integration/enable-azure-advanced-threat-protection).  

Pomocí služby Azure ATP s Microsoft Cloud App Security nabízí Analýza aktivit a výstrahy na základě uživatele a Entity chování Analytics (Behavioral), identifikace nejrizikovějších chování ve vašem podniku, poskytuje komplexní šetření priority skóre, stejně jako Aktivita filtrování a přizpůsobitelné aktivity zásad. 

## <a name="prerequisites"></a>Požadavky

Úplné uživatelské funkce šetření napříč hybridním prostředím musíte mít:
- Platnou licenci pro Microsoft Cloud App Security
- Platné licence ochrany ATP v programu Azure připojené k vaší instanci služby Active Directory

>[!NOTE]
>Pokud nemáte předplatné pro Cloud App Security, portál Cloud App Security můžete prozkoumat upozornění ochrany ATP v programu Azure a podrobné informace o uživatelích a jejich místní spravované aktivity však zůstanou přehledy související s: vašich cloudových aplikací není k dispozici.

## <a name="filter-azure-atp-activities-in-cloud-app-security"></a>Filtrovat aktivity služby Azure ATP v Cloud App Security  
 
Azure aktivity ochrany ATP v programu je přístupný z hlavní Cloud App Security **prošetření** nabídky tak, že vyberete **protokolu aktivit** podnabídky, nebo z **výstrahy** nabídky podle stavu, kategorie, závažnosti, aplikace, uživatelské jméno nebo zásad.  

Pro přístup k Azure ATP aktivity podle uživatele:

1. Filtr **výstrahy** fronty pomocí pole uživatelské jméno. 
    ![Upozornění fronty](media/atp-mcas-alerts-queue.png)
1. Klikněte na uživatelské jméno u některého upozornění v seznamu výsledků otevřít **stránku uživatele** uživatele, kterou chcete prozkoumat. 
    
1. Filtrovat aktivity uživatele pomocí dostupná pole nebo přidat nové pravidlo filtru pomocí tlačítko +.
    ![Upozornění fronty](media/atp-mcas-activity-filter.png)

## <a name="create-activity-policies-in-cloud-app-security"></a>Vytvořit zásady aktivit v Cloud App Security

Po filtrování aktivit a chcete implementovat zásady aktivit nebo nesplňujících požadavky v rámci vaší organizace, použijte **vytvořit novou zásadu aktivit** možnost z nabídky Filtr okamžitě vytvořit nový vlastní zásady pro uživatele, zařízení nebo tenanta. 

Chcete-li vytvořit novou zásadu aktivit:

1. Z libovolného **protokolu aktivit** stránky, použijte filtr (jako je například aplikace, uživatelské jméno, typ aktivity) atd. 
    - Chcete-li filtrovat aktivity z ochrany ATP v programu Azure vyberte **služby Active Directory** volba ve filtru aplikace. 
    ![Vytvoření nové zásady aktivit](media/atp-mcas-create-new-policy.png)
1. Klikněte na tlačítko **nová zásada z hledání** tlačítko.    
1. Přidat **Název_zásady**. 
    ![Vytvořit novou zásadu aktivit – krok 2](media/atp-mcas-create-policy.png)
1. Přidání zásady **popis**.  
1. Přiřazení **závažnost** zásad.
1. Vyberte **kategorie** zásady.
1. Zvolte nebo upravte filtry k vytvoření a přiřazení zásad.
1. Upravit nebo přidat další filtry. 
1. Uložit a použít nové zásady.  


## <a name="next-steps"></a>Další postup

Další informace o vyšetřování priority bodování a další funkce [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/) funkce.
  
## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) ještě dnes!





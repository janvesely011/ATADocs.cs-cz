---
title: Rozšířená ochrana před internetovými útoky v Microsoft Cloud App Security | Dokumentace Microsoftu
description: Přehled funkcí služby Azure ATP v rámci Microsoft Cloud App Security.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 5169dffc-75c4-4eb0-b997-b5359cecda97
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b66b2f0a087bbaacc09eda54958824da693209b3
ms.sourcegitcommit: f60835d655e68ffaa8ed8c43bd9fa20233d7e495
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506503"
---
# <a name="using-azure-atp-with-microsoft-cloud-app-security"></a>Ochrana ATP v programu Azure pomocí Microsoft Cloud App Security 


Tento článek slouží k vám pomůžou pochopit a přejděte možnosti pro rozšířené zkoumání během používání portálu společnosti Microsoft Cloud App Security pomocí služby Azure ATP. 

Využití stávajících detekcí místní a neobvyklé chování analytics, přístup k portálu Microsoft Cloud App Security pomocí služby Azure ATP umožňuje přidání zjišťovat a upozorňovat na průsak citlivých dat ven napříč vaší organizace a zároveň filtru aktivity a vytváření užitečných zásad. Tuto nabídku hybridní analyzuje aktivity a upozornění na základě uživatele a analýzy chování entit (Behavioral) k určení nebezpečné chování a poskytuje skóre priority šetření zjednodušit vaše reakce na incidenty pro ohrožení zabezpečení identity. 

V tomto článku se dozvíte:

> [!div class="checklist"]
> * Přehled služby
> * Nové možnosti pro přístup k Azure ATP
> * Licenční požadavky
> * Kde najít ochrany ATP v programu Azure sledovat aktivity ve službě Cloud App Security

## <a name="service-overview"></a>Přehled služby

Integrace s Azure ATP, portál Cloud App Security nabízí výstrahy a přehledy na základě:
- Microsoft Cloud App Security, které identifikuje útoků v rámci relace cloud, pokrývá pouze produkty Microsoftu, ale také aplikací třetích stran
- Azure Advanced Threat Protection, který využívá strojové učení a behaviorální analýzy k identifikaci útoků ve vaší místní síti
- Azure Active Directory Identity Protection, která zjistí a proaktivně brání rizika uživatele a přihlaste se k identit v cloudu

## <a name="access-azure-atp"></a>Přístup k Azure ATP

Zvolte možnost k pokračování využití služby Azure ATP v rámci ochrany ATP v programu Azure portal nebo upozornění služby Azure ATP a vyhodnocování identit na portálu Microsoft Cloud App Security můžete přistupovat. V obou pracovních postupů nastavení a konfiguraci úlohy ochrany ATP v programu Azure nadále zpracovávány v rámci ochrany ATP v programu Azure portal. 

 

## <a name="prerequisites"></a>Požadavky

Úplné uživatelské funkce šetření napříč hybridním prostředím musíte mít:
- Platnou licenci pro Microsoft Cloud App Security
- Platné licence ochrany ATP v programu Azure připojené k vaší instanci služby Active Directory
 
>[!NOTE]
>Pokud nemáte předplatné pro Cloud App Security, bude ji moct prozkoumat upozornění ochrany ATP v programu Azure pomocí portálu Cloud App Security a podívejte se na uživatele a jejich místní spravovat aktivit, ale neobdržíte žádné související přehledy z vašeho cloudu aplikace.

Zobrazit [integrace služby Azure ATP](https://docs.microsoft.com/cloud-app-security/aatp-integration) se naučíte rychle povolit Azure ATP v Cloud App Security.  
 
## <a name="azure-atp-in-cloud-app-security"></a>Azure ATP v Cloud App Security 

Zobrazit [rychlý start Cloud App Security](https://docs.microsoft.com/cloud-app-security/getting-started-with-cloud-app-security) se seznámit se základními funkcemi na portálu Cloud App Security. 

Přístup k vaší ochrany ATP v programu Azure datům a nových funkcích pro hybridní nasazení v rámci upozornění, aktivit a stránky uživatele Cloud App Security. 

## <a name="alerts"></a>Upozornění

Upozornění Azure ochrany ATP v programu se zobrazí v Cloud App Security **výstrahy** fronty. Další možnosti filtrování výstrah jsou k dispozici pouze při zobrazení výstrah pomocí Cloud App Security. Upozornění ochrany ATP v programu Azure jsou filtrovány pomocí filtru, který aplikace k **služby Active Directory**. 

## <a name="alert-management"></a>Správa výstrah
Při použití služby Azure ATP s Cloud app security, zavírání výstrah v jedné službě nebude automaticky zavře je v jiné službě. Rozhodněte, kam ke správě a náprava výstrahy a vyhněte se duplicitním úsilí. 

## <a name="siem-notification"></a>Oznámení SIEM

Pokud obě služby (ochrany ATP v programu Azure a Cloud App Security) jsou aktuálně nakonfigurované k odeslání oznámení do systému SIEM, po povolení integrace služby Azure ATP v Cloud App Security, budete začít přijímat duplicitní SIEM oznámení pro stejnou výstrahu. Jedna výstraha něhož budou vydány z každé služby a budou mít různé ID výstrah. Nechcete duplicity a provádí nejasnosti, rozhodněte, kam chcete provádět Správa výstrah a poté zastavte SIEM oznámení odeslané z jiné služby.  

## <a name="activities"></a>Aktivity

Upozornění Azure ochrany ATP v programu se zobrazí v Cloud App Security **protokolu aktivit**. Možnosti filtrování další aktivity a funkce jsou k dispozici pouze při zobrazení výstrah pomocí Cloud App Security. Zobrazit [aktivity ochrany ATP v programu Azure pomocí Microsoft Cloud App Security](https://docs.microsoft.com/azure-advanced-threat-protection/atp-activities-filtering-mcas) informace o filtrování a vytvořit nové zásady aktivit.  

## <a name="user-pages"></a>Uživatel stránky 

Obsahují stránky uživatele [skóre Priority šetření](https://docs.microsoft.com/cloud-app-security/tutorial-ueba) každého uživatele a protokolu aktivity všech akcí. 

Ke stránce uživatele systému uživatele:
1. Otevřít **výstrahy** z hlavní nabídky.
1. Výběr a filtrování pomocí fronty upozornění pro konkrétního uživatele **uživatelské jméno** pole.

 nebo

1. Z **prošetření** nabídce vyberte možnost **protokolu aktivit**. 
1. Filtrování protokolu fronty aktivity podle uživatele. 

    ![Protokol aktivit](media/atp-mcas-activity-filter.png)

## <a name="next-steps"></a>Další postup

Zobrazit [aktivity ochrany ATP v programu Azure pomocí Microsoft Cloud App Security](https://docs.microsoft.com/azure-advanced-threat-protection/atp-activities-filtering-mcas) informace o filtrování a vytvořit nové zásady aktivit. 
  
## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) ještě dnes!





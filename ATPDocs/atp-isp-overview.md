---
title: Stav posouzení zabezpečení identity rozšířené ochrany před internetovými útoky v Azure | Microsoft Docs
description: Tento článek poskytuje přehled sestav hodnocení zabezpečení stav v Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 71b15bd9-3183-4e24-b18a-705023ccc313
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b36095568d0e48d34c3b904b59e6d10c8ebf244e
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71005232"
---
# <a name="azure-atps-identity-security-posture-assessments"></a>Posouzení stav zabezpečení identity v Azure ATP
 
Organizace všech velikostí obvykle mají omezený přehled o tom, zda jejich místní aplikace a služby mohly způsobit ohrožení zabezpečení jejich organizace. Problém omezené viditelnosti je obzvláště pravda, pokud jde o použití nepodporovaných nebo zastaralých komponent. 

I když vaše společnost může investovat značnou dobu a úsilí na posílení identit a infrastruktury identit (jako je Active Directory, Active Directory Connect) jako prohlášený projekt, snadno si zachováte nevědomě běžných chybových konfigurací a používání starších verzí. komponenty, které reprezentují jedno z největších rizik pro hrozby vaší organizace. Microsoft Security Research odhalí, že většina útoků na identity využívá běžné neúspěšné konfigurace služby Active Directory a pokračuje v používání starších komponent (například protokolu ověřovací NTLMv1) k ohrožení identit a k úspěšnému porušení vaší organizace. Za účelem boje proti tomu Azure ATP teď nabízí proaktivní posuzování stav zabezpečení identity pro zjišťování a navrhování akcí zlepšování napříč místními konfiguracemi služby Active Directory. 

## <a name="what-do-azure-atp-identity-security-posture-assessments-provide"></a>Co stav posouzení zabezpečení identity v Azure ATP?  
- Detekce a kontextová data pro známé zneužitelné součásti a chyby konfigurace spolu s příslušnými cestami k nápravě.
- Azure ATP detekuje nejen podezřelé aktivity, ale aktivně sleduje místní identity a infrastrukturu identit pro slabá označení pomocí stávajícího senzoru ATP Azure. 
- Přesné sestavy hodnocení aktuálního stav zabezpečení organizace, které umožňují monitorování rychlých odpovědí a efektů v nepřetržitém cyklu. 

## <a name="how-do-i-get-started"></a>Návody začít? 

### <a name="access"></a>Access

Posouzení zabezpečení ATP Azure je dostupné po zapnutí integrace ATP Azure pomocí Microsoft Cloud App Securityového portálu. Informace o tom, jak integrovat Azure ATP do Cloud App Security, najdete v tématu [integrace služby Azure ATP](https://docs.microsoft.com/cloud-app-security/aatp-integration). 

### <a name="licensing"></a>Správa licencí

Přístup k sestavám vyhodnocení zabezpečení Azure ATP v Cloud App Security nevyžadují licenci Cloud App Security, vyžaduje se jenom licence Azure ATP. 

## <a name="access-azure-atp-using-cloud-app-security"></a>Přístup k Azure ATP pomocí Cloud App Security 

V [Cloud App Security rychlém startu](https://docs.microsoft.com/cloud-app-security/getting-started-with-cloud-app-security) se seznamte se základy používání portálu Cloud App Security. 

**Stav vyhodnocení zabezpečení identity**

Azure ATP nabízí následující posouzení stav zabezpečení identity. Každé posouzení je sestava ke stažení s pokyny pro použití a nástroje pro sestavení akčního plánu, který chcete opravit nebo vyřešit. 

**Sestavy posouzení**
- Zabránit úniku [údajů](atp-cas-isp-clear-text.md) o nešifrovaných textech
- Zabránit [komunikaci starších protokolů](atp-cas-isp-legacy-protocols.md)
- Zabránit [slabému použití šifry](atp-cas-isp-weak-cipher.md)
- Zabránit [neomezením delegování protokolu Kerberos](atp-cas-isp-unconstrained-kerberos.md)
- Zakázat [službu zařazování tisku na řadičích domény](atp-cas-isp-print-spooler.md)
- Odebrat [entity neaktivní z citlivých skupin](atp-cas-isp-dormant-entities.md)

Přístup k vyhodnocování stav identity Security:
1. Otevřete portál **Microsoft Cloud App Security** . 
    ![Přístup k sestavám zabezpečení Azure ATP identity stav v Cloud App Security](media/atp-cas-isp-report-1.png)
1. V nabídce vlevo vyberte **prozkoumat** a pak v rozevírací nabídce klikněte na **zabezpečení identity stav** . 
1. Klikněte na vyhodnocování stav identity Security, které chcete zkontrolovat, ze seznamu **sestavy posouzení zabezpečení** , které se otevře.  


## <a name="next-steps"></a>Další kroky
- [Další informace o použití Cloud App Security s využitím Azure ATP](atp-activities-filtering-mcas.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)


---
title: Vyhodnocení expozice prostého textu v Azure Advanced Threat Protection | Microsoft Docs
description: Tento článek poskytuje přehled zprávy o posouzení stav zabezpečení identity v Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 124957bb-5882-4fcf-bab2-b74b0c69571d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8e99ab22e65538aba6f645d6bb7929330244cafc
ms.sourcegitcommit: 475df3e87d8476ff13e48ebc7a722f46f29dab70
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71007558"
---
# <a name="security-assessment-entities-exposing-credentials-in-clear-text-----preview"></a>Posouzení zabezpečení: Entity, které zpřístupňují přihlašovací údaje ve formátu prostého textu – Preview

![Zabránit úniku přihlašovacích údajů nezašifrovaných textů v Cloud App Security](media/atp-cas-isp-clear-text-1.png)

## <a name="what-information-does-the-prevent-clear-text-security-assessment-provide"></a>Jaké informace poskytuje vyhodnocování zabezpečení zabránit jasnému textu? 

Toto posouzení zabezpečení monitoruje váš provoz u všech entit, které vystavují přihlašovací údaje ve formě prostého textu, a upozorňuje vás na aktuální rizika při expozici (nejvíce ovlivněných entit) ve vaší organizaci s navrhovanou nápravou. 

## <a name="why-is-clear-text-credential-exposure-risky"></a>Proč je jasné, že rizikové přihlašovací údaje nezpůsobují riziko?  
Entity, které vystavují přihlašovací údaje ve formě prostého textu, jsou rizikové nejen pro danou nevystavenou entitu, ale pro celou organizaci.  

Zvýšení rizika je způsobeno tím, že nezabezpečený provoz, jako je například jednoduchá vazba LDAP, je vysoce náchylná k zachycení prostřednictvím útoků prostředníkem. Tyto typy útoků způsobují škodlivé aktivity, včetně ohrožení přihlašovacích údajů, kdy útočník může využít přihlašovací údaje ke škodlivým účelům. 

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Návody pomocí tohoto posouzení zabezpečení zlepšit stav podnikového zabezpečení? 

1. Přečtěte si téma posouzení zabezpečení ovlivněných entit. 
    ![Kontrola nejdůležitějších ovlivněných entit a vytvoření plánu akcí](media/atp-cas-isp-clear-text-2.png)
1. Prozkoumat, proč tyto entity používají protokol LDAP ve formě prostého textu. 
1. Opravte problémy a zastavte expozici. 
1. Po potvrzení nápravy doporučujeme vyžadovat podepisování LDAP na úrovni řadiče domény. Další informace o podepisování serveru LDAP najdete v tématu [požadavky na podpis serveru LDAP řadiče domény](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements). 
 

## <a name="next-steps"></a>Další postup
- [Filtrování aktivit v Azure ATP v Cloud App Security](atp-activities-filtering-mcas.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

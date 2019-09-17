---
title: Rozšířená ochrana před internetovými útoky Azure – stav posouzení zabezpečení identity protokolu Kerberos | Microsoft Docs
description: Tento článek poskytuje přehled stavch hodnotících sestav zabezpečení identity protokolu Kerberos v Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7eea354b-7a50-40d9-bfa7-dcccaef23179
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1343d0359750744890fdb3e15b5f49adfd2459d1
ms.sourcegitcommit: 475df3e87d8476ff13e48ebc7a722f46f29dab70
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71007445"
---
# <a name="security-assessment-unsecure-kerberos-delegation---preview"></a>Posouzení zabezpečení: Nezabezpečené delegování protokolu Kerberos – Preview


## <a name="what-is-kerberos-delegation"></a>Co je delegování protokolu Kerberos? 

Delegování protokolu Kerberos je nastavení delegování umožňující aplikacím vyžadovat přihlašovací údaje pro přístup koncových uživatelů k přístupu k prostředkům jménem původního uživatele.  

## <a name="what-risk-does-unsecure-kerberos-delegation-pose-to-an-organization"></a>Jaké riziko nezabezpečuje delegování protokolu Kerberos organizaci? 

Nezabezpečené delegování protokolu Kerberos dává entitě možnost zosobnit se k libovolné jiné zvolené službě. Představte si například, že máte web IIS a že účet fondu aplikací je nakonfigurovaný s neomezeným delegováním. Web IIS má také povolený ověřování systému Windows, povoluje nativní ověřování protokolem Kerberos a lokalita používá back-endové SQL Server pro obchodní data. Pomocí účtu správce domény přejděte na web IIS a ověřte ho. Web s použitím neomezeného delegování je schopný získat lístek služby z řadiče domény do služby SQL a zadat ho do svého jména.

Hlavní problém s delegováním protokolu Kerberos je, že je potřeba, abyste aplikaci důvěřovali tak, aby vždy měla správnou věc. Škodlivé objekty actor mohou místo toho vynutit, aby aplikace provedla nesprávné věci. Pokud jste přihlášeni jako **správce domény**, lokalita může vytvořit lístek k jakékoli jiné službě, kterou chce, a jednat jako vy, **správce domény**. Lokalita může například zvolit řadič domény a provést změny ve skupině **Enterprise Admins** . Podobně může web získat hodnotu hash účtu KRBTGT nebo si stáhnout zajímavý soubor od vašeho oddělení lidských zdrojů. Riziko je jasné a možnosti nezabezpečeného delegování jsou skoro nekonečné. 

 
## <a name="how-do-i-use-this-security-assessment"></a>Návody použít toto posouzení zabezpečení?

1. Pomocí tabulky sestav můžete zjistit, které z jiných entit řadičů domény jsou nakonfigurované pro **nezabezpečené delegování protokolu Kerberos**.    
    <br>![Nezabezpečené vyhodnocení zabezpečení delegování protokolu Kerberos](media/atp-cas-isp-kerberos-delegation-2.png)
1. V případě rizikových uživatelů, jako je odebrání jejich neomezeného atributu nebo jejich změna na bezpečnější omezené delegování, proveďte příslušné akce.

## <a name="remediation"></a>Náprava

Další informace o Oprava těchto typů účtů najdete v tématu [Odebrání účtů využívajících neomezená delegování protokolu Kerberos](https://blogs.technet.microsoft.com/389thoughts/2017/04/18/get-rid-of-accounts-that-use-kerberos-unconstrained-delegation/).

## <a name="next-steps"></a>Další kroky
- [Filtrování aktivit v Azure ATP v Cloud App Security](atp-activities-filtering-mcas.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

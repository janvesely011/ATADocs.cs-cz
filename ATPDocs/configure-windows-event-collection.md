---
title: Konfigurovat shromažďování událostí Windows Azure Advanced Threat Protection | Microsoft Docs
description: V tomto kroku instalace ATP nakonfigurujete shromažďování událostí systému Windows.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0478ab7dea7a8476faf61175654e6c50b10e9418
ms.sourcegitcommit: 0a98c0c151be2a81a3bb9ff1301d35a3091079ea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71217752"
---
# <a name="configure-windows-event-collection"></a>Konfigurace shromažďování událostí systému Windows

Aby bylo možné zlepšit možnosti detekce hrozeb, Azure Advanced Threat Protection (Azure ATP) potřebuje následující události systému Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045 a 8004. Tyto události mohou být buď automaticky čteny pomocí snímače ATP v Azure, nebo pokud není senzor Azure ATP nasazený, dá se jednomu ze dvou způsobů přesměrovat do samostatného senzoru Azure ATP, protože [nakonfigurujeme samostatný senzor Azure ATP](configure-event-forwarding.md) , aby naslouchal Siem. události nebo [konfigurace předávání událostí systému Windows](configure-event-forwarding.md).

> [!NOTE]
> Před povolením shromažďování událostí je důležité zkontrolovat a ověřit [zásady auditu](atp-advanced-audit-policy.md) , aby bylo zajištěno, že řadiče domény budou správně nakonfigurovány pro zaznamenávání potřebných událostí. 

Kromě shromažďování a analýzy síťového provozu do a z řadičů domény může Azure ATP využít události systému Windows k dalšímu vylepšení detekce. Azure ATP používá pro protokol NTLM událost 4776 a 8004, což vylepšuje různé detekce a události 4732, 4733, 4728, 4729, 4756, 4757 a 7045 a 8004 pro zlepšení detekce citlivých úprav skupin a vytváření služeb. Tyto události mohou být přijímány ze služby SIEM nebo nastavením předávání událostí Windows z řadiče domény. Shromážděné události poskytují Azure ATP dalšími informacemi, které nejsou k dispozici prostřednictvím síťového provozu řadiče domény.

## <a name="ntlm-authentication-using-windows-event-8004"></a>Ověřování NTLM pomocí události systému Windows 8004

Konfigurace kolekce Event 8004 pro Windows:
1. Přejít na: Cestě konfigurace možnosti počítače \ \ pro Policies\Security
2. Nastavte **Zásady skupiny domény** následujícím způsobem:
   - Zabezpečení sítě: Omezit protokol NTLM: Odchozí přenosy protokolu NTLM na vzdálené servery = **Auditovat vše**
   - Zabezpečení sítě: Omezit protokol NTLM: Auditovat ověřování NTLM v této doméně = **Povolit vše**
   - Zabezpečení sítě: Omezit protokol NTLM: Auditovat příchozí přenosy protokolu NTLM = **Povolit auditování pro všechny účty**

Když je událost 8004 systému Windows analyzována pomocí senzoru ATP Azure ATP, aktivity ověřování pomocí protokolu NTLM pro Azure ATP se rozšiřují pomocí dat pro přístup k serveru.

## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Reference k protokolu Azure ATP SIEM](cef-format-sa.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

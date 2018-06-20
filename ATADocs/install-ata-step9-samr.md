---
title: Konfigurace SAM-R, aby se povolilo rozpoznání laterálního pohybu cestu v Advanced Threat Analytics | Microsoft Docs
description: Popisuje postup konfigurace SAM-R, aby se povolilo rozpoznání laterálního pohybu cestu v Advanced Threat Analytics (ATA)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/25/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6e32f3ce59b049d0ced68a1330eefca7315bf49d
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/30/2018
ms.locfileid: "32298363"
---
*Platí pro: Advanced Threat Analytics verze 1.9*

# <a name="install-ata---step-9"></a>Instalace ATA – krok 9

>[!div class="step-by-step"]
[«Krok 8](install-ata-step7.md)

## <a name="step-9-configure-sam-r-required-permissions"></a>Krok 9: Konfigurace SAM-R požadované oprávnění

[Laterální pohyb cesta](use-case-lateral-movement-path.md) detekce spoléhá na dotazy, které identifikují místní správci na konkrétní počítače. Tyto dotazy se provádí pomocí protokolu SAM-R, prostřednictvím účtu služby ATA vytvořené v [kroku 2. Připojení ke službě AD](install-ata-step2.md).
 
K zajištění, že Windows klienty a servery povolit účet služby ATA k provedení této operace SAM-R změny vašeho **zásady skupiny** musí být provedeny, přidá účet služby ATA kromě nakonfigurované účty uvedené v **přístup k síti** zásad.

1. Vyhledejte zásady:

 - Název zásady: Přístup k síti – omezovat klienty povolit vzdálené volání SAM
 - Umístění: Konfigurace, nastavení systému Windows, nastavení zabezpečení, místní zásady zabezpečení možnosti
  
  ![Vyhledejte zásady](./media/samr-policy-location.png)

2. Služba ATA přidejte do seznamu schválených účtů může k provedení této akce na vaše moderní systémy Windows.
 
  ![Přidání služby](./media/samr-add-service.png)

3. **Služba ATA** (služba ATA vytvoří během instalace) teď má správná oprávnění k provedení SAMR v prostředí.

Další informace o SAM-R a tyto zásady skupiny, najdete v článku [přístup k síti: omezovat klienty povolit vzdálené volání SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Krok 8](install-ata-step7.md)

## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

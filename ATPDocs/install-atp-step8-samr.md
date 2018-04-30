---
title: Konfigurace SAM-R, aby se povolilo rozpoznání laterálního pohybu cestu v Azure ATP | Microsoft Docs
description: Popisuje postup konfigurace SAM-R, aby se povolilo rozpoznání laterálního pohybu cestu v Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 24b42c5425933d8931a85e0ba454a69e0ca94a21
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/30/2018
---
*Platí pro: Azure Advanced Threat Protection*

# <a name="install-azure-atp---step-8"></a>Nainstalovat Azure ATP - krok 8

>[!div class="step-by-step"]
[«Krok 7](install-atp-step7.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>Krok 8: Konfigurace SAM-R požadované oprávnění

[Laterální pohyb cesta](use-case-lateral-movement-path.md) detekce spoléhá na dotazy, které identifikují místní správci na konkrétní počítače. Tyto dotazy se provádí pomocí protokolu SAM-R, prostřednictvím účtu služby Azure ATP vytvořené v [kroku 2. Připojení ke službě AD](install-atp-step2.md).
 
K zajištění Windows klienty a servery povolit účet Azure ATP k provedení této operace SAM-R změnu **zásad skupiny** musí být provedeny pro přidání účtu služby Azure ATP kromě nakonfigurované účty uvedené v  **Přístup k síti** zásad.

1. Vyhledejte zásady:

 - Název zásady: Přístup k síti – omezovat klienty povolit vzdálené volání SAM
 - Umístění: Konfigurace, nastavení systému Windows, nastavení zabezpečení, místní zásady zabezpečení možnosti
  
  ![Vyhledejte zásady](./media/samr-policy-location.png)

2. Službu Azure ATP přidejte do seznamu schválených účtů může k provedení této akce na vaše moderní systémy Windows.
 
  ![Přidání služby](./media/samr-add-service.png)

3. **AATP služby** (vytvoření během instalace služby Azure ATP) teď má správná oprávnění k provedení SAMR v prostředí.

Další informace o SAM-R a tyto zásady skupiny, najdete v článku [přístup k síti: omezovat klienty povolit vzdálené volání SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Krok 7](install-atp-step7.md)



## <a name="see-also"></a>Viz také
- [Příčin laterální pohyb cesta útoky s Azure ATP](use-case-lateral-movement-path.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
---
title: "Konfigurace SAM-R, aby se povolilo rozpoznání laterálního pohybu cestu v Azure ATP | Microsoft Docs"
description: "Popisuje postup konfigurace SAM-R, aby se povolilo rozpoznání laterálního pohybu cestu v Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0e2ac4fb68fb1429610a0416582c871c9ae704df
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*

# <a name="install-azure-atp---step-8"></a>Nainstalovat Azure ATP - krok 8

>[!div class="step-by-step"]
[«Krok 7](install-atp-step7.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>Krok 8: Konfigurace SAM-R požadované oprávnění

[Laterální pohyb cesta](use-case-lateral-movement-path.md) detekce spoléhá na dotazy, které identifikují místní správci na konkrétní počítače. Tyto dotazy se provádí pomocí protokolu SAM-R, prostřednictvím účtu služby Azure ATP vytvořené v [kroku 2. Připojení ke službě AD](install-atp-step2.md).
 
Aby klienti systému Windows a servery, aby účet služby Azure ATP k provedení této operace SAM-R, musí být provedeny úpravy zásad skupiny.

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
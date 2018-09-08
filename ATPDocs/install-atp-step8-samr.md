---
title: Konfigurace SAM-R povolit zjišťování cesty laterální pohyb v ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Popisuje postup konfigurace SAM-R povolení zjišťování cesty laterální pohyb v Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/31/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 63fee52a45913685c75872df156fecdddc5a6803
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125817"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*

# <a name="install-azure-atp---step-8"></a>Instalace služby Azure ATP - kroku 8

>[!div class="step-by-step"]
[«Krok 7](install-atp-step7.md)
[kroku 9»](atp-multi-forest.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>Krok 8: Konfigurace SAM-R, vyžaduje oprávnění

[Cesty laterální pohyb](use-case-lateral-movement-path.md) detekce spoléhá na dotazy, které identifikují místními správci na konkrétní počítače. Tyto dotazy se provádí pomocí protokolu SAM-R, pomocí služby Azure ATP účet vytvořený [kroku 2. Připojení ke službě AD](install-atp-step2.md).
 
K zajištění Windows klienty a servery povolit váš účet služby Azure ATP provádět SAM-R, úpravy **zásad skupiny** přidání účtu služby Azure ATP kromě zobrazené v nakonfigurované účty se musí provádět  **Přístup k síti** zásad.

1. Vyhledejte zásady:

 - Název zásady: Přístup k síti – omezovat klienty moct vzdáleně volat SAM
 - Umístění: Konfigurace, nastavení Windows, nastavení zabezpečení, místní zásady zabezpečení možnosti
  
  ![Vyhledejte zásady](./media/samr-policy-location.png)

2. Přidáte službu ochrany ATP v programu Azure do seznamu schválených účtů schopen provést tuto akci do moderního systému Windows.
 
  ![Přidat službu](./media/samr-add-service.png)

3. **Služba AATP** (službu ochrany ATP v programu Azure vytvoří během instalace) má teď oprávnění potřebná k provedení SAM-R v prostředí.

> [!NOTE]
> Ještě před vynucením nové zásady, ujistěte se, že vaše prostředí zůstalo zabezpečené, aniž by to ovlivnilo vaše kompatibilita aplikací povolením a ověření navrhovaných změn v režimu auditování.

Další informace o SAM-R a tyto zásady skupiny, najdete v článku [přístup do sítě: omezit klienti můžou vzdáleně volat SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Krok 7](install-atp-step7.md)
[kroku 9»](atp-multi-forest.md)



## <a name="see-also"></a>Viz také
- [Prošetření útoků v cesty laterální pohyb pomocí služby Azure ATP](use-case-lateral-movement-path.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
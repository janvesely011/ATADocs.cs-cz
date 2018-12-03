---
title: Konfigurace SAM-R povolit zjišťování cesty laterální pohyb v ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Vysvětluje, jak nakonfigurovat služby Azure ATP pro vzdáleně volat SAM
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 020517e576f93b79e00158bbb7c6553d722a73b1
ms.sourcegitcommit: f4f2a1b2c674c4dba7a46ece0624f5ea10c4865e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/02/2018
ms.locfileid: "52744383"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*

# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>Konfigurace ochrany ATP v programu Azure k vzdáleně volat SAM
Ochrana ATP v programu Azure [cesty laterální pohyb](use-case-lateral-movement-path.md) detekce spoléhá na dotazy, které identifikují místními správci na konkrétní počítače. Tyto dotazy se provádí pomocí protokolu SAM-R, pomocí účtu služby ochrany ATP v programu Azure vytvoří během instalace služby Azure ATP [kroku 2. Připojení ke službě AD](install-atp-step2.md).

## <a name="configure-sam-r-required-permissions"></a>Konfigurace SAM-R, vyžaduje oprávnění
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



## <a name="see-also"></a>Viz také
- [Prošetření útoků v cesty laterální pohyb pomocí služby Azure ATP](use-case-lateral-movement-path.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
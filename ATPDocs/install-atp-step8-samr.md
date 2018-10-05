---
title: Konfigurace SAM-R povolit zjišťování cesty laterální pohyb v ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Popisuje postup konfigurace služby Azure ATP pro vzdáleně volat SAM
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d7875202c05deb98c301cb18153f8080fa42459c
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782875"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*

# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>Konfigurace ochrany ATP v programu Azure k vzdáleně volat SAM

<a name="-head"></a><<<<<<< HEAD
=======
> [!div class="step-by-step"]
> [«Krok 7](install-atp-step7.md)
> [kroku 9»](atp-multi-forest.md)
>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04

## <a name="configure-sam-r-required-permissions"></a>Konfigurace SAM-R, vyžaduje oprávnění


[Cesty laterální pohyb](use-case-lateral-movement-path.md) detekce spoléhá na dotazy, které identifikují místními správci na konkrétní počítače. Tyto dotazy se provádí pomocí protokolu SAM-R, pomocí účtu služby ochrany ATP v programu Azure vytvoří během instalace služby Azure ATP [kroku 2. Připojení ke službě AD](install-atp-step2.md).
 
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


<a name="-head"></a><<<<<<< HEAD
=======
> [!div class="step-by-step"]
> [«Krok 7](install-atp-step7.md)
> [kroku 9»](atp-multi-forest.md)


>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04

## <a name="see-also"></a>Viz také
- [Prošetření útoků v cesty laterální pohyb pomocí služby Azure ATP](use-case-lateral-movement-path.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
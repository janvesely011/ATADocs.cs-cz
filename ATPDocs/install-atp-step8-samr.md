---
title: Konfigurace SAM-R povolit zjišťování cesty laterální pohyb v ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Vysvětluje, jak nakonfigurovat služby Azure ATP pro vzdáleně volat SAM
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b4e62c858799129ea511dda32f9f5f030ab715e9
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58673462"
---
# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>Konfigurace ochrany ATP v programu Azure k vzdáleně volat SAM
Ochrana ATP v programu Azure [cesty laterální pohyb](use-case-lateral-movement-path.md) detekce spoléhá na dotazy, které identifikují místními správci na konkrétní počítače. Tyto dotazy se provádí pomocí protokolu SAM-R, pomocí účtu služby ochrany ATP v programu Azure vytvoří během instalace služby Azure ATP [kroku 2. Připojení ke službě AD](install-atp-step2.md).

## <a name="configure-sam-r-required-permissions"></a>Konfigurace SAM-R, vyžaduje oprávnění
K zajištění Windows klienty a servery povolit váš účet služby Azure ATP provádět SAM-R, úpravy **zásad skupiny** přidání účtu služby Azure ATP kromě zobrazené v nakonfigurované účty se musí provádět  **Přístup k síti** zásad.

> [!Note]
> Ještě před vynucením nové zásady, jako je ten, je velmi důležité, abyste měli jistotu, že prostředí zůstalo zabezpečené a všechny změny nebude mít vliv na kompatibilitu vašich aplikací. K tomu prvním povolení a ověřením kompatibility navrhovaných změn v režimu auditování, před provedením změn v provozním prostředí.

1. Vyhledejte zásady:

   - Název zásad: Přístup k síti – omezovat klienty moct vzdáleně volat SAM
   - Umístění: Konfigurace nastavení Windows, nastavení zabezpečení, místní zásady, možnosti zabezpečení
  
   ![Vyhledejte zásady](./media/samr-policy-location.png)

2. Přidáte službu ochrany ATP v programu Azure do seznamu schválených účtů schopen provést tuto akci do moderního systému Windows.
 
   ![Přidat službu](./media/samr-add-service.png)

3. **Služba AATP** (službu ochrany ATP v programu Azure vytvoří během instalace) má teď oprávnění potřebná k provedení SAM-R v prostředí.



Další informace o SAM-R a tyto zásady skupiny, najdete v článku [přístup k síti: Omezit klienti můžou vzdáleně volat SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).



## <a name="see-also"></a>Viz také
- [Prošetření útoků v cesty laterální pohyb pomocí služby Azure ATP](use-case-lateral-movement-path.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

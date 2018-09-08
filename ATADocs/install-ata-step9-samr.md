---
title: Konfigurace SAM-R povolit zjišťování cesty laterální pohyb v Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje postup konfigurace SAM-R povolit zjišťování cesty laterální pohyb v Advanced Threat Analytics (ATA)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/30/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8a1de6e0f3d5234eb96d710b54ded8c8a894f440
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125732"
---
*Platí pro: Advanced Threat Analytics verze 1.9*

# <a name="install-ata---step-9"></a>Instalace ATA – krok 9

>[!div class="step-by-step"]
[«Krok 8](install-ata-step7.md)

## <a name="step-9-configure-sam-r-required-permissions"></a>Krok 9: Konfigurace SAM-R, vyžaduje oprávnění

[Cesty laterální pohyb](use-case-lateral-movement-path.md) detekce spoléhá na dotazy, které identifikují místními správci na konkrétní počítače. Tyto dotazy se provádí pomocí protokolu SAM-R, prostřednictvím vytvořené v účtu služby ATA [kroku 2. Připojení ke službě AD](install-ata-step2.md).
 
K zajištění, že Windows klienty a servery povolit účet služby ATA k provedení této operace SAM-R, úpravy vaše **zásady skupiny** musí být provedeny, který přidá účet služby ATA kromě nakonfigurované účty uvedené v **přístup k síti** zásad.

1. Vyhledejte zásady:

 - Název zásady: Přístup k síti – omezovat klienty moct vzdáleně volat SAM
 - Umístění: Konfigurace, nastavení Windows, nastavení zabezpečení, místní zásady zabezpečení možnosti
  
  ![Vyhledejte zásady](./media/samr-policy-location.png)

2. Služba ATA přidáte do seznamu schválených účtů schopen provést tuto akci do moderního systému Windows.
 
  ![Přidat službu](./media/samr-add-service.png)

3. **Služba ATA** (služba ATA vytvoří během instalace) teď má správná oprávnění k provedení SAM-R v prostředí.

> [!NOTE]
> Ještě před vynucením nové zásady, ujistěte se, že vaše prostředí zůstalo zabezpečené, aniž by to ovlivnilo kompatibilita aplikací umožňující a ověření vašich navrhovaných změn v režimu auditování. 

 Další informace o SAM-R a zásadami skupiny, najdete v části [přístup do sítě: omezit klienti můžou vzdáleně volat SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Krok 8](install-ata-step7.md)

## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

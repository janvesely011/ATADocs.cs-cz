---
title: Konfigurace SAM-R pro povolení detekce cesty bočního pohybu v Advanced Threat Analytics | Microsoft Docs
description: Popisuje, jak nakonfigurovat SAM-R, aby bylo možné v Advanced Threat Analytics povolit detekci cest po pohybu (ATA).
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/08/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5d266de0344a699ed3c3934246311f21b1b00c09
ms.sourcegitcommit: e4f108aec3cbfd88562217e36195b5d1250a1bbd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2019
ms.locfileid: "70803197"
---
# <a name="install-ata---step-9"></a>Instalace ATA – krok 9

*Platí pro: Advanced Threat Analytics verze 1,9*

> [!div class="step-by-step"]
> [«Krok 8](install-ata-step7.md)

> [!NOTE]
> Než začnete s vynucováním nové zásady, ujistěte se, že vaše prostředí zůstane zabezpečené, aniž by to mělo vliv na kompatibilitu aplikací, a to tak, že nejprve povolíte a ověříte navrhované změny v režimu auditování. 

## <a name="step-9-configure-sam-r-required-permissions"></a>Krok 9: Konfigurace požadovaných oprávnění SAM-R

Detekce [cesty bočního pohybu](use-case-lateral-movement-path.md) spoléhá na dotazy, které identifikují místní správce na určitých počítačích. Tyto dotazy se provádějí pomocí protokolu Sam-R prostřednictvím účtu služby ATA vytvořeného v [kroku 2. Připojte se ke](install-ata-step2.md)službě AD.
 
Aby bylo zajištěno, že klienti a servery systému Windows umožňují účtu služby ATA provádět tuto operaci SAM-R, je nutné provést úpravy **zásad skupiny** , které kromě nakonfigurovaných účtů uvedených v síti přidávají účet služby ATA.  **zásady přístupu** . Tyto zásady skupiny by se měly použít pro každé zařízení ve vaší organizaci. 

1. Vyhledejte zásadu:

   - Název zásady: Přístup k síti – omezení klientů, kteří mají povoleno provádět Vzdálená volání do SAM
   - Oblasti Konfigurace počítače, nastavení systému Windows, nastavení zabezpečení, místní zásady, možnosti zabezpečení
  
   ![Vyhledat zásadu](./media/samr-policy-location.png)

2. Přidejte ATA Service do seznamu schválených účtů, které můžou tuto akci provést v moderních systémech Windows.
 
   ![Přidat službu](./media/samr-add-service.png)

3. **Služba ATA** (služba ATA vytvořená během instalace) teď má správná oprávnění k provádění Sam-R v prostředí.

 Další informace o Sam-R a zásady skupiny najdete v tématu [přístup k síti: Omezí počet klientů, kteří mají povoleno provádět Vzdálená](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls)volání do Sam.


> [!div class="step-by-step"]
> [«Krok 8](install-ata-step7.md)

## <a name="see-also"></a>Viz také
- [Průvodce nasazením pro ATA podle ověření](http://aka.ms/atapoc)
- [Nástroj pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

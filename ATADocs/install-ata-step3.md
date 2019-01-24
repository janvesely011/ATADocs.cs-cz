---
title: Instalace Advanced Threat Analytics – krok 3 | Dokumenty Microsoftu
description: Třetí krok instalace ATA vám pomůže stáhnout instalační balíček ATA Gateway.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b73a82b2dc301de0d464f9f0dc936cce17a2fb10
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2019
ms.locfileid: "54841113"
---
# <a name="install-ata---step-3"></a>Instalace ATA – krok 3

*Platí pro: Advanced Threat Analytics verze 1.9*

> [!div class="step-by-step"]
> [« Krok 2](install-ata-step2.md)
> [Krok 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Krok 3. Stažení instalačního balíčku ATA Gateway

Po konfiguraci nastavení připojení k doméně si můžete stáhnout instalační balíček ATA Gateway. ATA Gateway se dá nainstalovat na vyhrazený server nebo na řadič domény. Pokud nainstalujete ho na řadič domény, nainstaluje se jako ATA Lightweight Gateway. Další informace o ATA Lightweight Gateway najdete v tématu [Architektura ATA](ata-architecture.md). 

Klikněte na tlačítko **stáhnout instalační program brány** v seznamu kroků uvedených v horní části stránky a přejděte tak **brány** stránky.

![Nastavení konfigurace ATA Gateway](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> Pokud se budete chtít na obrazovku konfigurace komponenty Gateway později vrátit, klikněte na **ikonu nastavení** (pravý horní roh), vyberte možnost **Configuration** (Konfigurace) a potom pod položkou **System** (Systém) klikněte na **Gateways** (Komponenty Gateway).  

1.  Klikněte na **Gateway Setup** (Instalace Gateway).
  ![Stažení instalačního programu ATA Gateway](media/download-gateway-setup.png)
2.  Uložte balíček místně.
3.  Zkopírujte balíček na vyhrazený server nebo řadič domény, na který instalujete ATA Gateway. Další možností je otevřít konzolu ATA z vyhrazeného serveru nebo řadiče domény a přeskočit tento krok.

Soubor zip obsahuje následující soubory:

-   Instalační program ATA Gateway

-   Soubor nastavení konfigurace s požadovanými informacemi pro připojení k ATA Center


> [!div class="step-by-step"]
> [« Krok 2](install-ata-step2.md)
> [Krok 4 »](install-ata-step4.md)


## <a name="related-videos"></a>Související videa
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Volba správného typu komponenty ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

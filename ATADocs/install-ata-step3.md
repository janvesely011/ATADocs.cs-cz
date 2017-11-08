---
title: "Instalace Advanced Threat Analytics – krok 3 | Dokumenty Microsoftu"
description: "Třetí krok instalace ATA vám pomůže stáhnout instalační balíček ATA Gateway."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ab80ec5b172311e955a25fed677c40cee1e95269
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="install-ata---step-3"></a>Instalace ATA – krok 3

>[!div class="step-by-step"]
[« Krok 2](install-ata-step2.md)
[Krok 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Krok 3. Stažení instalačního balíčku ATA Gateway
Po konfiguraci nastavení připojení k doméně si můžete stáhnout instalační balíček ATA Gateway. ATA Gateway se dá nainstalovat na vyhrazený server nebo na řadič domény. Pokud musíte jej nainstalovat na řadič domény, je nainstalována jako ATA Lightweight Gateway. Další informace o ATA Lightweight Gateway najdete v tématu [Architektura ATA](ata-architecture.md). 

Klikněte na tlačítko **stáhnout instalační program brány** seznam kroků uvedených v horní části stránky přejít na **brány** stránky.

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


>[!div class="step-by-step"]
[« Krok 2](install-ata-step2.md)
[Krok 4 »](install-ata-step4.md)


## <a name="related-videos"></a>Související videa
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Výběr správné typu ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

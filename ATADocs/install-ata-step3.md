---
title: "Instalace Advanced Threat Analytics – krok 3 | Dokumenty Microsoftu"
description: "Třetí krok instalace ATA vám pomůže stáhnout instalační balíček ATA Gateway."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 68c169ffd0f42bd8b030dc12f4711cbde2718a99
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/30/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="install-ata---step-3"></a>Instalace ATA – krok 3

>[!div class="step-by-step"]
[« Krok 2](install-ata-step2.md)
[Krok 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Krok 3. Stažení instalačního balíčku ATA Gateway
Po konfiguraci nastavení připojení k doméně si můžete stáhnout instalační balíček ATA Gateway. ATA Gateway se dá nainstalovat na vyhrazený server nebo na řadič domény. Pokud tuto komponentu nainstalujete na řadič domény, nainstaluje se jako ATA Lightweight Gateway. Další informace o ATA Lightweight Gateway najdete v tématu [Architektura ATA](ata-architecture.md). 

V seznamu postupu klikněte na možnost stažení instalace komponenty Gateway v horní části stránky a přejděte tak na stránku s komponentami Gateway:

![Nastavení konfigurace ATA Gateway](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> Pokud se budete chtít na obrazovku konfigurace komponenty Gateway později vrátit, klikněte na **ikonu nastavení** (pravý horní roh), vyberte možnost **Configuration** (Konfigurace) a potom pod položkou **System** (Systém) klikněte na **Gateways** (Komponenty Gateway).  

1.  Klikněte na **Gateway Setup** (Instalace Gateway).
  ![Stažení instalačního programu ATA Gateway](media/download-gateway-setup.png)
2.  Uložte balíček místně.
3.  Zkopírujte balíček na vyhrazený server nebo řadič domény, na který instalujete ATA Gateway. Další možností je otevřít konzolu ATA z vyhrazeného serveru nebo řadiče domény a přeskočit tento krok.

Soubor zip obsahuje následující:

-   Instalační program ATA Gateway

-   Soubor nastavení konfigurace s požadovanými informacemi pro připojení k ATA Center


>[!div class="step-by-step"]
[« Krok 2](install-ata-step2.md)
[Krok 4 »](install-ata-step4.md)

## <a name="see-also"></a>Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

---
title: Nainstalovat Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Třetí krok instalace ochrany ATP v programu Azure umožňuje stáhnout instalační balíček senzoru služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4816fe56b8a28d349c970be5a304d025875de748
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085227"
---
# <a name="install-azure-atp---step-3"></a>Instalace služby Azure ATP – krok 3

> [!div class="step-by-step"]
> [« Krok 2](install-atp-step2.md)
> [Krok 4 »](install-atp-step4.md)

## <a name="download-the-azure-atp-sensor-setup-package"></a>Stažení instalačního balíčku senzoru služby Azure ATP
Po dokončení konfigurace nastavení připojení k doméně, můžete stáhnout instalační balíček senzoru služby Azure ATP. Instalačního balíčku senzoru služby Azure ATP můžete nainstalovat na vyhrazený server nebo na řadič domény. Při instalaci přímo na řadiče domény, je nainstalována jako senzoru služby Azure ATP při instalaci na vyhrazeném serveru a pomocí zrcadlení portů, je nainstalován jako samostatný senzor ochrany ATP v programu Azure. Další informace o senzoru služby Azure ATP najdete v tématu [Architektura ochrany ATP v programu Azure](atp-architecture.md). 

Klikněte na tlačítko **Stáhnout** v seznamu kroků uvedených v horní části stránky a přejděte tak **senzor** stránky.

![Nastavení konfigurace senzoru služby Azure ochrany ATP v programu](media/atp-sensor-config.png)

> [!NOTE] 
> Na obrazovce pro konfiguraci senzor později, klikněte **ikona nastavení** (pravém horním rohu) a vyberte **konfigurace**, pak v části **systému**, klikněte na tlačítko **senzor**.  

1.  Klikněte na tlačítko **senzor**.
2.  Uložte balíček místně.
3.  Kopírovat **přístup** **klíč**. Přístupový klíč se vyžaduje pro připojení k vaší instanci služby Azure ATP senzoru služby Azure ATP. Přístupový klíč je jednoho heslem pro nasazení ze senzorů, po jejímž uplynutí veškerá komunikace se provádí pomocí certifikátů pro ověřování a šifrování TLS. Použití **znovu vygenerovat** tlačítko Pokud byste zas někdy potřebovali obnovit nový přístupový klíč, můžete, a to nebude mít vliv na všechny dříve nasazené senzorů, protože se používá jenom pro první registraci senzoru.
4.  Zkopírujte balíček na vyhrazený server nebo řadič domény, na který instalujete senzoru služby Azure ATP. Alternativně můžete otevřít na portálu ochrany ATP v programu Azure ze vyhrazený server nebo řadič domény a tento krok přeskočit.

Soubor zip obsahuje následující soubory:

-   Instalační služby systému senzor Azure ATP

-   Soubor nastavení konfigurace s požadovanými informacemi pro připojení ke cloudové službě ochrana ATP v programu Azure


> [!div class="step-by-step"]
> [« Krok 2](install-atp-step2.md)
> [Krok 4 »](install-atp-step4.md)


## <a name="see-also"></a>Viz také

- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)

- [Konfigurace shromažďování událostí](configure-event-collection.md)

- [Požadavky služby Azure ATP](atp-prerequisites.md)

- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
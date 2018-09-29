---
title: Instalace Azure Advanced Threat Protection – krok 3 | Dokumentace Microsoftu
description: Třetí krok instalace ochrany ATP v programu Azure umožňuje stáhnout instalační balíček služby Azure ATP samostatného senzoru.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 96d459bd00d39bb21ce363d079b5b24ceca4ace7
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454016"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="install-azure-atp---step-3"></a>Instalace služby Azure ATP – krok 3

> [!div class="step-by-step"]
> [« Krok 2](install-atp-step2.md)
> [Krok 4 »](install-atp-step4.md)

## <a name="step-3-download-the-azure-atp-sensor-setup-package"></a>Krok 3: Stažení instalačního balíčku senzoru služby Azure ATP
Po dokončení konfigurace nastavení připojení k doméně, můžete stáhnout instalační balíček senzoru služby Azure ATP. Instalačního balíčku senzoru služby Azure ATP můžete nainstalovat na vyhrazený server nebo na řadič domény. Při instalaci přímo na řadiče domény, je nainstalována jako senzoru služby Azure ATP při instalaci na vyhrazeném serveru a pomocí zrcadlení portů, je nainstalován jako samostatný senzor ochrany ATP v programu Azure. Další informace o senzoru služby Azure ATP najdete v tématu [Architektura ochrany ATP v programu Azure](atp-architecture.md). 

Klikněte na tlačítko **Stáhnout** v seznamu kroků uvedených v horní části stránky a přejděte tak **senzor** stránky.

![Nastavení konfigurace senzoru služby Azure ochrany ATP v programu](media/atp-sensor-config.png)

> [!NOTE] 
> Na obrazovce pro konfiguraci senzor později, klikněte **ikona nastavení** (pravém horním rohu) a vyberte **konfigurace**, pak v části **systému**, klikněte na tlačítko **senzor**.  

1.  Klikněte na tlačítko **senzor**.
2.  Uložte balíček místně.
3.  Kopírovat **přístupový klíč**. Přístupový klíč se vyžaduje senzoru služby Azure ATP pro připojení k vašemu pracovnímu prostoru služby Azure ATP. Přístupový klíč je jednoho heslem pro nasazení ze senzorů, po jejímž uplynutí veškerá komunikace se provádí pomocí certifikátů pro ověřování a šifrování TLS. Použití **znovu vygenerovat** tlačítko Pokud byste zas někdy potřebovali obnovit nový přístupový klíč, můžete, a to nebude mít vliv na všechny dříve nasazené senzorů, protože se používá jenom pro první registraci senzoru.
4.  Zkopírujte balíček na vyhrazený server nebo řadič domény, na který instalujete senzoru služby Azure ATP. Alternativně můžete otevřít na portálu ochrany ATP v programu Azure pracovní prostor ze vyhrazený server nebo řadič domény a tento krok přeskočit.

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

- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
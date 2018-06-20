---
title: Instalace Azure Advanced Threat Protection – krok 3 | Microsoft Docs
description: Třetí krok instalace Azure ATP vám pomůže stáhnout instalační balíček Azure ATP samostatné senzor.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: aa07d6ce4418c051362652e70968a8e41313affb
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446040"
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-3"></a>Nainstalovat Azure ATP – krok 3

>[!div class="step-by-step"]
[« Krok 2](install-atp-step2.md)
[Krok 4 »](install-atp-step4.md)

## <a name="step-3-download-the-azure-atp-sensor-setup-package"></a>Krok 3: Stáhnout instalační balíček Azure ATP senzor
Po dokončení konfigurace nastavení připojení k doméně, si můžete stáhnout instalační balíček senzor Azure ATP. Instalační balíček senzor Azure ATP lze nainstalovat na vyhrazený server nebo na řadiči domény. Při instalaci přímo na řadiči domény, je nainstalován jako senzor Azure ATP při instalaci na vyhrazený server a pomocí zrcadlení portů, je nainstalován jako samostatné senzor Azure ATP. Další informace o senzoru Azure ATP najdete v tématu [architektura ATP Azure](atp-architecture.md). 

Klikněte na tlačítko **Stáhnout** seznam kroků uvedených v horní části stránky přejít na **senzor** stránky.

![Nastavení konfigurace Azure ATP senzor](media/atp-sensor-config.png)

> [!NOTE] 
> Pokud chcete dostat na obrazovce konfigurace senzor později, klikněte na tlačítko **ikonu nastavení** (pravém horním rohu) a vyberte **konfigurace**, potom v části **systému**, klikněte na tlačítko **senzor**.  

1.  Klikněte na tlačítko **senzor**.
2.  Uložte balíček místně.
3.  Kopírování **přístupový klíč**. Přístupový klíč je požadované pro připojení do pracovního prostoru Azure ATP senzoru Azure ATP. Přístupový klíč je jednoho-bránu-heslo pro nasazení senzor, po jejímž uplynutí veškerá komunikace se provádí pomocí certifikátů pro ověřování a šifrování TLS. Použití **znovu vygenerovat** tlačítko Pokud byste někdy potřebovali znovu vygenerovat nový přístupový klíč, můžete a ho nebude mít vliv na všechny nasazené předtím senzorů, protože se používá pouze pro počáteční registrace senzoru.
4.  Zkopírujte balíček na vyhrazený server nebo řadič domény, na který instalujete senzoru Azure ATP. Alternativně můžete otevřít na portálu Azure ATP prostoru z vyhrazený server nebo řadič domény a Přeskočit tento krok.

Soubor zip obsahuje následující soubory:

-   Azure instalační program senzor ATP

-   Soubor nastavení konfigurace s požadovanými informacemi pro připojení ke cloudové službě Azure ATP


>[!div class="step-by-step"]
[« Krok 2](install-atp-step2.md)
[Krok 4 »](install-atp-step4.md)


## <a name="see-also"></a>Viz také

- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)

- [Konfigurace shromažďování událostí](configure-event-collection.md)

- [Požadavky Azure ATP](atp-prerequisites.md)

- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
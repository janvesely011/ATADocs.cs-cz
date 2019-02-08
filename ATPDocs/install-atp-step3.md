---
title: Stáhněte si balíček ochrany ATP v programu Azure senzor nastavení tohoto rychlého startu | Dokumentace Microsoftu
description: Třetí krok instalace ochrany ATP v programu Azure umožňuje stáhnout instalační balíček senzoru služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 02/05/2019
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.openlocfilehash: 8648e3bacadaa64570e127ce3728c33f87d3393c
ms.sourcegitcommit: 96752da28f43896e7b8e5945947b32c4810bdff6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/07/2019
ms.locfileid: "55831425"
---
# <a name="quickstart-download-the-azure-atp-sensor-setup-package"></a>Rychlý start: Stažení instalačního balíčku senzoru služby Azure ATP

V tomto rychlém startu budete stažení instalačního balíčku senzoru služby Azure ATP z portálu.

## <a name="prerequisites"></a>Požadavky

- [Instance služby Azure ATP](install-atp-step1.md) to [připojeným ke službě Active Directory](install-atp-step2.md).

## <a name="download-the-setup-package"></a>Stáhnout instalační balíček

Po dokončení konfigurace nastavení připojení k doméně, můžete stáhnout instalační balíček senzoru služby Azure ATP. Instalačního balíčku senzoru služby Azure ATP můžete nainstalovat na vyhrazený server nebo na řadič domény. Při instalaci přímo na řadiče domény, je nainstalována jako senzoru služby Azure ATP při instalaci na vyhrazeném serveru a pomocí zrcadlení portů, je nainstalován jako samostatný senzor ochrany ATP v programu Azure. Další informace o senzoru služby Azure ATP najdete v tématu [Architektura ochrany ATP v programu Azure](atp-architecture.md). 

Klikněte na tlačítko **Stáhnout** v seznamu kroků uvedených v horní části stránky a přejděte tak **senzor** stránky.

![Nastavení konfigurace senzoru služby Azure ochrany ATP v programu](media/atp-sensor-config.png)

 Na obrazovce pro konfiguraci senzor později, klikněte **ikona nastavení** (pravém horním rohu), vyberte **konfigurace**, pak v části **systému**, klikněte na tlačítko **senzor**.  

1. Klikněte na tlačítko **senzor**.
2. Uložte balíček místně.
3. Kopírovat **přístup** **klíč**. Přístupový klíč se vyžaduje pro připojení k vaší instanci služby Azure ATP senzoru služby Azure ATP. Přístupový klíč je jednoho heslem pro nasazení ze senzorů, po jejímž uplynutí veškerá komunikace se provádí pomocí certifikátů pro ověřování a šifrování TLS. Použití **znovu vygenerovat** tlačítko Pokud byste zas někdy potřebovali obnovit nový přístupový klíč, můžete, a to nebude mít vliv na všechny dříve nasazené senzorů, protože se používá jenom pro první registraci senzoru.
4. Zkopírujte balíček na vyhrazený server nebo řadič domény, na který instalujete senzoru služby Azure ATP. Alternativně můžete otevřít na portálu ochrany ATP v programu Azure ze vyhrazený server nebo řadič domény a tento krok přeskočit.

Soubor zip obsahuje následující soubory:

- Instalační služby systému senzor Azure ATP

- Soubor nastavení konfigurace s požadovanými informacemi pro připojení ke cloudové službě ochrana ATP v programu Azure

## <a name="next-steps"></a>Další postup

> [!div class="step-by-step"]
> [«Krok 2: připojení ke službě Active Directory](install-atp-step2.md)
> [krok 4 – instalace služby Azure ATP senzor»](install-atp-step4.md)

## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://aka.ms/azureatpcommunity) ještě dnes!
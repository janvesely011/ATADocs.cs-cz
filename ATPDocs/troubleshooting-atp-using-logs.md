---
title: Řešení potíží s Azure Advanced Threat Protection pomocí protokolů | Dokumentace Microsoftu
description: Popisuje, jak můžete k řešení potíží pomocí protokolů služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 10/04/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: de796346-647d-48e1-970a-8f072e990f1e
ms.reviewer: ''
ms.suite: ''
ms.openlocfilehash: e461aa7302ee515f33e2ad69f0f2c0c9f83ceaf8
ms.sourcegitcommit: 139e8dd63c06a5d9c9a3c348958e4f7fd74041b8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2019
ms.locfileid: "67155888"
---
# <a name="troubleshooting-azure-advanced-threat-protection-atp-sensor-using-the-atp-logs"></a>Řešení problémů s Azure Advanced Threat Protection (ATP) ze senzorů pomocí protokolů ochrany ATP v programu
Ochrana ATP v programu protokoly poskytují přehled o tom, co jednotlivé komponenty senzoru služby Azure ATP dělá v libovolném časovém okamžiku v čase.


Ochrana ATP v programu Azure protokoly jsou umístěné v podsložce s názvem **protokoly** kde je nainstalován ochrany ATP v programu; výchozí umístění je: **C:\Program Files\Azure Advanced Threat Protection Sensor\\** . Ve výchozím umístění instalace můžete najít na: **C:\Program Files\Azure Advanced Threat Protection Sensor\version number\Logs**.

Senzoru služby Azure ATP využívá tyto protokoly:

-   **Microsoft.Tri.Sensor.log** – tento protokol obsahuje všechno, co se děje v senzoru služby Azure ATP (včetně překladu a chyb). Nejčastěji se využívá ke zjištění celkového stavu všech operací v chronologickém pořadí, ve kterém k nim došlo.

-   **Microsoft.Tri.Sensor-Resolution.log** – tento protokol obsahuje podrobnosti o řešení entit v provozu zjištěných senzor ochrany ATP v programu. Nejčastěji se využívá ke zkoumání příčin problémů s překladem entit.

-   **Microsoft.Tri.Sensor-Errors.log** – tento protokol obsahuje jenom chyby, které zachytila komponenta senzor ochrany ATP v programu. Nejčastěji se využívá k provádění kontroly stavu a zkoumání příčin problémů, které je potřeba časově zařadit.

-   **Microsoft.Tri.Sensor.Updater.log** – tento protokol se používá pro aktualizační proces senzor, který je zodpovědný za automatickou aktualizaci senzor ochrany ATP v programu, pokud k tomu automaticky nakonfigurované. 


> [!NOTE]
> První tři soubory protokolů mají maximální velikost až 50 MB. Při dosažení této velikosti se otevře nový soubor protokolu a předchozí je přejmenován na &lt;původní název souboru&gt;-Archived-00000 (číslo při každém přejmenování zvětší). Pokud již existuje více než 10 souborů stejného typu, budou nejstarší z nich ve výchozím nastavení odstraněny.

## <a name="azure-atp-deployment-logs"></a>Protokoly nasazení Azure ATP
Protokoly nasazení služby Azure ATP jsou umístěné v adresáři temp uživatele, který příslušný produkt nainstaloval. Ve výchozím umístění instalace můžete najít na: **C:\Users\Administrator\AppData\Local\Temp** (nebo jednomu adresáři % temp %).

Protokoly nasazení senzoru Azure ochrany ATP v programu:

-  **Azure Protection Advanced Threat-Microsoft.Tri.Sensor.Deployment.Deployer_YYYYMMDDHHMMSS.log** – tento protokol obsahuje celý proces nasazení senzoru a najdete ve složce temp již bylo zmíněno dříve, nebo C:\Windows\Temp. 

-   **Azure Protection Advanced Threat-Sensor_YYYYMMDDHHMMSS.log** -tomto protokolu jsou uvedené kroky procesu nasazení senzoru služby Azure ATP. Nejčastěji se ke sledování procesu nasazení senzoru služby Azure ATP.

-   **Azure Protection Advanced Threat-Sensor_YYYYMMDDHHMMSS_001_MsiPackage.log** – tento soubor protokolu jsou uvedené kroky procesu nasazení binárních souborů senzoru služby Azure ATP. Nejčastěji se ke sledování nasazení binárních souborů senzoru služby Azure ATP.


> [!NOTE] 
> Kromě zde uvedených protokolů nasazení jsou k dispozici další protokoly, které začínají řetězcem "Azure Advanced Threat Protection", který také poskytují další informace o procesu nasazení.


## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

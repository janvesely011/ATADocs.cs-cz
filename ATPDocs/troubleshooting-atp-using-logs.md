---
title: Řešení potíží s pokročilou ochranou před internetovými útoky v Azure pomocí protokolů | Microsoft Docs
description: Popisuje, jak můžete pomocí protokolů ATP Azure řešit problémy.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 08/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: de796346-647d-48e1-970a-8f072e990f1e
ms.reviewer: ''
ms.suite: ''
ms.openlocfilehash: 0105630931c6cbebfe2b919946f305ba031bb755
ms.sourcegitcommit: 8df26fb312472b8df1da70e581517223d26de8c2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/05/2019
ms.locfileid: "68781902"
---
# <a name="troubleshooting-azure-advanced-threat-protection-atp-sensor-using-the-atp-logs"></a>Řešení potíží se senzorem Azure Advanced Threat Protection (ATP) pomocí protokolů ATP
Protokoly ATP poskytují přehled o tom, co každá součást snímače ATP Azure dělá v jakémkoli okamžiku.


Protokoly ATP Azure jsou umístěné v podsložce s názvem **protokoly** , kde je nainstalovaná atp. výchozí umístění je: **C:\Program Files\Azure – senzor\\ochrany před internetovými útoky** Ve výchozím umístění instalace je možné ji najít na adrese: **C:\Program Files\Azure – Rozšířená ochrana před internetovými útoky Sensor\version number\Logs**.

Senzor ATP Azure má následující protokoly:

-   **Microsoft. Tri. snímač. log** – tento protokol obsahuje všechno, co se děje ve snímači ATP Azure (včetně řešení a chyb). Nejčastěji se využívá ke zjištění celkového stavu všech operací v chronologickém pořadí, ve kterém k nim došlo.

-   **Microsoft. Tri. Sensor-Errors. log** – tento protokol obsahuje jenom chyby, které zachycuje senzor atp. Nejčastěji se využívá k provádění kontroly stavu a zkoumání příčin problémů, které je potřeba časově zařadit.

-   **Microsoft. Tri. snímač. isUpdating. log** – tento protokol se používá pro proces aktualizace senzorů, který je zodpovědný za aktualizaci senzoru ATP, pokud je nakonfigurován tak, aby automaticky provedený. 


> [!NOTE]
> První tři soubory protokolů mají maximální velikost až 50 MB. Při dosažení této velikosti se otevře nový soubor protokolu a předchozí je přejmenován na &lt;původní název souboru&gt;-Archived-00000 (číslo při každém přejmenování zvětší). Pokud již existuje více než 10 souborů stejného typu, budou nejstarší z nich ve výchozím nastavení odstraněny.

## <a name="azure-atp-deployment-logs"></a>Protokoly nasazení ATP Azure
Protokoly nasazení ATP Azure se nacházejí v adresáři Temp pro uživatele, který produkt nainstaloval. Ve výchozím umístění instalace je možné ji najít na adrese: **C:\Users\Administrator\AppData\Local\Temp** (nebo jeden adresář nad% Temp%).

Protokoly nasazení senzoru ATP Azure:

-  **Rozšířená ochrana před internetovými útoky v Azure – Microsoft. Tri. senzor. Deployment. Deployer_YYYYMMDDHHMMSS. log** – tento soubor protokolu poskytuje celý proces nasazení senzoru a je možné ho najít v dočasné složce uvedené výše, nebo v C:\Windows\Temp. 

-   **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS. log** – v tomto protokolu jsou uvedené kroky procesu nasazení senzoru ATP Azure. Jeho hlavní využití sleduje proces nasazení senzoru Azure ATP.

-   **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS_001_MsiPackage. log** – v tomto souboru protokolu jsou uvedené kroky procesu nasazení binárních souborů senzorů Azure atp. Jeho hlavní využití sleduje nasazení binárních souborů senzorů Azure ATP.


> [!NOTE] 
> Kromě zde uvedených protokolů nasazení jsou k dispozici další protokoly, které začínají "Azure Advanced Threat Protection", které mohou také poskytovat další informace o procesu nasazení.


## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

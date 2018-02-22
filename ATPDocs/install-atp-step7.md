---
title: "Instalace Azure Advanced Threat Protection – krok 7 | Microsoft Docs"
description: "V posledním kroku instalace Azure ATP konfiguraci uživatele Honeytokenu."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bef13d0f4799a4483eda6604a8ed96befaa13508
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-7"></a>Nainstalovat Azure ATP – krok 7

>[!div class="step-by-step"]
[« Krok 6](install-atp-step6-vpn.md)
[Krok 8 »](install-atp-step8-samr.md)

## <a name="step-7-configure-detection-exclusions-and-honeytoken-user"></a>Krok 7: Konfigurace vyloučení detekce a uživatele honeytokenu

Azure ATP umožňuje vyloučení určité IP adresy nebo uživatelé z několika detekce. 

Například při **vyloučení DNS Reconnaissance** se může jednat o kontrolu zabezpečení, která jako mechanismus pro prohledávání používá službu DNS. Vyloučení pomáhá ignorovat takové skenery ATP Azure.  

Azure ATP taky umožňuje konfiguraci uživatele Honeytokenu, který se používá jako depeše nebezpečného actors – ověřování spojené s tímto účtem (obvykle spících) aktivuje výstrahu.

To můžete nakonfigurovat, postupujte takto:

1.  Z portálu Azure ATP pracovního prostoru, klikněte na ikonu nastavení a vyberte **konfigurace**.

    ![Nastavení konfigurace Azure ATP](media/atp-config-menu.png)

2.  V části **detekce**, klikněte na tlačítko **značek entit**.

3. V části **účtů Honeytokenu** zadejte název účtu Honeytokenu a klikněte na tlačítko  **+**  přihlášení. Pole účtů Honeytokenu je prohledávat a entity se automaticky zobrazí ve vaší síti. Klikněte na **Uložit**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Klikněte na **Vyloučení**. Pro jednotlivé typy hrozeb zadejte uživatelský účet nebo IP adresu, které mají být vyloučené z detekce těchto hrozeb, a klikněte na znaménko *plus*. Pole **Add entity** (Přidat entitu) (uživatele nebo počítač) je možné prohledávat a automaticky se vyplní entitami ve vaší síti. Další informace najdete v tématu [vyloučení entity z detekce](excluding-entities-from-detections.md) a [Průvodce podezřelou aktivitu](suspicious-activity-guide.md).

   ![Vyloučení](media/exclusions.png)

5.  Klikněte na **Uložit**.


Blahopřejeme, úspěšně jste nasadili Azure Advanced Threat Protection.

Zkontrolujte časovou osu útoků, abyste viděli zjištěné podezřelé aktivity a našli uživatele nebo počítače a zobrazili jejich profily.

Azure ATP spustí vyhledávání podezřelých aktivit okamžitě. Některé detekce, jako je například neobvyklé úpravy skupiny, vyžadují dobou učení a nejsou k dispozici ihned po nasazení Azure ATP.



>[!div class="step-by-step"]
[« Krok 6](install-atp-step6-vpn.md)
[Krok 8 »](install-atp-step8-samr.md)

## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)

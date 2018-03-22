---
title: Instalace Advanced Threat Analytics - krok 8 | Microsoft Docs
description: "V posledním kroku instalace ATA nakonfigurujete uživatele honeytokenu."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 8d7d53222c4eb98fba554b59f14d8728a88c9d95
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/22/2018
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="install-ata---step-8"></a>Instalace ATA – krok 8

>[!div class="step-by-step"]
[«Krok 7](vpn-integration-install-step.md)
[kroku 9»](install-ata-step9-samr.md)

## <a name="step-8-configure-ip-address-exclusions-and-honeytoken-user"></a>Krok 8: Konfigurace vyloučení IP adres a uživatele honeytokenu
ATA umožňuje vyloučit z řady detekcí konkrétní IP adresy nebo uživatele. 

Například při **vyloučení DNS Reconnaissance** se může jednat o kontrolu zabezpečení, která jako mechanismus pro prohledávání používá službu DNS. Vyloučení pomáhá službě ATA takové kontroly ignorovat. Příkladem vyloučení *Pass-the-Ticket* je zařízení NAT.    

ATA taky umožňuje konfiguraci uživatele Honeytokenu, který se používá jako depeše nebezpečného actors – ověřování spojené s tímto účtem (obvykle spících) aktivuje výstrahu.

To můžete nakonfigurovat, postupujte takto:

1.  V konzole ATA klikněte na ikonu nastavení a vyberte **Konfigurace**.

    ![Nastavení konfigurace ATA](media/ATA-config-icon.png)

2.  V části **Detekce** klikněte na **Obecné**.

2. V části **Účty honeytokenu** zadejte název účtu honeytokenu. Pole účtů Honeytokenu je prohledávat a entity se automaticky zobrazí ve vaší síti.

   ![Honeytoken](media/honeytoken.png)

3. Klikněte na **Vyloučení**. Pro jednotlivé typy hrozeb zadejte uživatelský účet nebo IP adresu, které mají být vyloučené z detekce těchto hrozeb, a klikněte na znaménko *plus*. Pole **Add entity** (Přidat entitu) (uživatele nebo počítač) je možné prohledávat a automaticky se vyplní entitami ve vaší síti. Další informace najdete v tématu [Vyloučení entit z detekce](excluding-entities-from-detections.md).

   ![Vyloučení](media/exclusions.png)

4.  Klikněte na **Uložit**.


Blahopřejeme, úspěšně jste nasadili Microsoft Advanced Threat Analytics.

Zkontrolujte časovou osu útoků, abyste viděli zjištěné podezřelé aktivity a našli uživatele nebo počítače a zobrazili jejich profily.

ATA spustí vyhledávání podezřelých aktivit okamžitě. Některé aktivity, například některé aktivity podezřelého chování, není k dispozici, až ATA bude mít čas vytvořit profily chování (nejméně tři týdny).

Pokud chcete zkontrolovat, jestli je ATA v provozu a odchytává průniky do vaší sítě, můžete vyzkoušet [scénář simulace útoku ATA](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).


>[!div class="step-by-step"]
[«Krok 7](vpn-integration-install-step.md)
[kroku 9»](install-ata-step9-samr.md)


## <a name="related-videos"></a>Související videa
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Výběr správné typu ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)


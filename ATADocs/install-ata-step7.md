---
title: Instalace Advanced Threat Analytics – krok 8 | Dokumentace Microsoftu
description: V posledním kroku instalace ATA nakonfigurujete uživatele honeytokenu.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b237ce62e3828e1dced51a05d6d5a2977bf11285
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076551"
---
# <a name="install-ata---step-8"></a>Instalace ATA – krok 8

*Platí pro: Advanced Threat Analytics verze 1.9*

> [!div class="step-by-step"]
> [«Krok 7](vpn-integration-install-step.md)
> [kroku 9»](install-ata-step9-samr.md)

## <a name="step-8-configure-ip-address-exclusions-and-honeytoken-user"></a>Krok 8: Konfigurace vyloučení IP adres a uživatele honeytokenu

ATA umožňuje vyloučit z řady detekcí konkrétní IP adresy nebo uživatele. 

Například při **vyloučení DNS Reconnaissance** se může jednat o kontrolu zabezpečení, která jako mechanismus pro prohledávání používá službu DNS. Vyloučení pomáhá službě ATA takové kontroly ignorovat. Příkladem vyloučení *Pass-the-Ticket* je zařízení NAT.    

ATA také umožňuje konfiguraci uživatele Honeytokenu, který slouží jako past pro útočníky – jakákoliv autorizace přidružená tomuto účtu (obvykle neaktivnímu) spustí výstrahu.

Pokud chcete nastavit tuto konfiguraci, postupujte podle těchto kroků:

1.  V konzole ATA klikněte na ikonu nastavení a vyberte **Konfigurace**.

    ![Nastavení konfigurace ATA](media/ATA-config-icon.png)

2.  V části **detekce**, klikněte na tlačítko **značky entit**.

2. V části **Účty honeytokenu** zadejte název účtu honeytokenu. Pole účtu Honeytokenu lze prohledávat a automaticky zobrazí entity ve vaší síti.

   ![Honeytoken](media/honeytoken.png)

3. Klikněte na **Vyloučení**. Pro jednotlivé typy hrozeb zadejte uživatelský účet nebo IP adresu, které mají být vyloučené z detekce těchto hrozeb, a klikněte na znaménko *plus*. Pole **Add entity** (Přidat entitu) (uživatele nebo počítač) je možné prohledávat a automaticky se vyplní entitami ve vaší síti. Další informace najdete v tématu [Vyloučení entit z detekce](excluding-entities-from-detections.md).

   ![Vyloučení](media/exclusions.png)

4.  Klikněte na **Uložit**.


Blahopřejeme, úspěšně jste nasadili Microsoft Advanced Threat Analytics.

Zkontrolujte časovou osu útoků, abyste viděli zjištěné podezřelé aktivity a našli uživatele nebo počítače a zobrazili jejich profily.

ATA spustí vyhledávání podezřelých aktivit okamžitě. Některé aktivity, jako jsou třeba konkrétní aktivity podezřelého chování, není k dispozici, dokud ATA má určitá čas vytvořit profily chování (nejméně tři týdny).

Pokud chcete zkontrolovat, jestli je ATA v provozu a odchytává průniky do vaší sítě, můžete vyzkoušet [scénář simulace útoku ATA](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).


> [!div class="step-by-step"]
> [«Krok 7](vpn-integration-install-step.md)
> [kroku 9»](install-ata-step9-samr.md)


## <a name="related-videos"></a>Související videa
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Volba správného typu komponenty ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)


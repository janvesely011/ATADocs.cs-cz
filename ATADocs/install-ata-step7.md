---
title: "Instalace Advanced Threat Analytics – krok 7 | Dokumentace Microsoftu"
description: "V posledním kroku instalace ATA nakonfigurujete uživatele honeytokenu."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 09/03/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f5cb87148741c92dc7832da16cc37a749fa72fae
ms.sourcegitcommit: 654500928025e3cb127e095c17cc1d6444defd3a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="install-ata---step-7"></a>Instalace ATA – krok 7

>[!div class="step-by-step"]
[« Krok 6](install-ata-step6.md)

## <a name="step-7-configure-ip-address-exclusions-and-honeytoken-user"></a>Krok 7: Konfigurace vyloučení IP adres a uživatele honeytokenu
ATA umožňuje vyloučit z řady detekcí konkrétní IP adresy nebo uživatele. 

Například při **vyloučení DNS Reconnaissance** se může jednat o kontrolu zabezpečení, která jako mechanismus pro prohledávání používá službu DNS. Vyloučení pomáhá službě ATA takové kontroly ignorovat. Příkladem vyloučení *Pass-the-Ticket* je zařízení NAT.    

ATA také umožňuje konfiguraci uživatele honeytokenu, který slouží jako past pro útočníky – jakákoliv autorizace přidružená k tomuto účtu (obvykle neaktivnímu) spustí výstrahu.

Výše uvedené možnosti nakonfiguruje následovně:

1.  V konzole ATA klikněte na ikonu nastavení a vyberte **Konfigurace**.

    ![Nastavení konfigurace ATA](media/ATA-config-icon.png)

2.  V části **Detekce** klikněte na **Obecné**.

2. V části **Účty honeytokenu** zadejte název účtu honeytokenu. Pole účtu honeytokenu lze prohledávat a automaticky zobrazí entity ve vaší síti.

   ![Honeytoken](media/honeytoken.png)

3. Klikněte na **Vyloučení**. Pro jednotlivé typy hrozeb zadejte uživatelský účet nebo IP adresu, které mají být vyloučené z detekce těchto hrozeb, a klikněte na znaménko *plus*. Pole **Add entity** (Přidat entitu) (uživatele nebo počítač) je možné prohledávat a automaticky se vyplní entitami ve vaší síti. Další informace najdete v tématu [Vyloučení entit z detekce](excluding-entities-from-detections.md).

   ![Vyloučení](media/exclusions.png)

4.  Klikněte na **Uložit**.


Blahopřejeme, úspěšně jste nasadili Microsoft Advanced Threat Analytics.

Zkontrolujte časovou osu útoků, abyste viděli zjištěné podezřelé aktivity a našli uživatele nebo počítače a zobrazili jejich profily.

ATA okamžitě spustí vyhledávání podezřelých aktivit. Některé aktivity, jako jsou třeba konkrétní typy podezřelého chování, budou dostupné, až ATA bude mít čas vytvořit profily chování (nejméně tři týdny).

Pokud chcete zkontrolovat, jestli je ATA v provozu a odchytává průniky do vaší sítě, můžete vyzkoušet [scénář simulace útoku ATA](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).


>[!div class="step-by-step"]
[« Krok 6](install-ata-step6.md)



## <a name="related-videos"></a>Související videa
- [Výběr správné typu ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)


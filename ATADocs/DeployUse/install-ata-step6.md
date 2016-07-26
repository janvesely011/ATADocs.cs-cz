---
title: Instalace ATA | Microsoft ATA
description: "V posledním kroku instalace ATA nakonfigurujete podsítě s krátkodobým zapůjčením a uživatele honeytokenu."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 461b59e0f03bd6ba6d982767fa78bb415d2c16e0


---

# Instalace ATA – Krok 6

>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)

## Krok 6: Konfigurace podsítí s krátkodobým zapůjčením a uživatele honeytokenu
Podsítě s krátkodobým zapůjčením jsou podsítě, ve kterých se přiřazení IP adresy mění velmi rychle – během několika sekund nebo minut. Příkladem jsou IP adresy použité pro připojení VPN a IP adresy pro Wi-Fi. Pokud chcete zadat seznam podsítí s krátkodobým zapůjčením, které se používají ve vaší organizaci, postupujte takto:

1.  Z konzoly ATA na počítači ATA Gateway klikněte na ikonu nastavení a vyberte **Konfigurace**.

    ![Nastavení konfigurace ATA](media/ATA-config-icon.JPG)

2.  V části **Detekce** zadejte pro podsítě s krátkodobým zapůjčením následující údaje. Zadejte podsítě s krátkodobým zapůjčením pomocí formátu zápisu s lomítkem, například `192.168.0.0/24`, a klikněte na symbol plus.

3.  Jako SID účtů honeytokenu zadejte SID pro uživatelský účet, který nebude mít žádnou síťovou aktivitu, a klikněte na symbol plus. Příklad: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > Pokud chcete zjistit SID pro uživatele, najděte ho v konzole ATA a potom klikněte na kartu **Informace o účtu**. 

4.  Konfigurace vyloučení: Můžete nakonfigurovat IP adresy, které mají být vyloučené z konkrétní podezřelých aktivit. Další informace najdete v tématu [Práce s nastavením detekce ATA](working-with-detection-settings.md).

5.  Klikněte na **Uložit**.

![Uložení změn](media/ATA-VPN-Subnets.JPG)

Blahopřejeme, úspěšně jste nasadili Microsoft Advanced Threat Analytics.

Zkontrolujte časovou osu útoků, abyste viděli zjištěné podezřelé aktivity a našli uživatele nebo počítače a zobrazili jejich profily.

ATA okamžitě spustí vyhledávání podezřelých aktivit. Některé aktivity, jako jsou třeba konkrétní typy podezřelého chování, budou dostupné, až ATA bude mít čas vytvořit profily chování (nejméně tři týdny).


>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)


## Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jul16_HO3-->



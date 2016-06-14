---
# required metadata

title: Instalace ATA | Microsoft Advanced Threat Analytics
description: V posledním kroku instalace ATA nakonfigurujete podsítě s krátkodobým zapůjčením a uživatele honeytokenu.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalace ATA – Krok 6

>[!div class="step-by-step"]

## « Krok 5 Krok 6:
Konfigurace podsítí s krátkodobým zapůjčením a uživatele honeytokenu Podsítě s krátkodobým zapůjčením jsou podsítě, ve kterých se přiřazení IP adresy mění velmi rychle – během několika sekund nebo minut. Příkladem jsou IP adresy použité pro připojení VPN a IP adresy pro Wi-Fi.

1.  Pokud chcete zadat seznam podsítí s krátkodobým zapůjčením, které se používají ve vaší organizaci, postupujte takto:

    ![Z konzoly ATA na počítači ATA Gateway klikněte na ikonu nastavení a vyberte **Konfigurace**.](media/ATA-config-icon.JPG)

2.  Nastavení konfigurace ATA V části **Detekce** zadejte pro podsítě s krátkodobým zapůjčením následující údaje.

3.  Zadejte podsítě s krátkodobým zapůjčením pomocí formátu zápisu s lomítkem, například `192.168.0.0/24`, a klikněte na symbol plus. Jako SID účtů honeytokenu zadejte SID pro uživatelský účet, který nebude mít žádnou síťovou aktivitu, a klikněte na symbol plus.

    > Například: 

4.  Pokud chcete zjistit SID pro uživatele, najděte ho v konzole ATA a potom klikněte na kartu **Informace o účtu**. Konfigurace vyloučení: Můžete nakonfigurovat IP adresy, které mají být vyloučené z konkrétní podezřelých aktivit.

5.  Další informace najdete v tématu [Práce s nastavením detekce ATA](working-with-detection-settings.md).

![Klikněte na **Uložit**.](media/ATA-VPN-Subnets.JPG)

Uložení změn

Blahopřejeme, úspěšně jste nasadili Microsoft Advanced Threat Analytics.

Zkontrolujte časovou osu útoků, abyste viděli zjištěné podezřelé aktivity a našli uživatele nebo počítače a zobrazili jejich profily. ATA okamžitě spustí vyhledávání podezřelých aktivit.


>Některé aktivity, jako jsou třeba konkrétní typy podezřelého chování, budou dostupné, až ATA bude mít čas vytvořit profily chování (nejméně tři týdny).


## [!div class="step-by-step"]

- [« Krok 5](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Viz také](configure-event-collection.md)
- [Podívejte se na fórum ATA!](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jun16_HO1-->



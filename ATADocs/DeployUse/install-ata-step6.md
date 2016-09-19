---
title: Instalace ATA | Microsoft ATA
description: "V posledním kroku instalace ATA nakonfigurujete podsítě s krátkodobým zapůjčením a uživatele honeytokenu."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 57fe1272e95f69ef9d614505bbef0bb6c1d8ccb6


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# Instalace ATA – Krok 6

>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)

## Krok 6: Konfigurace vyloučení IP adres a uživatele honeytokenu
ATA umožňuje vyloučení určitých IP adres a podsítí protokolu IP ze dvou typů detekcí: **DNS Reconnaissance** a **Pass-the-Ticket**. 

Například při **vyloučení DNS Reconnaissance** se může jednat o kontrolu zabezpečení, která jako mechanismus pro prohledávání používá službu DNS. Vyloučení pomáhá službě ATA takové kontroly ignorovat. Příkladem vyloučení *Pass-the-Ticket* je zařízení NAT.    

ATA také umožňuje konfiguraci uživatele honeytokenu, který slouží jako past pro útočníky – jakákoliv autorizace přidružená k tomuto účtu (obvykle neaktivnímu) spustí výstrahu.

Výše uvedené možnosti nakonfiguruje následovně:

1.  V konzole ATA klikněte na ikonu nastavení a vyberte **Konfigurace**.

    ![Nastavení konfigurace ATA](media/ATA-config-icon.JPG)

2.  V části **Vyloučení detekcí** zadejte následující pro IP adresy *DNS Reconnaissance* nebo *Pass-the-Ticket* . Použijte například formát CIDR:  `192.168.1.0/24` a klikněte na znaménko *plus*.

    ![Uložení změn](media/ATA-exclusions.png)

3.  V části **Nastavení detekce** zadejte identifikátory SID účtu Honeytoken a klikněte na znaménko plus. Příklad: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    ![Nastavení konfigurace ATA](media/ATA-honeytoken.png)

    > [!NOTE]
    > Pokud chcete zjistit SID pro uživatele, najděte ho v konzole ATA a potom klikněte na kartu **Informace o účtu**. 

4.  Klikněte na **Uložit**.


Blahopřejeme, úspěšně jste nasadili Microsoft Advanced Threat Analytics.

Zkontrolujte časovou osu útoků, abyste viděli zjištěné podezřelé aktivity a našli uživatele nebo počítače a zobrazili jejich profily.

ATA okamžitě spustí vyhledávání podezřelých aktivit. Některé aktivity, jako jsou třeba konkrétní typy podezřelého chování, budou dostupné, až ATA bude mít čas vytvořit profily chování (nejméně tři týdny).


>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)


## Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Aug16_HO5-->



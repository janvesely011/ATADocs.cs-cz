---
title: "Práce s nastavením detekce ATA | Microsoft ATA"
description: "Popisuje, jak nakonfigurovat seznam IP adres a podsítí, které mají neobvyklé okolnosti a který by měly být zpracovávané jinak než ostatní entity v síti."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 28b6211599395317eb6336c37fd3461b8f5635f6
ms.openlocfilehash: 09248cdd5f8a66a164a5cd275f2765107f5c706d


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# Práce s nastavením detekce ATA
Konfigurační stránka **Detekce** umožňuje nastavit seznam IP adres a podsítí, které mají neobvyklé okolnosti a který by měly být zpracovávané trochu jinak než ostatní entity v síti.

## Nastavení detekce
V části **Detekce** můžete definovat následující položky:

-   **SID účtů honeytokenu** – Jedná se o uživatelský účet, který by neměl mít žádnou síťovou aktivitu. Tento účet se nakonfiguruje jako uživatel honeytokenu ATA. Pokud se někdo pokusí použít tento uživatelský účet, ATA vytvoří podezřelou aktivitu jako indikaci škodlivé aktivity. Ke konfiguraci uživatele honeytokenu budete potřebovat SID účtu uživatele, nikoli jeho uživatelské jméno.

>[!NOTE]
> SID uživatele můžete najít v konzole ATA v profilu uživatele na kartě *Informace o účtu*.


![Honeytoken nastavení detekce ATA](media/ata-detection-settings-honeytoken-1.7.png)


**Vyloučení detekce**: Můžete vyloučit IP adresy z následujících detekcí. Pokud zadáte IP adresu do jednoho z těchto seznamů, ATA vyloučí tuto IP adresu z konkrétního typu zjišťované aktivity.

-   Vyloučení IP adres pro rekognoskaci DNS

-   Vyloučení IP adres pro Pass-the-Ticket

![Vyloučení nastavení detekce ATA](media/ata-detection-settings-exclusions-1.7.png)


## Viz také
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Změna konfigurace ATA](modifying-ata-configuration.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->



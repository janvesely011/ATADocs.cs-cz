---
title: "Práce s nastavením detekce ATA | Microsoft ATA"
description: "Popisuje, jak nakonfigurovat seznam IP adres a podsítí, které mají neobvyklé okolnosti a který by měly být zpracovávané jinak než ostatní entity v síti."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 692247420a849db5d77c3c035ee59c4a5c533686


---

# Práce s nastavením detekce ATA
Konfigurační stránka **Detekce** umožňuje nastavit seznam IP adres a podsítí, které mají neobvyklé okolnosti a který by měly být zpracovávané trochu jinak než ostatní entity v síti.

## Nastavení detekce
Na stránce **Detekce** můžete definovat následující položky:

-   **Podsítě s krátkodobým zapůjčením** – Pokud má vaše organizace podsítě, ve kterých jsou IP adresy velmi krátkodobé, například podsítě IP adres sítě VPN nebo podsítě Wi-Fi, je důležité zadat tyto IP adresy a podsítě do ATA, aby se přidružení mezi počítačem a IP adresou z tohoto rozsahu ukládala po kratší dobu než pro ostatní IP adresy.

-   **SID účtů honeytokenu** – Jedná se o uživatelský účet, který by neměl mít žádnou síťovou aktivitu. Tento účet se nakonfiguruje jako uživatel honeytokenu ATA. Pokud se někdo pokusí použít tento uživatelský účet, ATA vytvoří podezřelou aktivitu jako indikaci škodlivé aktivity. Ke konfiguraci uživatele honeytokenu budete potřebovat SID účtu uživatele, nikoli jeho uživatelské jméno.

Můžete vyloučit IP adresy z následujících detekcí. Pokud zadáte IP adresu do jednoho z těchto seznamů, ATA vyloučí tuto IP adresu z konkrétního typu zjišťované aktivity.

-   Vyloučení IP adres pro rekognoskaci DNS

-   Vyloučení IP adres pro Pass-the-Ticket

## Viz také
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Změna konfigurace ATA](modifying-ata-configuration.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->



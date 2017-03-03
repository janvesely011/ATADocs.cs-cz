---
title: "Nastavení detekce Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Popisuje, jak nakonfigurovat seznam IP adres a podsítí, které mají neobvyklé okolnosti a který by měly být zpracovávané jinak než ostatní entity v síti."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: c88d74793c6210704f2a187df6508bf525907118


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="working-with-ata-detection-settings"></a>Práce s nastavením detekce ATA
Konfigurační stránka **Detekce** umožňuje nastavit seznam IP adres a podsítí, které mají neobvyklé okolnosti a který by měly být zpracovávané trochu jinak než ostatní entity v síti.

## <a name="setting-up-detection"></a>Nastavení detekce
V části **Detekce** můžete definovat následující položky:

-   **SID účtů honeytokenu** – Jedná se o uživatelský účet, který by neměl mít žádnou síťovou aktivitu. Tento účet se nakonfiguruje jako uživatel honeytokenu ATA. Pokud se někdo pokusí použít tento uživatelský účet, ATA vytvoří podezřelou aktivitu jako indikaci škodlivé aktivity. Ke konfiguraci uživatele honeytokenu budete potřebovat SID účtu uživatele, nikoli jeho uživatelské jméno.

>[!NOTE]
> SID uživatele můžete najít v konzole ATA v profilu uživatele na kartě *Informace o účtu*.


![Honeytoken nastavení detekce ATA](media/ata-detection-settings-honeytoken-1.7.png)


**Vyloučení detekce**: Můžete vyloučit IP adresy z následujících detekcí. Pokud zadáte IP adresu do jednoho z těchto seznamů, ATA vyloučí tuto IP adresu z konkrétního typu zjišťované aktivity.

-   Vyloučení IP adres pro rekognoskaci DNS

-   Vyloučení IP adres pro Pass-the-Ticket

![Vyloučení nastavení detekce ATA](media/ata-detection-settings-exclusions-1.7.png)


## <a name="see-also"></a>Viz také
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Změna konfigurace ATA](modifying-ata-configuration.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->



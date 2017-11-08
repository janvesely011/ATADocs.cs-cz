---
title: "Práce s protokoly auditu ATA | Dokumentace Microsoftu"
description: "Tento článek popisuje práci s protokoly auditu ATA v protokolu událostí Windows."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 287bb370f216c2f921eb954dfd4a34ceb8f095c7
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*

# <a name="working-with-ata-audit-logs"></a>Práce s protokoly auditu ATA

Protokoly auditu ATA se uchovávají v protokolu událostí Windows v oblasti **Protokoly aplikací a služeb** > **Microsoft ATA** na počítačích s komponentami ATA Center a ATA Gateway.

Protokol auditu pro ATA Center obsahuje:
-   Informace o podezřelých aktivitách
-   Monitorovací upozornění (stránku se stavem)
-   Přihlášení ke konzole ATA
-   Všechny změny konfigurace*

Protokol auditu pro ATA Gateway obsahuje:
-   Změny konfigurace brány* 

(Všechny změny konfigurace ATA Gateway se konfigurují přes ATA Center, ale pořád se auditují na samotném počítači s bránou.)

* V protokolu auditování změn konfigurace obsahuje předchozí konfiguraci a novou konfiguraci.


## <a name="see-also"></a>Viz také
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

---
title: "Změna konfigurace ATA – certifikát IIS | Microsoft Advanced Threat Analytics"
description: "Popisuje, jak změnit certifikát používaný službou IIS pro ATA Center."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 07888a46e26a7f87dc3b6424d97aba0813b43d02


---

# Změna konfigurace ATA – certifikát IIS

>[!div class="step-by-step"]
[« IP adresa konzoly ATA](modifying-ata-config-consoleip.md)
[Heslo připojení k doméně »](modifying-ata-config-dcpassword.md)

## Změna certifikátu IIS
V konzole můžete vybrat a změnit certifikát pro službu ATA Center, ale nejde změnit certifikát používaný službou IIS.

Pokud ho chcete změnit, postupujte takto:

> [!NOTE]
> Po úpravě certifikátu IIS byste si měli před instalací nových ATA Gateway stáhnout instalační balíček ATA Gateway.

Pokud potřebujete změnit certifikát používaný službou IIS pro ATA Center, proveďte tyto kroky ze serveru ATA Center.

1.  Nainstalujte nový certifikát na server ATA Center.

2.  Otevřete Správce Internetové informační služby (IIS).

3.  Rozbalte název serveru a rozbalte **Weby**.

4.  Vyberte web konzoly Microsoft ATA a v podokně **Akce** klikněte na **Vazby**.

    ![Akce vazby pro konzolu ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Vyberte **HTTPS** a klikněte na **Upravit**.

6.  V části **Certifikát SSL** vyberte nový certifikát.

7.  Před instalací nové ATA Gateway stáhněte instalační balíček ATA Gateway.

>[!div class="step-by-step"]
[« IP adresa konzoly ATA](modifying-ata-config-consoleip.md)
[Heslo připojení k doméně »](modifying-ata-config-dcpassword.md)

## Viz také
- [Práce s konzolou ATA](working-with-ata-console.md)
- [Instalace ATA](install-ata.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->



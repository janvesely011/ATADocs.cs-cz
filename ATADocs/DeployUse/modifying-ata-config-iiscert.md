---
title: "Změna konfigurace ATA – certifikát IIS | Microsoft ATA"
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
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 6516500f3134228cc92e269ef5ea8bfe4faa19d9


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



<!--HONumber=Jul16_HO3-->



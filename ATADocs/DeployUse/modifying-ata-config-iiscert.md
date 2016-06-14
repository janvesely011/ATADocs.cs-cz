---
# required metadata

title: Změna konfigurace ATA – certifikát IIS | Microsoft Advanced Threat Analytics
description: Popisuje, jak změnit certifikát používaný službou IIS pro ATA Center.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Změna konfigurace ATA – certifikát IIS

>[!div class="step-by-step"]

## « IP adresa konzoly ATA
Heslo připojení k doméně »

Změna certifikátu IIS

> V konzole můžete vybrat a změnit certifikát pro službu ATA Center, ale nejde změnit certifikát používaný službou IIS.

Pokud ho chcete změnit, postupujte takto:

1.  Po úpravě certifikátu IIS byste si měli před instalací nových ATA Gateway stáhnout instalační balíček ATA Gateway.

2.  Pokud potřebujete změnit certifikát používaný službou IIS pro ATA Center, proveďte tyto kroky ze serveru ATA Center.

3.  Nainstalujte nový certifikát na server ATA Center.

4.  Otevřete Správce Internetové informační služby (IIS).

    ![Rozbalte název serveru a rozbalte **Weby**.](media/ATA-console-change-IP-bindings.jpg)

5.  Vyberte web konzoly Microsoft ATA a v podokně **Akce** klikněte na **Vazby**.

6.  Akce vazby pro konzolu ATA

7.  Vyberte **HTTPS** a klikněte na **Upravit**.

>V části **Certifikát SSL** vyberte nový certifikát.

## Před instalací nové ATA Gateway stáhněte instalační balíček ATA Gateway.
- [[!div class="step-by-step"]](working-with-ata-console.md)
- [« IP adresa konzoly ATA](install-ata.md)
- [Heslo připojení k doméně »](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Jun16_HO1-->



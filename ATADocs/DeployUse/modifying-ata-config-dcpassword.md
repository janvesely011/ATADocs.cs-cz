---
# required metadata

title: Změna konfigurace ATA – heslo připojení k doméně | Microsoft Advanced Threat Analytics
description: Popisuje způsob změny hesla připojení k doméně na ATA Gateway.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Změna konfigurace ATA – heslo připojení k doméně

>[!div class="step-by-step"]


## « Certifikát IIS
Změna hesla připojení k doméně Pokud změníte heslo připojení k doméně, ujistěte se, že je zadané heslo správné.

Pokud není, služba ATA Gateway se zastaví.
`The supplied credential is invalid.`

Pokud máte podezření, že se to stalo, vyhledejte v souboru Microsoft.Tri.Gateway-Errors.log na ATA Gateway následující:

1.  Když to chcete opravit, podle následujícího postupu aktualizujte na ATA Gateway heslo připojení k doméně:

2.  Na ATA Gateway otevřete konzolu ATA.

    ![Vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**.](media/ATA-config-icon.JPG)

3.  Ikona nastavení konfigurace ATA

    ![Vyberte možnost **Obecné**.](media/ATA-GW-change-DC-password.JPG)

4.  Obrázek změny hesla pro ATA Gateway

5.  V části **Obecné** změňte heslo.

6.  Klikněte na **Uložit**.

>Po změně hesla ručně zkontrolujte, že je služba ATA Gateway na serverech ATA Gateway spuštěná.

## [!div class="step-by-step"]
- [« Certifikát IIS](working-with-ata-console.md)
- [Viz také](install-ata.md)
- [Práce s konzolou ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Jun16_HO1-->



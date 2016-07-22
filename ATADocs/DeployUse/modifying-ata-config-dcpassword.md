---
title: "Změna konfigurace ATA – heslo připojení k doméně | Microsoft Advanced Threat Analytics"
description: "Popisuje způsob změny hesla připojení k doméně na ATA Gateway."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: df1dbed75ad0c88de5a6c51d2e5d7e521a2577c4


---

# Změna konfigurace ATA – heslo připojení k doméně

>[!div class="step-by-step"]
[« Certifikát IIS](modifying-ata-config-iiscert.md)


## Změna hesla připojení k doméně
Pokud změníte heslo připojení k doméně, ujistěte se, že je zadané heslo správné. Pokud není, služba ATA Gateway se zastaví.

Pokud máte podezření, že se to stalo, vyhledejte v souboru Microsoft.Tri.Gateway-Errors.log na ATA Gateway následující:
`The supplied credential is invalid.`

Když to chcete opravit, podle následujícího postupu aktualizujte na ATA Gateway heslo připojení k doméně:

1.  Na ATA Gateway otevřete konzolu ATA.

2.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

3.  Vyberte **Obecné**.

    ![Obrázek změny hesla pro ATA Gateway](media/ATA-GW-change-DC-password.JPG)

4.  V části **Obecné** změňte heslo.

5.  Klikněte na **Uložit**.

6.  Po změně hesla ručně zkontrolujte, že je služba ATA Gateway na serverech ATA Gateway spuštěná.

>[!div class="step-by-step"]
[« Certifikát IIS](modifying-ata-config-iiscert.md)

## Viz také
- [Práce s konzolou ATA](working-with-ata-console.md)
- [Instalace ATA](install-ata.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->



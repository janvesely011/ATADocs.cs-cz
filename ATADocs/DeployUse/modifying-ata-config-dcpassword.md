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
[« Certifikát IIS](modifying-ata-config-iiscert.md)
[Název síťového adaptéru pro zachytávání »](modifying-ata-config-nicname.md)

## Změna hesla připojení k doméně
Pokud změníte heslo připojení k doméně, ujistěte se, že je zadané heslo správné. Pokud není, služba ATA se na serverech ATA Gateway zastaví.

Pokud máte podezření, že se to stalo, vyhledejte v souboru Microsoft.Tri.Gateway-Errors.log na ATA Gateway následující:
`The supplied credential is invalid.`

Když to chcete opravit, podle následujícího postupu aktualizujte na ATA Gateway heslo připojení k doméně:

1.  Na ATA Gateway otevřete konzolu ATA.

2.  Vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**..

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

3.  Vyberte **ATA Gateway**..

    ![Obrázek změny hesla pro ATA Gateway](media/ATA-GW-change-DC-password.JPG)

4.  V části **Nastavení připojení k doméně** změňte heslo.

5.  Klikněte na **Uložit**..

6.  Po změně hesla ručně zkontrolujte, že je služba ATA Gateway na serverech ATA Gateway spuštěná.

>[!div class="step-by-step"]
[« Certifikát IIS](modifying-ata-config-iiscert.md)
[Název síťového adaptéru pro zachytávání »](modifying-ata-config-nicname.md)

## Viz také
- [Práce s konzolou ATA](/advanced-threat-analytics/understand-explore/working-with-ata-console)
- [Instalace ATA](install-ata.md)
- [Podporu získáte na našem fóru!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO4-->



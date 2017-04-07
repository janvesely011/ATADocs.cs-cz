---
title: "Změna konfigurace Advanced Threat Analytics – heslo připojení k doméně | Dokumentace Microsoftu"
description: "Popisuje způsob změny hesla připojení k doméně na ATA Gateway."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e9cb7bcf6f32559f7b2f330df4333c3fdc55a283
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="change-ata-configuration---domain-connectivity-password"></a>Změna konfigurace ATA – heslo připojení k doméně

>[!div class="step-by-step"]
[« Adresa URL konzoly ATA](modifying-ata-config-consoleurl.md)


## <a name="change-the-domain-connectivity-password"></a>Změna hesla připojení k doméně
Pokud změníte heslo připojení k doméně, ujistěte se, že je zadané heslo správné. Pokud není, služba ATA Gateway se zastaví.

Pokud máte podezření, že se to stalo, vyhledejte v souboru Microsoft.Tri.Gateway-Errors.log na ATA Gateway toto: `The supplied credential is invalid.`

Když to chcete opravit, podle následujícího postupu aktualizujte na ATA Center heslo připojení k doméně:

1.  V ATA Center otevřete konzolu ATA.

2.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

3.  Vyberte **Adresářové služby**.

    ![Obrázek změny hesla pro ATA Gateway](media/ATA-GW-change-DC-password.png)

4.  V části **Heslo** změňte heslo.

    Pokud služba ATA Center má k dispozici připojení k doméně, použijte tlačítko **Testovat připojení** a ověřte platnost přihlašovacích údajů.

5.  Klikněte na **Uložit**.

6.  Po změně hesla ručně zkontrolujte, že je služba ATA Gateway na serverech ATA Gateway spuštěná.

>[!div class="step-by-step"]
[« Adresa URL konzoly ATA](modifying-ata-config-consoleurl.md)

## <a name="see-also"></a>Viz také
- [Práce s konzolou ATA](working-with-ata-console.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

---
title: "Změna konfigurace Advanced Threat Analytics – heslo připojení k doméně | Dokumentace Microsoftu"
description: "Popisuje způsob změny hesla připojení k doméně na ATA Gateway."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 19eee0466269bbc2255d3a83e2f8c073057ba356
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/30/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# Změna konfigurace ATA – heslo připojení k doméně
<a id="change-ata-configuration---domain-connectivity-password" class="xliff"></a>



## Změna hesla připojení k doméně
<a id="change-the-domain-connectivity-password" class="xliff"></a>
Pokud změníte heslo připojení k doméně, ujistěte se, že je zadané heslo správné. Pokud není, služba ATA Gateway se zastaví.

Pokud máte podezření, že se to stalo, vyhledejte v souboru Microsoft.Tri.Gateway-Errors.log na ATA Gateway toto: `The supplied credential is invalid.`

Když to chcete opravit, podle následujícího postupu aktualizujte na ATA Center heslo připojení k doméně:

1.  V ATA Center otevřete konzolu ATA.

2.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.png)

3.  Vyberte **Adresářové služby**.

    ![Obrázek změny hesla pro ATA Gateway](media/ATA-GW-change-DC-password.png)

4.  V části **Heslo** změňte heslo.

    Pokud služba ATA Center má k dispozici připojení k doméně, použijte tlačítko **Testovat připojení** a ověřte platnost přihlašovacích údajů.

5.  Klikněte na **Uložit**.

6.  Po změně hesla ručně zkontrolujte, že je služba ATA Gateway na serverech ATA Gateway spuštěná.



## Viz také
<a id="see-also" class="xliff"></a>
- [Práce s konzolou ATA](working-with-ata-console.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

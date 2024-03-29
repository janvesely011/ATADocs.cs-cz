---
title: Změna konfigurace Advanced Threat Analytics – heslo připojení k doméně | Dokumentace Microsoftu
description: Popisuje způsob změny hesla připojení k doméně na ATA Gateway.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 345d888047b10777239efaf96b789c477a62a81b
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65197106"
---
# <a name="change-ata-configuration---domain-connectivity-password"></a>Změna konfigurace ATA – heslo připojení k doméně

*Platí pro: Advanced Threat Analytics verze 1.9*

## <a name="change-the-domain-connectivity-password"></a>Změna hesla připojení k doméně

Pokud změníte heslo připojení k doméně, ujistěte se, že je zadané heslo správné. Pokud není, služba ATA Gateway se zastaví na komponenty ATA Gateway.

Pokud máte podezření, že se to stalo v komponentě ATA Gateway, vyhledejte v souboru Microsoft.Tri.Gateway-Errors.log následující chyby: `The supplied credential is invalid.`

Když to chcete opravit, podle následujícího postupu aktualizujte na ATA Center heslo připojení k doméně:

1.  V ATA Center otevřete konzolu ATA.

2.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.png)

3.  Vyberte **Adresářové služby**.

    ![Obrázek změny hesla pro ATA Gateway](media/ATA-GW-change-DC-password.png)

4.  V části **Heslo** změňte heslo.

    Pokud ATA Center připojená k doméně, použijte **Test připojení** tlačítko ověřit přihlašovací údaje

5.  Klikněte na **Uložit**.

6.  Po změně hesla ručně zkontrolujte, že je služba ATA Gateway na serverech ATA Gateway spuštěná.



## <a name="see-also"></a>Viz také
- [Práce s konzolou ATA](working-with-ata-console.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

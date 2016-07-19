---
title: "Instalace ATA – Krok 2 | Microsoft Advanced Threat Analytics"
description: "Druhý krok instalace ATA vám pomůže nakonfigurovat nastavení připojení k doméně na serveru ATA Center."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 73e2eb84e1e21cbc5afcb7a100f9a67da63c66a5


---

# Instalace ATA – Krok 2

>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)

## Krok 2: Konfigurace obecného nastavení ATA Gateway
Nastavení v části **Obecné** platí pro všechny komponenty ATA Gateway, které spravuje ATA Center.

Pokud chcete konfigurovat obecné nastavení ATA Gateway, postupujte takto:

1.  Otevřete konzolu ATA a přihlaste se. Pokyny najdete v tématu [Práce s konzolou ATA](working-with-ata-console.md).

2.  Klikněte na ikonu Nastavení a vyberte **Konfigurace**.

    ![Nastavení konfigurace ATA Gateway](media/ATA-config-icon.JPG)

3.  Na kartě **Obecné** v části **ATA Gateways** zadejte následující informace a klikněte na **Uložit**.

    |Pole|Komentáře|
    |---------|------------|
    |**Uživatelské jméno** (povinné)|Zadejte uživatelské jméno jen pro čtení, například **uživatel1**.|
    |**Heslo** (povinné)|Zadejte heslo pro uživatele, který je jen pro čtení, například **Pencil1**. **Poznámka:** Zkontrolujte, že je toto heslo správné. Pokud uložíte chybné heslo, služba ATA se na serverech ATA Gateway zastaví.|
    |**Doména** (povinné)|Zadejte doménu pro uživatele, který je jen pro čtení, například **contoso.com**. **Poznámka:** Je důležité, abyste zadali kompletní plně kvalifikovaný název domény, ve které je uživatel umístěný. Pokud je například účet uživatele v doméně corp.contoso.com, musíte zadat `corp.contoso.com`, a ne contoso.com.|
    |Automaticky aktualizovat všechny komponenty ATA Gateway |Pokud povolíte toto nastavení, ve vydáních příštích verzí se při aktualizaci komponenty ATA Center budou automaticky aktualizovat všechny komponenty ATA Gateway.|

    ![Obrázek nastavení připojení k doméně ATA](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)


## Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jun16_HO4-->



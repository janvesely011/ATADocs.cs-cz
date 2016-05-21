---
# required metadata

title: Instalace ATA – Krok 2 | Microsoft Advanced Threat Analytics
description: Druhý krok instalace ATA vám pomůže nakonfigurovat nastavení připojení k doméně na serveru ATA Center.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalace ATA – Krok 2

>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)

## Krok 2: Konfigurace nastavení připojení k doméně ATA Gateway
Nastavení v části nastavení připojení k doméně platí pro všechny komponenty ATA Gateway, které spravuje ATA Center.

Chcete-li konfigurovat nastavení připojení k doméně, proveďte na serveru ATA Center následující kroky.

1.  Otevřete konzolu ATA a přihlaste se. Pokyny najdete v tématu [Práce s konzolou ATA](/advanced-threat-analytics/understand-explore/working-with-ata-console)..

2.  Při prvním přihlášení do konzoly ATA po instalaci ATA Center budete automaticky přesměrování na konfigurační stránku komponent ATA Gateway. Pokud potřebujete změnit libovolné nastavení později, klikněte na ikonu Nastavení a vyberte **Konfigurace**..

    ![Nastavení konfigurace ATA Gateway](media/ATA-config-icon.JPG)

3.  Na stránce **Brány** klikněte na **Nastavení připojení k doméně**, zadejte následující informace a klikněte na **Uložit**..

    |Pole|Komentáře|
    |---------|------------|
    |**Uživatelské jméno** (povinné)|Zadejte uživatelské jméno jen pro čtení, například: **uživatel1**..|
    |**Heslo** (povinné)|Zadejte heslo pro uživatele, který je jen pro čtení, například: **Pencil1**. **Poznámka:** Zkontrolujte, že je toto heslo správné. Pokud uložíte chybné heslo, služba ATA se na serverech ATA Gateway zastaví.|
    |**Doména** (povinné)|Zadejte doménu pro uživatele, který je jen pro čtení, například **contoso.com**. **Poznámka:** Je důležité, abyste zadali plně kvalifikovaný název domény, kde je uživatel umístěn. Pokud je například účet uživatele v doméně corp.contoso.com, musíte zadat `corp.contoso.com`, a ne contoso.com.|
    ![Obrázek nastavení připojení k doméně ATA](media/ATA-Domain-Connectivity-User.JPG)


>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)


## Viz také

- [Podporu získáte na našem fóru!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurace shromažďování událostí](/advanced-threat-analytics/plan-design/configure-event-collection)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=Apr16_HO4-->



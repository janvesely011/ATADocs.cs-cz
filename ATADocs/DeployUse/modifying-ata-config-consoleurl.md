---
title: "Změna konfigurace ATA – IP adresa konzoly ATA | Microsoft Advanced Threat Analytics"
description: "Popisuje, jak změnit IP adresu konzoly ATA, která se používá k vytvoření zástupce konzoly ATA na komponentách ATA Gateway."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 08/24/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: b3d11a87f1909c1fd964fa990e5d36a91691a844


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# Změna konfigurace ATA – adresa URL konzoly ATA

>[!div class="step-by-step"]
[« Certifikát ATA Center](modifying-ata-config-centercert.md)
[Heslo připojení k doméně »](modifying-ata-config-dcpassword.md)

## Změna adresy URL konzoly ATA
Ve výchozím nastavení adresa URL konzoly ATA je IP adresa, vybraná pro konzolu ATA při instalaci ATA Center.

Adresa URL se používá v následujících scénářích:

-   Instalace komponent ATA Gateway – Při instalaci se ATA Gateway registruje v ATA Center. Tento proces registrace je uskutečněn připojením ke konzole ATA. Pokud zadáte plně kvalifikovaný název domény pro adresu URL konzoly ATA, je potřeba zajistit, že ATA Gateway umí přeložit tento plně kvalifikovaný název domény na IP adresu, na kterou je konzola ATA vázaná.

-   Výstrahy – Když ATA rozešle výstrahu SIEM nebo e-mailovou výstrahu, zahrnuje odkaz na podezřelou aktivitu. Hostitelská část odkazu je nastavení adresy URL konzoly ATA.

-   Pokud jste nainstalovali certifikát z vaší interní certifikační autority (CA), budete pravděpodobně chtít, aby se adresa URL shodovala s názvem předmětu v certifikátu, takže uživatelům se nebudou zobrazovat upozornění při připojování ke konzole ATA.

-   Použití plně kvalifikovaného názvu domény pro adresu URL konzoly ATA umožňuje změnit IP adresu, kterou používá konzola ATA bez přerušení výstrah, které byly rozeslány dřív, a bez nutnosti znovu stahovat balíček ATA Gateway. Je potřeba jenom aktualizovat DNS novou IP adresou.

> [!NOTE]
> Po úpravě adresy URL konzoly ATA byste si měli před instalací nových ATA Gateway stáhnout instalační balíček ATA Gateway.

Pokud potřebujete změnit adresu URL pro konzolu ATA, proveďte tyto kroky na serveru ATA Center.

1.  Otevřete konzolu ATA.

2.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

3.  Vyberte možnost **Center**.

4.  V části **IP adresa konzoly** vyberte jednu z existujících IP adres

5.  V části **Adresa URL konzoly** podle potřeby upravte adresu URL:

    ![Adresa URL konzoly ATA](media/ATA-chge-center-URL.png)
6.  Klikněte na **Uložit**.

>[!div class="step-by-step"]
[« Certifikát ATA Center](modifying-ata-config-centercert.md)
[Heslo připojení k doméně »](modifying-ata-config-dcpassword.md)


## Viz také
- [Práce s konzolou ATA](working-with-ata-console.md)
- [Instalace ATA](install-ata.md)
- [Podívejte se na fórum ATA!](https://aka.ms/ata-forum)



<!--HONumber=Aug16_HO5-->



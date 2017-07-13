---
title: "Instalace Advanced Threat Analytics – krok 2 | Dokumentace Microsoftu"
description: "Druhý krok instalace ATA vám pomůže nakonfigurovat nastavení připojení k doméně na serveru ATA Center."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: aa5e752fa10644165cb70d2cd8c08a1145261edb
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/03/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# Instalace ATA – krok 2
<a id="install-ata---step-2" class="xliff"></a>

>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)

## Krok 2: Zadejte uživatelské jméno a heslo pro připojení k vaší doménové struktuře Active Directory.
<a id="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest" class="xliff"></a>

Při prvním otevření konzoly ATA se objeví následující obrazovka:

![Uvítání ATA fáze 1](media/ATA_1.7-welcome-provide-username.png)

1.  Zadejte následující informace a klikněte na **Uložit**.

    |Pole|Komentáře|
    |---------|------------|
    |**Uživatelské jméno** (povinné)|Zadejte uživatelské jméno jen pro čtení, například **ATAuser**.|
    |**Heslo** (povinné)|Zadejte heslo pro uživatele, který je jen pro čtení, například **Pencil1**.|
    |**Doména** (povinné)|Zadejte doménu pro uživatele, který je jen pro čtení, například **contoso.com**. **Poznámka:** Je důležité, abyste zadali kompletní plně kvalifikovaný název domény, ve které je uživatel umístěný. Pokud je například účet uživatele v doméně corp.contoso.com, musíte zadat `corp.contoso.com`, a ne contoso.com.|

2. Kliknutím na **Test připojení** můžete otestovat připojení k doméně a ověřit, že zadané přihlašovací údaje poskytují přístup. Bude to fungovat jenom v případě, že je komponenta ATA Center připojená k doméně.   

    Po uložení se uvítací zpráva v konzole změní na následující: ![Uvítání ATA fáze 1 dokončeno](media/ATA_1.7-welcome-provide-username-finished.png)

3. Na konzole pokračujte kliknutím na **Stáhnout instalační soubor brány a nainstalovat první bránu**.


>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)


## Viz také
<a id="see-also" class="xliff"></a>

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

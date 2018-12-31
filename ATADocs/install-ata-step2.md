---
title: Instalace Advanced Threat Analytics – krok 2 | Dokumentace Microsoftu
description: Druhý krok instalace ATA vám pomůže nakonfigurovat nastavení připojení k doméně na serveru ATA Center.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/30/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c02b495903a30acb47d86c8245e67377adebd14d
ms.sourcegitcommit: 1bdaccbddf2896be517885fbcee1c2bc47f4de8d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/30/2018
ms.locfileid: "53815052"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="install-ata---step-2"></a>Instalace ATA – krok 2

> [!div class="step-by-step"]
> [« Krok 1](install-ata-step1.md)
> [Krok 3 »](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Krok 2. Zadejte uživatelské jméno a heslo pro připojení k vaší doménové struktuře Active Directory.

Při prvním otevření konzoly ATA se objeví následující obrazovka:

![Uvítání ATA fáze 1](media/ATA_1.7-welcome-provide-username.png)

1.  Zadejte následující informace a klikněte na **Uložit**.

    |Pole|Komentáře|
    |---------|------------|
    |**Uživatelské jméno** (povinné)|Zadejte jméno uživatele jen pro čtení, například: **ATAuser**. **Poznámka:** Proveďte **není** pomocí formátu UPN pro své uživatelské jméno.|
    |**Heslo** (povinné)|Zadejte heslo pro uživatele jen pro čtení, například: **Pencil1**.|
    |**Doména** (povinné)|Zadejte doménu pro uživatele, který je jen pro čtení, například **contoso.com**. **Poznámka:** Je důležité, abyste zadali plně kvalifikovaný název domény, ve kterém se uživatel zdržuje. Pokud je například účet uživatele v doméně corp.contoso.com, musíte zadat `corp.contoso.com`, a ne contoso.com.|

2. Kliknutím na **Test připojení** můžete otestovat připojení k doméně a ověřit, že zadané přihlašovací údaje poskytují přístup. Tento postup funguje, pokud se komponenta ATA Center připojená k doméně.    

    Po uložení se uvítací zpráva v konzole změní na následující zpráva: ![Uvítání ATA fáze 1 dokončeno](media/ATA_1.7-welcome-provide-username-finished.png)

3. Na konzole pokračujte kliknutím na **Stáhnout instalační soubor brány a nainstalovat první bránu**.


> [!div class="step-by-step"]
> [« Krok 1](install-ata-step1.md)
> [Krok 3 »](install-ata-step3.md)


## <a name="see-also"></a>Viz také
## <a name="related-videos"></a>Související videa
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Volba správného typu komponenty ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

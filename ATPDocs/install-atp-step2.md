---
title: Připojení ochrany ATP v programu Azure k rychlému startu pro Active Directory | Dokumentace Microsoftu
description: Druhý krok instalace ochrany ATP v programu Azure vám pomůže nakonfigurovat nastavení připojení k doméně na cloudové služby Azure ATP
author: mlottner
ms.author: mlottner
ms.date: 02/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 3e39bcdd5b3ffbe7a1d39064d28851fba7058d94
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263946"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>Rychlý start: Připojte se k vaší doménové struktury služby Active Directory

V tomto rychlém startu se připojíte ochrany ATP v programu Azure pro Active Directory (AD) pro načtení data o uživatelích a počítačích. Pokud se připojujete několik doménových struktur, přečtěte si článek [podporu více doménovými strukturami](atp-multi-forest.md) článku.

## <a name="prerequisites"></a>Požadavky

- [Instance služby Azure ATP](install-atp-step1.md).
- Zkontrolujte [požadavky služby Azure ATP](atp-prerequisites.md) článku.
- **Místní** AD uživatelský účet a heslo s oprávněním ke čtení pro všechny objekty v monitorovaném domén.

## <a name="provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Zadejte uživatelské jméno a heslo pro připojení k vaší doménové struktury služby Active Directory

Při prvním otevření ochrany ATP v programu Azure portal, zobrazí se následující obrazovka:

![Azure ATP úvodní fáze 1](media/directory-services.png)


1. Zadejte následující informace a klikněte na **Uložit**.

    |Pole|Komentáře|
    |---------|------------|
    |**Uživatelské jméno** (povinné)|Zadejte uživatelské jméno služby Active Directory jen pro čtení. Příklad: **ATPuser**.  Je nutné použít **místní** uživatelský účet AD. **Není** pomocí formátu UPN pro své uživatelské jméno.|
    |**Heslo** (povinné)|Zadejte heslo pro daného uživatele jen pro čtení. Příklad: **Pencil1**.|
    |**Doména** (povinné)|Zadejte doménu pro uživatele jen pro čtení. Příklad: **contoso.com**. Je důležité, abyste zadali plně kvalifikovaný název domény, ve kterém se uživatel zdržuje. Pokud je například účet uživatele v doméně corp.contoso.com, musíte zadat `corp.contoso.com`, a ne contoso.com.|

2. Na portálu ochrany ATP v programu Azure, klikněte na tlačítko **stáhnout instalaci senzoru a nainstalovat první senzor** pokračujte.


## <a name="next-steps"></a>Další postup

> [!div class="step-by-step"]
> [«Krok 1: vytvoření instance služby Azure ATP](install-atp-step1.md)
> [krok 3 – stáhnout instalaci senzoru»](install-atp-step3.md)

## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://aka.ms/azureatpcommunity) ještě dnes!

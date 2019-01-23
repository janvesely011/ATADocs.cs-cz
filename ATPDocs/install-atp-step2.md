---
title: Nainstalovat Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Druhý krok instalace ochrany ATP v programu Azure vám pomůže nakonfigurovat nastavení připojení k doméně na cloudové služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/30/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7ff0324da5cff1ac9ff6aa73fd32d0328279c12b
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/23/2019
ms.locfileid: "54458678"
---
# <a name="install-azure-atp---step-2"></a>Instalace služby Azure ATP – krok 2

> [!div class="step-by-step"]
> [« Krok 1](install-atp-step1.md)
> [Krok 3 »](install-atp-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Krok 2. Zadejte uživatelské jméno a heslo pro připojení k vaší doménové struktury služby Active Directory

Při prvním otevření ochrany ATP v programu Azure portal, zobrazí se následující obrazovka:

![Azure ATP úvodní fáze 1](media/directory-services.png)

> [!IMPORTANT]
> Přihlašovací údaje uživatele v tomto poli musí být pro uživatelský účet v místní Active Directory. 


1.  Zadejte následující informace a klikněte na **Uložit**.

    |Pole|Komentáře|
    |---------|------------|
    |**Uživatelské jméno** (povinné)|Zadejte jen pro čtení služby Active Directory uživatelské jméno, například: **ATPuser**. **Poznámka:** Proveďte **není** pomocí formátu UPN pro své uživatelské jméno.|
    |**Heslo** (povinné)|Zadejte heslo pro uživatele jen pro čtení, například: **Pencil1**.|
    |**Doména** (povinné)|Zadejte doménu pro uživatele, který je jen pro čtení, například **contoso.com**. **Poznámka:** Je důležité, abyste zadali plně kvalifikovaný název domény, ve kterém se uživatel zdržuje. Pokud je například účet uživatele v doméně corp.contoso.com, musíte zadat `corp.contoso.com`, a ne contoso.com.|

3. Na portálu ochrany ATP v programu Azure, klikněte na tlačítko **stáhnout instalaci senzoru a nainstalovat první senzor** pokračujte.


> [!div class="step-by-step"]
> [« Krok 1](install-atp-step1.md)
> [Krok 3 »](install-atp-step3.md)


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
---
title: Instalace Azure Advanced Threat Protection – krok 2 | Dokumentace Microsoftu
description: Druhý krok instalace ochrany ATP v programu Azure vám pomůže nakonfigurovat nastavení připojení k doméně na cloudové služby Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 45c1ddfc80c481549ceb08ed45f535ca029b9626
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453829"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="install-azure-atp---step-2"></a>Instalace služby Azure ATP – krok 2

> [!div class="step-by-step"]
> [« Krok 1](install-atp-step1.md)
> [Krok 3 »](install-atp-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Krok 2: Zadejte uživatelské jméno a heslo pro připojení k vaší doménové struktury služby Active Directory

Při prvním otevření pracovního prostoru portálu ochrany ATP v programu Azure, zobrazí se následující obrazovka:

![Azure ATP úvodní fáze 1](media/directory-services.png)

> [!IMPORTANT]
> Přihlašovací údaje uživatele v tomto poli musí být pro uživatelský účet v místní Active Directory. 


1.  Zadejte následující informace a klikněte na **Uložit**.

    |Pole|Komentáře|
    |---------|------------|
    |**Uživatelské jméno** (povinné)|Zadejte jen pro čtení služby Active Directory uživatelské jméno, například: **ATPuser**.|
    |**Heslo** (povinné)|Zadejte heslo pro uživatele, který je jen pro čtení, například **Pencil1**.|
    |**Doména** (povinné)|Zadejte doménu pro uživatele, který je jen pro čtení, například **contoso.com**. **Poznámka:** Je důležité, abyste zadali kompletní plně kvalifikovaný název domény, ve které je uživatel umístěný. Pokud je například účet uživatele v doméně corp.contoso.com, musíte zadat `corp.contoso.com`, a ne contoso.com.|

3. Na portálu pracovního prostoru klikněte na tlačítko **stáhnout instalaci senzoru a nainstalovat první senzor** pokračujte.


> [!div class="step-by-step"]
> [« Krok 1](install-atp-step1.md)
> [Krok 3 »](install-atp-step3.md)


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
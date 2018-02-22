---
title: "Instalace Azure Advanced Threat Protection – krok 2 | Microsoft Docs"
description: "Krok 2 instalace Azure ATP vám pomůže nakonfigurovat nastavení připojení k doméně v Azure ATP cloudové služby"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 11f9d5bf69ffda0843a94c7a2bb31869dc980dce
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-2"></a>Nainstalovat Azure ATP – krok 2

>[!div class="step-by-step"]
[« Krok 1](install-atp-step1.md)
[Krok 3 »](install-atp-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Krok 2: Zadejte uživatelské jméno a heslo pro připojení k vaší doménové struktury služby Active Directory

Při prvním spuštění portálu Azure ATP pracovního prostoru, zobrazí se následující obrazovka:

![Azure ATP úvodní fáze 1](media/directory-services.png)

> [!IMPORTANT]
> Přihlašovací údaje uživatele v tomto poli musí být pro uživatelský účet ve službě Active Directory v místě. 


1.  Zadejte následující informace a klikněte na **Uložit**.

    |Pole|Komentáře|
    |---------|------------|
    |**Uživatelské jméno** (povinné)|Zadejte jen pro čtení služby Active Directory uživatelské jméno, například: **ATPuser**.|
    |**Heslo** (povinné)|Zadejte heslo pro uživatele, který je jen pro čtení, například **Pencil1**.|
    |**Doména** (povinné)|Zadejte doménu pro uživatele, který je jen pro čtení, například **contoso.com**. **Poznámka:** Je důležité, abyste zadali kompletní plně kvalifikovaný název domény, ve které je uživatel umístěný. Pokud je například účet uživatele v doméně corp.contoso.com, musíte zadat `corp.contoso.com`, a ne contoso.com.|

3. V prostoru portálu, klikněte na **senzor instalační program stáhnout a nainstalovat první senzoru** pokračujte.


>[!div class="step-by-step"]
[« Krok 1](install-atp-step1.md)
[Krok 3 »](install-atp-step3.md)


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
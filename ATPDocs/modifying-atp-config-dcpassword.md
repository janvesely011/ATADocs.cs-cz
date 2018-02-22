---
title: "Změna konfigurace Azure Advanced Threat Protection – heslo připojení k doméně | Microsoft Docs"
description: "Popisuje, jak chcete-li změnit heslo připojení k doméně na samostatné senzoru Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 369f00b1b33fe509850bc331b0d5b45ae161f91c
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="change-azure-atp-workspace-portal-configuration---domain-connectivity-password"></a>Změna Azure ATP prostoru portálu konfigurace – heslo připojení k doméně



## <a name="change-the-domain-connectivity-password"></a>Změna hesla připojení k doméně
Pokud potřebujete změnit heslo připojení k doméně, ujistěte se, že je zadáno správné heslo, které zadáte. Pokud není, pro všechny nasazené senzorů zastaví službu senzor Azure ATP.

Pokud máte podezření, že se to stalo, na samostatné senzoru Azure ATP, prohlédněte si soubor Microsoft.Tri.sensor-Errors.log pro následující chyby: `The supplied credential is invalid.`

Podle následujícího postupu aktualizace hesla připojení k doméně na portálu Azure ATP pracovního prostoru:

> [!NOTE]
> Toto je uživatelské jméno a heslo z místního nasazení služby Active Directory a nikoli z Azure AD.

1.  Otevřete portál Azure ATP prostoru na přístupu k adresa URL pracovního prostoru.

2.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace Azure ATP](media/atp-config-menu.png)

3.  Vyberte **Adresářové služby**.

    ![Azure senzor samostatné ATP změnit heslo image](media/directory-services.png)

4.  V části **Heslo** změňte heslo.

 > [!NOTE]
 > Zadejte uživatele služby Active Directory a heslo, zde není Azure Active Directory.

5.  Klikněte na **Uložit**.

6.  Po změně hesla ručně zkontrolujte, že Azure ATP samostatné senzor služby spuštěná na serveru Azure ATP samostatné senzor.

7. Na portálu prostoru v části **konfigurace**, přejděte na **senzor** stránky a zkontrolujte stav snímače.

## <a name="see-also"></a>Viz také

- [Integrace s programem Windows Defender ATP](integrate-wd-atp.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
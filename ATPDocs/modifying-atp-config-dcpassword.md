---
title: Změna konfigurace rozšířené ochrany před internetovými útoky pro Azure – heslo připojení k doméně | Dokumentace Microsoftu
description: Popisuje, jak změnit heslo připojení k doméně na samostatný senzor ochrany ATP v programu Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a175a23a087b11d481dbcf055bff4fe5577b4f8e
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783113"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="change-azure-atp-workspace-portal-configuration---domain-connectivity-password"></a>Změna ochrany ATP v programu Azure konfigurace portálu pracovního prostoru – heslo připojení k doméně



## <a name="change-the-domain-connectivity-password"></a>Změna hesla připojení k doméně
Pokud je potřeba změnit heslo připojení k doméně, ujistěte se, že je zadáno správné heslo, které zadáte. Pokud není, zastaví službu sensor ochrany ATP v programu Azure pro všechny senzory nasazené.

Pokud máte podezření, že se to stalo, na samostatného senzoru služby Azure ATP, vyhledejte v souboru Microsoft.Tri.sensor-Errors.log následující chyby: `The supplied credential is invalid.`

Postupujte podle následujícího postupu aktualizujte heslo připojení k doméně na portálu ochrany ATP v programu Azure:

> [!NOTE]
> Toto je uživatelské jméno a heslo z místního nasazení služby Active Directory a nikoli z Azure AD.

1.  Otevřít na portálu ochrany ATP v programu Azure díky přístupu do adresy URL pracovního prostoru.

2.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace služby Azure ATP](media/atp-config-menu.png)

3.  Vyberte **Adresářové služby**.

    ![Azure ATP samostatný senzor změnit heslo image](media/directory-services.png)

4.  V části **Heslo** změňte heslo.

 > [!NOTE]
 > Zadejte uživatele služby Active Directory a heslo, nikoli Azure Active Directory.

5.  Klikněte na **Uložit**.

6.  Po změně hesla ručně zkontrolujte, že služba sensor samostatné ochrany ATP v programu Azure běží na samostatných serverech senzoru služby Azure ATP.

7. Na portálu ochrany ATP v programu Azure v rámci **konfigurace**, přejděte na stránku **senzor** stránku a zkontrolovat stav snímačům.

## <a name="see-also"></a>Viz také

- [Integrace s programem Windows Defender ATP](integrate-wd-atp.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
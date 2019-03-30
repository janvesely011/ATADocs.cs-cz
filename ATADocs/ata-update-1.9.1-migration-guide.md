---
title: Aktualizaci Advanced Threat Analytics na 1.9.1 Průvodce migrací | Dokumentace Microsoftu
description: Postup aktualizace ATA na verzi 1.9.1
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 12/10/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: c4ce44d19993f6c157885d1bd7c316b0811633b0
ms.sourcegitcommit: 62b631f64a639f5df04bf805755f26c69b40e8e4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/29/2019
ms.locfileid: "58639166"
---
# <a name="ata-version-191"></a>ATA verze 1.9.1


Tento článek popisuje opravených chybách v aktualizaci 1 pro Microsoft Advanced Threat Analytics (ATA) verze 1.9. Číslo sestavení této aktualizace je 1.9.7412.

## <a name="fixed-issues-included-in-this-update"></a>Opravené problémy, které jsou součástí této aktualizace

- Možnost selhání migrace mezi ATA verze 1.8 verze 1.9 u velkých databází.
- Pokud používáte nejnovější verzi prohlížeče Microsoft Edge a přepínání uživatelů, prohlížeče může přestat reagovat.
- V některých scénářích na stránku profilu uživatele chybí informace o datech adresáře.
- Při přidávání uživatele do seznamu vyloučení pro detekce neobvyklého chování, není vždy použita vyloučení. 
- Aktualizovaná verze databáze MongoDB.
- Nekonzistentní resynchronizace po upgradu na verze 1.9 všechny entity služby Active Directory, které ATA.
- Nekonzistentní exporty podezřelých aktivit do aplikace Microsoft Excel. Příležitostné selhání pomocí generování chyb.  


## <a name="improvements-included-in-this-update"></a>Vylepšení zahrnutá v této aktualizaci
- Změny požadované standardy usnadnění společnosti Microsoft (MAS) k certifikaci.
- Zahrnuje další opravy zabezpečení a výkonu.

## <a name="get-this-update"></a>Získat tuto aktualizaci

Jsou k dispozici na webu Microsoft Update nebo ruční stažení aktualizace pro Microsoft Advanced Threat Analytics verze 1.9.

### <a name="microsoft-update"></a>Microsoft Update
Tato aktualizace je dostupná ve službě Microsoft Update. Další informace o tom, jak používat službu Microsoft Update najdete v tématu [jak získat aktualizace pomocí služby Windows Update](https://support.microsoft.com/help/3067639).

### <a name="manual-download"></a>Ruční stažení
Pokud chcete získat samostatného balíčku pro tuto aktualizaci, najdete na webu Microsoft Download Center: [Stáhněte si balíček ATA 1.9](https://www.microsoft.com/en-us/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Požadavky
Pokud chcete nainstalovat tuto aktualizaci, musí mít ATA verze 1.9 (1.9.7312), aktualizace 1 pro ATA verze 1.8 (1.8.6765) nebo ATA verze 1.8 (1.8.6645) nainstalovaný.

### <a name="restart-requirement"></a>Požadavky na restartování
Počítač vyžaduje restartování počítače po instalaci této aktualizace.

### <a name="update-replacement-information"></a>Aktualizovat informace o nahrazení
Tato aktualizace nahrazuje ATA verze 1.9 (1.9.7312).


## <a name="see-also"></a>Viz také:

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Verze ATA](ata-versions.md)

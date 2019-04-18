---
title: Aktualizaci Advanced Threat Analytics na 1.9.2 Průvodce migrací | Dokumentace Microsoftu
description: Postup aktualizace ATA na verzi 1.9.2
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 04/02/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 65a3b7c07b421a141fd61aa1c1e93160aae6a46f
ms.sourcegitcommit: 7a32dcb65edc38fb9b3d340763045b21ea92feee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/18/2019
ms.locfileid: "59745379"
---
# <a name="ata-version-192"></a>ATA verze 1.9.2


Jsme s radostí oznamujeme dostupnost Advanced Threat Analytics 1.9 aktualizace 2 pro Microsoft.

Tento článek popisuje opravených chybách v Update 2 z Microsoft Advanced Threat Analytics (ATA) verze 1.9. Číslo sestavení této aktualizace je 1.9.7478.

## <a name="improvements-included-in-this-update"></a>Vylepšení zahrnutá v této aktualizaci

Tato aktualizace zahrnuje jako podporovaný operační systém pro System Center, brány Lightweight gateway součásti i 2019 serveru systému Windows (včetně základní verze, ale ne Nano).

Tato aktualizace zahrnuje také vylepšení výkonu a stability spolu s opravy problémů hlášených zákazníky.

## <a name="fixed-issues-included-in-this-update"></a>Opravené problémy, které jsou součástí této aktualizace

- Opravuje problém, ve kterém adresáři zobrazuje zobrazení dat s přímým přístupem správce a rekurzivní členství ve skupinách.
- Opravuje problém, ve kterém konfigurace adresy URL pro ATA Center není vždy uveden místní IP adresy nebo názvu místního počítače.
- Opravy problému se stavem stahování výstrahy po upozornění na stav obsahuje neexistující brány.
- Řeší problémy překladu.
- Opravuje problém, ve kterém nebyla aktualizována na verzi databáze MongoDB.
- Opravuje výjimečných scénář, ve kterém se problémy s velkou pamětí došlo během synchronizace služby Active Directory.
- Opravuje výjimečných scénář, ve kterém konzole pouze povolené výběru nepodporované certifikátu.
- Opravuje výjimečných scénář, ve kterém byla přijata falešně pozitivní instance zprávy "Podezření na krádež identity na základě neobvyklého chování".
- Opravuje výjimečných případů v které časová osa přechod došlo k chybě při výstrahy se automaticky aktualizují.

## <a name="get-this-update"></a>Získat tuto aktualizaci

Pokud chcete získat samostatného balíčku pro tuto aktualizaci, najdete na webu Microsoft Download Center: [Stáhnout balíček ATA 1.9.2](https://www.microsoft.com/en-us/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Požadavky

Chcete-li nainstalovat tuto aktualizaci, musí mít jednu z následujících verzí ATA nainstalovaná: 
- Aktualizace 1 pro ATA 1.9 (verze 1.9.7412)
- ATA 1.9 (verze 1.9.7312)
- Aktualizace 1 pro verzi ATA 1.8 (verze 1.8.6765)
- ATA 1.8 (verze 1.8.6645)

### <a name="restart-requirement"></a>Požadavky na restartování

Počítač vyžaduje restartování počítače po instalaci této aktualizace.

### <a name="update-replacement-information"></a>Aktualizovat informace o nahrazení

Tato aktualizace nahrazuje ATA na verzi 1.9.1 (1.9.7412).


## <a name="see-also"></a>Viz také:

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Verze ATA](ata-versions.md)
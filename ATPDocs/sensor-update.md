---
title: Aktualizace senzorů vaší ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Popisuje postup aktualizace senzorů v ochrany ATP v programu Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/06/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 603d9e09-a07d-4357-862f-d5682c8bc3dd
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8dce45be6b1e4fa383eea3993f120fa504239f34
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125715"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="update-azure-atp-sensors"></a>Aktualizace služby Azure ATP senzorů
Je nezbytné k zajištění aktuálnosti nejlepší možné ochranu pro vaši organizaci povolit rozšířené ochrany před internetovými útoky pro Azure.

Služba Ochrana ATP v programu Azure se aktualizuje několikrát za měsíc s opravy chyb a vylepšení výkonu, nové detekce. V některých těchto aktualizací vyžadují odpovídající aktualizaci ke snímačům. 

Pokud nechcete aktualizovat vaše senzory, se nebudou moct komunikovat s cloudovou službou ochrany ATP v programu Azure, což může způsobit snížení služby.

Každá aktualizace je otestovali a ověřili na všech podporovaných operačních systémech způsobí minimálním dopadem na operace a síť.

### <a name="azure-atp-sensor-update-types"></a>Azure typy aktualizací senzor ochrany ATP v programu   

Azure ATP senzorů podporuje dva typy aktualizace:
- Vedlejší verze aktualizace: 
  - Časté 
  - Vyžadovat, aby nebyla instalace MSI a žádné změny v registru
  - Azure restartování služby ochrany ATP v programu senzor
  - Řadiče domény a server není potřeba restartovat

- Hlavní verze aktualizace:
 - Výjimečných
 - Může vyžadovat restartování řadiče domény a servery
 - Obsahují významné změny 

> [!NOTE]
>- Na stránce konfigurace se dá řídit automatické restartování snímačů (v hlavní aktualizace). 
> - Senzoru služby Azure ATP vždy zachováno alespoň 15 % paměti a procesoru, které jsou k dispozici. Pokud služba spotřebovává příliš mnoho paměti se automaticky restartuje službou ochrany ATP v programu Azure senzor updater.

## <a name="delayed-sensor-update"></a>Zpožděné aktualizace senzorů
Pokud chcete povolit více postupné proces aktualizace, ochrana ATP v programu Azure vám umožní nastavit senzoru jako **zpožděné aktualizace** Release candidate. 

Obvykle senzorů automaticky aktualizovat při aktualizaci cloudové službě ochrana ATP v programu Azure. Nastavte senzorů na **zpožděné aktualizace** aktualizuje po 24 hodinách od aktualizace počáteční cloudové služby.

To vám umožňuje vybrat konkrétní senzory, na kterých nasazení aktualizace automaticky a aktualizujte zbytek vašeho senzory na zpoždění, až poté, co vidíte plynule nepovedlo počáteční aktualizace.

> [!NOTE]
> Pokud dojde k chybě a snímače se neaktualizuje, otevřete lístek podpory.

Nastavení senzoru zpožděné aktualizace:

1. Z portálu pracovního prostoru ochrana ATP v programu Azure klikněte na ikonu nastavení a vyberte **konfigurace**.
2. Klikněte na **aktualizace** kartu.
3. V řádku tabulky, vedle každého senzor, kterou chcete zpožděně, nastavte **zpožděné aktualizace** posuvníku **na**.
4. Klikněte na **Uložit**.
 
## <a name="sensor-update-process"></a>Procesu aktualizace senzorů

Každých několik minut, senzory ochrany ATP v programu Azure zkontrolujte, jestli se mají nejnovější verzi. Po aktualizaci na novější verzi cloudové službě ochrana ATP v programu Azure službu sensor ochrany ATP v programu Azure zahájí proces aktualizace:

1. Ochrana ATP v programu Azure cloud service aktualizace na nejnovější verzi.
2. Aktualizační službu senzoru služby Azure ATP zjistí, že je aktualizovaná verze.
3. Snímače, které nejsou nastaveny **zpožděné aktualizace** zahájíte proces aktualizace:
  1. Aktualizační služba sensor ochrany ATP v programu Azure získává aktualizovanou verzi z cloudové služby (ve formátu souboru cab).
  2. Aktualizátor senzoru služby Azure ATP ověří podpis souboru.
  3. Aktualizační službu senzoru služby Azure ATP extrahovat soubor cab do nové složky ve složce instalace senzoru. Ve výchozím nastavení budou extrahovány do *C:\Program Files\Azure Advanced Threat ochrany senzor\<číslo verze >*
  4. Aktualizační službu senzoru služby Azure ATP restartuje službu sensor ochrany ATP v programu Azure.
  5. Službu sensor ochrany ATP v programu Azure odkazuje na nové soubory extrahovány ze souboru cab.
  > [!NOTE]
  >Dílčí aktualizace čidel nelze nainstalovat Instalační služba MSI nebo změnit hodnoty registru nebo soubory systému. Čeká na restartování nebudou mít vliv na aktualizace snímačům. 
  6. Snímačům spouštět na základě nově aktualizovaná verze.
  7. Snímač přijímá odbavení z cloudové služby Azure. Můžete to ověřit v **aktualizace** stránky.
  8. Další senzor zahájí proces aktualizace. 

4. Po 24 hodinách od služby Azure ATP cloudovou službu aktualizovat, senzory vybraných pro ** aktualizace zpoždění spuštění procesu aktualizace.

![aktualizace ze senzorů](./media/sensor-update.png)


V případě selhání Pokud senzor nedokončil proces aktualizace relevantní monitorovací upozornění se aktivuje a odesílají je jako upozornění.

![senzor zastaralé](./media/sensor-outdated.png)


## <a name="see-also"></a>Viz také

- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
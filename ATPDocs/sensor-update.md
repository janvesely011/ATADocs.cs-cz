---
title: Aktualizace senzorů vaší ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Popisuje, jak aktualizovat a zpoždění aktualizace senzorů v ochrany ATP v programu Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 603d9e09-a07d-4357-862f-d5682c8bc3dd
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 78ffb0df8e0750a41d262a984fc0915522cf9ddb
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58675257"
---
# <a name="update-azure-atp-sensors"></a>Aktualizace služby Azure ATP senzorů

Průběžná senzorů vaší rozšířené ochrany před internetovými útoky pro Azure poskytuje nejlepší možnou ochranu pro vaši organizaci.

Služba Ochrana ATP v programu Azure se obvykle aktualizuje několikrát za měsíc s nové detekce, funkce a vylepšení výkonu. Obvykle tyto aktualizace zahrnují odpovídající dílčí aktualizace ke snímačům. Azure ATP senzory a odpovídající aktualizace nikdy mají oprávnění k zápisu do řadiče domény. Balíčky aktualizací senzor řídit jenom senzoru služby Azure ATP a možnosti detekce senzor. 

### <a name="azure-atp-sensor-update-types"></a>Azure typy aktualizací senzor ochrany ATP v programu   

Azure ATP senzorů podporují dva typy aktualizace:
- Vedlejší verze aktualizace: 
    - Časté 
    - Vyžaduje, aby nebyla instalace MSI a žádné změny v registru
    - Restartování: Senzor služby Azure ATP 
    - Nelze restartovat: Služby řadiče domény a serverový operační systém

- Hlavní verze aktualizace:
    - Výjimečných
    - Obsahuje významné změny 
    - Restartování: Senzor služby Azure ATP
    - Je to možné je vyžadováno restartování: Služby řadiče domény a serverový operační systém

> [!NOTE]
>- Řízení senzor automatické restartování (pro **hlavní** aktualizace) na stránce Konfigurace portálu ochrany ATP v programu Azure. 
> - Azure ATP senzor rezervuje vždy alespoň 15 % dostupné paměti a procesoru, které jsou k dispozici na řadiči domény, kde je nainstalovaný. Pokud službě ochrana ATP v programu Azure spotřebovává příliš mnoho paměti, služba automaticky zastavit a restartovat službu updater senzoru služby Azure ATP.

### <a name="update-requirement"></a>Požadavek na aktualizaci

Selhání její aktualizace vašeho senzory pro funkce více než jednu aktualizaci verze znamená, že vaše senzorů už nemůže komunikovat s cloudovou službou ochrany ATP v programu Azure a může způsobit nedostupnost služby bez ochrany ATP v programu Azure a žádná ochrana pro vaši organizaci.  

## <a name="delayed-sensor-update"></a>Zpožděné aktualizace senzorů

Zadaný rychlé rychlost probíhající aktualizace služby Azure ATP vývoje a vydávání verzí, můžete rozhodnout definujte skupinu dílčí vaše snímačů jako zpožděné aktualizačního procesu aktualizace postupné senzor. Ochrana ATP v programu Azure vám umožní vybrat jak aktualizace a nastavit každý ze senzorů jako vaše senzory **zpožděné aktualizace** Release candidate.  

Není vybrána pro zpožděné aktualizace senzorů se automaticky aktualizují, pokaždé, když se aktualizuje službě ochrana ATP v programu Azure. Senzorů nastavena na **zpoždění aktualizace** se aktualizují na zpoždění 72 hodin, po oficiálním vydání každou aktualizaci služby. 

**Zpožděné aktualizace** možnost vám umožňuje vybrat konkrétní senzorů jako automatické aktualizační kanál, na kterém všechny se aktualizace zavedou automaticky a zbytek vašeho snímačů a aktualizovat na zpoždění, získáte tak čas Ujistěte se, že sada automaticky aktualizované senzorů proběhly úspěšně.

> [!NOTE]
> Pokud dojde k chybě a snímače se neaktualizuje, otevřete lístek podpory. Váš proxy server pouze komunikovat s vaší instancí dál posiluje, najdete v článku [konfiguraci proxy serveru](configure-proxy.md).
Ověřování mezi vaší senzory a cloudové služby Azure využívá silné a na základě certifikátů vzájemného ověřování. 

Každá aktualizace je otestovali a ověřili na všech podporovaných operačních systémech způsobí minimálním dopadem na operace a síť.


Nastavení senzoru zpožděné aktualizace:

1. Z ochrany ATP v programu Azure portal, klikněte na ikonu nastavení a vyberte **konfigurace**.
2. Klikněte na **aktualizace** kartu.
3. V řádku tabulky, vedle každého senzor, kterou chcete zpožděně, nastavte **zpožděné aktualizace** posuvníku **na**.
4. Klikněte na **Uložit**.
 
## <a name="sensor-update-process"></a>Procesu aktualizace senzorů

Každých několik minut, senzory ochrany ATP v programu Azure zkontrolujte, jestli se mají nejnovější verzi. Po aktualizaci na novější verzi cloudové službě ochrana ATP v programu Azure službu sensor ochrany ATP v programu Azure zahájí proces aktualizace:

1. Ochrana ATP v programu cloud service aktualizace Azure na nejnovější verzi.
2. Azure ATP senzor aktualizační službu zjistí, že je aktualizovaná verze.
3. Snímače, které nejsou nastaveny **zpožděné aktualizace** zahájíte proces aktualizace na základě ze senzorů pomocí senzoru:
   1. Azure ATP senzor aktualizační službu stáhne aktualizované verze z cloudové služby (ve formátu souboru cab).
   2. Azure updater senzor ochrany ATP v programu ověří podpis souboru.
   3. Azure ATP senzor aktualizační službu extrahuje soubor cab do nové složky ve složce instalace senzoru. Ve výchozím nastavení je extrahován do *C:\Program Files\Azure Advanced Threat ochrany senzor\<číslo verze >*
   4. Službu sensor Azure ATP odkazuje na nové soubory extrahovány ze souboru cab.    
   5. Azure ATP senzor aktualizační službu restartuje službu sensor ochrany ATP v programu Azure.
       > [!NOTE]
      >Aktualizace podverze senzor nainstalovat žádné instalační služby MSI, změní žádné hodnoty registru nebo soubory systému. Čeká na restartování nemá žádný vliv na aktualizace ze senzorů. 
   6. Senzorů spouštět na základě nově aktualizovaná verze.
   7. Senzor přijímá odbavení z cloudové služby Azure. Stav ze senzorů v si můžete ověřit **aktualizace** stránky.
   8. Další senzor zahájí proces aktualizace. 

4. 72 hodin, po aktualizaci cloudové službě ochrana ATP v programu Azure senzorů vybraná **zpoždění aktualizace** spusťte proces jejich aktualizace podle stejného procesu aktualizace jako automaticky aktualizované senzory.

![aktualizace ze senzorů](./media/sensor-update.png)


K žádnému senzoru, kterému se nedaří dokončit proces aktualizace relevantní monitorovací upozornění se aktivuje a se odešle jako oznámení.

![Neúspěšná aktualizace senzorů](./media/sensor-outdated.png)


## <a name="see-also"></a>Viz také

- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

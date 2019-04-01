---
title: Azure Advanced překlad názvů sítě ochrany před internetovými útoky | Dokumentace Microsoftu
description: Tento článek obsahuje přehled služby Azure ATP překlad síťových názvů pokročilé funkce a používá.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ac873fc-b763-41d7-878e-7c08da421cb5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c484d1e2c184358531d4f4a746f49760f47ea4dd
ms.sourcegitcommit: a0d1ae7e221fd8bbaf81bf8ae4833ae77fb80ae8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2019
ms.locfileid: "58752230"
---
# <a name="what-is-network-name-resolution"></a>Co je překlad síťových názvů?

Překlad síťových názvů nebo (NNR) je hlavní součástí služby Azure ATP funkce. Ochrana ATP v programu Azure zaznamenává aktivity na základě síťového provozu, Windows, událostí a trasování událostí pro Windows – tyto aktivity obvykle obsahují data IP adresy.  

Použití ÚTOKŮ, ochrana ATP v programu Azure je možnost provést korelaci mezi nezpracovaná aktivity (který obsahuje IP adresy) a relevantní počítačů zahrnutých v každé aktivity. Založené na aktivitách nezpracovaná, ochrana ATP v programu Azure profily entit, včetně počítačů a generuje upozornění zabezpečení na podezřelé aktivity.

NNR dat je zásadní pro detekci hrozeb následující:

- Krádež identity podezřelého softwaru (pass-the-ticket)
- Podezřelý útok DCSync (replikace adresářových služeb)
- Mapování sondování sítě (DNS)
- Podezření na útok přenosového protokolu NTLM (účet Exchange)

K překladu IP adres na názvy počítačů, senzory ochrany ATP v programu dotazu IP adresu pro název počítače "za" IP adresu, pomocí jedné z následujících metod:

1. NTLM přes RPC (port TCP 135)
2. NetBIOS (port UDP 137)
3. Protokol RDP (portu TCP 3389) – jenom první paket **Client hello**
4. Zadat dotaz na server DNS pomocí zpětného vyhledávání DNS IP adresy (UDP 53)

> [!NOTE]
>Na všech portech neprobíhá žádné ověřování.

Po načtení názvu počítače, senzoru služby Azure ATP ověří ve službě Active Directory a zjistěte, jestli je objekt korelační počítače se stejným názvem počítače. Pokud senzor najde korelace, související senzor tato IP adresa na tento objekt počítače.

### <a name="prerequisites"></a>Požadavky
|Protocol (Protokol)|  Přenos|  Port|   Zařízení| Direction|
|--------|--------|------|-------|------|
|NTLM přes RPC| TCP |135|   Všechna zařízení v síti| Příchozí|
|NetBIOS|   UDP|    137|    Všechna zařízení v síti| Příchozí|
|DNS|   UDP|    53| Řadiče domény| Odchozí|
|

Když se otevře port 3389 na zařízení ve vašem prostředí, senzoru služby Azure ATP pomocí pro účely řešení název sítě.
Otevření portu 3389 **není povinné**, je jenom další metodu, která můžete zadat název počítače, pokud port je již otevřen pro jiné účely.

Ujistěte se, že služby Azure ATP v ideálním případě funguje a je prostředí správně nakonfigurováno, ochrany ATP v programu Azure kontroluje stav řešení každý ze souboru a vydává monitorovací upozornění pro jednu metodu, proto poskytuje seznam senzorů ochrany ATP v programu Azure s nízkou úspěšnost aktivní názvu rozlišení použití každé metody.

Každé monitorování výstraha poskytuje konkrétní podrobnosti metody, senzory, problematické zásady stejně jako doporučené konfigurace.

![Upozornění na nízkou úspěšnost sítě název řešení ÚTOKŮ](media/atp-health-alert-audit-policy.png)


### <a name="configuration-recommendations"></a>Doporučené konfigurace

- RPC přes protokol NTLM:
    - Zkontrolujte, že je Port 135 otevřené pro příchozí komunikace ze senzorů ochrany ATP v programu Azure, na všech počítačích v prostředí.
    - Zkontrolujte, že všechny sítě (Brána firewall), protože to může zabránit komunikaci na příslušné porty.

- NetBIOS:
    - Zkontrolujte, že je Port 137 otevřené pro příchozí komunikace ze senzorů ochrany ATP v programu Azure, na všech počítačích v prostředí.
    - Zkontrolujte, že všechny sítě (Brána firewall), protože to může zabránit komunikaci na příslušné porty.
- Reverzní DNS:
    - Zkontrolujte, že senzor můžete připojit k serveru DNS a že jsou povolené zóny zpětného vyhledávání.


## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)

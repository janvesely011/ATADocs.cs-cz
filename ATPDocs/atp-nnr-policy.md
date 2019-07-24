---
title: Překlad názvu sítě rozšířené ochrany před internetovými útoky pro Azure | Microsoft Docs
description: Tento článek obsahuje přehled pokročilé funkce překladu síťových názvů v Azure ATP a používá nástroj.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ac873fc-b763-41d7-878e-7c08da421cb5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0161c0f63e652bd62ee8ccf4a6677f2ec0d90f4d
ms.sourcegitcommit: b7b3d4a401faaa3edb4bd669a1a003a6d21a4322
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2019
ms.locfileid: "68298948"
---
# <a name="what-is-network-name-resolution"></a>Co je překlad síťových názvů?

Překlad názvu sítě nebo (útoků) je hlavní součástí funkcí Azure ATP. Azure ATP zachycuje aktivity na základě síťového provozu, událostí Windows a ETW – tyto aktivity obvykle obsahují data IP.  

Pomocí útoků může Azure ATP korelovat mezi nezpracovanými aktivitami (obsahujícími IP adresami) a souvisejícími počítači, které se podílejí na jednotlivých činnostech. Na základě nezpracovaných aktivit, entit profilů ATP Azure, včetně počítačů, a vygeneruje výstrahy zabezpečení pro podezřelé aktivity.

K překladu IP adres na názvy počítačů se senzory Azure ATP dotazují IP adresu názvu počítače za "za" IP adresy, a to pomocí jedné z následujících metod:

1. NTLM přes RPC (port TCP 135)
2. NetBIOS (port UDP 137)
3. RDP (TCP port 3389) – pouze první paket **klienta Hello**
4. Zadá dotaz na server DNS pomocí zpětného vyhledávání DNS IP adresy (UDP 53).

> [!NOTE]
>Na žádném z portů se neprovede žádné ověřování.

Azure ATP vyhodnocuje a určuje operační systém zařízení na základě síťového provozu. Po načtení názvu počítače zkontroluje senzor Azure ATP službu Active Directory a použije otisky prstů TCP, aby bylo možné zjistit, zda existuje korelační objekt počítače se stejným názvem počítače. Použití otisků prstů TCP pomáhá identifikovat neregistrovaná zařízení a jiná zařízení než Windows a přispěje v procesu šetření. Když senzor ATP Azure najde korelaci, připojí se k objektu počítače IP. 

V případech, kdy se žádný název nenačte, vytvoří se **nerozpoznaný profil počítače podle IP** adresy a příslušné zjištěné aktivity.

![Nerozpoznaný profil počítače](media/unresolved-computer-profile.png)


ÚTOKŮ data jsou zásadní pro detekci následujících hrozeb:

- Krádež identity podezřelého softwaru (pass-the-ticket)
- Podezřelý útok DCSync (replikace adresářových služeb)
- Mapování sítě rekognoskace (DNS)

Aby bylo možné zjistit, zda je výstraha falešně **pozitivní (transakční)** nebo **falešně pozitivní (FP)** , Azure ATP zahrnuje stupeň jistoty při překladu názvů počítačů do legitimace jednotlivých výstrah zabezpečení. 
 
Například když jsou názvy počítačů vyřešeny s **vysokou jistotou** , zvyšuje se spolehlivost výsledné výstrahy zabezpečení jako **skutečný pozitivní** nebo **transakční**program. 

Legitimace obsahuje čas, IP adresu a název počítače, na které byla IP adresa přeložena. Pokud je jistota řešení **Nízká**, pomocí těchto informací Prozkoumejte a ověřte, které zařízení bylo v tuto chvíli skutečným zdrojem IP adresy. Po potvrzení zařízení můžete zjistit, zda je výstraha **falešně pozitivní** nebo **FP**, podobně jako v následujících příkladech:

- Podezření na krádež identity (pass-the-Ticket) – výstraha se aktivovala pro stejný počítač.
- Podezřelý útok DCSync (replikace adresářových služeb) – výstraha se aktivovala z řadiče domény.
- Mapování sítě rekognoskace (DNS) – výstraha se aktivovala ze serveru DNS.

    ![Jistota legitimace](media/nnr-high-certainty.png)


### <a name="prerequisites"></a>Požadavky
|Protocol|  Přenos|  Port|   Zařízení| Direction|
|--------|--------|------|-------|------|
|NTLM přes RPC| TCP |135|   Všechna zařízení v síti| Příchozí|
|NetBIOS|   UDP|    137|    Všechna zařízení v síti| Příchozí|
|DNS|   UDP|    53| Řadiče domény| Odchozí|
|

Když je na zařízeních v prostředí otevřený port 3389, senzor služby Azure ATP, který ho používá pro účely překladu síťových názvů.
Otevření portu 3389 není požadavkem, jedná se pouze o další metodu, která může zadat název počítače, pokud je již port otevřen pro jiné účely.

Abyste se ujistili, že služba Azure ATP je v ideálním prostředí a že je prostředí správně nakonfigurované, Azure ATP kontroluje stav řešení každého senzoru a vydává výstrahu monitorování na jednotlivé metody. poskytuje seznam senzorů ATP Azure s nízkou mírou úspěšnosti aktivního názvu. rozlišení pomocí jednotlivých metod.

Každá výstraha monitorování poskytuje konkrétní podrobnosti o metodě, senzorech, problematických zásadách a také doporučeních pro konfiguraci.

![Výstraha pro rozlišení síťového názvu sítě (útoků) s nízkou mírou úspěšnosti](media/atp-nnr-success-rate.png)


### <a name="configuration-recommendations"></a>Doporučení pro konfiguraci

- RPC over NTLM:
    - Ověřte, že je port TCP 135 otevřený pro příchozí komunikaci ze senzorů Azure ATP na všech počítačích v prostředí.
    - Ověřte všechny konfigurace sítě (brány firewall), protože to může zabránit komunikaci s příslušnými porty.

- Názv
    - Ověřte, že je na všech počítačích v prostředí otevřený port UDP 137 pro příchozí komunikaci ze senzorů Azure ATP.
    - Ověřte všechny konfigurace sítě (brány firewall), protože to může zabránit komunikaci s příslušnými porty.
- Reverzní DNS:
    - Ověřte, že senzor má přístup k serveru DNS a že jsou povolené zóny zpětného vyhledávání.


## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)

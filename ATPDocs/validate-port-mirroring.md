---
title: Ověření zrcadlení portů v rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje, jak ověřit, že je zrcadlení portů nakonfigurované správně v Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 10/04/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 0a56cf27-9eaa-4ad0-ae6c-9d0484c69094
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d3eb36b75e9500920bdaea70864839a5de7e3de1
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196420"
---
# <a name="validate-port-mirroring"></a>Ověření zrcadlení portů
> [!NOTE] 
> Tento článek je relevantní pouze pokud nasazujete nasadit samostatný senzor ochrany ATP v programu Azure místo senzor ochrany ATP v programu Azure. Pokud chcete zjistit, pokud budete muset použít snímač ochrany ATP v programu Azure, najdete v článku [výběr správné senzor pro vaše nasazení](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment).
 
Následující kroky vás provedou procesem ověření, že je zrcadlení portů správně nakonfigurované. Pro služby Azure ATP fungovalo správně musí mít možnost sledovat provoz do a z řadiče domény samostatného senzoru služby Azure ATP. Hlavní zdroj dat používají ochrany ATP v programu Azure je hloubková kontrola paketů síťového provozu do a z řadičů domény. Pro služby Azure ATP zobrazíte síťový provoz zrcadlení portů je potřeba nakonfigurovat. Zrcadlení portů kopíruje provoz z jednoho portu (zdrojový port) na jiný port (cílový port).

## <a name="validate-port-mirroring-using-net-mon"></a>Ověření zrcadlení portů pomocí Net Mon
1.  Nainstalujte [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) na samostatný senzor ochrany ATP v programu, který chcete ověřit.

    > [!IMPORTANT]
    > Pokud se rozhodnete nainstalovat Wireshark, aby ověření zrcadlení portů, restartujte službu ochrany ATP v programu Azure samostatný senzor po ověření.

2.  Otevřete Sledování sítě a vytvořte novou kartu zachycení.

    1.  Vyberte pouze síťový adaptér pro **zachytávání** nebo síťový adaptér připojený k portu přepínače, který je nakonfigurovaný jako cíl zrcadlení portů.

    2.  Ověřte, že je povolený režim P.

    3.  Klikněte na tlačítko **Nové zachytávání**.

        ![Obrázek karty Vytvořit nové zachytávání](media/atp-port-mirroring-capture.png)

3.  V okně filtru zobrazení zadejte filtr: **KerberosV5 nebo LDAP** a potom klikněte na tlačítko **použít**.

    ![Obrázek použití filtru KerberosV5 nebo LDAP](media/atp-port-mirroring-filter-settings.png)

4.  Kliknutím na **Spustit** spusťte relaci zachytávání. Pokud nevidíte provoz do a z řadiče domény, zkontrolujte konfiguraci zrcadlení portů.

    ![Obrázek spuštění relace zachytávání](media/atp-port-mirroring-capture-traffic.png)

    > [!NOTE]
    > Je důležité se ujistit, že vidíte provoz do a z řadičů domény.
    

5.  Pokud se zobrazí pouze provoz v jednom směru, pracujete s vaší sítí nebo virtualizace týmům vyřešit potíže s konfigurací zrcadlení portů.

## <a name="see-also"></a>Viz také

- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Konfigurace zrcadlení portů](configure-port-mirroring.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

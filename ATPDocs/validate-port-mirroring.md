---
title: Ověření zrcadlení portů v rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje, jak ověřit, že je zrcadlení portů nakonfigurované správně v Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: conceptual
ms.service: ''
ms.technology: ''
ms.assetid: 0a56cf27-9eaa-4ad0-ae6c-9d0484c69094
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 15e53ef145b9d7bbbc980730acec6c3b92c1a0fa
ms.sourcegitcommit: e0b9252c770b3a3695af1642b76e3304f3df15d4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2018
ms.locfileid: "46566600"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



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

3.  V okně filtru zobrazení zadejte filtr **KerberosV5 nebo LDAP** a potom klikněte na **Použít**.

    ![Obrázek použití filtru KerberosV5 nebo LDAP](media/atp-port-mirroring-filter-settings.png)

4.  Kliknutím na **Spustit** spusťte relaci zachytávání. Pokud nevidíte provoz do a z řadiče domény, zkontrolujte konfiguraci zrcadlení portů.

    ![Obrázek spuštění relace zachytávání](media/atp-port-mirroring-capture-traffic.png)

    > [!NOTE]
    > Je důležité se ujistit, že vidíte provoz do a z řadičů domény.
    

5.  Pokud se zobrazí pouze provoz v jednom směru, pracujete s vaší sítí nebo virtualizace týmům vyřešit potíže s konfigurací zrcadlení portů.

## <a name="see-also"></a>Viz také

- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Konfigurace zrcadlení portů](configure-port-mirroring.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)

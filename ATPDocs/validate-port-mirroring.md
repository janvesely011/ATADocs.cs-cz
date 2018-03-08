---
title: "Ověření zrcadlení portů v Azure Advanced Threat Protection | Microsoft Docs"
description: "Popisuje, jak ověřit, že je zrcadlení portů nakonfigurované správně v Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/3/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 0a56cf27-9eaa-4ad0-ae6c-9d0484c69094
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7628fa491ddbe477cab7eb414409028c0f94f44d
ms.sourcegitcommit: 84556e94a3efdf20ca1ebf89a481550d7f8f0f69
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/08/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="validate-port-mirroring"></a>Ověření zrcadlení portů
> [!NOTE] 
> Tento článek se týká pouze pokud nasazujete nasadit Azure ATP samostatné senzor místo senzor ATP Azure. Pokud chcete zjistit, pokud budete muset použít snímač ATP Azure, najdete v části [výběr správné senzoru pro vaše nasazení](atp-capacity-planning#choosing-the-right-sensor-type-for-your-deployment).
 
Následující kroky vás provedou procesem ověření, že je zrcadlení portů správně nakonfigurované. Pro Azure ATP fungovalo správně musí být samostatné senzoru Azure ATP moci zobrazit provoz do a z řadiče domény. Hlavní zdroj dat používá Azure ATP je hloubková kontrola paketů síťového provozu do a z řadičů domény. Pro Azure ATP sledovat síťový provoz zrcadlení portů je potřeba nakonfigurovat. Zrcadlení portů kopíruje provoz z jednoho portu (zdrojový port) na jiný port (cílový port).

## <a name="validate-port-mirroring-using-net-mon"></a>Ověření zrcadlení portů pomocí Net Mon
1.  Nainstalujte [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) na samostatné senzor ATP, který chcete ověřit.

    > [!IMPORTANT]
    > Pokud si zvolíte-li ověření zrcadlení portů, nainstalujte Wireshark, restartujte službu Azure ATP samostatné senzor po ověření.

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
    

5.  Pokud se zobrazí jenom přenosy v jednom směru, pracujete s týmům sítě nebo virtualizace pomoct řešit problémy s konfigurací zrcadlení portů.

## <a name="see-also"></a>Viz také

- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Konfigurace zrcadlení portů](configure-port-mirroring.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)

---
title: Nastavení e-mailových oznámení v rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje, jak máte služby Azure ATP upozornění (e-mailem nebo předáváním událostí služby Azure ATP) při zjištění podezřelých aktivit
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 399773b174f52cfc26888fcaa9923de4f258e897
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166880"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="integrate-with-syslog"></a>Integrace se Syslogem

Ochrana ATP v programu Azure může upozornit, pokud detekuje podezřelé aktivity a upozornění na stav zasláním oznámení na váš server Syslog. Pokud povolíte upozornění pro Syslog, můžete pro ně nastavit následující parametry.

1.  Před konfigurací upozornění pro Syslog zjistěte ve spolupráci s vaším správcem systému SIEM následující informace:

    -   Plně kvalifikovaný název domény nebo IP adresa serveru SIEM

    -   Port, na kterém naslouchá server SIEM

    -   Používaného přenosu: UDP, TCP nebo TLS (Syslog se zabezpečením)

    -   Formát odesílání dat: RFC 3164 nebo 5424

2.  Zadejte pracovní prostor portál adresy URL.

3.  Zadejte svoje služby Azure Active Directory uživatelské jméno a heslo a klikněte na tlačítko **přihlášení**.

4.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace služby Azure ATP](media/ATP-config-menu.png)

5.  Klikněte na tlačítko **oznámení**a pak v části **oznámení Syslogu** klikněte na tlačítko **konfigurovat** a zadejte následující informace:

    |Pole|Popis|
    |---------|---------------|
    |Senzor|Vyberte určené senzoru odpovědný za agregaci všechny události protokolu Syslog a předává je na váš server SIEM.|
    |Koncový bod služby|Plně kvalifikovaný název domény serveru Syslog a volitelně změňte číslo portu (výchozí hodnota 514)|
    |Přenos|Může být UDP, TCP nebo TLS (Syslog se zabezpečením)|
    |Formát|To je formát, který ochrany ATP v programu Azure používá k odesílání událostí na server SIEM – RFC 5424, nebo RFC 3164.|

 ![Obrázek nastavení serveru Azure ochrany ATP v programu Syslog](media/atp-syslog.png)

6. Můžete vybrat, které události odesílat na váš server Syslog. V části **oznámení Syslogu**, určete oznámení, která se mají odesílat na váš server Syslog – nové výstrahy zabezpečení, výstrah zabezpečení se aktualizovalo a nové problémy v oblasti stavu.


## <a name="see-also"></a>Viz také

- [Práce s citlivými účty](sensitive-accounts.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
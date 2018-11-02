---
title: Nastavení e-mailových oznámení v rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje, jak máte služby Azure ATP upozornění (e-mailem nebo předáváním událostí služby Azure ATP) při zjištění podezřelých aktivit
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 30ce04565611852d289883935004b5f90cb36c90
ms.sourcegitcommit: 034d5cbd077a0dd18638d27aabbcf7b735993b08
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/01/2018
ms.locfileid: "50748914"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="integrate-with-syslog"></a>Integrace se Syslogem

Ochrana ATP v programu Azure může upozornit při zjištění podezřelých aktivit a výstrahy zabezpečení problémy, stejně jako upozornění na stav zasláním oznámení na váš server Syslog. Pokud povolíte upozornění pro Syslog, můžete nastavit následující:

1.  Před konfigurací upozornění pro Syslog zjistěte ve spolupráci s vaším správcem systému SIEM následující informace:

    -   Plně kvalifikovaný název domény nebo IP adresa serveru SIEM

    -   Port, na kterém naslouchá server SIEM

    -   Používaného přenosu: UDP, TCP nebo TLS (Syslog se zabezpečením)

    -   Formát odesílání dat: RFC 3164 nebo 5424

2.  Zadejte adresu URL pracovního prostoru.

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

> [!NOTE]
> Pokud budete chtít vytvořit automatizace nebo skriptů pro protokolů SIEM ochrany ATP v programu Azure, doporučujeme použít **externalId** pole k identifikaci typu výstrahy místo názvu upozornění pro tento účel. Upozornění názvy mohou být občas upravit, zatímco **externalId** jednotlivých výstrah je trvalá. Další informace najdete v tématu [referenční informace k protokolům SIEM ochrany ATP v programu Azure](cef-format-sa.md). 


## <a name="see-also"></a>Viz také

- [Práce s citlivými účty](sensitive-accounts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
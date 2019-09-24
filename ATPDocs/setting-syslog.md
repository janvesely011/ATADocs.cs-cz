---
title: Nastavení nastavení syslog v Rozšířené ochraně před internetovými útoky Azure | Microsoft Docs
description: Popisuje, jak vám Azure ATP upozorní (e-mailem nebo předáváním událostí v Azure ATP), když detekuje podezřelé aktivity.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ab96c0a17344d93c00f25ca5ca97a1fb2c0a22b7
ms.sourcegitcommit: 15f882cf45776877fdaca8367a7a0fe7f06a7917
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/23/2019
ms.locfileid: "71185733"
---
# <a name="integrate-with-syslog"></a>Integrace se Syslogem

> [!NOTE]
> Funkce ATP Azure, které jsou na této stránce popsané, jsou dostupné taky pomocí nového [portálu](https://portal.cloudappsecurity.com).

Azure ATP vás může informovat, když detekuje podezřelé aktivity a vystavuje výstrahy zabezpečení a upozornění na stav odesláním oznámení na váš server syslog. Výstrahy se odesílají z snímače ATP Azure, který zjistil aktivitu přímo na serveru syslog. 


Po povolení oznámení syslog můžete nastavit následující:

   |Pole|Popis|
   |---------|---------------|
   |Elektrické|Vyberte určený senzor, který bude zodpovědný za agregaci všech událostí syslog a jejich předání na server SIEM.|
   |Koncový bod služby|Plně kvalifikovaný název domény serveru Syslog a volitelně změňte číslo portu (výchozí hodnota 514)|
   |Přenos|Může být UDP, TCP nebo TLS (zabezpečený syslog)|
   |Formát|Jedná se o formát, který Azure ATP používá k posílání událostí na server SIEM – RFC 5424 nebo RFC 3164.|

1. Před konfigurací upozornění pro Syslog zjistěte ve spolupráci s vaším správcem systému SIEM následující informace:

   -   Plně kvalifikovaný název domény nebo IP adresa serveru SIEM

   -   Port, na kterém naslouchá server SIEM

   -   Jaký přenos se má použít: UDP, TCP nebo TLS (zabezpečený syslog)

   -   Formát odesílání dat: RFC 3164 nebo 5424

1. Otevřete portál Azure ATP. 
2. Klikněte na **Nastavení**.
3. V dílčí nabídce **oznámení a sestavy** vyberte **oznámení**. 
1. V možnosti **Služba Syslog** klikněte na **Konfigurovat**.
1. Vyberte **senzor**. 
1. Zadejte adresu URL **koncového bodu služby** .
1. Vyberte **Transportní** protokol (TCP nebo UDP). 
1. Vyberte formát (RFC 3164 nebo RFC 5424). 
1. Vyberte **Odeslat text zprávy syslog** a pak ověřte, že se zpráva obdrží v řešení infrastruktury syslog. 
1. Klikněte na **Uložit**. 

Chcete-li zkontrolovat nebo změnit nastavení syslogu.  

3. Klikněte na **oznámení**a potom v části **oznámení syslog** klikněte na **Konfigurovat** a zadejte následující informace:

   ![Obrázek nastavení serveru syslog pro Azure ATP](media/atp-syslog.png)

4. Můžete vybrat, které události se mají odeslat na váš server syslog. V části **oznámení syslogu**určete, která oznámení se mají odeslat na váš server syslog – nové výstrahy zabezpečení, aktualizované výstrahy zabezpečení a nové problémy se stavem.

> [!NOTE]
> Pokud budete chtít vytvořit automatizace nebo skriptů pro protokolů SIEM ochrany ATP v programu Azure, doporučujeme použít **externalId** pole k identifikaci typu výstrahy místo názvu upozornění pro tento účel. Upozornění názvy mohou být občas upravit, zatímco **externalId** jednotlivých výstrah je trvalá. Další informace najdete v tématu [Přehled protokolu Azure ATP Siem](cef-format-sa.md). 


## <a name="see-also"></a>Viz také

- [Práce s citlivými účty](sensitive-accounts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

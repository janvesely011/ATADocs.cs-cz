---
title: "Nastavení e-mailových oznámení v Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Popisuje, jak vám má ATA doručovat upozornění (e-mailem nebo předáváním událostí ATA) při zjištění podezřelých aktivit."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 70e076dea5b1ff200b1b9f2a6529a76c175c7a88
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="provide-ata-with-your-email-server-settings"></a>Nastavení e-mailového serveru pro ATA
ATA vás může upozornit, když zjistí podezřelou aktivitu. Aby řešení ATA mohlo odesílat e-mailová oznámení, musíte nejdřív nakonfigurovat **nastavení e-mailového serveru**.

1.  Na serveru ATA Center klikněte na ikonu **Správa Microsoft Advanced Threat Analytics** na ploše.

2.  Zadejte uživatelské jméno a heslo a klikněte na **Přihlásit**.

3.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.png)

4.  V části **Oznámení** pod položkou **Poštovní server** vyplňte následující pole:

    |Pole|Popis|Hodnota|
    |---------|---------------|---------|
    |Koncový bod serveru SMTP (povinné)|Zadejte plně kvalifikovaný název domény serveru SMTP a volitelně změňte číslo portu (výchozí hodnota 25).|Například:<br />smtp.contoso.com|
    |SSL|Přepněte SSL, pokud SMTP server vyžaduje protokol SSL. **Poznámka:** Pokud povolíte protokol SSL, musíte taky změňte číslo portu.|Ve výchozím nastavení je zakázáno.|
    |Ověřování|Povolte, pokud váš server SMTP vyžaduje ověření. **Poznámka:** Pokud povolíte ověřování, je nutné zadat uživatelské jméno a heslo e-mailový účet, který má oprávnění pro připojení k serveru SMTP.|Ve výchozím nastavení je zakázáno.|
    |Odesilatel (povinné)|Zadejte e-mailovou adresu odesilatele e-mailu.|Například:<br />ATA@contoso.com|
    ![Obrázek nastavení e-mailového serveru ATA](media/ata-email-server.png)

## <a name="provide-ata-with-your-syslog-server-settings"></a>Nastavení serveru Syslog pro ATA
Když ATA zjistí podezřelou aktivitu, může vás upozornit tak, že zašle upozornění na váš server Syslog. Pokud povolíte upozornění pro Syslog, můžete pro ně nastavit následující parametry.

1.  Před konfigurací upozornění pro Syslog zjistěte ve spolupráci s vaším správcem systému SIEM následující informace:

    -   Plně kvalifikovaný název domény nebo IP adresa serveru SIEM

    -   Port, na kterém naslouchá server SIEM

    -   Typ používaného přenosu: UDP, TCP nebo TLS (Syslog se zabezpečením)

    -   Formát odesílání dat: RFC 3164 nebo 5424

2.  Na serveru ATA Center klikněte na ikonu **Správa Microsoft Advanced Threat Analytics** na ploše.

3.  Zadejte uživatelské jméno a heslo a klikněte na **Přihlásit**.

4.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.png)

5.  V části Oznámení vyberte **Server Syslog** a zadejte následující informace:

    |Pole|Popis|
    |---------|---------------|
    |Koncový bod serveru Syslog|Plně kvalifikovaný název domény serveru Syslog a volitelně změňte číslo portu (výchozí hodnota 514)|
    |Přenos|Může být UDP, TCP nebo TLS (Syslog se zabezpečením)|
    |Formát|To je formát, který ATA používá k odesílání událostí na server SIEM – RFC 5424, nebo RFC 3164.|

 ![Obrázek nastavení serveru ATA Syslog](media/ata-syslog-server-settings.png)



## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

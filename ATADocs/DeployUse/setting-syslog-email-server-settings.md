---
title: "Nastavení oznámení ATA | Microsoft ATA"
description: "Popisuje, jak vám má ATA doručovat upozornění (e-mailem nebo předáváním událostí ATA) při zjištění podezřelých aktivit."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 10a7f4c003bc974d344129756f30df990dadf13d


---

## Nastavení e-mailového serveru pro ATA
ATA vás může upozornit, když zjistí podezřelou aktivitu. Aby řešení ATA mohlo odesílat e-mailová oznámení, musíte nejdřív nakonfigurovat **nastavení e-mailového serveru**.

1.  Na serveru ATA Center klikněte na ikonu **Správa Microsoft Advanced Threat Analytics** na ploše.

2.  Zadejte uživatelské jméno a heslo a klikněte na **Přihlásit**.

3.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

4.  Na kartě **Obecné** v části **E-mailový server** zadejte následující informace:

    |Pole|Popis|Hodnota|
    |---------|---------------|---------|
    |Koncový bod serveru SMTP (povinné)|Zadejte plně kvalifikovaný název domény serveru SMTP.|Například:<br />smtp.contoso.com|
    |SSL|Přepněte SSL, pokud SMTP server vyžaduje protokol SSL. **Poznámka:** Pokud povolíte protokol SSL, bude taky nutné změnit číslo portu.|Ve výchozím nastavení je zakázáno.|
    |Ověřování|Povolte, pokud váš server SMTP vyžaduje ověření. **Poznámka:** Pokud povolíte ověřování, je nutné zadat uživatelské jméno a heslo pro e-mailový účet, který má oprávnění pro připojení k serveru SMTP.|Ve výchozím nastavení je zakázáno.|
    |Odesilatel (povinné)|Zadejte e-mailovou adresu odesilatele e-mailu.|Například:<br />ATA@contoso.com|
    ![Obrázek nastavení e-mailového serveru ATA](media/ATA-email-server.png)

## Nastavení serveru Syslog pro ATA
Když ATA zjistí podezřelou aktivitu, může vás upozornit tak, že zašle upozornění na váš server Syslog. Pokud povolíte upozornění pro Syslog, můžete pro ně nastavit následující parametry.

1.  Před konfigurací upozornění pro Syslog zjistěte ve spolupráci s vaším správcem systému SIEM následující informace:

    -   Plně kvalifikovaný název domény nebo IP adresa serveru SIEM

    -   Port, na kterém naslouchá server SIEM

    -   Typ používaného přenosu: UDP ,TCP nebo TLS (Syslog se zabezpečením)

    -   Formát odesílání dat: RFC 3164 nebo 5424

2.  Na serveru ATA Center klikněte na ikonu **Správa Microsoft Advanced Threat Analytics** na ploše.

3.  Zadejte uživatelské jméno a heslo a klikněte na **Přihlásit**.

4.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

5.  Vyberte **Server syslog** a zadejte následující informace:

    |Pole|Popis|
    |---------|---------------|
    |Koncový bod serveru Syslog|Plně kvalifikovaný název domény serveru Syslog|
    |Přenos|Může být UDC, TCP nebo TLS (Syslog se zabezpečením)|
    |Formát|To je formát, který ATA používá k odesílání událostí na server SIEM – RFC 5424, nebo RFC 3164.|





## Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->



---
# required metadata

title: Nastavení výstrah ATA | Microsoft Advanced Threat Analytics
description: Popisuje, jak vám má ATA doručovat výstrahy (e-mailem nebo předáváním událostí ATA) při zjištění podezřelých aktivit. 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Nastavení výstrah ATA
ATA vás může upozornit, když zjistí podezřelou aktivitu, a to buď e-mailem, nebo pomocí předávání událostí ATA a předáváním události na váš server SIEM/syslog. Pokud povolíte jeden nebo oba tyto typy výstrah, můžete pro ně nastavit následující.

> [!NOTE]
> -   E-mailová oznámení zahrnují odkaz, který přenese uživatele přímo k podezřelé aktivitě, která byla zjištěna. Část názvu hostitele v odkazu je převzatá z nastavení adresy URL konzoly ATA na stránce ATA Center. Ve výchozím nastavení adresa URL konzoly ATA je IP adresa vybraná při instalaci ATA Center.  Pokud chcete nakonfigurovat e-mailové výstrahy, doporučuje se použít jako adresu URL konzoly ATA plně kvalifikovaný název domény.
> -   Výstraha stavu systému se odesílají jenom e-mailem.
> -   Výstrahy se z ATA Center posílají na server SMTP, nebo na server Syslog.
> -   E-mailové výstrahy pro podezřelé aktivity se odesílají jenom při vytvoření podezřelé aktivity.

## Nastavení jazyka a frekvence
Nastavení **Jazyk** se vztahuje na oznámení odesílaná e-mailem i na oznámení odeslaná na server Syslog.

Nastavení **Frekvence** se vztahuje jenom na oznámení odesílaná na server Syslog.

1.  Otevřete konzolu ATA.

2.  Vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**..

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

3.  Vyberte **Výstrahy**..

4.  V části **Jazyk** vyberte požadovaný jazyk.

5.  V části **Frekvence** vyberte **Nízká frekvence**, pokud chcete dostávat stručná oznámení jenom v případě, že se vygeneruje nová výstraha. Vyberte **Vysoká frekvence**, pokud chcete dostávat podrobné oznámení, když se vygeneruje nová výstraha nebo když dojde k úpravě existující výstrahy.

    ![Obrázek konfigurace podrobností výstrah](media/ATA-alerts-verbosity-language.png)

6.  Klikněte na **Uložit**..

## Nastavení e-mailových výstrah
ATA vás může upozornit, když zjistí podezřelou aktivitu. Pokud povolíte e-mailové výstrahy, můžete pro ně nastavit následující.

1.  Na serveru ATA Center klikněte na ikonu **Správa Microsoft Advanced Threat Analytics** na ploše.

2.  Zadejte uživatelské jméno a heslo a klikněte na **Přihlásit**..

3.  Vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**..

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

4.  Vyberte **Výstrahy**..

5.  Zapněte možnost **Pošta**, aby se povolily e-mailové výstrahy, a zadejte následující informace:

    |Pole|Popis|Hodnota|
    |---------|---------------|---------|
    |Koncový bod serveru SMTP (povinné)|Zadejte plně kvalifikovaný název domény serveru SMTP.|Například:<br />smtp.contoso.com|
    |SSL|Přepněte SSL, pokud SMTP server vyžaduje protokol SSL. **Poznámka:** Pokud povolíte protokol SSL, bude taky nutné změnit číslo portu.|Ve výchozím nastavení je zakázáno.|
    |Ověřování|Povolte, pokud váš server SMTP vyžaduje ověření. **Poznámka:** Pokud povolíte ověřování, je nutné zadat uživatelské jméno a heslo pro e-mailový účet, který má oprávnění pro připojení k serveru SMTP.|Ve výchozím nastavení je zakázáno.|
    |Odesilatel (povinné)|Zadejte e-mailovou adresu odesilatele e-mailu.|Například:<br />ATA@contoso.com|
    |Příjemce (povinné)|Zadejte e-mailové adresy uživatelů nebo e-mailových skupin, kterým bude poslán e-mail, když ATA zjistí podezřelou aktivitu. **Poznámka:** Postupně zadávejte jednotlivé e-mailové adresy a přidávejte je kliknutím na znaménko plus.|Například:<br />securityteam@contoso.com|

## Nastavení předávání událostí ATA systému SIEM
ATA vás může upozornit, když zjistí podezřelou aktivitu, zasláním události na váš server Syslog. Pokud povolíte výstrahy pro Syslog, můžete pro ně nastavit následující.

1.  Před konfigurací výstrah pro Syslog zjistěte ve spolupráci s vaším správcem systému SIEM následující informace:

    -   Plně kvalifikovaný název domény nebo IP adresa serveru SIEM

    -   Port, na kterém naslouchá server SIEM

    -   Typ používaného přenosu: UDP ,TCP nebo zabezpečený TCP

    -   Formát odesílání dat: RFC 3164 nebo 5424

2.  Na serveru ATA Center klikněte na ikonu **Správa Microsoft Advanced Threat Analytics** na ploše.

3.  Zadejte uživatelské jméno a heslo a klikněte na **Přihlásit**..

4.  Vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**..

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

5.  Vyberte **Výstrahy**..

6.  Zapněte možnost **Syslog**, aby se povolilo odesílání výstrah o podezřelých aktivitách na server Syslog, a zadejte následující informace:

    |Pole|Popis|
    |---------|---------------|
    |Koncový bod serveru Syslog|Plně kvalifikovaný název domény serveru Syslog|
    |Přenos|Může to být UDC, TCP nebo zabezpečený TCP.|
    |Formát|To je formát, který ATA používá k odesílání událostí na server SIEM – RFC 5424, nebo RFC 3164.|

## Viz také
[Podporu získáte na našem fóru!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO4-->



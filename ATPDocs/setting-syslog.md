---
title: Nastavení e-mailových oznámení v Azure Advanced Threat Protection | Microsoft Docs
description: Popisuje, jak mají ATP Azure (e-mailem nebo předáváním událostí Azure ATP) vám to oznámí při zjištění podezřelých aktivit
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 74fe9976df769ae01c58a5d66ca491c3fa8958d9
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
ms.locfileid: "29445991"
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="integrate-with-syslog"></a>Integrovat Syslog

Azure ATP vás může upozornit, když zjistí podezřelé aktivity a stav výstrahy zasláním oznámení na váš server Syslog. Pokud povolíte upozornění pro Syslog, můžete pro ně nastavit následující parametry.

1.  Před konfigurací upozornění pro Syslog zjistěte ve spolupráci s vaším správcem systému SIEM následující informace:

    -   Plně kvalifikovaný název domény nebo IP adresa serveru SIEM

    -   Port, na kterém naslouchá server SIEM

    -   Typ používaného přenosu: UDP, TCP nebo TLS (Syslog se zabezpečením)

    -   Formát odesílání dat: RFC 3164 nebo 5424

2.  Přejít na portál pro pracovní prostor adresy URL.

3.  Zadejte Azure Active Directory uživatelské jméno a heslo a klikněte na tlačítko **přihlásit**.

4.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace Azure ATP](media/ATP-config-menu.png)

5.  Klikněte na tlačítko **oznámení**a pak v části **oznámení Syslog** klikněte na tlačítko **konfigurace** a zadejte následující informace:

    |Pole|Popis|
    |---------|---------------|
    |Senzor|Vyberte určené senzor odpovědný za agregování všechny události procesu Syslog a předává je na váš server SIEM.|
    |Koncový bod služby|Plně kvalifikovaný název domény serveru Syslog a volitelně změňte číslo portu (výchozí hodnota 514)|
    |Přenos|Může být UDP, TCP nebo TLS (Syslog se zabezpečením)|
    |Formát|To je formát, který Azure ATP používá k odesílání událostí na server SIEM – RFC 5424, nebo RFC 3164.|

 ![Obrázek nastavení serveru Azure ATP Syslog](media/atp-syslog.png)

6. Můžete vybrat události, které k odeslání na váš server Syslog. V části **oznámení Syslog**, určete oznámení, která se mají odesílat na váš server Syslog - nové výstrahy zabezpečení, výstrahy aktualizované zabezpečení a nové problémy v oblasti stavu.


## <a name="see-also"></a>Viz také

- [Práce s citlivé účty](sensitive-accounts.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
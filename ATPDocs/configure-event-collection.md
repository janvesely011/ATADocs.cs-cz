---
title: Nainstalovat Azure Advanced Threat Protection | Dokumentace Microsoftu
description: V tomto kroku instalace ATP nakonfigurujete zdroje dat.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8416c2d6e3b12d15f52a0f27381d845fdb268cdd
ms.sourcegitcommit: 15f882cf45776877fdaca8367a7a0fe7f06a7917
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/23/2019
ms.locfileid: "71185530"
---
# <a name="configure-event-collection"></a>Konfigurace shromažďování událostí

Za účelem vylepšení možností detekce potřebuje Azure ATP následující události systému Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045 a 8004. Tyto události mohou být buď automaticky čteny pomocí snímače ATP v Azure, nebo pokud není senzor Azure ATP nasazený, dá se jednomu ze dvou způsobů přesměrovat na samostatný senzor Azure ATP. nakonfigurujeme tak samostatný senzor Azure ATP, aby naslouchal pro události SIEM nebo < c. 0 > konfiguraci předávání událostí systému Windows.

> [!NOTE]
> Před konfigurací shromažďování událostí je důležité spustit skript auditování ATP Azure ATP, aby bylo zajištěno, že řadiče domény budou správně nakonfigurovány pro zaznamenávání potřebných událostí. 

Kromě shromažďování a analýzy síťového provozu do a z řadičů domény může Azure ATP využít události systému Windows k dalšímu vylepšení detekce. Azure ATP používá pro protokol NTLM událost 4776 a 8004, což vylepšuje různé detekce a události 4732, 4733, 4728, 4729, 4756, 4757 a 7045, aby se zlepšila detekce citlivých změn skupin a vytváření služeb. Tyto události mohou být přijímány ze služby SIEM nebo nastavením předávání událostí Windows z řadiče domény. Shromážděné události poskytují Azure ATP dalšími informacemi, které nejsou k dispozici prostřednictvím síťového provozu řadiče domény.

## <a name="ntlm-authentication-using-windows-event-8004"></a>Ověřování NTLM pomocí události systému Windows 8004

Konfigurace kolekce Event 8004 pro Windows:
1. Přejít na: Cestě konfigurace možnosti počítače \ \ pro Policies\Security
2. Nastavte **Zásady skupiny domény** následujícím způsobem:
   - Zabezpečení sítě: Omezit protokol NTLM: Odchozí přenosy protokolu NTLM na vzdálené servery = **Auditovat vše**
   - Zabezpečení sítě: Omezit protokol NTLM: Auditovat ověřování NTLM v této doméně = **Povolit vše**
   - Zabezpečení sítě: Omezit protokol NTLM: Auditovat příchozí přenosy protokolu NTLM = **Povolit auditování pro všechny účty**

Když je událost 8004 systému Windows analyzována pomocí senzoru ATP Azure ATP, aktivity ověřování pomocí protokolu NTLM pro Azure ATP se rozšiřují pomocí dat pro přístup k serveru.

## <a name="siemsyslog"></a>SIEM/Syslog
Aby mohl Azure ATP využívat data ze serveru syslog, je nutné provést následující kroky:

- Nakonfigurujte servery senzorů Azure ATP na naslouchání a přijímání událostí předávaných ze serveru SIEM/syslog.

  > [!NOTE]
  > Azure ATP naslouchá jenom na IPv4 a ne na IPv6. 

- Nakonfigurujte server SIEM/syslog tak, aby předali konkrétní události do senzoru ATP Azure.

> [!IMPORTANT]
> -   Nepředávejte všechna data syslog do snímače ATP Azure.
> -   Azure ATP podporuje přenosy UDP ze serveru SIEM/syslog.

Informace o konfiguraci předávání určitých událostí na jiný server najdete v dokumentaci k produktu pro server SIEM/Syslog. 

> [!NOTE]
>Pokud nepoužíváte server SIEM/syslog, můžete nakonfigurovat řadiče domény systému Windows tak, aby přenesly všechny požadované události, které mají být shromažďovány a analyzovány službou Azure ATP.

## <a name="configuring-the-azure-atp-sensor-to-listen-for-siem-events"></a>Konfigurace snímače ATP Azure pro naslouchání událostem SIEM

1.  V konfiguraci ATP Azure v části **zdroje dat** klikněte na **Siem** a zapněte **syslog** a klikněte na **Uložit**.

    ![Obrázek povolení UDP naslouchacího procesu Syslog](media/atp-siem-config.png)

2.  Nakonfigurujte server SIEM nebo syslog tak, aby předal všechny požadované události na IP adresu jednoho ze senzorů ATP Azure. Další informace o konfiguraci SIEM najdete v online nápovědě k SIEM nebo v možnostech technické podpory pro konkrétní požadavky na formátování pro každý server SIEM.

Azure ATP podporuje události SIEM v následujících formátech:  

## <a name="rsa-security-analytics"></a>RSA Security Analytics
&lt;Hlavička Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Hlavička Syslog je nepovinná.

-   Znak oddělovače \n je vyžadován mezi všemi poli.

-   Pole jsou postupně následující:

    1.  Konstanta RsaSA (musí být uvedena).

    2.  Časové razítko skutečné události (Ujistěte se, že se nejedná o časové razítko doručení do SIEM nebo při odeslání do ATP). V případě přesnosti v milisekundách je to důležité.

    3.  ID události Windows

    4.  Název zprostředkovatele událostí Windows

    5.  Název protokolu událostí Windows

    6.  Název počítače přijímajícího událost (v tomto případě řadič domény)

    7.  Název ověřování uživatele

    8.  Název hostitele zdroje

    9. Kód výsledku NTLM

-   Pořadí je důležité a nic jiného by ve zprávě nemělo být zahrnuto.

## <a name="hp-arcsight"></a>HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Řadič domény se pokusil ověřit pověření účtu.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   Musí být v souladu s definicí protokolu.

-   Žádná hlavička syslog.

-   Část hlavičky (část, která je oddělená znakem |) musí existovat (jak je uvedeno v protokolu).

-   Následující klíče v části _rozšíření_ musí být v události přítomné:

    -   externalId = ID události Windows

    -   RT = časové razítko skutečné události (Ujistěte se, že se nejedná o časové razítko doručení do SIEM nebo při odeslání do ATP). V případě přesnosti v milisekundách je to důležité.

    -   cat = Název protokolu událostí Windows

    -   shost = Název hostitele zdroje

    -   dhost = Název počítače přijímajícího událost (v tomto případě řadič domény)

    -   duser = Ověřování uživatele

-   Pořadí není pro část _rozšíření_ důležité.

-   Musí být přítomné vlastní klíče a hodnoty pro tato dvě pole:

    -   EventSource

    -   Reason or Error Code = Kód výsledku NTLM

## <a name="splunk"></a>Splunk
&lt;Hlavička Syslog&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

Počítač se pokusil o ověření přihlašovacích údajů pro účet.

Ověřovací balíček:              MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Přihlašovací účet: Správce

Zdrojová pracovní stanice:       SIEM

Kód chyby:         0x0

-   Hlavička Syslog je nepovinná.

-   Mezi všemi požadovanými poli je znakový oddělovač \r\n.

-   Pole jsou ve formátu klíč = hodnota.

-   Následující klíče musí existovat a mít hodnotu:

    -   EventCode = ID události Windows

    -   Logfile = Název protokolu událostí Windows

    -   SourceName = Název zprostředkovatele událostí Windows

    -   TimeGenerated = časové razítko skutečné události (Ujistěte se, že se nejedná o časové razítko doručení do SIEM nebo při odeslání do ATP). Formát by měl odpovídat RRRRMMDDHHMMSS. FFFFFF, pokud možno s přesností na milisekundy, to je důležité.

    -   ComputerName = Název hostitele zdroje

    -   Message = Původní text události z události Windows

-   Klíč Message a hodnota musí být poslední.

-   Pořadí není pro dvojice klíč=hodnota důležité.

## <a name="qradar"></a>QRadar
QRadar umožňuje shromažďování událostí prostřednictvím agenta. Pokud se data shromažďují pomocí agenta, formát času se shromažďuje bez údajů o milisekundách. Vzhledem k tomu, že Azure ATP vyžaduje data v milisekundách, je potřeba nastavit QRadar na použití bez agentů pro Windows shromažďování událostí. Další informace najdete v tématu [http://www-01.ibm.com/support/docview.wss?uid=swg21700170] (http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Shromažďování událostí systému Windows bez agentů pomocí protokolu")MSRPC.

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Potřebná pole:

- Typ agenta pro shromažďování
- Název zprostředkovatele protokolu událostí Windows
- Zdroj protokolu událostí Windows
- Plně kvalifikovaný název domény pro řadič domény
- ID události Windows

TimeGenerated je časové razítko skutečné události (Ujistěte se, že se nejedná o časové razítko doručení do SIEM nebo při odeslání do ATP). Formát by měl odpovídat RRRRMMDDHHMMSS. FFFFFF, pokud možno s přesností na milisekundy, to je důležité.

Message je původní text události z události Windows.

Nezapomeňte použít oddělit páry klíč=hodnota pomocí \t.

>[!NOTE] 
> Použití funkce WinCollect pro shromažďování událostí Windows se nepodporuje.




## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Reference k protokolu Azure ATP SIEM](cef-format-sa.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

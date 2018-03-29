---
title: Nainstalovat Azure Advanced Threat Protection | Microsoft Docs
description: V tomto kroku instalace ATP nakonfigurujete datové zdroje.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/28/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2c2a8e6d70d937c559c110a18feec4afc75271e9
ms.sourcegitcommit: 45d0108d0cbf8fe7550d13486d3d9c06c1e58506
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="install-azure-atp"></a>Nainstalovat Azure ATP

## <a name="configure-event-collection"></a>Konfigurace shromažďování událostí

K vylepšení možností detekce, Azure ATP vyžaduje následující události systému Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 a 7045. Tyto může buď přečíst automaticky senzoru Azure ATP nebo v případě, že Azure ATP senzoru není nasazený, můžete přesměrovávají na samostatné senzoru Azure ATP v jednom ze dvou způsobů, tím nakonfigurujete senzoru samostatné Azure ATP tak, aby naslouchala událostem SIEM nebo [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md).

> [!NOTE]
> Je důležité, abyste spustili ATA před konfigurací shromažďování událostí auditování skriptu zajistit, že řadiče domény jsou správně nakonfigurovány, aby záznam nezbytné události. 

Kromě shromažďování a analýzy síťových přenosů do a z řadičů domény, Azure ATP slouží k dalšímu vylepšení detekce útoků události systému Windows. Událost 4776 používá pro protokol NTLM, což zlepšuje různé detekce a události 4732, 4733, 4728, 4729, 4756, 4757 a 7045 pro zlepšení detekce citlivou skupinu úpravy a vytvoření služby. Tyto události může přijímat buď od svého systému SIEM, nebo tak, že si nastavíte předávání událostí systému Windows ze svého řadiče domény. Shromážděné události poskytují Azure ATP společně s dalšími informacemi, které nejsou dostupné prostřednictvím síťových přenosů řadičů domény.

### <a name="siemsyslog"></a>SIEM/Syslog
Pro Azure ATP moct využívat data ze serveru Syslog musíte provést následující kroky:

-   Konfiguraci serverů senzor Azure ATP a naslouchání na akceptovat události, které jsou předávány ze serveru SIEM/Syslog.

 > [!NOTE]
 > Azure ATP naslouchá jenom na IPv4 a IPv6 není. 

-   Nakonfigurujte server SIEM/Syslog aby předával určité události do Azure ATP senzoru.

> [!IMPORTANT]
> -   Nepředávat všechna data Syslog na Azure ATP senzoru.
> -   Azure ATP podporuje přenosy protokolem UDP ze serveru SIEM/Syslog.

Informace o konfiguraci předávání určitých událostí na jiný server najdete v dokumentaci k produktu pro server SIEM/Syslog. 

> [!NOTE]
>Pokud nepoužíváte server SIEM/Syslog, můžete nakonfigurovat své řadiče domény Windows předávat všechny požadované události shromažďovat a analyzovat ATP.

### <a name="configuring-the-azure-atp-sensor-to-listen-for-siem-events"></a>Konfigurace senzoru Azure ATP tak, aby naslouchala událostem SIEM

1.  V konfiguraci ATP Azure v části **zdroje dat** klikněte na tlačítko **SIEM** a zapněte **Syslog** a klikněte na tlačítko **Uložit**.

    ![Obrázek povolení UDP naslouchacího procesu Syslog](media/atp-siem-config.png)

2.  Nakonfigurujte server SIEM nebo Syslog předávat všechny požadované události na IP adresu jednoho ze senzorů Azure ATP. Další informace o konfiguraci vašeho systému SIEM najdete v online nápovědě SIEM nebo možnosti technické podpory pro speciální požadavky formátování pro každý server SIEM.

Azure ATP podporuje události SIEM v následujících formátech:  

### <a name="rsa-security-analytics"></a>RSA Security Analytics
&lt;Hlavička Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Hlavička Syslog je nepovinná.

-   Znak oddělovače \n je vyžadován mezi všemi poli.

-   Pole jsou postupně následující:

    1.  Konstanta RsaSA (musí být uvedena).

    2.  Časové razítko skutečné události (ujistěte se, že není časové razítko přijetí do systému SIEM nebo odeslání do ATP). Pokud možno na milisekundy, to je důležité.

    3.  ID události Windows

    4.  Název zprostředkovatele událostí Windows

    5.  Název protokolu událostí Windows

    6.  Název počítače přijímajícího událost (v tomto případě řadič domény)

    7.  Název ověřování uživatele

    8.  Název hostitele zdroje

    9. Kód výsledku NTLM

-   Pořadí je důležité a nic jiného by ve zprávě nemělo být zahrnuto.

### <a name="hp-arcsight"></a>HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Řadič domény se pokusil ověřit pověření účtu.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   Musí být v souladu s definicí protokolu.

-   Žádná hlavička syslog.

-   Část hlavičky (část, která je oddělená znakem |) musí existovat (jak je uvedeno v protokolu).

-   Následující klíče v části _rozšíření_ musí být v události přítomné:

    -   externalId = ID události Windows

    -   RT = časové razítko skutečné události (ujistěte se, že není časové razítko přijetí do systému SIEM nebo odeslání do ATP). Pokud možno na milisekundy, to je důležité.

    -   cat = Název protokolu událostí Windows

    -   shost = Název hostitele zdroje

    -   dhost = Název počítače přijímajícího událost (v tomto případě řadič domény)

    -   duser = Ověřování uživatele

-   Pořadí není pro část _rozšíření_ důležité.

-   Musí být přítomné vlastní klíče a hodnoty pro tato dvě pole:

    -   EventSource

    -   Reason or Error Code = Kód výsledku NTLM

### <a name="splunk"></a>Splunk
&lt;Hlavička Syslog&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

Počítač se pokusil o ověření přihlašovacích údajů pro účet.

Ověřovací balíček:              MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Účet přihlášení: Administrator

Zdrojová pracovní stanice:       SIEM

Kód chyby:         0x0

-   Hlavička Syslog je nepovinná.

-   Mezi všemi požadovanými poli je znakový oddělovač \r\n.

-   Pole jsou ve formátu klíč = hodnota.

-   Následující klíče musí existovat a mít hodnotu:

    -   EventCode = ID události Windows

    -   Logfile = Název protokolu událostí Windows

    -   SourceName = Název zprostředkovatele událostí Windows

    -   TimeGenerated = časové razítko skutečné události (ujistěte se, že není časové razítko přijetí do systému SIEM nebo odeslání do ATP). Formát by měl odpovídat yyyyMMddHHmmss.FFFFFF, pokud možno na milisekundy, to je důležité.

    -   ComputerName = Název hostitele zdroje

    -   Message = Původní text události z události Windows

-   Klíč Message a hodnota musí být poslední.

-   Pořadí není pro dvojice klíč=hodnota důležité.

### <a name="qradar"></a>QRadar
QRadar umožňuje shromažďování událostí prostřednictvím agenta. Pokud se data shromažďují pomocí agenta, formát času se shromažďuje bez údajů o milisekundách. Protože Azure ATP vyžaduje údaje o milisekundách, je nutné nastavit Qradaru bez agentů shromažďování událostí Windows. Další informace najdete v tématu [ http://www-01.ibm.com/support/docview.wss?uid=swg21700170 ] (http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless kolekce událostí systému Windows pomocí protokolu MSRPC").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Potřebná pole:

- Typ agenta pro shromažďování
- Název zprostředkovatele protokolu událostí Windows
- Zdroj protokolu událostí Windows
- Plně kvalifikovaný název domény pro řadič domény
- ID události Windows

TimeGenerated je časové razítko skutečné události (ujistěte se, že není časové razítko přijetí do systému SIEM nebo odeslání do ATP). Formát by měl odpovídat yyyyMMddHHmmss.FFFFFF, pokud možno na milisekundy, to je důležité.

Message je původní text události z události Windows.

Nezapomeňte použít oddělit páry klíč=hodnota pomocí \t.

>[!NOTE] 
> Použití funkce WinCollect pro shromažďování událostí Windows se nepodporuje.




## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Odkazy na Azure protokol ATP SIEM](cef-format-sa.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)

---
title: "Instalace Advanced Threat Analytics – krok 6 | Dokumentace Microsoftu"
description: V tomto kroku instalace ATA nakonfigurujete zdroje dat.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/5/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ffab11a99ae62c1c0b37c43ee212d87508f886b8
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/05/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# Instalace ATA – krok 6
<a id="install-ata---step-6" class="xliff"></a>

>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)

## Krok 6: Konfigurace shromažďování událostí a sítě VPN
<a id="step-6-configure-event-collection-and-vpn" class="xliff"></a>
### Konfigurace shromažďování událostí
<a id="configure-event-collection" class="xliff"></a>
Kvůli vylepšení detekčních schopností potřebuje ATA následující události Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757. Tyto události buď může automaticky číst ATA Lightweight Gateway, nebo mohou být jedním ze dvou způsobů předávány komponentě ATA Gateway (v případě, že komponenta ATA Lightweight Gateway není nasazená), a to konfigurací komponenty ATA Gateway pro naslouchání událostem SIEM, nebo [konfigurací předávání událostí Windows](#configuring-windows-event-forwarding).

> [!NOTE]
> U ATA verze 1.8 a vyšších se u komponent ATA Lightweight Gateway shromažďování událostí už nemusí konfigurovat. ATA Lightweight Gateway teď dokáže číst události místně bez nutnosti konfigurace předávání událostí.

Kromě shromažďování a analýzy síťového provozu na řadičích domény dokáže ATA dál vylepšit detekce pomocí událostí Windows. Využívá událost 4776 protokolu NTLM, která vylepšuje různé detekce, a události 4732, 4733, 4728, 4729, 4756 a 4757, které vylepšují detekci úprav citlivých skupin. Tyto události může přijímat buď od svého systému SIEM, nebo tak, že si nastavíte předávání událostí systému Windows ze svého řadiče domény. Shromážděné události poskytují řešení ATA další informace, které není možné zjistit z monitorování provozu na řadiči domény.

#### SIEM/Syslog
<a id="siemsyslog" class="xliff"></a>
Aby řešení ATA mohlo využívat data ze serveru Syslog, je třeba provést následující:

-   Nakonfigurujte servery ATA Gateway, aby naslouchaly událostem, které jsou předávány ze serveru SIEM/Syslog, a přijímaly je.
> [!NOTE]
> ATA naslouchá jenom na IPv4, ne na IPv6. 
-   Nakonfigurujte server SIEM/Syslog, aby předával určité události komponentě ATA Gateway.

> [!IMPORTANT]
> -   Nepředávejte komponentě ATA Gateway všechna data Syslog.
> -   ATA podporuje ze serveru SIEM/Syslog provoz UDP.

Informace o konfiguraci předávání určitých událostí na jiný server najdete v dokumentaci k produktu pro server SIEM/Syslog. 

> [!NOTE]
>Pokud nepoužíváte server SIEM/Syslog, můžete nakonfigurovat své řadiče domény Windows pro předávání událostí systému Windows s ID 4776, aby se mohly pomocí ATA shromažďovat a analyzovat. Události systému Windows s ID 4776 poskytují data týkající se ověřování NTLM.

#### Konfigurace komponenty ATA Gateway pro naslouchání událostem SIEM
<a id="configuring-the-ata-gateway-to-listen-for-siem-events" class="xliff"></a>

1.  V okně Konfigurace ATA klikněte v oblasti **Zdroje dat** na **SIEM**, zapněte **Syslog** a klikněte na **Uložit**.

    ![Obrázek povolení UDP naslouchacího procesu Syslog](media/ATA-enable-siem-forward-events.png)

2.  Nakonfigurujte server Syslog nebo SIEM, aby předával události systému Windows s ID 4776 na IP adresu jedné ze součástí ATA Gateway. Další informace o konfiguraci vašeho systému SIEM najdete v online nápovědě SIEM nebo použijte možnosti technické podpory pro speciální požadavky formátování pro každý server SIEM.

ATA podporuje události SIEM v následujících formátech:  

#### RSA Security Analytics
<a id="rsa-security-analytics" class="xliff"></a>
&lt;Hlavička Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Hlavička Syslog je nepovinná.

-   Znak oddělovače \n je vyžadován mezi všemi poli.

-   Pole jsou postupně následující:

    1.  Konstanta RsaSA (musí být uvedena).

    2.  Časové razítko skutečné události (ujistěte se, že to není časové razítko přijetí do systému SIEM nebo odeslání do ATA). Pokud možno s přesností na milisekundy, to je velmi důležité.

    3.  ID události Windows

    4.  Název zprostředkovatele událostí Windows

    5.  Název protokolu událostí Windows

    6.  Název počítače přijímajícího událost (v tomto případě řadič domény)

    7.  Název ověřování uživatele

    8.  Název hostitele zdroje

    9. Kód výsledku NTLM

-   Pořadí je důležité a nic jiného by ve zprávě nemělo být zahrnuto.

#### HP Arcsight
<a id="hp-arcsight" class="xliff"></a>
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Řadič domény se pokusil ověřit pověření účtu.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   Musí být v souladu s definicí protokolu.

-   Žádná hlavička syslog.

-   Část hlavičky (část, která je oddělená znakem |) musí existovat (jak je uvedeno v protokolu).

-   Následující klíče v části _rozšíření_ musí být v události přítomné:

    -   externalId = ID události Windows

    -   rt = Časové razítko skutečné události (ujistěte se, že to není časové razítko přijetí do systému SIEM nebo odeslání nám). Pokud možno s přesností na milisekundy, to je velmi důležité.

    -   cat = Název protokolu událostí Windows

    -   shost = Název hostitele zdroje

    -   dhost = Název počítače přijímajícího událost (v tomto případě řadič domény)

    -   duser = Ověřování uživatele

-   Pořadí není pro část _rozšíření_ důležité.

-   Musí být přítomné vlastní klíče a hodnoty pro tato dvě pole:

    -   EventSource

    -   Reason or Error Code = Kód výsledku NTLM

#### Splunk
<a id="splunk" class="xliff"></a>
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

    -   TimeGenerated = Časové razítko skutečné události (ujistěte se, že to není časové razítko přijetí do systému SIEM nebo odeslání do ATA). Formát by měl odpovídat yyyyMMddHHmmss.FFFFFF, pokud možno s přesností na milisekundy, to je velmi důležité.

    -   ComputerName = Název hostitele zdroje

    -   Message = Původní text události z události Windows

-   Klíč Message a hodnota musí být poslední.

-   Pořadí není pro dvojice klíč=hodnota důležité.

#### QRadar
<a id="qradar" class="xliff"></a>
QRadar umožňuje shromažďování událostí prostřednictvím agenta. Pokud se data shromažďují pomocí agenta, formát času se shromažďuje bez údajů o milisekundách. Protože ale ATA údaje o milisekundách vyžaduje, je nutné v QRadaru nastavit shromažďování událostí Windows bez agenta. Další informace najdete v tématu [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol") (QRadar: Shromažďování událostí Windows bez agenta pomocí protokolu MSRPC).

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Potřebná pole:

- Typ agenta pro shromažďování
- Název zprostředkovatele protokolu událostí Windows
- Zdroj protokolu událostí Windows
- Plně kvalifikovaný název domény pro řadič domény
- ID události Windows

TimeGenerated je časové razítko skutečné události (ujistěte se, že to není časové razítko přijetí do systému SIEM nebo odeslání do ATA). Formát by měl odpovídat rrrrMMddHHmmss.FFFFFF, pokud možno s přesností na milisekundy, to je velmi důležité.

Message je původní text události z události Windows.

Nezapomeňte použít oddělit páry klíč=hodnota pomocí \t.

>[!NOTE] 
> Použití funkce WinCollect pro shromažďování událostí Windows se nepodporuje.


### Konfigurace sítě VPN
<a id="configuring-vpn" class="xliff"></a>

ATA shromažďuje data sítě VPN, která pomáhají při profilaci lokalit, ze kterých se počítače připojují k síti.

Data sítě VPN nakonfigurujete tak, že přejdete na **Konfigurace** > **Síť VPN** a zadáte **Sdílený tajný kód účtu Radius** vaší sítě VPN.

![Konfigurace sítě VPN](./media/vpn.png)

Informace o získání sdíleného tajného kódu najdete v dokumentaci k síti VPN. Podporovaní dodavatelé sítí VPN:

- Microsoft
- F5
- Check Point
- Cisco ASA



>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)
[Krok 7 »](install-ata-step7.md)


## Viz také
<a id="see-also" class="xliff"></a>

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)


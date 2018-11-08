---
title: Instalace Advanced Threat Analytics – krok 6 | Dokumentace Microsoftu
description: V tomto kroku instalace ATA nakonfigurujete zdroje dat.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3ef2d163ae96e5bf8f893367095eacd9a44c3411
ms.sourcegitcommit: 1a5880de35422d050fc1bc7a918dedc4180c45ad
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2018
ms.locfileid: "51265675"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="install-ata---step-6"></a>Instalace ATA – krok 6

> [!div class="step-by-step"]
> [« Krok 5](install-ata-step5.md)
> [Krok 7 »](vpn-integration-install-step.md)

## <a name="step-6-configure-event-collection"></a>Krok 6: Konfigurace shromažďování událostí
### <a name="configure-event-collection"></a>Konfigurace shromažďování událostí
Kvůli vylepšení detekčních schopností potřebuje ATA následující události Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 a 7045. Tyto události buď může automaticky číst ATA Lightweight Gateway, nebo mohou být jedním ze dvou způsobů předávány komponentě ATA Gateway (v případě, že komponenta ATA Lightweight Gateway není nasazená), a to konfigurací komponenty ATA Gateway pro naslouchání událostem SIEM, nebo [konfigurací předávání událostí Windows](configure-event-collection.md). 

> [!NOTE]
> U ATA verze 1.8 a vyšších se u komponent ATA Lightweight Gateway shromažďování událostí už nemusí konfigurovat. ATA Lightweight Gateway teď dokáže číst události místně bez nutnosti konfigurace předávání událostí.

Kromě shromažďování a analýzy síťového provozu na řadičích domény dokáže ATA dál vylepšit detekce pomocí událostí Windows. Využívá událost 4776 protokolu NTLM, která vylepšuje různé detekce a události 4732, 4733, 4728, 4729, 4756 a 4757, které vylepšují detekci úprav citlivých skupin. Tyto události může přijímat buď od svého systému SIEM, nebo tak, že si nastavíte předávání událostí systému Windows ze svého řadiče domény. Shromážděné události poskytují řešení ATA další informace, které není možné zjistit z monitorování provozu na řadiči domény.

#### <a name="siemsyslog"></a>SIEM/Syslog
Řešení ATA mohlo využívat data ze serveru Syslog je třeba provést následující kroky:

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

#### <a name="configuring-the-ata-gateway-to-listen-for-siem-events"></a>Konfigurace komponenty ATA Gateway pro naslouchání událostem SIEM

1.  V okně Konfigurace ATA klikněte v oblasti **Zdroje dat** na **SIEM**, zapněte **Syslog** a klikněte na **Uložit**.

    ![Obrázek povolení UDP naslouchacího procesu Syslog](media/ATA-enable-siem-forward-events.png)

2.  Nakonfigurujte server Syslog nebo SIEM, aby předával události systému Windows s ID 4776 na IP adresu jedné ze součástí ATA Gateway. Další informace o konfiguraci vašeho systému SIEM najdete v online nápovědě SIEM nebo možnosti technické podpory pro speciální požadavky formátování pro každý server SIEM.

ATA podporuje události SIEM v následujících formátech:  

#### <a name="rsa-security-analytics"></a>RSA Security Analytics
&lt;Hlavička Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Hlavička Syslog je nepovinná.

-   Znak oddělovače \n je vyžadován mezi všemi poli.

-   Pole jsou postupně následující:

    1.  Konstanta RsaSA (musí být uvedena).

    2.  Časové razítko skutečné události (ujistěte se, že to není časové razítko přijetí do systému SIEM nebo odeslání do ATA). Pokud možno na milisekundy, to je důležité.

    3.  ID události Windows

    4.  Název zprostředkovatele událostí Windows

    5.  Název protokolu událostí Windows

    6.  Název počítače přijímajícího událost (v tomto případě řadič domény)

    7.  Název ověřování uživatele

    8.  Název hostitele zdroje

    9. Kód výsledku NTLM

-   Pořadí je důležité a nic jiného by ve zprávě nemělo být zahrnuto.

#### <a name="hp-arcsight"></a>HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Řadič domény se pokusil ověřit pověření účtu.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   Musí být v souladu s definicí protokolu.

-   Žádná hlavička syslog.

-   Část hlavičky (část, která je oddělená znakem |) musí existovat (jak je uvedeno v protokolu).

-   Následující klíče v části _rozšíření_ musí být v události přítomné:

    -   externalId = ID události Windows

    -   RT = časové razítko skutečné události (ujistěte se, že to není časové razítko přijetí do systému SIEM nebo odeslání do ATA). Pokud možno na milisekundy, to je důležité.

    -   cat = Název protokolu událostí Windows

    -   shost = Název hostitele zdroje

    -   dhost = Název počítače přijímajícího událost (v tomto případě řadič domény)

    -   duser = Ověřování uživatele

-   Pořadí není pro část _rozšíření_ důležité.

-   Musí být přítomné vlastní klíče a hodnoty pro tato dvě pole:

    -   EventSource

    -   Reason or Error Code = Kód výsledku NTLM

#### <a name="splunk"></a>Splunk
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

    -   TimeGenerated = Časové razítko skutečné události (ujistěte se, že to není časové razítko přijetí do systému SIEM nebo odeslání do ATA). Formát by měl odpovídat yyyyMMddHHmmss.FFFFFF, pokud možno na milisekundy, to je důležité.

    -   ComputerName = Název hostitele zdroje

    -   Message = Původní text události z události Windows

-   Klíč Message a hodnota musí být poslední.

-   Pořadí není pro dvojice klíč=hodnota důležité.

#### <a name="qradar"></a>QRadar
QRadar umožňuje shromažďování událostí prostřednictvím agenta. Pokud se data shromažďují pomocí agenta, formát času se shromažďuje bez údajů o milisekundách. Protože ale ATA údaje o milisekundách vyžaduje, je nutné v QRadaru nastavit shromažďování událostí Windows bez agenta. Další informace najdete v tématu [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows shromažďování událostí pomocí protokolu MSRPC").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Potřebná pole:

- Typ agenta pro shromažďování
- Název zprostředkovatele protokolu událostí Windows
- Zdroj protokolu událostí Windows
- Plně kvalifikovaný název domény pro řadič domény
- ID události Windows

TimeGenerated je časové razítko skutečné události (ujistěte se, že to není časové razítko přijetí do systému SIEM nebo odeslání do ATA). Formát by měl odpovídat yyyyMMddHHmmss.FFFFFF, pokud možno na milisekundy, to je důležité.

Message je původní text události z události Windows.

Nezapomeňte použít oddělit páry klíč=hodnota pomocí \t.

>[!NOTE] 
> Použití funkce WinCollect pro shromažďování událostí Windows se nepodporuje.



> [!div class="step-by-step"]
> [« Krok 5](install-ata-step5.md)
> [Krok 7 »](vpn-integration-install-step.md)



## <a name="related-videos"></a>Související videa
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Volba správného typu komponenty ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)


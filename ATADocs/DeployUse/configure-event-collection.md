---
title: "Konfigurace shromažďování událostí | Microsoft ATA"
description: "Popisuje možnosti konfigurace shromažďování událostí v řešení ATA"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 6876339e1303438da10a56e23d8eb831cc17050c


---

# Konfigurace shromažďování událostí
K vylepšení možností detekce ATA vyžaduje událost systému Windows s ID 4776. Ten může být přeposílán komponentě ATA Gateway jedním ze dvou způsobů, buď konfigurací ATA Gateway tak, aby naslouchala událostem SIEM, nebo [nastavením předávání událostí systému Windows](#configuring-windows-event-forwarding).

## Shromažďování událostí
Kromě shromažďování a analýzy síťových přenosů z a do řadičů domény může ATA využít událost 4776 systému Windows k dalšímu vylepšení detekce útoků Pass-the-Hash. Tyto události může přijímat buď od vašeho systému SIEM, nebo nastavením předávání událostí systému Windows z vašeho řadiče domény. Shromážděné události poskytují řešení ATA další informace, které není možné zjistit z monitorování provozu na řadiči domény.

### SIEM/Syslog
Aby řešení ATA mohlo využívat data ze serveru Syslog, je třeba provést následující:

-   Nakonfigurujte jeden z vašich serverů ATA Gateway, aby naslouchal událostem, které jsou předávány ze serveru SIEM/Syslog, a přijímal je.

-   Nakonfigurujte server SIEM/Syslog, aby předával určité události komponentě ATA Gateway.

> [!IMPORTANT]
> -   Nepředávejte komponentě ATA Gateway všechna data Syslog.
> -   ATA podporuje ze serveru SIEM/Syslog provoz UDP.

Informace o konfiguraci předávání určitých událostí na jiný server najdete v dokumentaci k produktu pro server SIEM/Syslog. 

### Předávání událostí systému Windows
Pokud nepoužíváte server SIEM/Syslog, můžete nakonfigurovat své řadiče domény Windows pro předávání událostí systému Windows s ID 4776, aby se mohly pomocí ATA shromažďovat a analyzovat. Události systému Windows s ID 4776 poskytují data týkající se ověřování NTLM.

## Konfigurace komponenty ATA Gateway pro naslouchání událostem SIEM

1.  V konfiguraci ATA Gateway povolte **Syslog Listener UDP** (UDP naslouchacího procesu Syslog).

    Nastavte IP adresu naslouchání, jak je popsáno na obrázku níže. Výchozí port je 514.

    ![Obrázek povolení UDP naslouchacího procesu Syslog](media/ATA-enable-siem-forward-events.png)

2.  Nakonfigurujte server Syslog nebo SIEM, aby předával události systému Windows s ID 4776 na IP adresu vybranou výše. Další informace o konfiguraci vašeho systému SIEM najdete v online nápovědě SIEM nebo použijte možnosti technické podpory pro speciální požadavky formátování pro každý server SIEM.

### Podpora systému SIEM
ATA podporuje události SIEM v následujících formátech:

#### RSA Security Analytics
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

## Konfigurace předávání událostí systému Windows
Pokud nemáte server SIEM, můžete konfigurovat své řadiče domény, aby předávaly události systému Windows s ID 4776 přímo jedné z vašich komponent ATA Gateway.

1.  Přihlaste se na všechny řadiče domény a počítače ATA Gateway pomocí účtu domény s oprávněními správce.
2. Zajistěte, aby všechny řadiče domény a komponenty ATA Gateway, ke kterým se připojujete, byly připojené ke stejné doméně.
3.  V každém řadiči domény zadejte na příkazovém řádku se zvýšenými oprávněními následující:
```
winrm quickconfig
```
4.  V komponentě ATA Gateway zadejte na příkazovém řádku se zvýšenými oprávněními následující:
```
wecutil qc
```
5.  V každém řadiči domény v konzole **Uživatelé a počítače služby Active Directory** přejděte do složky **Builtin** a dvakrát klikněte na skupinu **Event Log Readers**.<br>
![wef_ad_eventlogreaders](media/wef_ad_eventlogreaders.png)<br>
Klikněte pravým tlačítkem a vyberte **Vlastnosti**. Na kartě **Členové** přidejte účet počítače každé komponenty ATA Gateway.
![Automaticky otevírané okno čtečky protokolu událostí wef_ad](media/wef_ad-event-log-reader-popup.png)
6.  V komponentě ATA Gateway otevřete Prohlížeč událostí a klikněte pravým tlačítkem na **Odběry** a vyberte **Vytvořit odběr**.  

    a. V části **Typ odběru a zdrojové počítače** klikněte na **Vybrat počítače**, přidejte řadiče domény a otestujte připojení.
    ![Vlastnosti wef_subscription](media/wef_subscription-prop.png)

    b. V části **Sbírané události** klikněte na **Vybrat události**. Vyberte **Podle protokolu**, posuňte se dolů a vyberte **Zabezpečení**. Pak do pole **Zahrne nebo vyloučí ID událostí** zadejte **4776**.<br>
    ![wef_4776](media/wef_4776.png)

    c. V části **Změnit uživatelský účet či nakonfigurovat rozšířené nastavení** klikněte na **Upřesnit**.
Nastavte **Protokol** na **HTTP** a **Port** na **5985**.<br>
    ![wef_http](media/wef_http.png)

7.  [Nepovinné] Pokud chcete kratší interval dotazování, nastavte na ATA Gateway prezenční signál odběru na 5 sekund kvůli vyšší rychlosti dotazování.
    wecutil ss <CollectionName>/cm:custom wecutil ss <CollectionName> /hi:5000

8. Na stránce konfigurace ATA Gateway povolte **Kolekce předávání událostí systému Windows**.

> [!NOTE]
> Pokud povolíte toto nastavení, bude ATA Gateway hledat v protokolu předávaných událostí ty události systému Windows, které byly předány z řadičů domény.

Další informace najdete v tématu [Konfigurace počítačů pro předání a shromáždění událostí](https://technet.microsoft.com/library/cc748890).

## Viz také
- [Instalace ATA](install-ata.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=Jul16_HO3-->



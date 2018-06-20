---
title: Řešení známých problémů ATA | Dokumentace Microsoftu
description: Tento článek popisuje řešení známých problémů v Advanced Threat Analytics.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: a7172447de5b4d4088da2d8d687a7bec47a01551
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010478"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="troubleshooting-ata-known-issues"></a>Řešení známých problémů ATA

Tato část podrobně popisuje možné chyby v nasazení ATA a kroky potřebné k jejich vyřešení.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>Chyby komponent ATA Gateway a Lightweight Gateway

> [!div class="mx-tableFixed"]
|Chyba|Popis|Řešení|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: Došlo k místní chybě|Nepovedlo se ověřit ATA Gateway na řadiči domény.|1. Ověřte, že záznam DNS řadiče domény je na serveru DNS správně nakonfigurovaný. <br>2. Ověřte, že čas komponenty ATA Gateway je synchronizovaný s časem řadiče domény.|
|System.IdentityModel.Tokens.SecurityTokenValidationException: Nepodařilo se ověřit řetěz certifikátů|Komponentě ATA Gateway se nepovedlo ověřit certifikát ATA Center.|1. Ověřte, že certifikát kořenové certifikační autority je nainstalovaný do úložiště certifikátů důvěryhodné certifikační autority v komponentě ATA Gateway. <br>2. Ověřte, že seznam odvolaných certifikátů (CRL) je dostupný a že jde provést ověření odvolání certifikátu.|
|Microsoft.Common.ExtendedException: Nepovedlo se analyzovat čas generování.|Komponentě ATA Gateway se nepovedlo analyzovat zprávy syslog, které předal systém SIEM.|Ověřte, že systém SIEM je nakonfigurovaný pro předávání zpráv v jednom z formátů, které podporuje ATA.|
|System.ServiceModel.FaultException: Došlo k chybě při ověřování zabezpečení zprávy.|Nepovedlo se ověřit ATA Gateway v komponentě ATA Center.|Ověřte, že čas komponenty ATA Gateway je synchronizovaný s časem komponenty ATA Center.|
|System.ServiceModel.EndpointNotFoundException: Nejde se připojit k net.tcp://center.ip.addr:443/IEntityReceiver|Komponentě ATA Gateway se nepovedlo navázat připojení ke komponentě ATA Center.|Zkontrolujte správnost nastavení sítě a ověřte, že síťové připojení mezi ATA Gateway a ATA Center je aktivní.|
|System.DirectoryServices.Protocols.LdapException: Server LDAP je nedostupný.|Komponentě ATA Gateway se nepovedlo odeslat dotaz na řadič domény pomocí protokolu LDAP.|1. Ověřte, že uživatelský účet, který ATA používá pro připojení k doméně Active Directory, má ke všem objektům ve stromové struktuře Active Directory přístup pro čtení. <br>2. Ověřte, že řadič domény nemá zesílené zabezpečení, které by zabraňovalo dotazům LDAP od uživatelského účtu, který používá ATA.|
|Microsoft.Tri.Infrastructure.ContractException: Výjimka kontraktu|Komponentě ATA Gateway se nepovedlo synchronizovat konfiguraci z ATA Center.|Dokončete konfiguraci ATA Gateway v ATA Console.|
|System.Reflection.ReflectionTypeLoadException: Jeden nebo několik požadovaných typů nejde načíst. Pokud chcete získat další informace, načtěte vlastnost LoaderExceptions.|Na ATA Gateway je nainstalovaný Message Analyzer.| Odinstalujte Message Analyzer.|
|Chyba [Layout] System.OutOfMemoryException: Vyvolala se výjimka typu System.OutOfMemoryException.|ATA Gateway nemá dost paměti.|Zvětšete velikost dostupné paměti na řadiči domény.|
|Spuštění živého příjemce se nepovedlo ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: Poskytovatel události PEFNDIS není připravený.|Modul PEF (Message Analyzer) se nenainstaloval správně.|Pokud používáte Hyper-V, zkuste upgradovat integrační služby Hyper-V, nebo se se žádostí o alternativní řešení obraťte na podporu.|
|Instalace se nepovedla s chybou: 0x80070652|Ve vašem počítači čekají na dokončení další instalace.|Počkejte na dokončení ostatních instalací a v případě potřeby restartujte počítač.|
|System.InvalidOperationException: Instance 'Microsoft.Tri.Gateway' v určené kategorii neexistuje.|Pro názvy procesů v bráně ATA byl povolen identifikátor PID|PID v názvech procesů zakážete pomocí [KB281884](https://support.microsoft.com/kb/281884)|
|System.InvalidOperationException: Kategorie neexistuje.|Čítače můžou být v registru zakázané|Čítače výkonu znovu sestavíte pomocí [KB2554336](https://support.microsoft.com/kb/2554336)|
|System.ApplicationException: Není možné spustit relaci ETW MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|V souboru hostitelů se nachází položka hostitele odkazující na krátký název počítače|Odeberte položku hostitele ze souboru C:\Windows\System32\drivers\etc\HOSTS nebo ji změňte na FQDN.|
|System.IO.IOException: Ověření se nezdařilo, protože vzdálená strana uzavřela přenosový stream.|Protokol TLS 1.0 je zakázána na ATA Gateway, ale .net je nastavený na použití protokolu TLS 1.2|Použijte jednu z následujících možností: </br> Povolení protokolu TLS 1.0 na bráně ATA Gateway </br>Povolení protokolu TLS 1.2 na rozhraní .net nastavením klíče registru, který chcete použít výchozí nastavení operačního systému pro protokol SSL a TLS, následujícím způsobem: </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001 `</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
|System.TypeLoadException: Nebylo možné načíst typ Microsoft.Opn.Runtime.Values.BinaryValueBufferManager ze sestavení Microsoft.Opn.Runtime, Verze=4.0.0.0, Jazyková verze=neutrální, PublicKeyToken=31bf3856ad364e35|Komponentě ATA Gateway se nepodařilo načíst požadované parsovací soubory.|Zkontrolujte, jestli je nainstalovaný Microsoft Message Analyzer. Instalace nástroje Message Analyzer společně s komponentami ATA Gateway / Lightweight Gateway není podporovaná. Odinstalujte Message Analyzer a restartujte službu Gateway.|
|System.Net.WebException: Vzdálený server vrátil chybu: (407) Vyžadováno ověřování proxy serveru|Komunikaci mezi ATA Gateway a ATA Center ruší proxy server.|Vypněte proxy server na počítači s ATA Gateway. <br></br>Nastavení proxy serveru můžou záviset na konkrétním účtu.|
|System.IO.DirectoryNotFoundException: Systém nemůže nalézt zadanou cestu. (Výjimka na základě hodnoty HRESULT: 0x80070003)|Jednu nebo více služeb potřebných pro provoz ATA se nepodařilo spustit.|Spusťte tyto služby: <br></br>Výstrahy a protokolování výkonu, Plánovač úloh.|
|System.Net.WebException: Vzdálený server vrátil chybu: (403) zakázán|ATA Gateway nebo Lightweight Gateway může bylo zakázáno z navazování připojení HTTP, protože komponenty ATA Center není důvěryhodný.|Přidejte název pro rozhraní NetBIOS a plně kvalifikovaný název domény pro ATA Center do seznamu důvěryhodných webů a vymažte mezipaměť na Interne Explorer (nebo na název komponenty ATA Center jako zadaný v konfiguraci, pokud je nakonfigurované se liší od pro rozhraní NetBIOS nebo plně kvalifikovaný název domény).|
|System.Net.Http.HttpRequestException: PostAsync failed [requestTypeName=StopNetEventSessionRequest]|ATA Gateway nebo ATA Lightweight Gateway nelze zastavit a spustit relaci trasování událostí pro Windows, která shromažďuje síťový provoz z důvodu problému rozhraní WMI|Postupujte podle pokynů v [rozhraní WMI: znovu sestavit úložiště služby WMI](https://blogs.technet.microsoft.com/askperf/2009/04/13/wmi-rebuilding-the-wmi-repository/) vyřešit problém, rozhraní WMI|
|System.Net.Sockets.SocketException: Byl proveden pokus o přístup k soketu způsobem, jeho přístupovými oprávněními|Na ATA Gateway je port 514 používá jiná aplikace|Použití `netstat -o` k vytvoření, které proces používá tento port.|
 
## <a name="deployment-errors"></a>Chyby nasazení
> [!div class="mx-tableFixed"]
|Chyba|Popis|Řešení|
|-------------|----------|---------|
|Instalace rozhraní .Net Framework 4.6.1 se nepovedla s chybou 0x800713ec.|Na serveru nejsou nainstalované nezbytné komponenty pro .Net Framework 4.6.1. |Před instalací ATA ověřte, že jsou na serveru nainstalované aktualizace systému Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) a [KB2919355](https://support.microsoft.com/kb/2919355).|
|System.Threading.Tasks.TaskCanceledException: Úloha byla zrušena.|Procesu nasazení vypršel časový limit, protože komponenta ATA Center nebyla dosažitelná.|1.    Zkontrolujte síťové připojení komponenty ATA Center tím, že na ni přejdete pomocí její IP adresy. <br></br>2.    Zkontrolujte konfiguraci proxy serveru nebo firewallu.|
|System.Net.Http.HttpRequestException: Při odesílání žádosti došlo k chybě. ---> System.Net.WebException: Vzdálený server vrátil chybu: (407) Vyžadováno ověřování proxy serveru|Procesu nasazení vypršel časový limit, protože kvůli chybné konfiguraci proxy serveru nebyla komponenta ATA Center dosažitelná.|Před nasazením zakažte konfiguraci proxy serveru a pak ji znovu povolte. Alternativně můžete v proxy serveru nakonfigurovat výjimku.|
|System.Net.Sockets.SocketException: Stávající připojení bylo vynuceně ukončeno vzdáleným hostitelem||Použijte jednu z následujících možností: </br>Povolení protokolu TLS 1.0 na bráně ATA Gateway </br>Povolení protokolu TLS 1.2 na rozhraní .net nastavením klíče registru, který chcete použít výchozí nastavení operačního systému pro protokol SSL a TLS, následujícím způsobem:</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
|Chyby [\[] DeploymentModel [\]] se nezdařilo ověření správy [\[] CurrentlyLoggedOnUser =<domain>\<uživatelské jméno > Stav = FailedAuthentication výjimka = [\]]|Proces nasazení ATA Gateway nebo ATA Lightweight Gateway nelze úspěšně ověřil v komponentě ATA Center|Otevřít prohlížeč z počítače, na kterém se nezdařil proces nasazení a zobrazit, pokud se lze připojit konzolu ATA. </br>V opačném případě spusťte řešení potíží s zobrazíte, proč nelze v prohlížeči ověřování na základě ATA Center. </br>Co je potřeba zkontrolovat: </br>Konfigurace proxy serveru</br>Problémy sítě</br>Nastavení zásad skupiny pro ověřování na tomto počítači, který se liší od ATA Center.|





## <a name="ata-gateway-and-lightweight-gateway-issues"></a>Problémy související s ATA Gateway a Lightweight Gateway

> [!div class="mx-tableFixed"]
|Problém|Popis|Řešení|
|-------------|----------|---------|
|Z řadiče domény se nepřijímá žádný provoz, jsou ale pozorována monitorovací upozornění|    Z řadiče domény nebyl pomocí zrcadlení portů přes ATA Gateway přijat žádný provoz|U síťové karty pro zachytávání na ATA Gateway zakažte v oblasti **Upřesnit nastavení** tyto funkce:<br></br>Slučování příjmových segmentů (IPv4)<br></br>Slučování příjmových segmentů (IPv6)|
|Zobrazí se tato monitorování výstraha: **není analyzované provoz v síti**|Pokud máte Lightweight Gateway nebo ATA Gateway na virtuální počítače VMware, zobrazí se tato výstraha monitorování. K tomu dochází z důvodu neshody konfigurace v prostředí VMware.|Nastavte následující nastavení **0** nebo **zakázané** v konfiguraci virtuálního počítače síťový adaptér: TsoEnable, LargeSendOffload, TSO snižování zátěže, snižování zátěže Obří TSO|Protokol TLS 1.0 je zakázána na ATA Gateway, ale .net je nastavený na použití protokolu TLS 1.2|




## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

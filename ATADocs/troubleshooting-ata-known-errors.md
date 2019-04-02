---
title: Řešení známých problémů ATA | Dokumentace Microsoftu
description: Tento článek popisuje řešení známých problémů v Advanced Threat Analytics.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/31/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: edac28031e9faa3e5c23bbbd82ef4ce023f1f249
ms.sourcegitcommit: db60935a92fe43fe149f6a4d3114fe0edaa1d331
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/01/2019
ms.locfileid: "58763997"
---
# <a name="troubleshooting-ata-known-issues"></a>Řešení známých problémů ATA


*Platí pro: Advanced Threat Analytics verze 1.9*

Tato část podrobně popisuje možné chyby v nasazení ATA a kroky potřebné k jejich vyřešení.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>Chyby komponent ATA Gateway a Lightweight Gateway

> [!div class="mx-tableFixed"]
> 
> |Chyba|Popis|Řešení|
> |-------------|----------|---------|
> |System.DirectoryServices.Protocols.LdapException: Došlo k místní chybě|Nepovedlo se ověřit ATA Gateway na řadiči domény.|1. Ověřte, že záznam DNS řadiče domény je na serveru DNS správně nakonfigurovaný. <br>2. Ověřte, že čas komponenty ATA Gateway je synchronizovaný s časem řadiče domény.|
> |System.IdentityModel.Tokens.SecurityTokenValidationException: Nepovedlo se ověřit řetěz certifikátů|Komponentě ATA Gateway se nepovedlo ověřit certifikát ATA Center.|1. Ověřte, že certifikát kořenové certifikační autority je nainstalovaný do úložiště certifikátů důvěryhodné certifikační autority v komponentě ATA Gateway. <br>2. Ověřte, že seznam odvolaných certifikátů (CRL) je dostupný a že jde provést ověření odvolání certifikátu.|
> |Microsoft.Common.ExtendedException: Nepovedlo se analyzovat čas generování.|Komponentě ATA Gateway se nepovedlo analyzovat zprávy syslog, které předal systém SIEM.|Ověřte, že systém SIEM je nakonfigurovaný pro předávání zpráv v jednom z formátů, které podporuje ATA.|
> |System.ServiceModel.FaultException: Při ověřování zabezpečení zprávy došlo k chybě.|Nepovedlo se ověřit ATA Gateway v komponentě ATA Center.|Ověřte, že čas komponenty ATA Gateway je synchronizovaný s časem komponenty ATA Center.|
> |System.ServiceModel.EndpointNotFoundException: Nelze se připojit k NET.TCP://Center.IP.addr: 443/IEntityReceiver|Komponentě ATA Gateway se nepovedlo navázat připojení ke komponentě ATA Center.|Zkontrolujte správnost nastavení sítě a ověřte, že síťové připojení mezi ATA Gateway a ATA Center je aktivní.|
> |System.DirectoryServices.Protocols.LdapException: LDAP server nedostupný.|Komponentě ATA Gateway se nepovedlo odeslat dotaz na řadič domény pomocí protokolu LDAP.|1. Ověřte, že uživatelský účet, který ATA používá pro připojení k doméně Active Directory, má ke všem objektům ve stromové struktuře Active Directory přístup pro čtení. <br>2. Ověřte, že řadič domény nemá zesílené zabezpečení, které by zabraňovalo dotazům LDAP od uživatelského účtu, který používá ATA.|
> |Microsoft.Tri.Infrastructure.ContractException: Výjimka kontraktu|Komponentě ATA Gateway se nepovedlo synchronizovat konfiguraci z ATA Center.|Dokončete konfiguraci ATA Gateway v ATA Console.|
> |System.Reflection.ReflectionTypeLoadException: Nelze načíst jeden nebo více požadovaných typů. Pokud chcete získat další informace, načtěte vlastnost LoaderExceptions.|Na ATA Gateway je nainstalovaný Message Analyzer.| Odinstalujte Message Analyzer.|
> |Chyba [Layout] System.OutOfMemoryException: Byla vyvolána výjimka typu "System.OutOfMemoryException".|ATA Gateway nemá dost paměti.|Zvětšete velikost dostupné paměti na řadiči domény.|
> |Nepovedlo se spuštění živého příjemce---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: Poskytovatel události PEFNDIS není připravený|Modul PEF (Message Analyzer) se nenainstaloval správně.|Pokud používáte Hyper-V, zkuste upgradovat integrační služby Hyper-V, nebo se se žádostí o alternativní řešení obraťte na podporu.|
> |Instalace se nezdařila s chybou: 0x80070652|Ve vašem počítači čekají na dokončení další instalace.|Počkejte na dokončení ostatních instalací a v případě potřeby restartujte počítač.|
> |System.InvalidOperationException: Instance 'Microsoft.Tri.Gateway' v určené kategorii neexistuje.|Pro názvy procesů v bráně ATA byl povolen identifikátor PID|PID v názvech procesů zakážete pomocí [KB281884](https://support.microsoft.com/kb/281884)|
> |System.InvalidOperationException: Kategorie neexistuje.|Čítače můžou být v registru zakázané|Čítače výkonu znovu sestavíte pomocí [KB2554336](https://support.microsoft.com/kb/2554336)|
> |System.ApplicationException: Nepovedlo se spustit relaci ETW MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|V souboru hostitelů se nachází položka hostitele odkazující na krátký název počítače|Odeberte položku hostitele ze souboru C:\Windows\System32\drivers\etc\HOSTS nebo ji změňte na FQDN.|
> |System.IO.IOException: Ověření se nezdařilo, protože vzdálená strana uzavřela přenosový stream.|Protokol TLS 1.0 je zakázaný v komponentě ATA Gateway, ale rozhraní .net je nastavené na použití protokolu TLS 1.2|Použijte jednu z následujících možností: </br> Povolení protokolu TLS 1.0 na bráně ATA Gateway </br>Protokol TLS 1.2 na rozhraní .net nastavením klíčů registru použít výchozí nastavení operačního systému pro protokol SSL a TLS, následujícím způsobem: </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001 `</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
> |System.TypeLoadException: Nelze načíst typ 'Microsoft.Opn.Runtime.Values.BinaryValueBufferManager' ze sestavení ' Microsoft.Opn.Runtime, verze = 4.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 "|Komponentě ATA Gateway se nepodařilo načíst požadované parsovací soubory.|Zkontrolujte, jestli je nainstalovaný Microsoft Message Analyzer. Instalace nástroje Message Analyzer společně s komponentami ATA Gateway / Lightweight Gateway není podporovaná. Odinstalujte Message Analyzer a restartujte službu Gateway.|
> |System.Net.WebException: Vzdálený server vrátil chybu: Vyžadováno ověřování proxy serveru (407)|Komunikaci mezi ATA Gateway a ATA Center ruší proxy server.|Vypněte proxy server na počítači s ATA Gateway. <br></br>Nastavení proxy serveru můžou záviset na konkrétním účtu.|
> |System.IO.DirectoryNotFoundException: Systém nemůže najít zadanou cestu. (Výjimka z HRESULT: 0x80070003)|Jednu nebo více služeb potřebných pro provoz ATA se nepodařilo spustit.|Spusťte tyto služby: <br></br>Výstrahy a protokolování výkonu, Plánovač úloh.|
> |System.Net.WebException: Vzdálený server vrátil chybu: Zakázáno (403)|ATA Gateway a Lightweight Gateway by byl zakázán z navazování připojení HTTP, protože komponenty ATA Center není důvěryhodný.|Přidejte název rozhraní NetBIOS a plně kvalifikovaný název domény z komponenty ATA Center do seznamu důvěryhodných webů a vymažte mezipaměť na Interne Explorer (nebo názvu komponenty ATA Center, jak je zadáno v konfiguraci, pokud je nakonfigurované se liší od rozhraní NetBIOS nebo plně kvalifikovaný název).|
> |System.Net.Http.HttpRequestException: PostAsync se nezdařilo [requestTypeName = StopNetEventSessionRequest]|ATA Gateway nebo ATA Lightweight Gateway nejde zastavit a spustit relaci trasování událostí pro Windows, která shromažďuje síťový provoz z důvodu problému s WMI|Postupujte podle pokynů v [rozhraní WMI: Znovu sestavit úložiště služby WMI](https://blogs.technet.microsoft.com/askperf/2009/04/13/wmi-rebuilding-the-wmi-repository/) k vyřešení tohoto problému rozhraní WMI|
> |System.Net.Sockets.SocketException: Byl proveden pokus o přístup k soketu tak automatické připojení zakázáno její přístupová oprávnění|Používá jiná aplikace portu 514 v komponentě ATA Gateway|Použití `netstat -o` stanovit, které proces používá daný port.|

## <a name="deployment-errors"></a>Chyby nasazení
> [!div class="mx-tableFixed"]
> 
> |Chyba|Popis|Řešení|
> |-------------|----------|---------|
> |Instalace rozhraní .Net Framework 4.6.1 se nepovedla s chybou 0x800713ec.|Na serveru nejsou nainstalované nezbytné komponenty pro .Net Framework 4.6.1. |Před instalací ATA ověřte, že jsou na serveru nainstalované aktualizace systému Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) a [KB2919355](https://support.microsoft.com/kb/2919355).|
> |System.Threading.Tasks.TaskCanceledException: Úloha byla zrušena|Procesu nasazení vypršel časový limit, protože komponenta ATA Center nebyla dosažitelná.|1.    Zkontrolujte síťové připojení komponenty ATA Center tím, že na ni přejdete pomocí její IP adresy. <br></br>2.    Zkontrolujte konfiguraci proxy serveru nebo firewallu.|
> |System.Net.Http.HttpRequestException: Při odesílání požadavku došlo k chybě. ---> System.Net.WebException: Vzdálený server vrátil chybu: Vyžadováno ověřování proxy serveru (407).|Procesu nasazení vypršel časový limit, protože kvůli chybné konfiguraci proxy serveru nebyla komponenta ATA Center dosažitelná.|Před nasazením zakažte konfiguraci proxy serveru a pak ji znovu povolte. Alternativně můžete v proxy serveru nakonfigurovat výjimku.|
> |System.Net.Sockets.SocketException: Stávající připojení vynuceně zavřel vzdálený hostitel||Použijte jednu z následujících možností: </br>Povolení protokolu TLS 1.0 na bráně ATA Gateway </br>Protokol TLS 1.2 na rozhraní .net nastavením klíčů registru použít výchozí nastavení operačního systému pro protokol SSL a TLS, následujícím způsobem:</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
> |Chyby [\[] DeploymentModel [\]] se nezdařilo ověřování pro správu [\[] CurrentlyLoggedOnUser =<domain>\<uživatelské jméno > Stav = FailedAuthentication výjimka = [\]]|Procesu nasazení komponenty ATA Gateway nebo ATA Lightweight Gateway se nepovedlo úspěšně ověřit komponentě ATA Center|Z počítače, na kterém procesu nasazení se nepodařilo otevřít prohlížeč a zobrazit, pokud se lze připojit konzolu ATA. </br>V opačném případě spusťte řešení potíží zobrazíte, proč se v prohlížeči nemůže ověřit komponentě ATA Center. </br>Co je potřeba zkontrolovat: </br>Konfigurace proxy serveru</br>Problémy sítě</br>Nastavení zásad skupiny pro ověřování v daném počítači, který se liší od komponenty ATA Center.|
> | Chyby [\[] DeploymentModel [\]] se nezdařilo ověřování pro správu|Ověřování certifikátu Center se nezdařilo.|Certifikát Center vyžaduje pro ověření připojení k Internetu. Ujistěte se, že vaše služba brány má konfiguraci proxy serveru správná umožňující připojení a ověřování.|



## <a name="ata-center-errors"></a>Chyby komponenty ATA Center
> [!div class="mx-tableFixed"]
> 
> |Chyba|Popis|Řešení|
> |-------------|----------|---------|
> |System.Security.Cryptography.CryptographicException: Přístup se odepřel.|Komponenty ATA Center se nepodařilo použít se zapisuje certifikát vydaný pro dešifrování. K tomu pravděpodobně dojít z důvodu použití certifikátu s specifikace klíče (KeyNumber) nastavena na podpis (na\_podpis) což není podporováno pro dešifrování, namísto použití pro výměnu (na\_pro výměnu).|1.    Zastavte službu ATA Center. <br></br>2.     Odstraníte certifikát ATA Center z úložiště certifikátů System center. (Před odstraněním, ujistěte se, že certifikát zálohovány pomocí soukromého klíče v souboru PFX.) <br></br>3.    Otevřete příkazový řádek se zvýšenými oprávněními a spusťte příkaz certutil - importpfx "CenterCertificate.pfx" AT\_pro výměnu <br></br>4.     Spuštění služby ATA Center. <br></br>5.     Ověřte, že všechno, co teď funguje podle očekávání.|


## <a name="ata-gateway-and-lightweight-gateway-issues"></a>Problémy související s ATA Gateway a Lightweight Gateway

> [!div class="mx-tableFixed"]
> 
> |Problém|Popis|Řešení|
> |-------------|----------|---------|
> |Z řadiče domény se nepřijímá žádný provoz, jsou ale pozorována monitorovací upozornění|    Z řadiče domény nebyl pomocí zrcadlení portů přes ATA Gateway přijat žádný provoz|U síťové karty pro zachytávání na ATA Gateway zakažte v oblasti **Upřesnit nastavení** tyto funkce:<br></br>Slučování příjmových segmentů (IPv4)<br></br>Slučování příjmových segmentů (IPv6)|
> |Zobrazí se toto monitorovací upozornění: Některý síťový provoz se neanalyzuje|Pokud máte ATA Gateway a Lightweight Gateway na virtuálních počítačích VMware, může se zobrazit toto monitorovací upozornění. K tomu dochází kvůli neshodě v konfiguraci ve VMware.|Nastavte následující nastavení 0 nebo jsou zakázaná v konfiguraci virtuálního počítače síťovou kartu: TsoEnable, LargeSendOffload, TSO Offload a Giant TSO Offload TLS 1.0 je zakázaný v komponentě ATA Gateway, ale rozhraní .net je nastavené na použití protokolu TLS 1.2|





## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

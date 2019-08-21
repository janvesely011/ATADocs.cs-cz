---
title: Řešení známých problémů ATA | Dokumentace Microsoftu
description: Tento článek popisuje řešení známých problémů v Advanced Threat Analytics.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 08/20/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: d20aecfd55dd5b348c459373cb69c37bba91d458
ms.sourcegitcommit: 2aab3c4244db694616ec02a9b8ae2e266d6fdddc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2019
ms.locfileid: "69629284"
---
# <a name="troubleshooting-ata-known-issues"></a>Řešení známých problémů ATA


*Platí pro: Advanced Threat Analytics verze 1,9*

Tato část podrobně popisuje možné chyby v nasazení ATA a kroky potřebné k jejich vyřešení.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>Chyby komponent ATA Gateway a Lightweight Gateway

> [!div class="mx-tableFixed"]
> 
> |Chyba|Popis|Řešení|
> |-------------|----------|---------|
> |System.DirectoryServices.Protocols.LdapException: Došlo k místní chybě.|Nepovedlo se ověřit ATA Gateway na řadiči domény.|1. Ověřte, že záznam DNS řadiče domény je na serveru DNS správně nakonfigurovaný. <br>2. Ověřte, že čas komponenty ATA Gateway je synchronizovaný s časem řadiče domény.|
> |System.IdentityModel.Tokens.SecurityTokenValidationException: Nepovedlo se ověřit řetěz certifikátů.|Komponentě ATA Gateway se nepovedlo ověřit certifikát ATA Center.|1. Ověřte, že certifikát kořenové certifikační autority je nainstalovaný do úložiště certifikátů důvěryhodné certifikační autority v komponentě ATA Gateway. <br>2. Ověřte, že seznam odvolaných certifikátů (CRL) je dostupný a že jde provést ověření odvolání certifikátu.|
> |Microsoft.Common.ExtendedException: Nepovedlo se analyzovat vygenerované časy.|Komponentě ATA Gateway se nepovedlo analyzovat zprávy syslog, které předal systém SIEM.|Ověřte, že systém SIEM je nakonfigurovaný pro předávání zpráv v jednom z formátů, které podporuje ATA.|
> |System. ServiceModel. FaultException: Při ověřování zabezpečení zprávy došlo k chybě.|Nepovedlo se ověřit ATA Gateway v komponentě ATA Center.|Ověřte, že čas komponenty ATA Gateway je synchronizovaný s časem komponenty ATA Center.|
> |System.ServiceModel.EndpointNotFoundException: Nepovedlo se připojit k NET. TCP://Center.IP.addr: 443/IEntityReceiver|Komponentě ATA Gateway se nepovedlo navázat připojení ke komponentě ATA Center.|Zkontrolujte správnost nastavení sítě a ověřte, že síťové připojení mezi ATA Gateway a ATA Center je aktivní.|
> |System.DirectoryServices.Protocols.LdapException: Server LDAP není k dispozici.|Komponentě ATA Gateway se nepovedlo odeslat dotaz na řadič domény pomocí protokolu LDAP.|1. Ověřte, že uživatelský účet, který ATA používá pro připojení k doméně Active Directory, má ke všem objektům ve stromové struktuře Active Directory přístup pro čtení. <br>2. Ověřte, že řadič domény nemá zesílené zabezpečení, které by zabraňovalo dotazům LDAP od uživatelského účtu, který používá ATA.|
> |Microsoft.Tri.Infrastructure.ContractException: Výjimka kontraktu|Komponentě ATA Gateway se nepovedlo synchronizovat konfiguraci z ATA Center.|Dokončete konfiguraci ATA Gateway v ATA Console.|
> |System.Reflection.ReflectionTypeLoadException: Nelze načíst jeden nebo více požadovaných typů. Pokud chcete získat další informace, načtěte vlastnost LoaderExceptions.|Na ATA Gateway je nainstalovaný Message Analyzer.| Odinstalujte Message Analyzer.|
> |Chyba [Layout] System. OutOfMemoryException: Vyvolala se výjimka typu System. OutOfMemoryException.|ATA Gateway nemá dost paměti.|Zvětšete velikost dostupné paměti na řadiči domény.|
> |Nepodařilo se spustit živého příjemce---> Microsoft. OPN. Runtime. Monitoring. MessageSessionException: Zprostředkovatel událostí PEFNDIS není připravený.|Modul PEF (Message Analyzer) se nenainstaloval správně.|Pokud používáte Hyper-V, zkuste upgradovat integrační služby Hyper-V, nebo se se žádostí o alternativní řešení obraťte na podporu.|
> |Instalace se nezdařila s chybou: 0x80070652|Ve vašem počítači čekají na dokončení další instalace.|Počkejte na dokončení ostatních instalací a v případě potřeby restartujte počítač.|
> |System.InvalidOperationException: Instance Microsoft. Tri. Gateway v zadané kategorii neexistuje.|Pro názvy procesů v bráně ATA byl povolen identifikátor PID|PID v názvech procesů zakážete pomocí [KB281884](https://support.microsoft.com/kb/281884)|
> |System.InvalidOperationException: Kategorie neexistuje.|Čítače můžou být v registru zakázané|Čítače výkonu znovu sestavíte pomocí [KB2554336](https://support.microsoft.com/kb/2554336)|
> |System. ApplicationException: Nelze spustit relaci trasování událostí pro Windows MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|V souboru hostitelů se nachází položka hostitele odkazující na krátký název počítače|Odeberte položku hostitele ze souboru C:\Windows\System32\drivers\etc\HOSTS nebo ji změňte na FQDN.|
> |System. IO. IOException: Ověření se nezdařilo, protože Vzdálená strana ukončila přenosový Stream nebo nemohl vytvořit zabezpečený kanál SSL/TLS.|Protokol TLS 1,0 je v bráně ATA zakázaný, ale rozhraní .NET je nastavené na použití TLS 1,2.|Použijte jednu z následujících možností: </br> Povolení protokolu TLS 1.0 na bráně ATA Gateway </br>Povolte TLS 1,2 na platformě .NET nastavením klíčů registru pro použití výchozích hodnot operačního systému pro SSL a TLS následujícím způsobem: </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001 `</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
> |System.TypeLoadException: Nejde načíst typ Microsoft. OPN. Runtime. Values. BinaryValueBufferManager v sestavení Microsoft. OPN. Runtime, Version = 4.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35.|Komponentě ATA Gateway se nepodařilo načíst požadované parsovací soubory.|Zkontrolujte, jestli je nainstalovaný Microsoft Message Analyzer. Instalace nástroje Message Analyzer společně s komponentami ATA Gateway / Lightweight Gateway není podporovaná. Odinstalujte Message Analyzer a restartujte službu Gateway.|
> |System.Net.WebException: Vzdálený server vrátil chybu: (407) vyžaduje se ověřování proxy.|Komunikaci mezi ATA Gateway a ATA Center ruší proxy server.|Vypněte proxy server na počítači s ATA Gateway. <br></br>Nastavení proxy serveru můžou záviset na konkrétním účtu.|
> |System. IO. DirectoryNotFoundException: Systém nemůže najít zadanou cestu. (Výjimka ze HRESULT: 0x80070003)|Jednu nebo více služeb potřebných pro provoz ATA se nepodařilo spustit.|Spusťte tyto služby: <br></br>Výstrahy a protokolování výkonu, Plánovač úloh.|
> |System.Net.WebException: Vzdálený server vrátil chybu: (403) zakázáno|Bráně ATA Gateway nebo zjednodušené bráně se nepodařilo vytvořit připojení HTTP, protože ATA Center není důvěryhodná.|Přidejte název rozhraní NetBIOS a plně kvalifikovaný název domény ATA Center do seznamu důvěryhodných webů a vymažte mezipaměť v Průzkumníkovi pro učně (nebo název ATA Center, jak je uvedeno v konfiguraci), pokud je nakonfigurovaný jinak než rozhraní NetBIOS nebo plně kvalifikovaný název domény.|
> |System.Net.Http.HttpRequestException: PostAsync se nezdařilo [requestTypeName = StopNetEventSessionRequest]|ATA Gateway nebo ATA Lightweight Gateway nemůžou zastavit a spustit relaci trasování událostí pro Windows, která shromažďuje síťový provoz kvůli problému s rozhraním WMI.|Postupujte podle pokynů v [tématu WMI: Nové sestavení úložiště](https://blogs.technet.microsoft.com/askperf/2009/04/13/wmi-rebuilding-the-wmi-repository/) služby WMI pro opravu problému se službou WMI|
> |System .NET. Sockets. SocketException: Byl proveden pokus o přístup k soketu způsobem, který zakázal jeho přístupová oprávnění.|Jiná aplikace používá port 514 na ATA Gateway.|Použijte `netstat -o` k určení, který proces používá tento port.|

## <a name="deployment-errors"></a>Chyby nasazení
> [!div class="mx-tableFixed"]
> 
> |Chyba|Popis|Řešení|
> |-------------|----------|---------|
> |Instalace rozhraní .Net Framework 4.6.1 se nepovedla s chybou 0x800713ec.|Na serveru nejsou nainstalované nezbytné komponenty pro .Net Framework 4.6.1. |Před instalací ATA ověřte, že jsou na serveru nainstalované aktualizace systému Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) a [KB2919355](https://support.microsoft.com/kb/2919355).|
> |System.Threading.Tasks.TaskCanceledException: Úloha byla zrušena.|Procesu nasazení vypršel časový limit, protože komponenta ATA Center nebyla dosažitelná.|1.    Zkontrolujte síťové připojení komponenty ATA Center tím, že na ni přejdete pomocí její IP adresy. <br></br>2.    Zkontrolujte konfiguraci proxy serveru nebo firewallu.|
> |System.Net.Http.HttpRequestException: Při odesílání žádosti došlo k chybě. ---> System .NET. WebException: Vzdálený server vrátil chybu: (407) je vyžadováno ověřování proxy serveru.|Procesu nasazení vypršel časový limit, protože kvůli chybné konfiguraci proxy serveru nebyla komponenta ATA Center dosažitelná.|Před nasazením zakažte konfiguraci proxy serveru a pak ji znovu povolte. Alternativně můžete v proxy serveru nakonfigurovat výjimku.|
> |System .NET. Sockets. SocketException: Existující připojení bylo vynuceně ukončeno vzdáleným hostitelem.||Použijte jednu z následujících možností: </br>Povolení protokolu TLS 1.0 na bráně ATA Gateway </br>Povolte TLS 1,2 na platformě .NET nastavením klíčů registru pro použití výchozích hodnot operačního systému pro SSL a TLS následujícím způsobem:</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
> |Chyba [\\[] DeploymentModel [\\]] neúspěšná ověřování správy\\[[] CurrentlyLoggedOnUser<domain>=\\<username>status = FailedAuthentication výjimka =\\[]]|Proces nasazení komponenty ATA Gateway nebo ATA Lightweight Gateway se nepodařilo úspěšně ověřit proti komponentě ATA Center.|Otevřete prohlížeč z počítače, ve kterém se proces nasazení nezdařil, a zjistěte, zda se můžete připojit ke konzole ATA. </br>Pokud ne, spusťte Poradce při potížích, abyste viděli, proč se prohlížeč nemůže ověřit pro ATA Center. </br>Co byste měli kontrolovat: </br>Konfigurace proxy serveru</br>Problémy sítě</br>Nastavení zásad skupiny pro ověřování na tomto počítači, které se liší od centra ATA.|
> | Chyba [\\[] DeploymentModel [\\]] ověřování správy se nezdařilo.|Nepovedlo se ověřit certifikát centra.|Certifikát centra může vyžadovat připojení k Internetu pro ověření. Ujistěte se, že má služba brány správnou konfiguraci proxy, aby bylo možné připojení a ověřování povolit.|


## <a name="ata-center-errors"></a>Chyby ATA Center
> [!div class="mx-tableFixed"]
> 
> |Chyba|Popis|Řešení|
> |-------------|----------|---------|
> |System.Security.Cryptography.CryptographicException: Přístup se odepřel.|ATA Center se nepodařilo použít vydaný certifikát k dešifrování. K tomuto nejpravděpodobnějšímu problému dochází v důsledku použití certifikátu s parametrem klíče (_SIGNATURE) nastaveným na signaturu (na adrese\\), který není pro dešifrování podporovaný, místo použití výměny (na\\_KEYEXCHANGE).|1.    Zastavte službu ATA Center. <br></br>2.     Odstraňte certifikát ATA Center z úložiště certifikátů centra. (Před odstraněním se ujistěte, že máte certifikát zálohovaný pomocí privátního klíče v souboru PFX.) <br></br>3.    Otevřete příkazový řádek se zvýšenými oprávněními a spusťte příkaz certutil-importPFX "CenterCertificate.\\PFX" na adrese _KEYEXCHANGE <br></br>4.     Spusťte službu ATA Center. <br></br>5.     Ověřte, že všechno teď funguje podle očekávání.|


## <a name="ata-gateway-and-lightweight-gateway-issues"></a>Problémy související s ATA Gateway a Lightweight Gateway

> [!div class="mx-tableFixed"]
> 
> |Problém|Popis|Řešení|
> |-------------|----------|---------|
> |Z řadiče domény se nepřijímá žádný provoz, jsou ale pozorována monitorovací upozornění|    Z řadiče domény nebyl pomocí zrcadlení portů přes ATA Gateway přijat žádný provoz|U síťové karty pro zachytávání na ATA Gateway zakažte v oblasti **Upřesnit nastavení** tyto funkce:<br></br>Slučování příjmových segmentů (IPv4)<br></br>Slučování příjmových segmentů (IPv6)|
> |Zobrazí se tato výstraha monitorování: Některý síťový provoz se neanalyzuje|Pokud máte ATA Gateway nebo odlehčenou bránu na virtuálních počítačích VMware, může se zobrazit tato výstraha monitorování. K tomu dochází z důvodu neshody konfigurace ve VMware.|Nastavte následující nastavení na hodnotu 0 nebo zakázáno v konfiguraci síťové karty virtuálního počítače: TsoEnable, LargeSendOffload, TSO Offload, Obří TSO Offload TLS 1,0 je v ATA Gateway zakázané, ale rozhraní .NET je nastavené na použití TLS 1,2|

## <a name="multi-processor-group-mode"></a>Režim více procesorů 
V operačních systémech Windows 2008 R2 a 2012 není ATA Gateway podporována v režimu více procesorů.

Navrhovaná možná řešení:
- Je-li technologie Hyper-Threading zapnutá, vypněte ji. To může snížit počet logických jader dostatečně, aby nedocházelo k tomu, že byste museli spouštět v režimu **více procesorů** . 

- Pokud má váš počítač méně než 64 logických jader a běží na hostiteli HP, možná budete moct změnit nastavení systému BIOS **Optimalizace velikosti skupiny NUMA** z výchozí hodnoty **CLUSTERED** na **plochý**. 




## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

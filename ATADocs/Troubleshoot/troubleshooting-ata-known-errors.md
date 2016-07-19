---
title: "Řešení potíží s protokolem chyb ATA | Microsoft Advanced Threat Analytics"
description: "Popisuje, jak je v ATA možné řešit běžné chyby."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e0745079465aecefd26571eea894d19b82cbc216
ms.openlocfilehash: c72bca3cb1eef1f3fb59f666c6143cf5c095bde9


---

# Řešení potíží s protokolem chyb ATA
Tato část podrobně popisuje možné chyby v nasazení ATA a kroky potřebné k jejich vyřešení.
## Chyby ATA Gateway
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
|Spuštění živého příjemce se nepovedlo ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: Poskytovatel události PEFNDIS není připravený.|Modul PEF (Message Analyzer) se nenainstaloval správně.|Se žádostí o alternativní řešení se obraťte na podporu.|
|Instalace se nepovedla s chybou: 0x80070652|Ve vašem počítači čekají na dokončení další instalace.|Počkejte na dokončení ostatních instalací a v případě potřeby restartujte počítač.|

## Chyby konzoly ATA
|Chyba|Popis|Řešení|
|-------------|----------|---------|
|Chyba protokolu HTTP 500.19 – vnitřní chyba serveru|Nepovedlo se správně nainstalovat modul IIS URL Rewrite.|Odinstalujte modul IIS URL a nainstalujte ho znovu.<br>[Stáhnout modul IIS URL Rewrite](http://go.microsoft.com/fwlink/?LinkID=615137)|

## Chyby nasazení
|Chyba|Popis|Řešení|
|-------------|----------|---------|
|Instalace rozhraní .Net Framework 4.6.1 se nepovedla s chybou 0x800713ec.|Na serveru nejsou nainstalované nezbytné komponenty pro .Net Framework 4.6.1. |Před instalací ATA ověřte, že jsou na serveru nainstalované aktualizace systému Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) a [KB2919355](https://support.microsoft.com/kb/2919355).|

![Obrázek chyby instalace .NET ATA](media/netinstallerror.png)


## Viz také
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurace sběru událostí](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurace předávání událostí systému Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO1-->



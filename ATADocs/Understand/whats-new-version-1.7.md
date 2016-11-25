---
title: Novinky ATA verze 1.7 | Dokumentace Microsoftu
description: "Uvádí novinky ATA verze 1.7 spolu se známými problémy."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/25/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: be9ee613-4eb3-40f1-8973-e7f0a707ff57
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fca7f1b2b8260cad6e0ce32aad1c9e1b53fc0ad5
ms.openlocfilehash: 8032e373567ce500c7741480d56d232f34b05446


---

# <a name="whats-new-in-ata-version-17"></a>Novinky ATA verze 1.7
Tyto poznámky k verzi obsahují informace o známých problémech v této verzi Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-17-update"></a>Co je nového v aktualizaci ATA 1.7?
Aktualizace ATA na verzi 1.7 přináší vylepšení v následujících oblastech:

-   Nové a aktualizované detekce

-   Řízení přístupu na základě role

-   Podpora systému Windows Server 2016 a jádra serveru Windows

-   Vylepšení uživatelského prostředí

-   Menší změny


### <a name="new-updated-detections"></a>Nové a aktualizované detekce


- **Rekognoskace pomocí výčtu adresářových služeb** V rámci fáze rekognoskace útočníci pomocí různých metod shromažďují informace o entitách v síti. Výčet adresářových služeb pomocí protokolu SAM-R útočníkům umožňuje získat seznam uživatelů a skupin v doméně a pochopit vztahy mezi různými entitami. 

- **Vylepšení proti útoku typu Pass-the-Hash** Abychom zlepšili detekci útoku typu Pass-the-Hash, přidali jsme do ověřovacích vzorců entit další modely chování. Tyto modely umožňují funkci ATA korelaci chování entity s podezřelými ověřeními NTLM a odliší skutečné útoky typu Pass-the-Hash od chování ve falešně pozitivních scénářích.

- **Vylepšení proti útoku typu Pass-the-Ticket** Abychom úspěšně zjistili pokročilé útoky a zejména útoky typu Pass-the-Ticket, musí být korelace mezi IP adresou a účtem počítače přesná. Jedná se o náročný úkol v prostředích, kde se IP adresy zcela normálně rychle mění (například sítě Wi-Fi a skupina virtuálních počítačů, které sdílení stejného hostitele). Abychom tento problém vyřešili a zlepšili přesnost detekce útoků typu Pass-the-Ticket, výrazně jsme vylepšili mechanismus překladu síťového názvu funkce ATA, který teď zaznamenává menší počet falešně pozitivních shod.

- **Vylepšení proti nestandardnímu chování** V ATA verze 1.7 jsme přidali data ověřování NTLM jak zdroj dat pro detekci nestandardního chování a rozšířili jsme pokrytí algoritmu pro chování entit v síti. 

- **Vylepšení proti neobvyklé implementaci protokolu** ATA teď detekuje neobvyklou implementaci protokolu v protokolu Kerberos a také další anomálie v protokolu NTLM. Konkrétně se tyto nové anomálie protokolu Kerberos běžně používají v útocích typu Over-pass-the-Hash.


### <a name="infrastructure"></a>Infrastruktura

- **Řízení přístupu na základě role** Možnost řízení přístupu na základě role (RBAC). ATA 1.7 obsahuje tři role: Správce ATA, Analytik ATA a Vedení ATA.

- **Podpora systému Windows Server 2016 a jádra serveru Windows** ATA 1.7 podporuje nasazení součástí Lightweight Gateways v řadičích domény, které používají jádro serveru pro systém Windows Server 2012 a jádro serveru pro systém Windows Server 2012 R2. Kromě toho tato verze podporuje Windows Server 2016 pro součásti ATA Center i ATA Gateway.

### <a name="user-experience"></a>Činnost koncového uživatele
- **Prostředí konfigurace** V této verzi bylo prostředí konfigurace ATA přepracováno, aby bylo uživatelsky vstřícnější a lépe podporovalo prostředí s několika ATA Gateway. Tato verze také zavádí stránku aktualizace ATA Gateway pro jednodušší, lepší správu automatických aktualizací pro různé brány.

## <a name="known-issues"></a>Známé problémy
V této verzi existují následující známé problémy.

### <a name="gateway-automatic-update-may-fail"></a>Automatické aktualizace brány se nemusí podařit.
**Příznaky:** V prostředích s pomalým připojením WAN může při aktualizaci ATA Gateway vypršet časový limit pro aktualizaci (100 sekund) a aktualizace se nepodaří.
V konzole ATA může ATA Gateway po dlouhou dobu zobrazovat stav „Probíhá aktualizace (stahování balíčku)“ a nakonec dojde k chybě.
**Alternativní řešení:** Pokud chcete tento problém vyřešit, stáhněte z konzoly ATA nejnovější balíček ATA Gateway a aktualizujte ATA Gateway ručně.

 > [!IMPORTANT]
 Automatické obnovení certifikátu pro certifikáty používané funkcí ATA není podporované. Použití těchto certifikátů po jejich automatickém obnovení může způsobit, že ATA přestane fungovat. 

### <a name="no-browser-support-for-jis-encoding"></a>Prohlížeče nepodporují kódování JIS
**Příznaky:** Konzola ATA nemusí fungovat dle očekávání v prohlížečích s kódováním JIS. **Řešení:** Změňte kódování prohlížeče na Unicode UTF-8.
 
### <a name="dropped-port-mirror-traffic-when-using-vmware"></a>Přerušené přenosy se zrcadlením portů při použití VMware

Upozornění na přerušené přenosy se zrcadlením portů při použití brány Lightweight Gateway na VMwaru

Pokud používáte řadiče domény na virtuálních počítačích VMware, můžou se vám zobrazit upozornění na **přerušené síťové přenosy se zrcadlením portů**. Toto může nastat kvůli neshodě v konfiguraci ve VMware. Pokud se chcete těmto upozorněním vyhnout, zkontrolujte, že následující nastavení mají hodnotu 0 nebo jsou na virtuálním počítači zakázaná:  

- TsoEnable
- LargeSendOffload(IPv4)
- IPv4 TSO Offload

Zvažte také zakázání procesu IPv4 Giant TSO Offload. Další informace najdete v dokumentaci k VMware.

### <a name="automatic-gateway-update-fail-when-updating-to-17-update-1"></a>Chyba automatické aktualizace brány při aktualizaci na verzi 1.7 (aktualizace 1)

Automatický proces aktualizace ATA Gateway a ruční instalace bran pomocí balíčku bran nefungují při aktualizaci z ATA 1.7 na ATA 1.7 aktualizace 1, jak by měly.
K tomuto problému dochází, pokud se certifikát používaný komponentou ATA Center před aktualizací ATA změnil.
Pokud chcete tento problém ověřit, podívejte se na protokol **Microsoft.Tri.Gateway.Updater.log** u ATA Gateway a hledejte následující výjimky: **System.Net.Http.HttpRequestException: Při odesílání požadavku došlo k chybě. ---> System.Net.WebException: Nadřízené připojení bylo uzavřeno: Došlo k neočekávané chybě při odeslání. ---> System.IdentityModel.Tokens.SecurityTokenValidationException: Nepodařilo se ověřit kryptografický otisk certifikátu.**

![Chyba aktualizace brány ATA](media/17update_gatewaybug.png)

Pokud chcete tento problém vyřešit, přejděte na příkazovém řádku se zvýšenými oprávněními po změně certifikátu do následujícího umístění : **%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** a spusťte tento příkaz:

1. Mongo.exe ATA (ATA musí být velkými písmeny) 

2. CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;

3. db.SystemProfile.update({_t:"ServiceSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}}, {multi: true})


## <a name="minor-changes"></a>Menší změny

- ATA teď pro konzolu ATA používá OWIN místo IIS.
- Pokud nefunguje služba ATA Center, nebudete mít přístup ke konzole ATA.
- Podsítě pro krátkodobé zapůjčení už nejsou potřebné z důvodu změn v ATA NNR.

## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizace ATA na verzi 1.7 – průvodce migrací](ata-update-1.7-migration-guide.md)




<!--HONumber=Nov16_HO3-->



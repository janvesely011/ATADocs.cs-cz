---
title: Novinky ATA verze 1.7 | Microsoft ATA
description: "Uvádí novinky ATA verze 1.7 spolu se známými problémy."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ae6a3295d2fffabdb8e5f713674379e4af499ac2
ms.openlocfilehash: af9101260b1a0d5d9da32398f638f76e0c8c40a7


---

# Novinky ATA verze 1.7
Tyto poznámky k verzi obsahují informace o známých problémech v této verzi Advanced Threat Analytics.

## Co je nového v aktualizaci ATA 1.7?
Aktualizace ATA na verzi 1.7 přináší vylepšení v následujících oblastech:

-   Nové a aktualizované detekce

-   Řízení přístupu na základě role

-   Podpora systému Windows Server 2016 a jádra serveru Windows

-   Vylepšení uživatelského prostředí


### Nové a aktualizované detekce


- **Rekognoskace pomocí výčtu adresářových služeb** V rámci fáze rekognoskace útočníci pomocí různých metod shromažďují informace o entitách v síti. Výčet adresářových služeb pomocí protokolu SAM-R útočníkům umožňuje získat seznam uživatelů a skupin v doméně a pochopit vztahy mezi různými entitami. 

- **Vylepšení proti útoku typu Pass-the-Hash** Abychom zlepšili detekci útoku typu Pass-the-Hash, přidali jsme do ověřovacích vzorců entit další modely chování. Tyto modely umožňují funkci ATA korelaci chování entity s podezřelými ověřeními NTLM a odliší skutečné útoky typu Pass-the-Hash od chování ve falešně pozitivních scénářích.

- **Vylepšení proti útoku typu Pass-the-Ticket** Abychom úspěšně zjistili pokročilé útoky a zejména útoky typu Pass-the-Ticket, musí být korelace mezi IP adresou a účtem počítače přesná. Jedná se o náročný úkol v prostředích, kde se IP adresy zcela normálně rychle mění (například sítě Wi-Fi a skupina virtuálních počítačů, které sdílení stejného hostitele). Abychom tento problém vyřešili a zlepšili přesnost detekce útoků typu Pass-the-Ticket, výrazně jsme vylepšili mechanismus překladu síťového názvu funkce ATA, který teď zaznamenává menší počet falešně pozitivních shod.

- **Vylepšení proti nestandardnímu chování** V ATA verze 1.7 jsme přidali data ověřování NTLM jak zdroj dat pro detekci nestandardního chování a rozšířili jsme pokrytí algoritmu pro chování entit v síti. 

- **Vylepšení proti neobvyklé implementaci protokolu** ATA teď detekuje neobvyklou implementaci protokolu v protokolu Kerberos a také další anomálie v protokolu NTLM. Konkrétně se tyto nové anomálie protokolu Kerberos běžně používají v útocích typu Over-pass-the-Hash.


### Infrastruktura

- **Řízení přístupu na základě role** Možnost řízení přístupu na základě role (RBAC). ATA 1.7 obsahuje tři role: Správce ATA, Analytik ATA a Vedení ATA.

- **Podpora systému Windows Server 2016 a jádra serveru Windows** ATA 1.7 podporuje nasazení součástí Lightweight Gateways v řadičích domény, které používají jádro serveru pro systém Windows Server 2012 a jádro serveru pro systém Windows Server 2012 R2. Kromě toho tato verze podporuje Windows Server 2016 pro součásti ATA Center i ATA Gateway.

### Činnost koncového uživatele
- **Prostředí konfigurace** V této verzi bylo prostředí konfigurace ATA přepracováno, aby bylo uživatelsky vstřícnější a lépe podporovalo prostředí s několika ATA Gateway. Tato verze také zavádí stránku aktualizace ATA Gateway pro jednodušší, lepší správu automatických aktualizací pro různé brány.

## Známé problémy
V této verzi existují následující známé problémy.

### Automatické aktualizace brány se nemusí podařit.
**Příznaky:** V prostředích s pomalým připojením WAN může při aktualizaci ATA Gateway vypršet časový limit pro aktualizaci (100 sekund) a aktualizace se nepodaří.
V konzole ATA může ATA Gateway po dlouhou dobu zobrazovat stav „Probíhá aktualizace (stahování balíčku)“ a nakonec dojde k chybě.

**Alternativní řešení:** Pokud chcete tento problém vyřešit, stáhněte z konzoly ATA nejnovější balíček ATA Gateway a aktualizujte ATA Gateway ručně.

### Selhání migrace při aktualizaci z ATA 1.6
Při aktualizaci na ATA 1.7 může proces aktualizace selhat s kódem chyby *0x80070643*:

![Chyba aktualizace na ATA 1.7](media/ata-update-error.png)

Vyhledejte příčinu selhání v protokolu nasazení. Protokol nasazení se nachází v tomto umístění: **%temp%\..\Microsoft Advanced Thread Analytics Center_{date_stamp}_MsiPackage.log**. 

V tabulce níže jsou uvedeny chyby, které je třeba vyhledat, a odpovídající skript Mongo, který slouží k opravě chyby. Postup spuštění skriptu Mongo naleznete v příkladu pod tabulkou:

| Chyba v souboru protokolu nasazení                                                                                                                  | Skript Mongo                                                                                                                                                                         |
|---|---|
| System.FormatException: Size {size},is larger than MaxDocumentSize 16777216 <br>Níže v souboru:<br>  Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateUniqueEntityProfiles(Boolean isPartial)                                                                                        | db.UniqueEntityProfile.find().forEach(function(obj){if(Object.bsonsize(obj) > 12582912) {print(obj._id);print(Object.bsonsize(obj));db.UniqueEntityProfile.remove({_id:obj._id});}}) |
| System.OutOfMemoryException: Exception of type 'System.OutOfMemoryException' was thrown<br>Níže v souboru:<br>Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.ReduceSuspiciousActivityDetailsRecords(IMongoCollection`1 suspiciousActivityCollection, Int32 deletedDetailRecordMaxCount) | db.SuspiciousActivity.find().forEach(function(obj){if(Object.bsonsize(obj) > 500000),{print(obj._id);print(Object.bsonsize(obj));db.SuspiciousActivity.remove({_id:obj._id});}})     |
|System.Security.Cryptography.CryptographicException: Bad Length<br>Níže v souboru:<br> Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateCenterSystemProfile(IMongoCollection`1 systemProfileCollection)| CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;db.SystemProfile.update({_t:"CenterSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}})|


Příslušný skript spustíte podle následujícího postupu. 

1.  Z příkazového řádku se zvýšenými oprávněními přejděte do následujícího umístění: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**
2.  Zadejte – **Mongo.exe ATA**   (*Poznámka*: ATA musí být velkými písmeny.)
3.  Z výše uvedené tabulky vložte skript, který odpovídá chybě v protokolu nasazení.

![Skript ATA Mongo](media/ATA-mongoDB-script.png)

V tomto okamžiku by mělo být možné upgrade spustit.

### Funkce ATA hlásí velký počet podezřelých aktivit *Rekognoskace pomocí výčtů služeb adresáře*:
 
Dochází k tomu pravděpodobně v případě, že je ve všech (nebo ve velkém počtu) klientských počítačích v organizaci spuštěn nástroj pro prohledávání sítě. Pokud dochází k tomuto problému:

1. V případě, že můžete identifikovat příčinu nebo konkrétní aplikaci spuštěnou v klientských počítačích, pošlete e-mail s informacemi na ATAEval na stránkách Microsoft.com.
2. Všechny tyto události zavřete pomocí následujícího skriptu mongo (postup spuštění skriptu mongo je popsán výše):

db.SuspiciousActivity.update({_t: "SamrReconnaissanceSuspiciousActivity"}, {$set: {Status: "Dismissed"}}, {multi: true})

### Služba ATA odesílá oznámení o zavřených (zrušených) podezřelých aktivitách:
Pokud jsou nakonfigurována oznámení, ATA může posílat e-maily, oznámení syslog či protokoly událostí týkající se zavřených podezřelých aktivit.
Pro tento problém není momentálně k dispozici žádné řešení. 

### Pokud jsou protokoly TLS 1.0 a TLS 1.1 neaktivní, ATA Gateway se nemusí podařit registrovat se do ATA Center:
Pokud jsou protokoly TLS 1.0 a TLS 1.1 na ATA Gateway (nebo Lightweight Gateway) neaktivní, bráně se nepodaří registrace do ATA Center

### Není podporováno automatické obnovení certifikátu pro certifikáty používané službou ATA
Pokud používáte automatické obnovení certifikátů, služba ATA může po automatickém obnovení jejího certifikátu přestat fungovat. 


## Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizace ATA na verzi 1.7 – průvodce migrací](ata-update-1.7-migration-guide.md)




<!--HONumber=Sep16_HO2-->



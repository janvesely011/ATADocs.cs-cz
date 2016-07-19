---
title: "Nejčastější dotazy k ATA | Microsoft Advanced Threat Analytics"
description: "Seznam nejčastějších dotazů týkajících se ATA a související odpovědi"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: bb6bc2bf0d0df3112ecfdb33c8e9d6e41f183145


---

# Nejčastější dotazy k ATA
Tento článek obsahuje seznam nejčastějších dotazů týkajících se ATA a poskytuje podrobné informace a odpovědi.


## Jak se ATA licencuje?
Informace o licencování najdete v tématu [Jak koupit Advanced Threat Analytics](https://www.microsoft.com/server-cloud/products/advanced-threat-analytics/Purchasing.aspx).


## Co mám dělat, když se ATA Gateway nespustí?
Podívejte se na poslední chybu v aktuálním protokolu chyb (ve složce Logs tam, je software ATA nainstalovaný).
## Jak se dá ATA otestovat?
Pomocí jedné z následujících akcí můžete simulovat podezřelé aktivity a provést tak kompletní test:

1.  Rekognoskace DNS s využitím Nslookup.exe
2.  Vzdálené spuštění s využitím psexec.exe


To je potřeba spustit vzdáleně nikoli z komponenty ATA Gateway, ale nad monitorovaným řadičem domény.

## Jak ověřím předávání událostí systému Windows?
Z příkazového řádku v adresáři můžete spustit tento příkaz: **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**:

        mongo ATA --eval "printjson(db.getCollectionNames())" | find /C "NtlmEvents"`
## Funguje ATA při šifrovaném provozu?
Šifrovaný provoz se nebude analyzovat (příklad: LDAPS, IPSEC ESP).
## Funguje ATA s obranou protokolu Kerberos?
ATA podporuje povolení obrany protokolu Kerberos, která se také označuje jako architektura FAST (Flexible Authentication Secure Tunneling). Výjimkou je detekce typu over-pass-the-hash, která nebude fungovat.
## Kolik komponent ATA Gateways budu potřebovat?

Za prvé se doporučuje použít ATA Lightweight Gateway pro všechny řadiče domény, které to umožňují. Potřebné informace najdete v části [Velikosti pro ATA Lightweight Gateway](/advanced-threat-analytics/plan-design/ata-capacity-planning#ata-lightweight-gateway-sizing). 

Pokud se všechny řadiče domény dají pokrýt komponentami ATA Lightweight Gateway, žádné ATA Gateway nejsou potřeba.

Pokud máte řadiče domény, které nejde pokrýt komponentami ATA Lightweight Gateway, při rozhodování o tom, kolik komponent ATA Gateway budete potřebovat, vezměte v úvahu tyto aspekty:

 - Celkový objem provozu, které vaše řadiče domény produkují, a také síťovou architekturu (kvůli konfiguraci zrcadlení portů). Další informace o způsobu určení, kolik provozu vaše řadiče domény produkují, najdete v tématu [Odhad provozu řadiče domény](/advanced-threat-analytics/plan-design/ata-capacity-planning#Domain-controller-traffic-estimation).
 - To, kolik komponent ATA Gateway budete potřebovat k podpoře všech řadičů domény, určují také provozní omezení pro zrcadlení portů. Může to být například podle přepínačů, podle datových center nebo podle oblastí – každé prostředí má svá specifika. 

## Jak velké úložiště budu pro ATA potřebovat?
Pro jeden plný den s průměrem 1000 paketů/s budete potřebovat 0,3 GB úložiště.<br /><br />Další informace o určení velikosti pro ATA Center najdete v tématu [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).


## Proč se některé účty považují za citlivé?
Dojde k tomu, když je účet členem konkrétních skupin, které označujeme jako citlivé (například Domain Admins).

Pokud chcete pochopit, proč je účet citlivý, můžete zkontrolovat jeho členství ve skupinách a zjistit, do kterých citlivých skupin patří (skupina, do které patří, může být citlivá také kvůli jiné skupině, takže je potřeba celý proces opakovat tak dlouho, až zjistíte citlivou skupinu nejvyšší úrovně).

## Jak můžu ATA využít k monitorování virtuálního řadiče domény?
Většina virtuálních řadičů domény se dá pokrýt komponentami ATA Lightweight Gateway. K určení, jestli je komponenta ATA Lightweight Gateway pro vaše prostředí vhodná, použijte informace v tématu [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).

Pokud se virtuální řadič domény nedá pokrýt komponentou ATA Lightweight Gateway, můžete komponenty ATA Gateway mít virtuální nebo fyzické, jak popisuje téma [Konfigurace zrcadlení portů](/advanced-threat-analytics/deploy-use/configure-port-mirroring).  <br />Nejjednodušší je mít virtuální ATA Gateway na každém hostiteli, kde existují virtuální řadiče domény.<br />Pokud se virtuální řadiče domény přesunují mezi hostiteli, je třeba provést jednu z následujících akcí:

-   Pokud se virtuální řadič domény přesune na jiného hostitele, pro ATA Gateway na tomto hostiteli předem nakonfigurujte příjem provozu z nedávno přesunutého virtuálního řadiče domény.
-   Zkontrolujte, že jste virtuální ATA Gateway přidružili k virtuálnímu řadiči domény, takže pokud se přesune, ATA Gateway se přesune s ním.
-   Některé virtuální přepínače mohou odesílat provoz mezi hostiteli.

## Jak se ATA dá zálohovat?
Musí se zálohovat dvě věci:

-   Provoz a události, které ATA ukládá. K jejich zálohování se dá využít libovolná podporovaná procedura zálohování databází. Další informace najdete v tématu [Správa databází ATA](/advanced-threat-analytics/deploy-use/ata-database-management). 
-   Konfigurace ATA, která je uložena v databázi a automaticky se zálohuje každou hodinu. 

## Co ATA dokáže rozpoznat?
ATA rozpoznává známé nebezpečné útoky a techniky, problémy zabezpečení a rizika.
Úplný seznam toho, co ATA detekuje, najdete v tématu [Co je Microsoft Advanced Threat Analytics?](what-is-ata.md).

## Jaký druh úložiště budu pro ATA potřebovat?
Doporučujeme rychlé úložiště (nikoli disky s 7200 ot./min) s nízkými hodnotami latence (méně než 10 ms). Konfigurace RAID vy měla podporovat velkou zátěž při zápisu (nikoli RAID-5/6 nebo odvozené konfigurace).

## Kolik síťových karet ATA Gateway vyžaduje?
ATA Gateway vyžaduje minimálně dva síťové adaptéry:<br>1. Síťovou kartu pro připojení k interní síti a komponentě ATA Center<br>2. Síťovou kartu, která se použije pro zachycení síťového provozu na řadiči domény prostřednictvím zrcadlení portů<br>* To neplatí pro komponentu ATA Lightweight Gateway, která nativně využívá všechny síťové adaptéry využívané řadičem domény.

## Jaký druh integrace se systémy SIEM ATA využívá?
Se systémy SIEM ATA využívá obousměrnou integraci:

1. Pro případ podezřelých aktivit se v ATA dá nakonfigurovat odesílání výstrahy Syslog na libovolný server SIEM s využitím formátu CEF.
2. V ATA se dá nakonfigurovat příjem zpráv z [těchto systémů SIEM](/advanced-threat-analytics/deploy-use/configure-event-collection#siem-support) pro všechny události systému Windows s ID 4776.

## Může ATA monitorovat řadiče domény vizualizované ve vašem řešení IaaS?

Ano, ATA Lightweight Gateway se dá použít k monitorování řadičů domény, které jsou v libovolném řešení IaaS.

## Jedná se o místní nebo cloudovou nabídku?
Microsoft Advanced Threat Analytics je místní produkt.

## Bude součástí Azure Active Directory nebo místní služby Active Directory?
Toto řešení se v současnosti nabízí samostatně. Není součástí Azure Active Directory ani místní služby Active Directory.

## Je potřeba psát vlastní pravidla a určovat prahové nebo základní hodnoty?
Microsoft Advanced Threat Analytics nevyžaduje vytváření pravidel ani prahových nebo základních hodnot a jejich následné vyladění. ATA analyzuje chování uživatelů, zařízení a prostředků a také jejich vzájemné vztahy. Dokáže rychle detekovat podezřelé aktivity a známé útoky. Tři týdny po nasazení ATA začne detekovat behaviorálně podezřelé aktivity. Naproti tomu známé útoky se zlými úmysly a problémy zabezpečení začne ATA detekovat bezprostředně po nasazení.

## Pokud už došlo k porušení zabezpečení, dokáže nástroj Microsoft Advanced Threat Analytics identifikovat neobvyklé chování?
Ano, i když se ATA nainstaluje až po porušení zabezpečení, dokáže rozpoznat podezřelé aktivity hackerů. ATA nejenom zkoumá chování uživatelů, ale současně se taky dívá na ostatní uživatele v organizační mapě zabezpečení. Pokud je chování útočníka během počáteční analýzy nestandardní, je identifikovaný jako „outlier“ a ATA bude toto nestandardní chování dál hlásit. ATA může dál detekovat podezřelou aktivitu, pokud se hacker pokusí ukrást přihlašovací údaje jiných uživatelů, třeba Pass-the-Ticket, nebo se pokusí provést vzdálené spuštění na jednom z řadičů domény.

## Využívají se přitom jenom přenosy služby Active Directory?
Kromě analýzy provozu služby Active Directory pomocí technologie hloubkové kontroly paketů ATA taky shromažďuje relevantní události ze služby SIEM (Security Information and Event Management) a na základě informací získaných ze služby Active Directory Domain Services vytváří profily entit. Pokud organizace nakonfiguruje předávání Protokolu událostí systému Windows, může ATA taky shromažďovat události z protokolů událostí.

## Co je zrcadlení portů?
Zrcadlení portů, které se taky označuje jako SPAN (Switched Port Analyzer), je metoda monitorování síťových aktivit. Pokud je zrcadlení portů povolené, přepínač odešle kopii všech síťových paketů zjištěných na jednom portu (nebo v celé síti VLAN) na jiný port, kde se tyto pakety dají analyzovat.

## Monitoruje ATA jenom zařízení připojená k doméně?
Ne. ATA monitoruje všechna zařízení v síti, která zpracovávají požadavky ověřování a autorizace pro službu Active Directory, včetně zařízení s jiným systémem než Windows a mobilních zařízení.

## Monitoruje ATA jak účty počítačů, tak uživatelské účty?
Ano. Vzhledem k tomu, že účty počítačů se (stejně jako ostatní entity) dají využít k provádění škodlivých aktivit, ATA monitoruje chování všech účtů počítačů a všechny ostatní entity v příslušném prostředí.

## Může ATA podporovat několik domén a doménových struktur?
Ve fázi obecné dostupnosti bude Microsoft Advanced Threat Analytics podporovat několik domén se stejnou hranicí doménové struktury. Doménová struktura samotná je skutečnou „hranicí zabezpečení“, takže poskytnutí vícedoménové podpory umožní našim zákazníkům zajistit 100% pokrytí jejich prostředí pomocí ATA.

## Dá se zjistit celkový stav nasazení?
Ano, můžete zobrazit celkový stav nasazení a taky konkrétní problémy související s konfigurací, možnostmi připojení atd. Když k nim dojde, dostanete upozornění.


## Viz také
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurace sběru událostí](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurace předávání událostí systému Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jun16_HO4-->



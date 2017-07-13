---
title: "Prošetření rekognoskace pomocí DNS | Dokumentace Microsoftu"
description: "Tento článek popisuje rekognoskaci pomocí DNS a poskytuje pokyny k prošetření, když ATA tuto hrozbu detekuje."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/4/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 436b96f679836060cfaf40f6be3b92cf96dc0e04
ms.sourcegitcommit: 4118dd4bd98994ec8a7ea170b09aa301a4be2c8a
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/05/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*

# Prošetření rekognoskace pomocí DNS
<a id="investigating-reconnaissance-using-dns" class="xliff"></a>

Pokud ATA ve vaší síti detekuje **rekognoskaci pomocí DNS** a zobrazí upozornění, pomůže vám tento článek toto upozornění prošetřit a zjistit, jak tento problém napravit.

## Co je rekognoskace pomocí DNS?
<a id="what-is-reconnaissance-using-dns" class="xliff"></a>

Upozornění na **rekognoskaci pomocí DNS** označuje, že nějaký neobvyklý hostitel pomocí podezřelých dotazů DNS (Domain Name System) provádí rekognoskaci vaší interní sítě.

DNS (Domain Name System) je služba implementovaná jako hierarchická distribuovaná databáze, která zajišťuje překlad názvů hostitelů a názvů domén. Názvy v databázi DNS tvoří hierarchickou stromovou strukturu, která se označuje jako obor názvů domény.
Pro nežádoucí osobu obsahuje DNS cenné informace sloužící ke zmapování interní sítě včetně seznamu všech serverů a často také klientů přiřazených k příslušným IP adresám. Tyto informace jsou cenné také kvůli tomu, že obsahují názvy hostitelů, které jsou v daném síťovém prostředí často popisné. Při získání těchto informací tak může nežádoucí osoba během kampaně lépe zaměřit své úsilí na relevantní entity. Funkce pro zjišťování hostitelů pomocí rekognoskace DNS poskytují nástroje typu [Nmap](https://nmap.org/), [Fierce](https://github.com/mschwager/fierce) a předinstalované nástroje jako [Nslookup](https://technet.microsoft.com/library/cc725991(v=ws.11).aspx).
Detekce rekognoskace pomocí dotazů DNS od některého interního hostitele je příčinou znepokojení a svědčí o možnosti napadení existujícího hostitele, rozsáhlejším napadení sítě nebo možném útoku zevnitř.

## Typy dotazů DNS
<a id="dns-query-types" class="xliff"></a>

Protokol DNS obsahuje několik typů dotazů. ATA detekuje žádosti AXFR (přenos) a při jejich existenci vytvoří upozornění. Tento typ dotazu by měl pocházet jen od serverů DNS.

## Zjištění útoku
<a id="discovering-the-attack" class="xliff"></a>

Když se útočník pokusí provést rekognoskaci pomocí DNS, ATA ji detekuje a označí střední závažností.

![ATA detekuje rekognoskaci pomocí DNS](./media/dns-recon.png)
 
ATA zobrazí název zdrojového počítače a další podrobnosti o skutečném dotazu DNS, který byl proveden. Od stejného hostitele může například pocházet několik pokusů.

## Prošetření
<a id="investigating" class="xliff"></a>

Při prošetřování rekognoskace pomocí DNS musíte nejprve určit příčinu těchto dotazů. Mohou spadat do jedné z následujících kategorií: 
-   Pravdivě pozitivní – ve vaší síti je útočník nebo škodlivý malware. Může se jednat o útočníka, který prolomil hranici sítě, nebo o útok zevnitř.
-   Neškodné pravdivě pozitivní – může se jednat o upozornění aktivované testováním průniku, činností zásahového týmu, kontrolou zabezpečení, firewallem nové generace nebo správci IT provádějícími schválené aktivity.
-   Falešně pozitivní – upozornění se mohou zobrazovat kvůli chybné konfiguraci, například pokud je mezi komponentou ATA Gateway a serverem DNS zablokovaný port 53 (nebo kvůli jinému síťovému problému).

Následující graf vám pomůže určit kroky, které byste při prošetřování měli učinit:

![Řešení rekognoskace DNS pomocí ATA](./media/dns-recon-diagram.png)
 
1.  První krok spočívá v identifikaci počítače, ze kterého upozornění pochází, jak je znázorněno níže:
 
    ![Zobrazení podezřelé aktivity rekognoskace DNS v ATA](./media/dns-recon-2.png)
2.  Zjistěte, o jaký počítač se jedná. Je to pracovní stanice, server, pracovní stanice správce, stanice pro testování průniku apod.?
3.  Pokud je tento počítač serverem DNS a má opravdu právo požadovat sekundární kopii zóny, je tato aktivita falešně pozitivní. Pokud najdete falešně pozitivní aktivitu, použijte možnost **Vyloučit**, abyste od tohoto počítače už nedostali toto konkrétní upozornění.
4. Ověřte, že je mezi komponentou ATA Gateway a serverem DNS otevřený port 53.
4.  Pokud se počítač používá ke správcovským činnostem nebo testování průniku, jedná se o neškodnou pravdivě pozitivní událost a dotyčný počítač lze také nakonfigurovat jako výjimku.
5.  Pokud se nepoužívá k testování průniku, zjistěte, jestli v počítači neběží kontrola zabezpečení nebo firewall nové generace, které mohou vydávat žádosti DNS typu AXFR.
6.  Pokud nejsou splněna žádná z těchto kritérií, může být tento počítač napadený a je potřeba ho kompletně prošetřit. 
7.  Pokud jsou dotazy izolované na konkrétní počítače a nepovažují se za neškodné, měli byste učinit následující kroky:
    1.  Zkontrolujte dostupné zdroje protokolů. 
    2.  Proveďte analýzu založenou na hostiteli. 
    3.  Pokud tato aktivita nepochází od podezřelého uživatele, mělo by se forenzní analýzou počítače zjistit, jestli není napadený malwarem.

## Následné prošetření
<a id="post-investigation" class="xliff"></a>

Mezi malware použitý k napadení hostitele mohou patřit trojské koně instalující zadní vrátka. Při zjištění úspěšného laterálního pohybu od napadeného hostitele by se nápravné akce měly rozšířit také na tyto hostitele, a to včetně změny všech hesel a přihlašovacích údajů na tomto hostiteli a všech hostitelích zahrnutých do laterálního pohybu. 

Pokud po nápravných krocích nelze potvrdit, že je postižený hostitel čistý, nebo pokud původní příčinu nelze identifikovat, doporučuje Microsoft zálohovat kritická data a tento hostitelský počítač znovu sestavit. Před umístěním do sítě by se mělo posílit zabezpečení nových nebo znovu sestavených hostitelů, aby nedošlo k jejich opětovné infekci. 

Microsoft doporučuje využívat profesionální tým Incident Response & Recovery, který můžete kontaktovat prostřednictvím svého týmu účtu Microsoft, aby vám pomohl zjistit, jestli útočník ve vaší síti nenasadil vytrvalé metody.

## Zmírnění dopadů
<a id="mitigation" class="xliff"></a>

Interní server DNS lze proti rekognoskaci pomocí DNS zabezpečit zakázáním nebo omezením přenosů zóny jen na konkrétní IP adresy. Další informace o omezení přenosů zóny najdete v článku [Omezení přenosů zóny](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx) pro Windows Server na Technetu. Omezené přenosy zóny lze dále uzamknout [zabezpečením přenosů zóny protokolem IPsec](https://technet.microsoft.com/library/ee649192(v=ws.10).aspx). Úprava přenosů zóny je jedním z úkolů na kontrolním seznamu, pomocí kterého byste měli své [servery DNS zabezpečit proti interním a externím útokům](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).



## Viz také
<a id="see-also" class="xliff"></a>
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

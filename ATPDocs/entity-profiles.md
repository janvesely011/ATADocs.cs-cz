---
title: Práce s profily uživatelů na portálu Azure Advanced Threat Protection | Microsoft Docs
description: Popisuje, jak prozkoumat uživatele z obrazovky profily uživatelů na portálu Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 17458706-79fb-4c23-aa42-66979164a45f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0bff9c9081951c234d2d0076d154a984898a0a31
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71004486"
---
# <a name="understanding-entity-profiles"></a>Principy profilů entit

> [!NOTE]
> Funkce ATP Azure, které jsou na této stránce popsané, jsou dostupné taky pomocí nového [portálu](https://portal.cloudappsecurity.com).

Profil entity poskytuje ucelenou stránku entit navrženou pro úplné podrobně vyšetřování uživatelů, počítačů, zařízení, prostředků, ke kterým mají přístup, a jejich historii. Stránka Profile využívá nový překladač logických aktivit Azure ATP, který se může podívat na skupinu aktivit, ke kterým dochází (agregované až do minut), a seskupovat je do jedné logické aktivity, která vám poskytne lepší přehled o skutečných činnostech Vaše uživatelé.

Chcete-li získat přístup na stránku profilu entity, klikněte na název entity, například uživatelské jméno, do časové osy podezřelé aktivity.

V nabídce vlevo najdete všechny informace o službě Active Directory, které jsou k dispozici v e-mailové adrese entity, doméně, datum prvního dne. Pokud je entita citlivá, dozvíte se, proč. Například je uživatel označený jako citlivý nebo členem citlivé skupiny?
Pokud se jedná o citlivého uživatele, uvidíte ikonu pod jménem uživatele.

## <a name="view-entity-activities"></a>Zobrazit aktivity entit

Chcete-li zobrazit všechny aktivity provedené uživatelem nebo provést u entity, klikněte na kartu **aktivity** . 

 ![aktivity uživatelského profilu](media/user-profile-activities.png)

Ve výchozím nastavení se v hlavním podokně profilu entity zobrazuje časová osa aktivit entit s historií až šesti měsíců zpět, ze které můžete také procházet k entitám, ke kterým uživatel přistupoval, nebo pro entity.

V horní části si můžete zobrazit souhrnnou dlaždici, která vám poskytne rychlý přehled o tom, co je třeba pochopit, kolik počítačů se uživateli přihlásilo, kolik prostředků bylo k dispozici a kde se uživatel přihlásil k síti VPN (Pokud je nakonfigurované). . 

Pomocí tlačítka **filtrovat podle** nad časovou osou aktivity můžete filtrovat aktivity podle typu aktivity. Můžete také vyfiltrovat konkrétní typ aktivity s vysokou úrovní platnosti. To je užitečné pro šetření, pokud chcete pochopit základy toho, co entita dělá v síti. Můžete také přejít na konkrétní datum a exportovat aktivity jako filtrované do aplikace Excel. Exportovaný soubor poskytuje stránku pro změny adresářové služby (věci, které se změnily ve službě Active Directory pro účet), a samostatnou stránku pro aktivity. 

## <a name="view-directory-data"></a>Zobrazit data adresáře

Karta **data adresáře** poskytuje statické informace, které jsou k dispozici ve službě Active Directory, včetně příznaků zabezpečení řízení přístupu uživatele. Azure ATP taky zobrazuje členství ve skupině pro uživatele, abyste mohli zjistit, jestli má uživatel přímé členství nebo rekurzivní členství. V případě skupin Azure ATP seznam členů skupiny.

 ![data adresáře profilu uživatele](media/user-profile-dir-data.png)

V části **řízení přístupu uživatele** jsou nastavení zabezpečení plochy Azure ATP, která můžou potřebovat vaše pozornost. Můžete vidět důležité příznaky uživatele, například pokud uživatel může stisknutím klávesy ENTER obejít heslo, a pokud má uživatel heslo, které nikdy nevyprší, atd. 

## <a name="view-lateral-movement-paths"></a>Zobrazit cesty bočního pohybu

Kliknutím na kartu cesty přesunu si můžete zobrazit úplnou dynamickou a možnost, která je k dispozici, která vám poskytne vizuální znázornění cest mezi okraji a s tímto uživatelem, které se dají použít k infiltrování sítě.

Mapa poskytuje seznam toho, kolik segmentů směrování mezi počítači nebo uživateli by útočník musel a od tohoto uživatele musel napadnout citlivý účet, a pokud má uživatel citlivý účet, můžete zjistit, kolik prostředků a účtů je přímo připojeno.

Pokud se pro entitu během posledních dvou dnů nezjistil potenciální LMP, graf se nezobrazí. Vyberte jiné datum pomocí **zobrazení jiného data** pro zobrazení předchozích cest přesunu, které jsou zjišťovány pro tuto entitu. [Sestava dráhy bočního pohybu](reports.md) je vždy k dispozici, aby vám poskytovala informace o možných zjištěných cestách při přesunu a bylo je možné přizpůsobit podle času.  

Další informace najdete v části [přepravní cesty](use-case-lateral-movement-path.md). 

 ![cesty k příčnému pohybu profilu uživatele](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Viz také

- [Prošetřování laterálních průnikových tras pomocí služby Azure ATP](use-case-lateral-movement-path.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

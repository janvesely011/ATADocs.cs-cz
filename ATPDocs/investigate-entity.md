---
title: Jak prozkoumat uživatele a počítače pomocí služby Azure ATP | Microsoft Docs
description: Popisuje, jak prozkoumat podezřelé aktivity prováděné uživateli, entitami, počítači nebo zařízeními pomocí Azure Advanced Threat Protection (ATP).
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6144f9f35e8ee3b7cec4b7522fe03a6a3e8673b0
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71004744"
---
# <a name="tutorial-investigate-an-entity"></a>Návodu Prozkoumat entitu

> [!NOTE]
> Funkce ATP Azure, které jsou na této stránce popsané, jsou dostupné taky pomocí nového [portálu](https://portal.cloudappsecurity.com).

V tomto kurzu se dozvíte, jak prozkoumat entity připojené k podezřelým aktivitám zjištěným službou Azure Advanced Threat Protection (ATP). Po zobrazení výstrahy zabezpečení na časové ose se dozvíte, jak přejít k podrobnostem o entitě, která je součástí výstrahy, a pomocí následujících parametrů a podrobností získat další informace o tom, co se stalo a co potřebujete k omezení rizika.

> [!div class="checklist"]
> * Ověřte profil entity
> * Kontrolovat značky entit
> * Kontrola příznaků řízení uživatelských účtů
> * Křížové kontroly v programu Windows Defender
> * Sledujte, jak citliví uživatelé a skupiny mají oči
> * Kontrola potenciálních cest pohybu
> * Zkontroluje stav honeytokenu.

## <a name="check-the-entity-profile"></a>Ověřte profil entity

Profil entity poskytuje komplexní stránku entity, která je navržená pro úplné podrobně vyšetřování uživatelů, počítačů, zařízení a prostředků, ke kterým mají přístup, spolu s jejich historií. Stránka Profile využívá nový překladač logických aktivit Azure ATP, který se může podívat na skupinu aktivit, ke kterým dochází (agregované až do minut), a seskupovat je do jedné logické aktivity, která vám poskytne lepší přehled o skutečných činnostech Vaše uživatelé.

Chcete-li získat přístup na stránku profilu entity, klikněte na název entity, jako je například uživatelské jméno, na časové ose výstrahy zabezpečení. Na stránce výstraha zabezpečení se zobrazí také zkrácená verze profilu entity, když najedete myší na název entity.

Profil entity umožňuje zobrazit aktivity entit, zobrazit data adresáře a zobrazit [cesty bočního pohybu](use-case-lateral-movement-path.md) pro danou entitu. Další informace o entitách najdete v tématu [Principy profilů entit ](entity-profiles.md).

## <a name="check-entity-tags"></a>Kontrolovat značky entit

Azure ATP vyžádá ze služby Active Directory značky, které vám poskytnou jedno rozhraní pro monitorování uživatelů a entit služby Active Directory. Tyto značky poskytují informace o entitě ze služby Active Directory, včetně:
- Částečné Tento uživatel, počítač nebo skupina nebyl synchronizován z domény a byl částečně vyřešen prostřednictvím globálního katalogu. Některé atributy nejsou k dispozici.
- Nevyřešené Tento počítač nebyl přeložen na platnou entitu v doménové struktuře služby Active Directory. K dispozici nejsou žádné informace o adresáři.
- Odstraňování Entita se odstranila ze služby Active Directory.
- Zakázáno: Entita je ve službě Active Directory zakázaná.
- Uzamčení Entita zadala nesprávné heslo příliš mnohokrát a je uzamčena.
- Vypršela Platnost entity vypršela ve službě Active Directory.
- New Entita byla vytvořena před méně než 30 dny.

## <a name="check-user-account-control-flags"></a>Kontrola příznaků řízení uživatelských účtů

Příznaky řízení uživatelských účtů se importují taky ze služby Active Directory. Data adresáře entit Azure ATP obsahují 10 příznaků, které jsou platné pro šetření: 
- Heslo je platné stále.
- Důvěryhodné pro delegování
- Karta smartcard požadována
- Platnost hesla vypršela.
- Prázdné heslo povoleno
- Heslo pro prostý text Uloženo
- Nedá se delegovat.
- Pouze šifrování DES
- Předběžné ověření protokolu Kerberos se nevyžaduje.
- Účet zakázán 

Azure ATP vám umožní zjistit, jestli jsou tyto příznaky zapnuté nebo vypnuté v Azure Active Directory. Barevné ikony a odpovídající přepínače označují stav každého příznaku. V následujícím příkladu je ve službě Active Directory zapnuto pouze heslo, které je stále **platné** .

 ![příznaky řízení uživatelských účtů](./media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>Křížové kontroly v programu Windows Defender

V rámci poskytování přehledů pro různé produkty poskytuje váš profil entity entity, které mají v programu Windows Defender otevřené výstrahy s označením. Tato výzva vám umožní zjistit, kolik otevřených upozornění má entita ve Windows Defenderu, a jaká je jejich úroveň závažnosti. Klikněte na BADGE a přejděte přímo k výstrahám souvisejícím s touto entitou v programu Windows Defender.


## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>Sledujte, jak citliví uživatelé a skupiny mají oči

Azure ATP importuje informace o uživatelích a skupinách z Azure Active Directory a umožňuje určit, kteří uživatelé se automaticky považují za citlivé, protože jsou členy následujících skupin ve službě Active Directory:

-   Správci
-   Power Users
-   Account Operators
-   Server Operators
-   Print Operators
-   Backup Operators
-   Replicators
-   Remote Desktop Users 
-   Network Configuration Operators 
-   Incoming Forest Trust Builders
-   Domain Admins
-   Domain Controllers
-   Group Policy Creator Owners 
-   Řadiče domény jen pro čtení 
-   Podnikové řadiče domény jen pro čtení 
-   Schema Admins 
-   Enterprise Admins

Kromě toho můžete **ručně označit** entity jako citlivé v rámci služby Azure atp. To je důležité, protože některé detekce ATP Azure, jako je detekce změny citlivé skupiny a cesta k postrannímu pohybu, spoléhají na stav citlivosti entity. Pokud ručně označíte další uživatele nebo skupiny jako citlivé, jako jsou například členové Rady, vedoucí společnosti a prodejní ředitelé, Azure ATP bude považovat za citlivé. Další informace najdete v tématu [práce s citlivými účty](sensitive-accounts.md).

## <a name="review-lateral-movement-paths"></a>Kontrola cest bočního pohybu

Azure ATP vám může pomáhat zabránit útokům, které používají cesty bočního pohybu. Příčný pohyb je v případě, že útočník proaktivně používá necitlivé účty k získání přístupu k citlivým účtům.

Pokud pro entitu existuje cesta bočního pohybu, na stránce profil entity budete moci kliknout na kartu **cesty přesunu** . Diagram, který se zobrazí, vám poskytne mapu možných cest k vašemu citlivému uživateli. 

Další informace najdete v tématu [prozkoumání cest po přesunu s využitím Azure ATP](use-case-lateral-movement-path.md).

## <a name="check-honeytoken-status"></a>Zkontroluje stav honeytokenu.

Před přesunutím do šetření je důležité zjistit, jestli je entita honeytokenu. Účty a entity můžete označit jako honeytokens ve službě Azure ATP. Když otevřete profil entity nebo zkrácený profil účtu nebo entity, které jste označili jako honeytokenu, zobrazí se výzva honeytokenu. Při šetření honeytokenu upozorňuje, že aktivita v rámci revize byla provedena účtem, který jste označili jako honeytokenu.

## <a name="see-also"></a>Viz také:

- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

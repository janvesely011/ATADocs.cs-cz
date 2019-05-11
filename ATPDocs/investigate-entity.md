---
title: Zkoumání uživatelé a počítače pomocí ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Popisuje, jak prozkoumat podezřelé aktivity prováděné uživateli, entity, počítače nebo zařízení pomocí Azure Advanced Threat Protection (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/3/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4868282aaf5dc45c5f25740e26d6c3c7f0403952
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65193564"
---
# <a name="tutorial-investigate-an-entity"></a>Kurz: Prozkoumat entity

V tomto kurzu dozvíte, jak zkoumat entity, které jsou připojené k podezřelým aktivitám zjistil pomocí Azure Advanced Threat Protection (ATP). Po zobrazení výstrahy zabezpečení na časové ose, se dozvíte, jak procházet entity účastnící se upozornění a použít následující parametry a podrobnosti se dozvíte více o co se stalo a co potřebujete dělat pro zmírnění rizika.

> [!div class="checklist"]
> * Zkontrolujte profil entity
> * Zaškrtněte značky entit
> * Zkontrolujte řídicí příznaky účtu uživatele
> * Zkontrolovat pomocí Windows Defenderu
> * Přehled o citlivé uživatele a skupiny
> * Projděte si potenciální cesty taktiky Lateral Movement
> * Kontrola stavu honeytokenu

## <a name="check-the-entity-profile"></a>Zkontrolujte profil entity

Na stránce komplexní entity navržena pro celý podrobný rozbor šetření uživatelů, počítačů, zařízení a prostředky, ke kterým mají přístup k spolu s jejich historie vám poskytne profil entity. Na stránce Profil využívá výhod nových překladač logické aktivity ochrany ATP v programu Azure, který můžete podívat na skupinu aktivit, ke kterým dochází (agregované až minutu) a seskupovat je do jedné logické aktivity umožňují lépe pochopit skutečné aktivity vaši uživatelé.

Chcete-li získat přístup stránku profil entity, klikněte na název sady entit, jako je například uživatelské jméno na časové ose výstrah zabezpečení. Uvidíte také zkrácenou verzi profil entity na stránce výstrah zabezpečení podržením ukazatele nad název entity.

Profil entity, které vám umožní zobrazit entity aktivity, data zobrazení adresáře a zobrazení [laterální pohyb cesty](use-case-lateral-movement-path.md) entity. Další informace o entitách, naleznete v tématu [Principy profily entit ](entity-profiles.md).

## <a name="check-entity-tags"></a>Zaškrtněte značky entit

Ochrana ATP v programu Azure si vyžádá značky z Active Directory a poskytují tak jednotné rozhraní pro monitorování uživatelů služby Active Directory a entity. Tyto značky poskytují informace o entitě ze služby Active Directory, včetně:
- Částečné: Tento uživatel, počítač nebo skupina se nesynchronizovali z domény a částečně se určili pomocí globálního katalogu. Některé atributy nejsou k dispozici.
- Nerozpoznané: Tento počítač se nepodařilo přeložit na platný entitu v doménové struktuře služby active directory. Nejsou dostupné žádné informace adresáře.
- Odstranit: Byla entita odstraněna ze služby Active Directory.
- Zakázáno: Entita je zakázaný ve službě Active Directory.
- Uzamčení: Entita příliš mnohokrát zadala chybné heslo a je uzamčen.
- Vypršela platnost: Platnost entity ve službě Active Directory.
- Nové: Se entita vytvořila před méně než 30 dny.

## <a name="check-user-account-control-flags"></a>Zkontrolujte řídicí příznaky účtu uživatele

Řídicí příznaky účtu uživatele budou importovány také ze služby Active Directory. Azure data adresáře ochrany ATP v programu entity obsahují 10 příznaky, které platí pro zkoumání: 
- Platnost hesla nikdy nevyprší
- Důvěryhodné pro delegaci
- Vyžaduje se čipová karta
- Vypršení platnosti hesla
- Prázdné heslo je povolené.
- Heslo jako prostý text
- Není možné delegovat
- Jen šifrování DES
- Předběžné ověření Kerberos se nevyžaduje
- Zakázaný účet 

Ochrana ATP v programu Azure vám umožňuje vědět, pokud jsou tyto příznaky zapnutí nebo vypnutí v Azure Active Directory. Barevnými ikonami a odpovídající přepínač informací o stavu všech příznaků. V níže uvedeném příkladu, pouze **platnost hesla nikdy nevyprší** nachází ve službě Active Directory.

 ![příznaky ovládacích prvků uživatelského účtu](./media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>Zkontrolovat pomocí Windows Defenderu

Váš profil entity poskytují přehledy mezi produkty, obsahuje entity, které mají otevřených upozornění v programu Windows Defender s odznáčkem. Tato oznámení "BADGE" vám umožňuje vědět, kolik otevřených upozornění entity má v programu Windows Defender a jaká je jejich úroveň závažnosti. Klikněte na oznámení "BADGE" můžete přejít přímo na výstrahy související s touto entitou v programu Windows Defender.


## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>Přehled o citlivé uživatele a skupiny

Ochrana ATP v programu Azure importuje uživatele a skupiny informace ze služby Azure Active Directory umožňuje určit, kteří uživatelé jsou automaticky považují za citlivé protože jsou členy z těchto skupin ve službě Active Directory:

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
-   Enterprise Read-only Domain Controllers 
-   Schema Admins 
-   Enterprise Admins

Kromě toho můžete **ručně označit** entity jako citlivé v rámci ochrany ATP v programu Azure. To je důležité, protože některé detekce ochrany ATP v programu Azure, jako je například zjišťování úpravy citlivých skupin a cesty laterální pohyb, závisí na citlivosti stavu entity. Pokud ručně označíte další uživatele nebo skupiny jako citlivé, jako je například členů vedení společnosti a prodejní ředitele, ochrana ATP v programu Azure bude zvažovat je citlivé. Další informace najdete v tématu [práce s citlivými účty](sensitive-accounts.md).

## <a name="review-lateral-movement-paths"></a>Projděte si cesty taktiky Lateral Movement

Ochrana ATP v programu Azure vám mohou pomoci zabránit útokům, které používají cesty taktiky Lateral Movement. Laterální pohyb je, když útočník proaktivně pomocí tohoto počtu účtů pro přístup k citlivým účtům.

Pokud existuje cesty laterální pohyb entity, na stránce profil entity, bude možné kliknout **laterální pohyb cesty** kartu. Diagram, který se zobrazí poskytuje mapování z možných cest pro citlivé uživatele. 

Další informace najdete v tématu [cesty taktiky Lateral Movement Investigating pomocí služby Azure ATP](use-case-lateral-movement-path.md).

## <a name="check-honeytoken-status"></a>Kontrola stavu honeytokenu

Teprve potom přejděte vaše šetření je důležité vědět, jestli je entita honeytokenu. Účty a entity můžete označit jako honeytokens v ochrany ATP v programu Azure. Při otevření profil entity nebo zkrácený profil entity, které jste označili jako honeytokenu nebo účet, zobrazí se Odznáček honeytokenu. Při zkoumání, honeytoken oznámení vás upozorní, že se pomocí účtu, který jste označili jako honeytokenu provedla aktivita probíhá kontrola.

## <a name="see-also"></a>Viz také:

- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

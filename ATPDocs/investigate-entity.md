---
title: Jak prozkoumat uživatelé a počítače s Azure ATP | Microsoft Docs
description: Popisuje, jak prozkoumat podezřelé aktivity uživatelů, entit, počítače nebo zařízení pomocí Azure Advanced Threat Protection (ATP)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/6/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4ef4151a311dd5b076737cba9f3c7aa7454a32a7
ms.sourcegitcommit: 39a1ddeb6c9dd0817f92870b711627350b7f6f03
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/08/2018
---
*Platí pro: Azure Advanced Threat Protection verze 1.9*



# <a name="investigate-an-entity-with-azure-atp"></a>Prozkoumat entity s Azure ATP

Tento článek popisuje proces pro zkoumání entity po podezřelé aktivity se zjistily s Azure Advanced Threat Protection (ATP). Po zobrazení podezřelou aktivitu v časové ose, můžete rozbalit entity účastní aktivity a pomocí následujících parametrů a podrobnosti o další informace o problému a co musíte udělat pro zmírnění rizik.

## <a name="look-at-the-entity-profile"></a>Podívejte se na profil entity

Profil entity poskytuje komplexní entity stránka s navržené pro úplné přímým – podrobnější prošetření uživatelů, počítačů, zařízení a prostředky, které mají přístup a jejich historii. Stránka profilu využívá výhod nového překladač logické aktivity Azure ATP, který můžete prohlížet skupinu aktivit, ke kterým dochází (agregované až několik minut) a seskupovat je do jedné logické aktivity umožňují lépe porozumět skutečné aktivity vaši uživatelé.

Pro přístup k stránku profil entity, klikněte na název entity, jako je například uživatelské jméno v časové osy podezřelých aktivit. Zkrácená verze na stránce podezřelých aktivit profilu entity také zobrazí ukazatele myši na název entity.

Profil entity umožňuje zobrazit aktivity entity, zobrazení dat adresáře a zobrazit laterální pohyb cesty pro entitu. Další informace najdete v tématu [příčin profily entit ](entity-profiles.md).

## <a name="check-entity-tags"></a>Zaškrtněte značky entity

Azure ATP vrátí značky ze služby Active Directory tak, abyste získali jednotné rozhraní pro monitorování uživatelů služby Active Directory a entity. Tyto značky poskytují informace o entitě ze služby Active Directory, včetně:
- Částečné: Tento uživatel, počítač nebo skupina nebyl synchronizované z domény a částečně vyřešila prostřednictvím globálního katalogu. Některé atributy nejsou k dispozici.
- Nerozpoznané: Tento počítač nebyl přeložit na platný entity v doménové struktuře služby active directory. Nejsou dostupné žádné informace adresáře.
- Odstraněné: Entita byla odstraněna ze služby Active Directory.
- Zakázáno: Entita je zakázána ve službě Active Directory.
- Uzamčena: Entita zadali nesprávné heslo příliš mnoho pokusů a uzamčeno.
- Vypršela platnost: Entita vypršela ve službě Active Directory.
- Nové: Byla vytvořena entita před méně než 30 dní.

## <a name="look-at-the-user-access-control-flags"></a>Podívejte se na příznaky ovládacích prvků přístupu uživatele

Příznaky ovládacích prvků přístupu uživatele se importují také ze služby Active Directory. Azure ATP zahrnuje 10 příznaky, které jsou platné pro šetření: 
- Heslo je platné stále
- Důvěryhodný pro delegování
- Požadované čipová karta
- Platnost hesla
- Prázdné heslo povoleno
- Uložená hesla ve formátu prostého textu
- Není možné delegovat
- Pouze šifrování DES
- Předběžné ověřování protokolu Kerberos není vyžadována
- Účet zakázán 

Azure ATP umožňuje vědět, pokud tyto příznaky jsou zapnout nebo vypnout v Azure Active Directory. Barevné ikony znamenat, že příznak na ve službě Active Directory; v příkladu níže, pouze **účet zakázán** je na ve službě Active Directory.

 ![příznaky ovládacích prvků přístupu uživatele](./media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>Zkontrolovat s programem Windows Defender

Abyste měli přehled smíšený produkt, poskytuje váš profil entity entity, které mají otevřené výstrahy v programu Windows Defender s oznámení "BADGE". Tato oznámení "BADGE" umožňuje sledovat, kolik otevřené výstrahy entita, která má v programu Windows Defender a jaké jsou jejich úroveň závažnosti. Kliknutím na oznámení "BADGE" přejít přímo na výstrahy související s touto entitou v programu Windows Defender.


## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>Dohlížet na citlivé uživatelů a skupin

Azure ATP importuje uživatele a informace o skupině z Azure Active Directory, které umožňují určit, kteří uživatelé jsou automaticky považovány za citlivé vzhledem k tomu, že jsou členy z těchto skupin ve službě Active Directory:

-   Administrators
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
-   Řadiče domény jen pro čtení Enterprise 
-   Schema Admins 
-   Enterprise Admins

Kromě toho můžete **ručně označit** entity jako citlivé v rámci Azure ATP. To je důležité, protože některé detekce, Azure ATP, jako je detekce úpravy citlivou skupinu a cestu laterální pohyb, závisí na stavu entity velkých a malých písmen. Můžete ručně označit další uživatele nebo skupiny jako citlivé informace, například členů vedení společnosti a ředitel prodeje, Azure ATP bude považovat je citlivé. Další informace najdete v tématu [práce s citlivé účty](sensitive-accounts.md).

## <a name="be-aware-of-lateral-movement-paths"></a>Mějte na paměti laterální pohyb cest

Azure ATP můžete zabránit útokům, které používají laterální pohyb cesty. Laterální pohyb je, když útočník aktivně používá necitlivých účty pro přístup k citlivým účtům.

Pokud neexistují laterální pohyb cesty pro entitu, na stránce profil entity nebudete moci kliknout na **pomoci odhalit laterální pohyb cesty** kartě. Diagram, který se zobrazí vám poskytne mapu možných cest pro vaše citlivé uživatele. 

Další informace najdete v tématu [Investigating laterální pohyb cesty s Azure ATP](use-case-lateral-movement-path.md).


## <a name="is-it-a-honeytoken-entity"></a>Je honeytokenu entity?

Před přesunete s šetření, je důležité vědět, zda je entita honeytokenu. Pro usnadnění vaší práce Azure ATP umožňuje značka účty a entity jako honeytokens. Potom během šetření, při otevření v profilu entity nebo zkrácený profil, zobrazí se oznámení "BADGE" honeytokenu vás upozorní, že aktivity, které se díváte byla provedena pomocí účtu, který jste označili jako honeytokenu.


    
## <a name="see-also"></a>Viz také

- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
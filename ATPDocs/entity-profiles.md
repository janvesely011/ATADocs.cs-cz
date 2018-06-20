---
title: Práce s profily uživatelů na portálu Azure Advanced Threat Protection prostoru | Microsoft Docs
description: Popisuje, jak prozkoumat uživatelé z obrazovky profily uživatelů na portálu Azure ATP pracovního prostoru
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 17458706-79fb-4c23-aa42-66979164a45f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6ceefeeba6a52abf5da7ff44135cff55e9beab02
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446068"
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="investigating-entity-profiles"></a>Zkoumání profily entit

Profil entity poskytuje komplexní entity stránka s navržené pro úplné přímým – podrobnější prošetření uživatelů, počítačů, zařízení a prostředky, které mají přístup a jejich historii. Stránka profilu využívá výhod nového překladač logické aktivity Azure ATP, který můžete prohlížet skupinu aktivit, ke kterým dochází (agregované až několik minut) a seskupovat je do jedné logické aktivity umožňují lépe porozumět skutečné aktivity vaši uživatelé.

Pro přístup k stránku profil entity, klikněte na název entity, jako je například uživatelské jméno v časové osy podezřelých aktivit.

V levé nabídce poskytuje všechny služby Active Directory informace k dispozici u entity - e-mailovou adresu, domény, první zobrazené datum. Pokud je entita citlivé, zde zjistíte, proč. Například je uživatel označené jako velká a malá písmena nebo člen skupiny citlivé?
Pokud je citlivé uživatel, zobrazí ikonu v části uživatelské jméno.

## <a name="view-entity-activities"></a>Zobrazit entity aktivity

Zobrazit všechny aktivity prováděné uživateli nebo provést s entitou, klikněte na **aktivity** kartě. 

 ![aktivity profilu uživatele](media/user-profile-activities.png)

Ve výchozím nastavení zobrazí hlavním podokně profilu entity termín entity aktivit s historii až šest měsíců zpět, ze kterého můžete také přejít dolů do entity přístupu uživatelem, nebo pro entity, uživatelé, kteří přístup entity.

V horní části můžete zobrazit souhrn dlaždice, které získáte rychlý přehled toho, co je potřeba pochopit v přehledu o entitě – kolik počítačů uživatel přihlášen do, kolik měla přístup k prostředkům a umístění, ze kterých přihlášený uživatel do sítě VPN (Pokud je nakonfigurováno) . 

Pomocí **filtrovat podle** tlačítko výše časové ose aktivity můžete filtrovat aktivity podle typu aktivity. Můžete také filtrovat na konkrétní (aktivní) typ aktivity. To je užitečné pro šetření, když chcete pochopit základy toho, co je to entity v síti. Můžete také přejít na určité datum a aktivity můžete exportovat jako filtruje tak, aby aplikace Excel. Exportovaný soubor obsahuje na stránce pro změny directory services (věcí, které změnily ve službě Active Directory pro účet) a samostatné stránce pro aktivity. 

## <a name="view-directory-data"></a>Zobrazení dat adresáře

**Dat adresáře** karta poskytuje statické informace, které jsou k dispozici ze služby Active Directory, včetně příznaky zabezpečení ovládacích prvků přístupu uživatele. Azure ATP také zobrazuje členství ve skupinách pro uživatele tak, aby se dá zjistit, jestli má uživatel přímé členství nebo rekurzivní členství. Pro skupiny Azure ATP uvádí členy skupiny.

 ![data uživatelského profilu adresáře](media/user-profile-dir-data.png)

V **řízení přístupu uživatelů** část, nastavení zabezpečení povrchy Azure ATP, které může být nutné vaše attentions. Uvidíte důležité příznaky o uživateli, například můžete stiskněte klávesu uživatele zadejte obejít heslo, uživatel nemá heslo, které je platné stále atd. 

## <a name="view-lateral-movement-paths"></a>Zobrazení laterální pohyb cesty

Kliknutím na kartu laterální pohyb cesty, můžete zobrazit plně dynamické a můžete kliknout mapování, které vám poskytne vizuální reprezentace cesty laterální pohyb do a z tohoto uživatele, který slouží k proniknout vaší sítě.

Mapy vám poskytne seznam kolik směrování mezi počítačů nebo uživatelů útočník by mohl do a z tohoto uživatele k ohrožení citlivých účet, a pokud má uživatel zpřístupnění citlivých účtů, uvidíte kolik prostředky a účty jsou přímo připojené.

Pokud není zjištěna aktivita za poslední dva dny, už se zobrazí graf, ale [pomoci odhalit laterální pohyb cesta sestavy](reports.md) bude k dispozici pro poskytují informace o způsobech laterální pohyb za posledních 60 dní. 

Další informace najdete v tématu [pomoci odhalit laterální pohyb cesty](use-case-lateral-movement-path.md). 

 ![cesty laterální pohyb profilu uživatele](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Viz také

- [Prozkoumat laterální pohyb cesty s Azure ATP](use-case-lateral-movement-path.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
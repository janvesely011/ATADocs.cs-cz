---
title: Práce s profily uživatelů na portálu Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Popisuje, jak prozkoumat uživatelů z obrazovky profily uživatelů na portálu služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 12/02/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 17458706-79fb-4c23-aa42-66979164a45f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 76333f50bd911e17ba97a11e65a761ff88b31b4e
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58675179"
---
# <a name="understanding-entity-profiles"></a>Principy profily entit

Profil entity vám poskytne komplexní entity stránky navržené pro celý podrobný rozbor šetření uživatelů, počítačů, zařízení, prostředky, které mají přístup k a jejich historie. Na stránce Profil využívá výhod nových překladač logické aktivity ochrany ATP v programu Azure, který můžete podívat na skupinu aktivit, ke kterým dochází (agregované až minutu) a seskupovat je do jedné logické aktivity umožňují lépe pochopit skutečné aktivity vaši uživatelé.

Chcete-li získat přístup stránku profil entity, klikněte na název sady entit, jako je například uživatelské jméno na časové ose podezřelé aktivity.

V levé nabídce poskytuje všechny služby Active Directory informace k dispozici na entitu, e-mailovou adresu, domény, první zjištěný datum. Pokud subjektem rozlišuje velká a malá písmena, zjistíte, proč. Například uživatel označené jako citlivé nebo člen citlivou skupinu?
Pokud je citlivé uživatele, zobrazí ikonu v části uživatelské jméno.

## <a name="view-entity-activities"></a>Zobrazení entity aktivity

Zobrazit všechny aktivity prováděné uživateli, nebo provést u entity, klikněte na **aktivity** kartu. 

 ![aktivity profilu uživatele](media/user-profile-activities.png)

Ve výchozím nastavení zobrazí v hlavním podokně profil entity časová osa entity aktivity s historií až šest měsíců zpět, ze kterého můžete také přecházet do entity přistupovat uživatelem nebo pro entity, uživatelé, kteří přístup entity.

V horní části stránky můžete zobrazit souhrn dlaždic, které získáte rychlý přehled toho, co je potřeba pochopit v přehledu o vašich entitu, kolik počítačů uživatel přihlášen k získal přístup k tom, kolik prostředků a umístění, ze kterých přihlášený uživatel do sítě VPN (je-li konfigurováno) . 

Použití **filtrovat podle** tlačítko nad časové osy aktivity můžete filtrovat aktivity podle typu aktivity. Můžete také filtrovat konkrétní (hlučného) typu aktivity. To je užitečné k prošetření, když chcete pochopit základy toho, co dělá entity v síti. Můžete také přejít na konkrétní datum a jak jsou vyfiltrovaná do aplikace Excel můžete exportovat aktivity. Exportovaný soubor obsahuje stránky pro změny v adresáři služby (věci, které se změnily v Active Directory pro účet) a samostatnou stránku aktivity. 

## <a name="view-directory-data"></a>Zobrazení dat adresáře

**Data adresáře** karta obsahuje statické informace, které jsou k dispozici ze služby Active Directory, včetně příznaky zabezpečení ovládacích prvků přístupu uživatele. Ochrana ATP v programu Azure také zobrazí členství ve skupinách pro uživatele, takže můžete určit, zda uživatel má přímé členství nebo rekurzivní členství. Pro skupiny ochrany ATP v programu Azure uvádí členy skupiny.

 ![adresář data uživatelského profilu](media/user-profile-dir-data.png)

V **řízení uživatelských účtů** části, nastavení zabezpečení zařízení Surface ochrany ATP v programu Azure, které může být nutné vaše attentions. Můžete zobrazit důležité příznaky informace o uživateli, například když na uživatele můžete stisknutím klávesy enter obejít heslo, a pokud má uživatel heslo, které je platné stále atd. 

## <a name="view-lateral-movement-paths"></a>Zobrazení cesty taktiky Lateral Movement

Když kliknete na kartu cesty laterální pohyb, se zobrazí plně dynamického a kliknout, čímž mapu, která vám poskytne vizuální reprezentace cesty taktiky Lateral Movement do a z tohoto uživatele, které je možné na míru vaší sítě.

Mapa vám poskytne přehled o tom, kolik segmentů směrování mezi počítače nebo uživatelé útočník by mohl do a z tohoto uživatele k ohrožení citlivých účtů, a pokud má uživatel citlivých účtů, můžete zobrazit, kolik prostředky a účty jsou přímo připojené.

Pokud pro entitu nebyl zjištěn potenciální LMP během posledních dvou dní, graf se nezobrazí. Vyberte jiné datum pomocí **zobrazit jiné datum** zobrazení předchozích grafů cesty laterální pohyb zjištěných pro tuto entitu. [Laterální pohyb cesta sestavy](reports.md) je vždy k dispozici pro poskytování informací o potenciální cesty taktiky Lateral Movement, které jsou zjištěny a je možné přizpůsobit podle času.  

Další informace najdete v tématu [laterální pohyb cesty](use-case-lateral-movement-path.md). 

 ![cesty taktiky Lateral Movement profilu uživatele](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Viz také

- [Prošetřování laterálních průnikových tras pomocí služby Azure ATP](use-case-lateral-movement-path.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

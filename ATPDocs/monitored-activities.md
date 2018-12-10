---
title: Ochrana ATP v programu Azure monitorovat aktivity domény | Dokumentace Microsoftu
description: Popisuje jednotlivé typy aktivit sledováno rozšířené ochrany před internetovými útoky pro Azure
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 37d1a032-65e7-4a89-be0b-c3f9cc2bacdb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f8bc815c3ffad4f75d84a69f2e6c30cc0707d8e3
ms.sourcegitcommit: d1c9c3e69b196f6086a8f100e527553cf0d95aac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/10/2018
ms.locfileid: "53125026"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="azure-atp-monitored-activities"></a>Ochrana ATP v programu Sledování aktivitách v Azure

Azure Advanced Threat Protection monitoruje informace generují z vaší organizace služby Active Directory, síťových aktivit a aktivity událostí ke zjištění podezřelé aktivity. Informace o monitorované aktivity umožňuje ochrany ATP v programu Azure umožňují určit platnost každý potenciální hrozbu a správně posuzovat a reagovat. 

V případě platných hrozeb nebo **pravdivě pozitivní upozornění**, ochrana ATP v programu Azure vám umožňuje zjistit rozsah porušení zabezpečení pro každý incident, zjistěte entit, které se podílejí a zjistěte, jak je opravit.

Informace sledováno ochrany ATP v programu Azure se zobrazí ve formuláři aktivit. Ochrana ATP v programu Azure v současné době podporuje monitorování následující typy aktivit:

> [!NOTE] 
> - Tento článek je relevantní pro všechny typy senzoru služby Azure ATP.
>- Na stránce profilu počítače i uživatele se zobrazí Azure ochrany ATP v programu monitorovat aktivity. 
 

## <a name="monitored-user-activities-user-account-ad-attribute-changes"></a>Monitoruje aktivity uživatelů: atribut změny uživatelského účtu AD

|Monitorovaných aktivit|Popis|
|---------------------|------------------|
|Účet omezeného delegování stav se změnil |Stav účtu je teď zapnutá nebo vypnutá delegování.|
|Hlavní názvy služby omezené delegování změnu účtu | Omezené delegování omezuje služby, ke kterým může zadaný server fungovat jménem uživatele.|
|Zakázané změnu účtu |Označuje, zda je účet zakázána nebo povolena.|
|Platnost účtu vypršela.|Datum vypršení platnosti účtu.|
|Došlo ke změně doby vypršení platnosti účtu |Změňte na datum, kdy vyprší platnost účtu.|
|Účet uzamčen změněné|Změňte na datum, kdy vyprší platnost účtu.|
|Změnit heslo k účtu|Uživatel změnil heslo.|
|Platnost hesla účtu |Platnost hesla uživatele.|
|Změnit účet, že platnost hesla nikdy nevyprší |Heslo uživatele se změní na platnost nikdy nevypršela.|
|Provedení změny účtu není vyžadováno heslo |Účet uživatele byl změněn povolit přihlášení pomocí prázdné heslo.|
|Provedení změny účtu vyžaduje čipovou kartu  |Změny účtu budou muset uživatelé přihlásit k zařízení pomocí čipové karty.|
|Podporované typy šifrování změnit účet |Typy šifrování podporované protokolem Kerberos se změnila (typy: Des, AES 129, AES 256)|
|Změnit hlavní uživatelské jméno účtu  |Hlavní název uživatele byl změněn.|
|Změnit členství ve skupině  |Uživatel byl, přidání nebo odebrání, z ní, jiným uživatelem nebo samy o sobě.|
|Změnit e-mailu uživatele|Atribut e-mailu uživatele byl změněn.|
|Změnit správce uživatelů|Atribut uživatele správce se změnil.|
|Změnit telefonní číslo uživatele|Atribut telefonního čísla uživatele byl změněn.|
|Změnit pozice uživatele |Název atributu uživatele byl změněn.|

## <a name="monitored-user-activities-ad-security-principal-operations"></a>Monitoruje aktivity uživatelů: operace instančního objektu zabezpečení AD

|Monitorovaných aktivit|Popis|
|---------------------|------------------|
|Vytvoření objektu zabezpečení |Vytvoření účtu (uživatel a počítač).|
|Odstranit objekt zabezpečení změnit  |Účet byl odstraněn nebo obnovit (uživatel a počítač).|
|Změnit zobrazovaný název objektu zabezpečení   |Zobrazovaný název účtu se změnil z X do Y.|
|Změnit název objektu zabezpečení  |Atribut názvu účtu se změnil.|
|Změněna cesta k objektu zabezpečení  |Rozlišující název účtu se změnil z X do Y.|
|Změnit název Sam objektu zabezpečení |Název SAM se změnil. (SAM je přihlašovací jméno používané pro podporu klientů a serverů se staršími verzemi operačního systému).|

## <a name="monitored-user-activities-domain-controller-based-user-operations"></a>Monitoruje aktivity uživatelů: řadič domény na základě operace uživatelů

|Monitorovaných aktivit|Popis|
|---------------------|------------------|
|Replikace adresářové služby  |Použít při pokusu o replikaci adresářové služby.|
|Dotaz DNS  |Uživatel provést dotaz AXFR proti řadiči domény.|
|Načítání dat soukromých  |Uživatel se pokusil/úspěšně dotazu privátní data pomocí protokolu LSARPC.|
|Vytvoření služby   |Uživatel se pokusil vzdáleně vytvořit konkrétní služby do vzdáleného počítače.|
|Výčet relací SMB   |Uživatel se pokusil vytvořit výčet všech uživatelů s otevřenými relacemi SMB na řadičích domény.|
|Kopírování souborů protokolu SMB| Uživatel zkopírovat soubory přes protokol SMB|
|Dotaz SAMR   |Uživatel provedl dotaz SAMR.|
|Plánování úkolů  |Uživatel se pokusil vzdáleně naplánovat X úkol ke vzdálenému počítači.|
|Spuštění WMI  |Uživatel se pokusil o vzdálené spuštění metody WMI.|

## <a name="monitored-user-activities-login-operations"></a>Monitoruje aktivity uživatelů: operace přihlášení

|Typ přihlášení|Monitorovaných aktivit|Popis|
|---------------------|---------------------|------------------|
|Typ přihlášení 2|Ověření přihlašovacích údajů  |Událost ověření účet domény pomocí metody ověřování protokolů NTLM a Kerberos.|
|Typ přihlášení 2|Interaktivní přihlášení  |Uživatel získal přístup k síti tak, že zadáte uživatelské jméno a heslo (metoda ověřování protokolu Kerberos).|
|Typ přihlášení 2|Připojení k síti VPN   |Uživatel připojené prostřednictvím sítě VPN – ověřování pomocí protokolu RADIUS.|
|Typ přihlášení 3|Přístup k prostředkům  |Uživatel získat přístup k prostředku pomocí ověřování protokolem Kerberos.|
|Typ přihlášení 8|Nešifrovaný text LDAP  |Uživatel byl ověřen pomocí protokolu LDAP s nešifrovaným textem heslo (jednoduché ověřování).|
|Typ přihlášení 10|Vzdálená plocha |Uživatel provedl relaci RDP ke vzdálenému počítači pomocí ověřování protokolem Kerberos.|
| --- |Neúspěšné přihlášení |Účet domény se nezdařil pokus o ověření (prostřednictvím protokolů NTLM a Kerberos) z důvodu následující: účet byl zakázán/vypršela platnost/uzamčen/používá nedůvěryhodný certifikát nebo termínu splnění neplatným přihlašovacím hodin/old vypršení platnosti hesla a heslo nebo nesprávné heslo.|


## <a name="monitored-machine-activities-machine-account"></a>Monitoruje aktivity počítače: účet počítače

|Monitorovaných aktivit|Popis|
|---------------------|------------------|
|Změnit operační systém počítače|Změňte na počítači operačního systému.


## <a name="see-also"></a>Viz také
- [Správa výstrah zabezpečení](working-with-suspicious-activities.md)
- [Průvodce výstrahami zabezpečení](suspicious-activity-guide.md)
- [Prošetřování entit](investigate-entity.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

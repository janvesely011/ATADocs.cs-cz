---
title: Přesunout rozšířené ochrany před internetovými útoky pro Azure Advanced Threat Analytics | Dokumentace Microsoftu
description: Zjistěte, jak přesunout existující instalace Advanced Threat Analytics do služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/02/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e734e382-c4b1-43ca-9a8d-96c91daf2578
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: dbc177aea1c237150542684885bc58d23382bf5f
ms.sourcegitcommit: 37299ed90b4bc7bf81f7065d0969bb8fb92622f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518151"
---
# <a name="advanced-threat-analytics-ata-to-azure-advanced-threat-protection-azure-atp"></a>Advanced Threat Analytics (ATA) do Azure Advanced Threat Protection (Azure ATP) 


Tento průvodce vám přesouvat existující instalace ATA ke službě Azure Advanced Threat Protection (služby Azure ATP). V Průvodci popisuje požadavky a předpoklady ochrany ATP v programu Azure a podrobně popisuje, jak naplánovat a potom přesunutí. Postup ověření a tipy, jak využít výhod nejnovějších hrozeb řešení pro ochranu a zabezpečení pomocí služby Azure ATP po instalaci jsou zahrnuté také. 

V této příručce provedete následující: 

> [!div class="checklist"]
> * Zkontrolujte a potvrďte požadavky služby Azure ATP
> * Zdokumentujte stávající konfigurace ATA
> * Plánování vašeho přechodu
> * Nastavení a konfigurace služby Azure ATP
> * Provedení po přesunutí kontroly a ověřování
> * Po dokončení přesunutí vyřadit z provozu ATA 

>[!NOTE]
> Přesun do služby Azure ATP z ATA je možné z libovolné verze ATA. Ale protože data nelze přesunout z ATA do ochrany ATP v programu Azure, se doporučuje pro zachování vašich dat ATA Center a výstrahy, které jsou požadované pro probíhající šetření, dokud všechny výstrahy ATA jsou uzavřeny nebo opravit. 

## <a name="prerequisites"></a>Požadavky

- Minimálně jeden globální zabezpečení a správce tenanta služby Azure Active Directory je potřeba vytvořit instanci služby Azure ATP. Každá instance služby Azure ATP podporuje více hranice doménové struktury služby Active Directory a doménovou strukturu funkční úroveň (ffl) v systémech Windows 2003 a novějších.

- Ochrana ATP v programu Azure vyžaduje .net Framework 4.7 a může vyžadovat řadič domény (restartovat), pokud aktuální .net Framework verze 4.7 není.

- Ujistěte se, že řadiče domény splňovat všechna [požadavky senzoru služby Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/atp-prerequisites#azure-atp-sensor-requirements) a vaše prostředí splňuje všechny [požadavky služby Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/atp-prerequisites).

- Ověřte, že všechny řadiče domény, který chcete použít mají dostatečný přístup k Internetu ke službě ochrana ATP v programu Azure. Zkontrolujte a potvrďte vaše splňují řadiče domény [požadavky na konfiguraci proxy služby Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/configure-proxy).

>[!NOTE]
> Tato příručka k migraci je určená pro pouze senzorů ochrany ATP v programu Azure. Další informace najdete v tématu [výběr správné senzor pro vaše nasazení](https://docs.microsoft.com/azure-advanced-threat-protection/atp-capacity-planning#choosing-the-right-sensor-type-for-your-deployment). 

## <a name="plan"></a>Plán 

Ujistěte se, že shromážděte následující informace před zahájením vašeho přechodu: 
1. Podrobnosti o účtu vašeho [Directory Services](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step2) účtu.
1. Oznámení Syslog [nastavení](https://docs.microsoft.com/azure-advanced-threat-protection/setting-syslog).
1. E-mailu [podrobnosti oznámení](https://docs.microsoft.com/azure-advanced-threat-protection/notifications).
1. Členství skupiny rolí ATA
1. Integrace sítě VPN
1. Výstrahy výjimky 
    - Vyloučení nejsou přenosná z ATA do služby Azure ATP, takže jsou požadovány pro podrobnosti o každé vyloučení [replikovat vyloučení v Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/excluding-entities-from-detections).
1. Podrobnosti o účtu pro účty Honeytokenu. 
    - Pokud ještě nemáte vyhrazené účty Honeytokenu, další informace o [HoneyTokens v Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step7) a vytvořit nové účty, které k tomuto účelu nepoužívat.
1. Úplný seznam všech entit (počítače, skupiny, uživatelé), budete chtít ručně označit jako citlivých entit. 
    - Další informace o důležitosti [citlivých entit](https://docs.microsoft.com/azure-advanced-threat-protection/sensitive-accounts) v ochrany ATP v programu Azure.
1. Plánování sestav [podrobnosti](https://docs.microsoft.com/azure-advanced-threat-protection/reports) (seznam sestav a plánované časování). 
1. Identifikace a podrobnosti o každé komponenty ATA Lightweight Gateway, která je kandidát na synchronizátora domény ochrany ATP v programu Azure. 
   - Další informace o důležitosti [kandidáti na synchronizátora domény](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5#configure-sensor-settings) v ochrany ATP v programu Azure.

> [!NOTE]
> Dokud se odeberou všechny komponenty ATA Gateway do odinstalace komponenty ATA Center. Odinstalace komponenty ATA Center pomocí komponenty ATA Gateway za chodu opustí organizaci vystavena s žádná ochrana před internetovými útoky.

## <a name="move"></a>Přesunout 

Dokončení vaší přesunutí do služby Azure ATP v dva jednoduché kroky:

### <a name="step-1-create-and-install-azure-atp-instance-and-sensors"></a>Krok 1: Vytvoření a instalace instancí služby Azure ATP a snímače

1. [Vytvoření nové instance služby Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step1)

2. Odinstalace komponenty ATA Lightweight Gateway na všechny řadiče domény.  

3. Instalace senzoru ochrany ATP v programu Azure na všechny řadiče domény:
     - [Stažení souborů senzoru služby Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step3).
     - [Načíst klíč přístup ochrany ATP v programu Azure](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step3#download-the-setup-package).
     - [Instalace služby Azure ATP senzorů na řadiče domény](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step4). 

### <a name="step-2-configure-and-validate-azure-atp-instance"></a>Krok 2: Konfigurace a ověření instance služby Azure ATP  

- [Nakonfigurovat senzor](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5)

>[!NOTE]
> Určité úlohy v následujícím seznamu nelze dokončit před instalací služby Azure ATP senzory a následné dokončení počáteční synchronizace, jako je například výběr entity pro ruční **citlivé** označování. Povolte až 2 hodin na dokončení počáteční synchronizace. 

#### <a name="configuration"></a>Konfiguraci

Přihlaste se k portálu ochrany ATP v programu Azure a dokončete těchto konfiguračních úloh.

| Krok    | Akce | Stav |
|--------------|------------|------------------|
| 1  | Nastavte [zpožděné aktualizací na výběr z řadiče domény](https://docs.microsoft.com/azure-advanced-threat-protection/sensor-update) | - [ ] |
| 2  | [Adresářové služby](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step2) Podrobnosti účtu| - [ ] |
| 3  | Konfigurace [kandidáti na synchronizátora domény](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5#configure-sensor-settings) | - [ ] |
| 4  | Konfigurace [oznámení Syslogu](https://docs.microsoft.com/azure-advanced-threat-protection/setting-syslog) | - [ ] |
| 5  | [Integrace sítě VPN](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step6-vpn) informace| - [ ] |
| 6  | Konfigurace [WDATP integrace](https://docs.microsoft.com/azure-advanced-threat-protection/integrate-wd-atp)| - [ ] |
| 7  | Nastavte [HoneyTokens](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step7) účty| - [ ] |
| 8  | Značka [citlivých entit](https://docs.microsoft.com/azure-advanced-threat-protection/sensitive-accounts)| - [ ] |
| 9  | Vytvoření [vyloučení upozornění zabezpečení](https://docs.microsoft.com/azure-advanced-threat-protection/excluding-entities-from-detections)| - [ ] |
| 10 | [Přepíná e-mailových oznámení](https://docs.microsoft.com/azure-advanced-threat-protection/notifications) | - [ ] |
| 11  | [Sestava nastavení plánu](https://docs.microsoft.com/azure-advanced-threat-protection/reports) (seznam sestav a plánované časování)| - [ ] |
| 12  | Konfigurace [oprávnění na základě rolí](https://docs.microsoft.com/azure-advanced-threat-protection/atp-role-groups) | - [ ] |
| 12  | [Konfigurace oznámení systému SIEM (IP adresa)](https://docs.microsoft.com/azure-advanced-threat-protection/configure-event-collection#siemsyslog)| - [ ] | 

#### <a name="validation"></a>Ověření

V rámci ochrany ATP v programu Azure portal:
- Kontroly všech [výstrahy týkající se stavu](https://docs.microsoft.com/azure-advanced-threat-protection/atp-health-center) známky problémy se službou. 
- Kontrola ochrany ATP v programu Azure [protokoly služby Sensor chyba](https://docs.microsoft.com/azure-advanced-threat-protection/troubleshooting-atp-using-logs) nějaké neobvyklé chyby.

## <a name="after-the-move"></a>Po přesunutí

Tato část průvodce popisuje akce, které lze provést po dokončení přesunutí. 

>[!NOTE]
> Importovat ze stávající výstrahy zabezpečení z ATA ochrany ATP v programu nejsou podporovány. Ujistěte se, že záznam nebo opravit všechny existující výstrahy ATA před vyřazení z provozu komponenty ATA Center.  

- **Vyřazení z provozu komponenty ATA Center** 
    - Referenční data komponenty ATA Center po přesunutí, doporučujeme pro určitou dobu uchovávání dat System center online. Po vyřazení z provozu komponenty ATA Center, kolik prostředků může obvykle snížit, zejména v případě, že jsou prostředky virtuálního počítače.  

- **Zálohování Mongo DB** 
    - Pokud chcete zachovat po neomezenou dobu, ATA data [zálohování Mongo DB](https://docs.microsoft.com/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database).  

## <a name="mission-accomplished"></a>Mise splněna

Blahopřejeme! Vaše přesun z ATA do ochrany ATP v programu Azure je dokončena. 

## <a name="next-steps"></a>Další postup

Další informace o [ochrany ATP v programu Azure](https://docs.microsoft.com/azure-advanced-threat-protection/what-is-atp) funkce, funkce, a [výstrahy zabezpečení](https://docs.microsoft.com/azure-advanced-threat-protection/understanding-security-alerts).  
## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) ještě dnes!





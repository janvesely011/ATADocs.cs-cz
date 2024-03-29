---
title: Novinky ATA verze 1.8 | Dokumentace Microsoftu
description: Tento článek obsahuje seznam novinek ATA verze 1.8 spolu se známými problémy.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 9/03/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 1f623642813c0474ddf3c7d050a91aebbd1b40b7
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196914"
---
# <a name="whats-new-in-ata-version-18"></a>Novinky ATA verze 1.8

Nejnovější aktualizovanou verzi ATA je možné [stáhnout z webu Download Center](https://www.microsoft.com/download/details.aspx?id=55536) nebo si můžete plnou verzi stáhnout z webu [Eval center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Tato zpráva k vydání verze obsahuje informace o aktualizacích, nových funkcích, opravách chyb a známých problémech v této verzi Advanced Threat Analytics.



## <a name="new--updated-detections"></a>Nové a aktualizované detekce

- Neobvyklá implementace protokolu byla vylepšena tak, aby byla schopna odhalit malware WannaCry.

- NOVINKA! **Neobvyklá úprava citlivých skupin** – jako součást fáze eskalace oprávnění upravují útočníci skupiny s vysokými oprávněními, aby získali přístup k citlivým prostředkům. ATA teď detekuje, pokud dojde u skupiny se zvýšenými oprávněními k neobvyklé změně.
- NOVINKA! **Podezřelé chyby ověřování** (behaviorální hrubá síla) – útočníci se pokoušejí prolomit účty hrubou silou s využitím přihlašovacích údajů. ATA teď při detekci neobvyklého chování při neúspěšném ověření zobrazí upozornění.   

- **Pokus o vzdálené spuštění – WMI exec** – útočníci se mohou pokusit o ovládnutí sítě vzdáleným spouštěním kódu na vašem řadiči domény. ATA má vylepšenou detekci vzdáleného spuštění obsahující detekci vzdáleného spuštění kódu pomocí metod WMI.

- Rekognoskace využívající dotazy adresářové služby – tato detekce byla vylepšena a je schopna odchytit dotazy na jedinou citlivou entitu a snížit počet falešně pozitivních událostí, které byly generovány v předchozí verzi. Pokud jste tuto funkci ve verzi 1.7 zakázali, při instalaci verze 1.8 se teď automaticky povolí.

- Aktivita zlatého lístku Kerberos – ATA 1.8 obsahuje další techniku pro detekci útoků pomocí zlatého lístku.
    - ATA teď detekuje podezřelé aktivity, kdy vyprší doba života zlatého lístku Kerberos. Pokud se lístek Kerberos používá déle než je povolená doba života, detekuje to ATA jako podezřelou aktivitu, že byl pravděpodobně vytvořen zlatý lístek Kerberos.
- Vylepšením následujících detekcí byly eliminovány falešně pozitivní události:  
    - Detekce eskalace oprávnění (zfalšovaný certifikát PAC) 
    - Aktivita související s oslabením šifrování (Skeleton Key)
    - Neobvyklá implementace protokolu
    - Porušení vztahu důvěryhodnosti

## <a name="improved-triage-of-suspicious-activities"></a>Vylepšené posouzení podezřelých aktivit

-   NOVINKA! Během posuzování podezřelých událostí umožňuje ATA 1.8 provést následující akce: 
    - **Vyloučit entity** z vyvolávání budoucích podezřelých aktivit a zabránit tak upozorněním při detekci neškodných pravdivě pozitivních událostí (například správce spouštějící vzdálený kód nebo detekování kontrol zabezpečení).
    - **Potlačit upozornění na opakované** podezřelé aktivity.
    - **Odstranit podezřelé aktivity** z časové osy útoků.
-   Reakce na upozornění na podezřelou aktivitu je teď mnohem efektivnější. Časová osa podezřelých aktivit byla přepracována. Ve verzi ATA 1.8 uvidíte na jedné obrazovce mnohem více podezřelých aktivit a užitečnějších informací pro účely posouzení a prošetření. 

## <a name="new-reports-to-help-you-investigate"></a>Nové sestavy, které pomáhají s prošetřením 
-   NOVINKA! Byla přidána **souhrnná sestava**, ve které vidíte veškerá sumarizovaná data z ATA včetně podezřelých aktivit, problémů se stavem a dalších údajů. Můžete dokonce definovat přizpůsobenou sestavu, která se pravidelně automaticky generuje.
-   NOVINKA! Byla přidána **sestava citlivých skupin**, která umožňuje zjistit všechny změny provedené v citlivých skupinách za určité období.


## <a name="infrastructure-improvements"></a>Vylepšení infrastruktury

-   Byl zvýšen výkon komponenty ATA Center. Ve verzi ATA 1.8 dokáže ATA Center zpracovat přes 1 milión paketů za sekundu.
-   ATA Lightweight Gateway teď dokáže číst události místně bez nutnosti konfigurace předávání událostí.
-   Teď můžete zvlášť nakonfigurovat e-mail pro monitorovací upozornění a podezřelé aktivity.

## <a name="security-improvements"></a>Vylepšení zabezpečení

-   NOVINKA! **Jednotné přihlašování při správě ATA**. ATA podporuje jednotné přihlašování integrované s ověřováním Windows – pokud jste už přihlášení ke svému počítači, použije ATA tento token pro přihlášení ke konzole ATA. K přihlášení můžete použít také čipovou kartu. Skripty pro tichou instalaci komponent ATA Gateway a ATA Lightweight Gateway teď používají kontext přihlášeného uživatele bez nutnosti zadávání přihlašovacích údajů.
-   Oprávnění Local System byla z procesu ATA Gateway odebrána, takže ke spuštění procesu ATA Gateway teď můžete použít virtuální účty (dostupné jen u samostatných komponent ATA Gateway), účty spravované služby a skupinové účty spravované služby.   
-   Byly přidány protokoly auditování komponent ATA Center a ATA Gateway a všechny akce jsou teď protokolované v protokolu událostí Windows.
-   Komponenta ATA Center byla doplněna o podporu certifikátů KSP.

## <a name="additional-changes"></a>Další změny

- Z podezřelých aktivit byla odebrána možnost přidávat poznámky.
- Z časové osy podezřelých aktivit byla odebrána doporučení pro jejich zmírnění.
- Od verze ATA verze 1.8 komponenty ATA Gateway a Lightweight Gateway spravujete své vlastní certifikáty a potřebujete zásah správce spravovat.

## <a name="known-issues"></a>Známé problémy

> [!WARNING]
> Aby bylo možné vyhnout těchto známých problémů prosím aktualizaci nebo nasazení můžete použít aktualizace 1.8 1.

### <a name="ata-gateway-on-windows-server-core"></a>ATA Gateway na jádru Windows Serveru

**Příznaky**: Upgrade ATA Gateway na verzi 1.8 na jádra Windows serveru 2012R2 s .net Frameworkem 4.7 může selhat s touto chybou: *Microsoft Advanced Threat Analytics Gateway přestala fungovat*. 

![Chyba jádra a Gateway](./media/gateway-core-error.png)

Na jádru Windows Serveru 2016 se chyba nemusí zobrazit, ale proces se při pokusu o instalaci selže a do protokolu událostí aplikace na serveru se zaznamenají události 1000 a 1001 (chybové ukončení procesu).

**Popis**: Je nějaký problém s rozhraním .NET framework 4.7, který způsobí, že aplikace využívající technologii WPF (jako je ATA) na nepodaří zavést. Více informací najdete v článku [KB 4034015](https://support.microsoft.com/help/4034015/wpf-window-can-t-be-loaded-after-you-install-the-net-framework-4-7-on). 

**Alternativní řešení:** Odinstalujte .net 4.7 [najdete v článku KB 3186497](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows) vrátit .NET na verzi .NET 4.6.2 a pak aktualizujte ATA Gateway na verzi 1.8. Po upgradu ATA můžete .Net 4.7 znovu nainstalovat.  Tento problém bude odstraněn aktualizací v budoucí verzi.

### <a name="lightweight-gateway-event-log-permissions"></a>Oprávnění protokolu událostí Lightweight Gateway

**Příznaky**: Při upgradu ATA na verzi 1.8, aplikacím nebo službám, které dříve měly oprávnění pro přístup k protokolu událostí zabezpečení tato oprávnění ztratit. 

**Popis**: Pokud chcete usnadnit nasazení ATA, přistupuje ATA 1.8 k protokolu událostí zabezpečení přímo, aniž by se vyžadovala konfigurace předávání událostí Windows. Současně ATA kvůli zachování přísnějšího zabezpečení běží jako místní služba s nízkou úrovní oprávnění. Aby měla služba ATA přístup ke čtení událostí, udělí si oprávnění pro protokol událostí zabezpečení. Přitom se mohou zakázat dříve nastavená oprávnění pro jiné služby.

**Alternativní řešení:** Spusťte následující skript prostředí Windows PowerShell. Tím se z ATA v registru odeberou nesprávně přidaná oprávnění a přidají se prostřednictvím jiného rozhraní API. Oprávnění pro jiné aplikace se tak můžou obnovit. Pokud ne, bude je nutné obnovit ručně. Tento problém bude odstraněn aktualizací v budoucí verzi. 

       $ATADaclEntry = "(A;;0x1;;;S-1-5-80-1717699148-1527177629-2874996750-2971184233-2178472682)"
        try {
        $SecurityDescriptor = Get-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        $ATASddl = "O:BAG:SYD:" + $ATADaclEntry 
        if($SecurityDescriptor.CustomSD -eq $ATASddl) {
        Remove-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        }
    }
    catch
    {
    # registry key does not exist
    }

    $EventLogConfiguration = New-Object -TypeName System.Diagnostics.Eventing.Reader.EventLogConfiguration("Security")
    $EventLogConfiguration.SecurityDescriptor = $EventLogConfiguration.SecurityDescriptor + $ATADaclEntry

### <a name="proxy-interference"></a>Interference proxy serveru

**Příznaky**: Po upgradu ATA Gateway na ATA 1.8 služby nemusí podařit spustit. V protokolu chyb ATA se může zobrazit následující výjimka: *System.Net.Http.HttpRequestException: Při odesílání požadavku došlo k chybě. ---> System.Net.WebException: Vzdálený server vrátil chybu: Vyžadováno ověřování proxy serveru (407).*

**Popis**: Spuštění z ATA 1.8 komunikuje ATA Gateway ve službě ATA Center pomocí protokolu http. Pokud počítač, na kterém je brána ATA Gateway nainstalovaná, používá pro připojení k ATA Center proxy server, může dojít k narušení této komunikace. 

**Alternativní řešení:** Zakážete používání proxy serveru v účtu služby ATA Gateway. Tento problém bude odstraněn aktualizací v budoucí verzi.

### <a name="report-settings-reset"></a>Obnovení nastavení sestavy

**Příznaky**: Všechna nastavení, které byly provedeny naplánované sestavy jsou vymazány při aktualizaci 1,8 update 1.

**Popis**: Aktualizace na 1.8 update 1 z 1.8 resetování sestavy nastavení plánu.

**Alternativní řešení:** Před aktualizací na 1.8 update 1, vytvořte kopii sestavy nastavení a zadejte je znovu, může jít prostřednictvím skriptu, další informace najdete v tématu [Export a Import konfigurace ATA](ata-configuration-file.md).


## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizace ATA na verzi 1.8 – průvodce migrací](ata-update-1.8-migration-guide.md)


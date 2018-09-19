---
title: Změna konfigurace ATA Center služby Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje, jak změnit IP adresu, port, adresu URL konzoly nebo certifikát pro ATA Center.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1d01b206cfab1edaef7774da5de8963e47fcb504
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133943"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="modifying-the-ata-center-configuration"></a>Změna konfigurace ATA Center


Po počátečním nasazení by se změny ATA Center měly dělat opatrně. Při aktualizaci adresu URL konzoly a certifikátu použijte následující postupy.

## <a name="the-ata-console-url"></a>Adresa URL konzoly ATA

Adresa URL se používá v následujících scénářích:

-   Toto je adresa URL používá komponenty ATA Gateway ke komunikaci s ATA Center.

- Instalace komponent ATA Gateway – Při instalaci se ATA Gateway registruje v ATA Center. Tento proces registrace je uskutečněn připojením ke konzole ATA. Pokud zadáte plně kvalifikovaný název domény pro adresu URL konzoly ATA, ujistěte se, že ATA Gateway umí přeložit plně kvalifikovaný název domény na IP adresu vázán ke konzole ATA.

-   Výstrahy – Když ATA rozešle výstrahu SIEM nebo e-mailovou výstrahu, zahrnuje odkaz na podezřelou aktivitu. Hostitelská část odkazu je nastavení adresy URL konzoly ATA.

-   Pokud jste nainstalovali certifikát z vaší interní certifikační autority (CA), aby se adresa URL název subjektu v certifikátu. To zabrání uživatelům v získání upozornění při připojování ke konzole ATA.

-   Použití plně kvalifikovaný název domény pro adresu URL konzoly ATA umožňuje změnit IP adresu, která se používá konzola ATA bez přerušení výstrah předchozí nebo instalačního balíčku ATA Gateway stáhnout znovu. Je potřeba jenom aktualizovat DNS novou IP adresou.

1. Ujistěte se, že chcete použít novou adresu URL přeloží na IP adresu konzoly ATA.

2. V nastavení ATA v části **Center**, zadejte novou adresu URL. V tomto okamžiku je služba ATA Center stále používá původní adresu URL. 

 ![Změna konfigurace ATA](media/change-center-config.png)

  > [!NOTE]
  > Pokud jste zadali vlastní IP adresu, nemůžete kliknout **aktivovat** dokud nenainstalujete IP adresu na ATA Center.
    
3. Vyčkat, než komponenty ATA Gateway k synchronizaci. Tito uživatelé teď mají dvě potenciální adresy URL, pomocí kterého je možné získat přístup ke konzole ATA. Tak dlouho, dokud se komponenta ATA Gateway můžete připojit pomocí původní adresu URL, nepokusí novou.

4. Po všechny komponenty ATA Gateway synchronizovaly s aktualizovanou konfigurací, na stránce konfigurace System Center, klikněte **aktivovat** tlačítko aktivovat novou adresu URL. Po aktivaci nové adresy URL komponenty ATA Gateway použije pro přístup ke komponentě ATA Center nyní nové adresy URL Po připojení ke službě ATA Center, ATA Gateway stáhne nejnovější konfiguraci a bude obsahovat pouze nové adresy URL pro konzolu ATA. 
5. 
 ![Aktivovat certifikát](media/center-activation.png)

> [!NOTE]
> -   Pokud při aktivaci nové adresy URL a nikdy nezískala aktualizovanou konfiguraci ATA Gateway byla ve stavu offline, ručně aktualizujte konfigurační soubor JSON v ATA Gateway.
> -   Pokud potřebujete nasadit novou ATA Gateway po aktivaci nové adresy URL, musíte znovu stahovat balíček ATA Gateway Setup.


## <a name="the-ata-center-certificate"></a>Certifikát ATA Center

> [!WARNING]
> - Postup obnovení existujícího certifikátu se nepodporuje. Jediný způsob, jak obnovit certifikát, je vytvoření nového certifikátu a konfiguraci řešení ATA možnost použití nového certifikátu.


Nahraďte certifikát pomocí následujícího postupu:

1. Předtím, než vyprší platnost aktuálního certifikátu, vytvořte nový certifikát a ujistěte se, že je nainstalovaná na serveru ATA Center. <br></br>Doporučuje se, že zvolíte certifikát od interní certifikační autority, ale je také možné vytvořit nový certifikát podepsaný svým držitelem. Další informace najdete v tématu [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

2. V nastavení ATA v části **Center**, vyberte tento nově vytvořeného certifikátu. V tomto okamžiku je služba ATA Center stále vázaná na původní certifikát. 

 ![Změna konfigurace ATA](media/change-center-config.png)

3. Vyčkat, než komponenty ATA Gateway k synchronizaci. Nyní mají dva potenciální certifikáty, které jsou platné pro vzájemné ověřování. Tak dlouho, dokud se komponenta ATA Gateway můžete připojit pomocí původního certifikátu, ne zkoušet nový.

4. Za všechny komponenty ATA Gateway synchronizovaly s aktualizovanou konfigurací aktivujte nový certifikát, který má služba ATA Center je vázán na. Po aktivaci nového certifikátu služba ATA Center vytvoří vazbu na nový certifikát. Nový certifikát komponenty ATA Gateway teď používají k ověření ve službě ATA Center. Po připojení ke službě ATA Center, ATA Gateway stáhne nejnovější konfiguraci a bude obsahovat pouze nový certifikát pro ATA Center. 

> [!NOTE]
> -   Pokud při aktivaci nového certifikátu a nikdy nezískala aktualizovanou konfiguraci ATA Gateway byla ve stavu offline, ručně aktualizujte konfigurační soubor JSON v ATA Gateway.
> -   Komponenty ATA Gateway musí důvěřovat certifikátu, který používáte.
> -   Certifikát se používá také pro konzolu ATA, takže by měl odpovídat adrese konzoly ATA na vyhnuli upozorněním prohlížeče.
> -   Pokud potřebujete nasadit novou ATA Gateway po aktivaci nového certifikátu, budete muset znovu stáhnout instalační balíček ATA Gateway.



 
## <a name="see-also"></a>Viz také
- [Práce s konzolou ATA](working-with-ata-console.md)
- [Podívejte se na fórum ATA!](https://aka.ms/ata-forum)

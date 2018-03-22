---
title: "Změna konfigurace ATA Center služby Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Popisuje, jak změnit IP adresu, port, adresu URL konzoly nebo certifikát pro ATA Center."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 294b9204f9ca6a40a835e5360a7011947e3255b4
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/22/2018
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="modifying-the-ata-center-configuration"></a>Změna konfigurace ATA Center


Po počátečním nasazení by se změny ATA Center měly dělat opatrně. Při aktualizaci adresu URL konzoly a certifikát, použijte následující postupy.

## <a name="the-ata-console-url"></a>Adresa URL konzoly ATA

Adresa URL se používá v následujících scénářích:

-   Toto je adresa URL používá ke komunikaci s ATA Center komponenty ATA Gateway.

- Instalace komponent ATA Gateway – Při instalaci se ATA Gateway registruje v ATA Center. Tento proces registrace je uskutečněn připojením ke konzole ATA. Pokud zadáte plně kvalifikovaný název domény pro adresu URL konzoly ATA, ujistěte se, že ATA Gateway umí přeložit plně kvalifikovaný název domény na IP adresu vázán ke konzole ATA.

-   Výstrahy – Když ATA rozešle výstrahu SIEM nebo e-mailovou výstrahu, zahrnuje odkaz na podezřelou aktivitu. Hostitelská část odkazu je nastavení adresy URL konzoly ATA.

-   Pokud jste nainstalovali certifikát z vaší interní certifikační autority (CA), shodovat s adresou URL k názvu subjektu v certifikátu. To zabrání uživatelům získávání upozornění při připojování ke konzole ATA.

-   Použití plně kvalifikovaný název domény pro adresu URL konzoly ATA umožňuje změnit IP adresu, která se používá konzolou ATA bez přerušení výstrah, předchozí nebo znovu stáhnout balíček ATA Gateway. Je potřeba jenom aktualizovat DNS novou IP adresou.

1. Zajistěte, aby nové adrese URL, kterou chcete použít přeloží na IP adresu konzoly ATA.

2. V nastavení ATA pod **Center**, zadejte nové adrese URL. V tomto okamžiku služba ATA Center stále používá původní adresu URL. 

 ![Změna konfigurace ATA](media/change-center-config.png)

  > [!NOTE]
  > Pokud jste zadali vlastní IP adresu, nelze kliknout **aktivovat** dokud nenainstalujete IP adresu na ATA Center.
    
3. Počkejte, než pro komponenty ATA Gateway k synchronizaci. Nyní mají dva potenciální adresy URL, pomocí kterého se přístup ke konzole ATA. Tak dlouho, dokud se ATA Gateway můžete připojit pomocí původní adresu URL, nepokusí novým.

4. Po všechny komponenty ATA Gateway synchronizovaly s aktualizovanou konfigurací, na stránce konfigurace Center klikněte **aktivovat** tlačítko aktivovat nové adrese URL. Po aktivaci nové adrese URL komponenty ATA Gateway teď použít nové adrese URL pro přístup k ATA Center. Po připojení ke službě ATA Center, ATA Gateway stáhne nejnovější konfiguraci a bude mít pouze nové adrese URL pro konzolu ATA. 
5. 
 ![Aktivovat certifikátu](media/center-activation.png)

> [!NOTE]
> -   Pokud ATA Gateway offline a aktivovat nové adrese URL a nikdy nezískala aktualizovanou konfiguraci, ručně aktualizujte konfigurační soubor JSON v ATA Gateway.
> -   Pokud potřebujete nasadit novou ATA Gateway po aktivaci nové adrese URL, budete muset znovu stáhnout balíček ATA Gateway Setup.


## <a name="the-ata-center-certificate"></a>Certifikát ATA Center

> [!WARNING]
> - Proces obnovení existujícího certifikátu není podporována. Jediný způsob, jak obnovit certifikát, je vytvoření nového certifikátu a konfiguraci ATA na použití nového certifikátu.


Nahraďte certifikát pomocí tohoto postupu:

1. Předtím, než vyprší platnost aktuálního certifikátu, vytvořte nový certifikát a ujistěte se, že je nainstalovaná na serveru ATA Center. <br></br>Doporučujeme vybrat si certifikát od interní certifikační autority, ale je také možné vytvořit nový certifikát podepsaný svým držitelem. Další informace najdete v tématu [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

2. V nastavení ATA pod **Center**, vyberte tento nově vytvořený certifikát. V tomto okamžiku je služba ATA Center stále vázaná na původní certifikát. 

 ![Změna konfigurace ATA](media/change-center-config.png)

3. Počkejte, než pro komponenty ATA Gateway k synchronizaci. Nyní mají dva potenciální certifikáty, které jsou platné pro vzájemné ověřování. Tak dlouho, dokud ATA Gateway bude moct připojit pomocí původního certifikátu, nepokusí novým.

4. Po všechny komponenty ATA Gateway synchronizovaly s aktualizovanou konfigurací aktivujte nový certifikát, který je služba ATA Center vázána. Po aktivaci nového certifikátu služba ATA Center vytvoří vazbu na nový certifikát. Komponenty ATA Gateway teď používají nový certifikát k ověření ve službě ATA Center. Po připojení ke službě ATA Center, ATA Gateway stáhne nejnovější konfiguraci a bude mít pouze nový certifikát pro ATA Center. 

> [!NOTE]
> -   Pokud ATA Gateway offline a aktivovat nový certifikát a nikdy nezískala aktualizovanou konfiguraci, ručně aktualizujte konfigurační soubor JSON v ATA Gateway.
> -   Komponenty ATA Gateway musí důvěřovat certifikátu, který používáte.
> -   Certifikát se také používá pro konzolu ATA, měla by se shodovat adresu konzoly ATA, aby se zabránilo upozornění prohlížeče.
> -   Pokud potřebujete nasadit novou ATA Gateway po aktivaci nového certifikátu, budete muset znovu stáhnout instalační balíček ATA Gateway.



 
## <a name="see-also"></a>Viz také
- [Práce s konzolou ATA](working-with-ata-console.md)
- [Podívejte se na fórum ATA!](https://aka.ms/ata-forum)

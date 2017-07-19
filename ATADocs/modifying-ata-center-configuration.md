---
title: "Změna konfigurace ATA Center služby Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Popisuje, jak změnit IP adresu, port, adresu URL konzoly nebo certifikát pro ATA Center."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1e9fa2d104c52087746e7c03fea27e3cb596adf0
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/30/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="modifying-the-ata-center-configuration"></a>Změna konfigurace ATA Center


Po počátečním nasazení by se změny ATA Center měly dělat opatrně. K aktualizaci IP adresy a portu, adresy URL konzoly a certifikátu použijte následující postupy.

## <a name="the-ata-center-ip-address"></a>Změna IP adresy u ATA Center

Komponenty ATA Gateway místně ukládají IP adresu pro ATA Center, ke kterému se potřebují připojit. V pravidelných intervalech se připojují k ATA Center a stahují změny konfigurace. Změna způsobu připojení komponent ATA Gateway k ATA Center se provádí ve dvou fázích.

-   První fáze – Aktualizujte IP adresu a port, které má služba ATA Center používat. V tomto okamžiku ATA Center stále naslouchá na původní IP adrese a při příští synchronizaci konfigurace bude mít ATA Gateway dvě IP adresy pro ATA Center. Dokud se komponenta ATA Gateway bude moct připojit pomocí původní (první) IP adresy, nebude zkoušet novou IP adresu a port.

-   Druhá fáze – Poté, co se všechny komponenty ATA Gateway synchronizovaly s aktualizovanou konfigurací, aktivujte novou IP adresu a port, na kterém ATA Center naslouchá. Po aktivaci nové IP adresy služba ATA Center vytvoří vazbu k nové IP adrese. Komponenty ATA Gateway se nebudou moct připojit k původní adrese a nyní se pokusí připojit s druhou (novou) IP adresou, kterou mají pro ATA Center. Po připojení k ATA Center pomocí nové IP adresy si ATA Gateway stáhne nejnovější konfiguraci a bude mít jednu IP adresu pro ATA Center. (Pokud nezahájíte postup znovu.)

> [!NOTE]
> -   Pokud během první fáze byla ATA Gateway offline a nikdy nezískala aktualizovanou konfiguraci, budete muset ručně aktualizovat konfigurační soubor JSON v ATA Gateway.
> -   Pokud je nová IP adresa nainstalovaná na serveru ATA Center, můžete ji při provádění změny vybrat ze seznamu IP adres. Nicméně pokud z nějakého důvodu nemůžete nainstalovat IP adresu na server ATA Center, můžete vybrat vlastní IP adresu a přidat ji ručně. Nebudete moct aktivovat novou IP adresu, dokud není IP adresa nainstalovaná na serveru.
> -   Pokud potřebujete nasadit novou ATA Gateway po aktivaci nové IP adresy, budete muset znovu stáhnout instalační balíček ATA Gateway.

## <a name="the-console-url"></a>Adresa URL konzoly

Adresa URL se používá v následujících scénářích:

-   Instalace komponent ATA Gateway – Při instalaci se ATA Gateway registruje v ATA Center. Tento proces registrace je uskutečněn připojením ke konzole ATA. Pokud zadáte plně kvalifikovaný název domény pro adresu URL konzoly ATA, je potřeba zajistit, že ATA Gateway umí přeložit tento plně kvalifikovaný název domény na IP adresu, na kterou je konzola ATA vázaná.

-   Výstrahy – Když ATA rozešle výstrahu SIEM nebo e-mailovou výstrahu, zahrnuje odkaz na podezřelou aktivitu. Hostitelská část odkazu je nastavení adresy URL konzoly ATA.

-   Pokud jste nainstalovali certifikát z vaší interní certifikační autority (CA), budete pravděpodobně chtít, aby se adresa URL shodovala s názvem předmětu v certifikátu, takže uživatelům se nebudou zobrazovat upozornění při připojování ke konzole ATA.

-   Použití plně kvalifikovaného názvu domény pro adresu URL konzoly ATA umožňuje změnit IP adresu, kterou používá konzola ATA bez přerušení výstrah, které byly rozeslány dřív, a bez nutnosti znovu stahovat balíček ATA Gateway. Je potřeba jenom aktualizovat DNS novou IP adresou.

> [!NOTE]
> Po úpravě adresy URL konzoly ATA byste si měli před instalací nových ATA Gateway stáhnout instalační balíček ATA Gateway.

## <a name="the-ata-center-certificate"></a>Certifikát ATA Center
Pokud se blíží konec platnosti vašeho certifikátu a je třeba ho obnovit nebo nahradit po instalaci nového certifikátu v úložišti místního počítače na server ATA Center, nahraďte certifikát pomocí následujícího dvoufázového postupu:

-   První fáze – Aktualizujte certifikát, který má služba ATA Center používat. V tomto okamžiku je služba ATA Center stále vázaná na původní certifikát. Pokud komponenty ATA Gateway synchronizují své konfigurace, budou mít dva potenciální certifikáty, které budou platné pro vzájemné ověřování. Dokud se komponenta ATA Gateway bude moct připojit pomocí původního certifikátu, nebude zkoušet nový.

-   Druhá fáze – Poté, co se všechny komponenty ATA Gateway synchronizovaly s aktualizovanou konfigurací, můžete aktivovat nový certifikát, ke kterému je služba ATA Center vázána. Po aktivaci nového certifikátu služba ATA Center vytvoří vazbu k certifikátu. Komponenty ATA Gateway nebudou moct správně provést vzájemné ověření se službou ATA Center a pokusí se ověřit druhý certifikát. Po připojení ke službě ATA Center si ATA Gateway stáhne nejnovější konfiguraci a bude mít jeden certifikát pro ATA Center. (Pokud nezahájíte postup znovu.)

> [!NOTE]
> -   Pokud během první fáze byla ATA Gateway offline a nikdy nezískala aktualizovanou konfiguraci, budete muset ručně aktualizovat konfigurační soubor JSON v ATA Gateway.
> -   Komponenty ATA Gateway musí důvěřovat certifikátu, který používáte.
> -   Certifikát se používá také pro konzolu ATA, takže by měl odpovídat adrese konzoly ATA, aby se předešlo zobrazování varování v prohlížeči.
> -   Pokud potřebujete nasadit novou ATA Gateway po aktivaci nového certifikátu, budete muset znovu stáhnout instalační balíček ATA Gateway.

## <a name="changing-the-ata-center-configuration"></a>Změna konfigurace u ATA Center

1.  Otevřete konzolu ATA.

2.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.png)

3.  Vyberte možnost **Center**.

  ![Změna konfigurace ATA](media/change-center-config.png)

4.  V části **URL** vyberte **Add custom DNS name / IP address** (Přidat vlastní název DNS nebo IP adresu) a přidejte nový název DNS nebo IP adresu nebo v části **Certificate** (Certifikát) vyberte nový certifikát.

5.  Klikněte na **Uložit**.

6.  Zobrazí se upozornění, kolik komponent ATA Gateway se synchronizovalo s nejnovější konfigurací.

    >[!IMPORTANT]
    >Před aktivací nové konfigurace ověřte, že jsou všechny komponenty ATA Gateway synchronizované s nejnovější konfigurací. Aktivace nové konfigurace dřív, než se synchronizují všechny komponenty ATA Gateway, může způsobit, že přestanou fungovat podle očekávání. Pokud některá z komponent ATA Gateway není synchronizovaná, zobrazí se po kliknutí na tlačítko pro aktivaci tato chyba:


7.  Po synchronizaci všech komponent ATA Gateway klikněte na **Activate** (Aktivovat) a aktivujte novou IP adresu nebo certifikát.

    > [!NOTE]
    > Pokud jste zadali vlastní IP adresu, nebudete moct kliknout na **Aktivovat**, dokud nenainstalujete IP adresu na ATA Center.

8.  Zajistěte, aby všechny komponenty ATA Gateway mohly po aktivaci změny synchronizovat své konfigurace. V oznamovacím pruhu se zobrazí, kolik komponent ATA Gateway úspěšně synchronizovalo svoji konfiguraci.




## <a name="see-also"></a>Viz také
- [Práce s konzolou ATA](working-with-ata-console.md)
- [Podívejte se na fórum ATA!](https://aka.ms/ata-forum)

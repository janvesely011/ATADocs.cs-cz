---
# required metadata

title: Změna konfigurace ATA – certifikát ATA Center | Microsoft Advanced Threat Analytics
description: Popisuje dvoufázový postup obnovení nebo nahrazení certifikátu v úložišti místního počítače na serveru ATA Center. 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Změna konfigurace ATA – certifikát ATA Center

>[!div class="step-by-step"]

## « IP adresa serveru ATA Center
IP adresa konzoly ATA »

-   Změna certifikátu ATA Center Pokud vaše certifikáty vyprší a je třeba je po instalaci nového certifikátu v úložišti místního počítače na server ATA Center obnovit nebo nahradit, nahraďte certifikát pomocí následujícího dvoufázového postupu: První fáze – Aktualizujte certifikát, který má služba ATA Center používat. V tomto okamžiku je služba ATA Center stále vázaná na původní certifikát.

-   Pokud komponenty ATA Gateway synchronizují své konfigurace, budou mít dva potenciální certifikáty, které budou platné pro vzájemné ověřování. Dokud se komponenta ATA Gateway bude moct připojit pomocí původního certifikátu, nebude zkoušet nový. Druhá fáze – Poté, co se všechny komponenty ATA Gateway synchronizovaly s aktualizovanou konfigurací, můžete aktivovat nový certifikát, ke kterému je služba ATA Center vázána. Po aktivaci nového certifikátu služba ATA Center vytvoří vazbu k certifikátu. Komponenty ATA Gateway nebudou moct správně provést vzájemné ověření se službou ATA Center a pokusí se ověřit druhý certifikát.

> [!NOTE]
> -   Po připojení ke službě ATA Center si ATA Gateway stáhne nejnovější konfiguraci a bude mít jeden certifikát pro ATA Center.
> -   (Pokud nezahájíte postup znovu.)
> -   Pokud během první fáze byla ATA Gateway offline a nikdy nezískala aktualizovanou konfiguraci, budete muset ručně aktualizovat konfigurační soubor JSON v ATA Gateway.

1.  Komponenty ATA Gateway musí důvěřovat certifikátu, který používáte.

2.  Pokud potřebujete nasadit novou ATA Gateway po aktivaci nového certifikátu, budete muset znovu stáhnout instalační balíček ATA Gateway.

    ![Otevřete konzolu ATA.](media/ATA-config-icon.JPG)

3.  Vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**.

4.  Ikona nastavení konfigurace ATA

5.  Vyberte **ATA Center**.

6.  V části **Certifikát** vyberte jeden z certifikátů v seznamu.

7.  Klikněte na **Uložit**.
    >[!IMPORTANT]
    >Zobrazí se upozornění, kolik komponent ATA Gateway se synchronizovalo s nejnovější konfigurací. Po synchronizaci všech ATA Gateway klikněte na **Aktivovat** a aktivujte nový certifikát. Před aktivací nové konfigurace ověřte, že jsou všechny komponenty ATA Gateway synchronizované s nejnovější konfigurací.
    >
    >    ![Aktivace nové konfigurace dřív, než se synchronizují všechny komponenty ATA Gateway, může způsobit, že přestanou fungovat podle očekávání.](media/ataGW-not-synced.png)

8.  Pokud některá z komponent ATA Gateway není synchronizovaná, zobrazí se po kliknutí na tlačítko pro aktivaci tato chyba:

>ATA Gateway – chyba synchronizace

## Zajistěte, aby všechny komponenty ATA Gateway mohly po aktivaci změny synchronizovat své konfigurace.
- [[!div class="step-by-step"]](working-with-ata-console.md)
- [« IP adresa serveru ATA Center](install-ata.md)
- [IP adresa konzoly ATA »](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Jun16_HO1-->



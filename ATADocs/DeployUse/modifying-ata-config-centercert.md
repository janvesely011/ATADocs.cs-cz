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
[« IP adresa serveru ATA Center](modifying-ata-config-centerip.md)
[IP adresa konzoly ATA »](modifying-ata-config-consoleip.md)

## Změna certifikátu ATA Center
Pokud vaše certifikáty vyprší a je třeba je po instalaci nového certifikátu v úložišti místního počítače na server ATA Center obnovit nebo nahradit, nahraďte certifikát pomocí následujícího dvoufázového postupu:

-   První fáze – Aktualizujte certifikát, který má služba ATA Center používat. V tomto okamžiku je služba ATA Center stále vázaná na původní certifikát. Pokud komponenty ATA Gateway synchronizují své konfigurace, budou mít dva potenciální certifikáty, které budou platné pro vzájemné ověřování. Dokud se komponenta ATA Gateway bude moct připojit pomocí původního certifikátu, nebude zkoušet nový.

-   Druhá fáze – Poté, co se všechny komponenty ATA Gateway synchronizovaly s aktualizovanou konfigurací, můžete aktivovat nový certifikát, ke kterému je služba ATA Center vázána. Po aktivaci nového certifikátu služba ATA Center vytvoří vazbu k certifikátu. Komponenty ATA Gateway nebudou moct správně provést vzájemné ověření se službou ATA Center a pokusí se ověřit druhý certifikát. Po připojení ke službě ATA Center si ATA Gateway stáhne nejnovější konfiguraci a bude mít jeden certifikát pro ATA Center. (Pokud nezahájíte postup znovu.)

> [!NOTE]
> -   Pokud během první fáze byla ATA Gateway offline a nikdy nezískala aktualizovanou konfiguraci, budete muset ručně aktualizovat konfigurační soubor JSON v ATA Gateway.
> -   Komponenty ATA Gateway musí důvěřovat certifikátu, který používáte.
> -   Pokud potřebujete nasadit novou ATA Gateway po aktivaci nového certifikátu, budete muset znovu stáhnout instalační balíček ATA Gateway.

1.  Otevřete konzolu ATA.

2.  Vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**..

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

3.  Vyberte **ATA Center**..

4.  V části **Certifikát** vyberte jeden z certifikátů v seznamu.

5.  Klikněte na **Uložit**..

6.  Zobrazí se upozornění, kolik komponent ATA Gateway se synchronizovalo s nejnovější konfigurací.

7.  Po synchronizaci všech ATA Gateway klikněte na **Aktivovat** a aktivujte nový certifikát.

8.  Zajistěte, aby všechny komponenty ATA Gateway mohly po aktivaci změny synchronizovat své konfigurace.

>[!div class="step-by-step"]
[« IP adresa serveru ATA Center](modifying-ata-config-centerip.md)
[IP adresa konzoly ATA »](modifying-ata-config-consoleip.md)

## Viz také
- [Práce s konzolou ATA](/advanced-threat-analytics/understand-explore/working-with-ata-console)
- [Instalace ATA](install-ata.md)
- [Podporu získáte na našem fóru!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO4-->



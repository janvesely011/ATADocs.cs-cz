---
title: "Změna konfigurace Advanced Threat Analytics – certifikát Center | Dokumentace Microsoftu"
description: "Popisuje dvoufázový postup obnovení nebo nahrazení certifikátu v úložišti místního počítače na serveru ATA Center."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 9d3e4a76c37fcd3cd90afe068e904e64cd9f45b0


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="change-ata-configuration---ata-center-certificate"></a>Změna konfigurace ATA – certifikát ATA Center

>[!div class="step-by-step"]
[« IP adresa serveru ATA Center](modifying-ata-config-centerip.md)
[adresa URL konzoly ATA »](modifying-ata-config-consoleurl.md)

## <a name="change-the-ata-center-certificate"></a>Změna certifikátu ATA Center
Pokud se blíží konec platnosti vašeho certifikátu a je třeba ho obnovit nebo nahradit po instalaci nového certifikátu v úložišti místního počítače na server ATA Center, nahraďte certifikát pomocí následujícího dvoufázového postupu:

-   První fáze – Aktualizujte certifikát, který má služba ATA Center používat. V tomto okamžiku je služba ATA Center stále vázaná na původní certifikát. Pokud komponenty ATA Gateway synchronizují své konfigurace, budou mít dva potenciální certifikáty, které budou platné pro vzájemné ověřování. Dokud se komponenta ATA Gateway bude moct připojit pomocí původního certifikátu, nebude zkoušet nový.

-   Druhá fáze – Poté, co se všechny komponenty ATA Gateway synchronizovaly s aktualizovanou konfigurací, můžete aktivovat nový certifikát, ke kterému je služba ATA Center vázána. Po aktivaci nového certifikátu služba ATA Center vytvoří vazbu k certifikátu. Komponenty ATA Gateway nebudou moct správně provést vzájemné ověření se službou ATA Center a pokusí se ověřit druhý certifikát. Po připojení ke službě ATA Center si ATA Gateway stáhne nejnovější konfiguraci a bude mít jeden certifikát pro ATA Center. (Pokud nezahájíte postup znovu.)

> [!NOTE]
> -   Pokud během první fáze byla ATA Gateway offline a nikdy nezískala aktualizovanou konfiguraci, budete muset ručně aktualizovat konfigurační soubor JSON v ATA Gateway.
> -   Komponenty ATA Gateway musí důvěřovat certifikátu, který používáte.
> -   Certifikát se používá také pro konzolu ATA, takže by měl odpovídat adrese konzoly ATA, aby se předešlo zobrazování varování v prohlížeči.
> -   Pokud potřebujete nasadit novou ATA Gateway po aktivaci nového certifikátu, budete muset znovu stáhnout instalační balíček ATA Gateway.

1.  Otevřete konzolu ATA.

2.  Na panelu nástrojů vyberte možnost nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace ATA](media/ATA-config-icon.JPG)

3.  Vyberte možnost **Center**.

4.  V části **Certifikát** vyberte jeden z certifikátů v seznamu.

5.  Klikněte na **Uložit**.

6.  Zobrazí se upozornění, kolik komponent ATA Gateway se synchronizovalo s nejnovější konfigurací.

7.  Po synchronizaci všech ATA Gateway klikněte na **Aktivovat** a aktivujte nový certifikát.
    >[!IMPORTANT]
    >Před aktivací nové konfigurace ověřte, že jsou všechny komponenty ATA Gateway synchronizované s nejnovější konfigurací. Aktivace nové konfigurace dřív, než se synchronizují všechny komponenty ATA Gateway, může způsobit, že přestanou fungovat podle očekávání. Pokud některá z komponent ATA Gateway není synchronizovaná, zobrazí se po kliknutí na tlačítko pro aktivaci tato chyba:
    >
    >    ![ATA Gateway – chyba synchronizace](media/ataGW-not-synced.png)

8.  Zajistěte, aby všechny komponenty ATA Gateway mohly po aktivaci změny synchronizovat své konfigurace.

>[!div class="step-by-step"]
[« IP adresa serveru ATA Center](modifying-ata-config-centerip.md)
[adresa URL konzoly ATA »](modifying-ata-config-consoleurl.md)

## <a name="see-also"></a>Viz také
- [Práce s konzolou ATA](working-with-ata-console.md)
- [Podívejte se na fórum ATA!](https://aka.ms/ata-forum)



<!--HONumber=Feb17_HO1-->



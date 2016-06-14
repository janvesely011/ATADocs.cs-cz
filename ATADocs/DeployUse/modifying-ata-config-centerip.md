---
# required metadata

title: Změna konfigurace ATA – IP adresa ATA Center | Microsoft Advanced Threat Analytics
description: Popisuje, jak změnit IP adresu, port nebo certifikát pro ATA Center.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Změna konfigurace ATA – IP adresa ATA Center

>[!div class="step-by-step"]

Certifikát ATA Center » Po počátečním nasazení by se změny ATA Center měly dělat opatrně.

## Pro aktualizaci IP adresy a portu nebo certifikátu použijte následující postupy.
Změna IP adresy používané serverem ATA Center

Pokud potřebujete změnit IP adresu a port nebo certifikát pro ATA Center, zvažte následující. Komponenty ATA Gateway místně ukládají IP adresu pro ATA Center, ke kterému se potřebují připojit. V pravidelných intervalech se připojují k ATA Center a stahují změny konfigurace.

-   Změna způsobu připojení komponent ATA Gateway k ATA Center se provádí ve dvou fázích. První fáze – Aktualizujte IP adresu a port, které má služba ATA Center používat. V tomto okamžiku ATA Center stále naslouchá na původní IP adrese a při příští synchronizaci konfigurace bude mít ATA Gateway dvě IP adresy pro ATA Center.

-   Dokud se komponenta ATA Gateway bude moct připojit pomocí původní (první) IP adresy, nebude zkoušet novou IP adresu a port. Druhá fáze – Poté, co se všechny komponenty ATA Gateway synchronizovaly s aktualizovanou konfigurací, aktivujte novou IP adresu a port, na kterém ATA Center naslouchá. Po aktivaci nové IP adresy služba ATA Center vytvoří vazbu k nové IP adrese. Komponenty ATA Gateway se nebudou moct připojit k původní adrese a nyní se pokusí připojit s druhou (novou) IP adresou, kterou mají pro ATA Center. Po připojení k ATA Center pomocí nové IP adresy si ATA Gateway stáhne nejnovější konfiguraci a bude mít jednu IP adresu pro ATA Center.

> [!NOTE]
> -   (Pokud nezahájíte postup znovu.)
> -   Pokud během první fáze byla ATA Gateway offline a nikdy nezískala aktualizovanou konfiguraci, budete muset ručně aktualizovat konfigurační soubor JSON v ATA Gateway. Pokud je nová IP adresa nainstalovaná na serveru ATA Center, můžete ji při provádění změny vybrat ze seznamu IP adres. Nicméně pokud z nějakého důvodu nemůžete nainstalovat IP adresu na server ATA Center, můžete vybrat vlastní IP adresu a přidat ji ručně.
> -   Nebudete moct aktivovat novou IP adresu, dokud není IP adresa nainstalovaná na serveru.

1.  Pokud potřebujete nasadit novou ATA Gateway po aktivaci nové IP adresy, budete muset znovu stáhnout instalační balíček ATA Gateway.

2.  Otevřete konzolu ATA.

    ![Vyberte na panelu nástrojů možnost nastavení a vyberte **Konfigurace**.](media/ATA-config-icon.JPG)

3.  Ikona nastavení konfigurace ATA

4.  Vyberte možnost **Obecné**.

5.  V části **ATA Center Service IP address: port** (IP adresa služby ATA Center: port) vyberte některou z existujících IP adres nebo vyberte **Add custom IP address** (Přidat vlastní IP adresu) a zadejte IP adresu.

6.  Klikněte na **Uložit**.

    ![Zobrazí se upozornění, kolik komponent ATA Gateway se synchronizovalo s nejnovější konfigurací.](media/ATA-chge-IP-after-clicking-save.png)

    >[!IMPORTANT]
    >Obrázek synchronizovaných bran ATA Center Před aktivací nové konfigurace ověřte, že jsou všechny komponenty ATA Gateway synchronizované s nejnovější konfigurací. Aktivace nové konfigurace dřív, než se synchronizují všechny komponenty ATA Gateway, může způsobit, že přestanou fungovat podle očekávání.
    >
    >    ![Pokud některá z komponent ATA Gateway není synchronizovaná, zobrazí se po kliknutí na tlačítko pro aktivaci tato chyba:](media/ataGW-not-synced.png)


7.  ATA Gateway – chyba synchronizace

    > Po synchronizaci všech ATA Gateway klikněte na **Aktivovat** a aktivujte novou IP adresu.

8.  Pokud jste zadali vlastní IP adresu, nebudete moct kliknout na **Aktivovat**, dokud nenainstalujete IP adresu na ATA Center. Zajistěte, aby všechny komponenty ATA Gateway mohly po aktivaci změny synchronizovat své konfigurace.

>V oznamovacím pruhu se zobrazí, kolik komponent ATA Gateway úspěšně synchronizovalo svoji konfiguraci.


## [!div class="step-by-step"]
- [Změna certifikátu ATA Center »](working-with-ata-console.md)
- [Viz také](install-ata.md)
- [Práce s konzolou ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Jun16_HO1-->



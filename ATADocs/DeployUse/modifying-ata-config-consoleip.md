---
# required metadata

title: Změna konfigurace ATA – IP adresa konzoly ATA | Microsoft Advanced Threat Analytics
description: Popisuje, jak změnit IP adresu konzoly ATA, která se používá k vytvoření zástupce konzoly ATA na komponentách ATA Gateway.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Změna konfigurace ATA – IP adresa konzoly ATA

>[!div class="step-by-step"]
[« Certifikát ATA Center](modifying-ata-config-centercert.md)
[Certifikát IIS »](modifying-ata-config-iiscert.md)

## Změna IP adresy konzoly ATA
Ve výchozím nastavení adresa URL konzoly ATA je IP adresa, vybraná pro konzolu ATA při instalaci ATA Center.

Adresa URL se používá v následujících scénářích:

-   Instalace komponent ATA Gateway – Při instalaci se ATA Gateway registruje v ATA Center. Tento proces registrace je uskutečněn připojením ke konzole ATA. Pokud zadáte plně kvalifikovaný název domény pro adresu URL konzoly ATA, je potřeba zajistit, že ATA Gateway umí přeložit tento plně kvalifikovaný název domény na IP adresu a že ATA konzola je vázána na službu IIS. Dále se adresa URL používá k vytvoření zástupce konzoly ATA na komponentách ATA Gateway.

-   Výstrahy – Když ATA rozešle výstrahu SIEM nebo e-mailovou výstrahu, zahrnuje odkaz na podezřelou aktivitu. Hostitelská část odkazu je nastavení adresy URL konzoly ATA.

-   Pokud jste nainstalovali certifikát z vaší interní certifikační autority (CA), budete pravděpodobně chtít, aby se adresa URL shodovala s názvem předmětu v certifikátu, takže uživatelům se nebudou zobrazovat upozornění při připojování ke konzole ATA.

-   Použití plně kvalifikovaného názvu domény pro adresu URL konzoly ATA umožňuje změnit IP adresu, kterou používá služba IIS pro konzolu ATA bez přerušení výstrah, které byly rozeslány dřív, a bez nutnosti znovu stahovat balíček ATA Gateway. Je potřeba jenom aktualizovat DNS novou IP adresou.

> [!NOTE]
> Po úpravě adresy URL konzoly ATA byste si měli před instalací nových ATA Gateway stáhnout instalační balíček ATA Gateway.

Pokud potřebujete změnit IP adresu používanou službou IIS pro konzolu ATA, proveďte tyto kroky na serveru ATA Center.

1.  Nainstalujte IP adresu na server ATA Center.

2.  Otevřete Správce Internetové informační služby (IIS).

3.  Rozbalte název serveru a rozbalte **Weby**..

4.  Vyberte web konzoly Microsoft ATA a v podokně **Akce** klikněte na **Vazby**..

    ![Obrázek akce vazby pro konzolu ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Vyberte **HTTP** a kliknutím na **Upravit** vyberte novou IP adresu. Totéž proveďte pro **HTTPS** výběrem stejné IP adresy.

    ![Obrázek Upravit vazbu webu](media/ATA-change-console-IP.jpg)

6.  V podokně **Akce** klikněte v části **Spravovat weby** na **Restartovat**..

7.  Otevřete příkazový řádek správce a aktualizujte ovladač HTTP.SYS pomocí následujících příkazů:

    -   Přidání nové IP adresy – `netsh http add iplisten ipaddress=newipaddress`

    -   Kontrola, že se nová adresa používá – `netsh http show iplisten`

    -   Odstranění staré IP adresy – `netsh http delete iplisten ipaddress=oldipaddress`

8.  Pokud adresa URL konzoly ATA pořád používá IP adresu, aktualizujte adresu URL konzoly ATA na novou IP adresu a stáhněte si před nasazením nových komponent ATA Gateway instalační balíček ATA Gateway.

9. Pokud adresa URL konzoly ATA je plně kvalifikovaný název domény, aktualizujte DNS novou IP adresou pro plně kvalifikovaný název domény.

>[!div class="step-by-step"]
[« Certifikát ATA Center](modifying-ata-config-centercert.md)
[Certifikát IIS »](modifying-ata-config-iiscert.md)


## Viz také
- [Práce s konzolou ATA](/advanced-threat-analytics/understand-explore/working-with-ata-console)
- [Instalace ATA](install-ata.md)
- [Podporu získáte na našem fóru!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO4-->



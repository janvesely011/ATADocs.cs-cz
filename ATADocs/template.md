---
# required metadata

title: [NÁZEV ČLÁNKU | NÁZEV SLUŽBY]
description:
keywords:
author: [GITHUB USERNAME]
manager: [ALIAS]
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: [GET ONE FROM guidgenerator.com]

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Šablona metadat a Markdownu

Tato šablona docs.ms obsahuje příklady syntaxe markdownu společně s pokyny k nastavení metadat. Je uložená v kořenovém adresáři jednotlivých úložišť EM Pilot (například ~/Azure-RMSDocs-pr/template.md) v podobě souboru Markdown, který je možné načíst. Můžete se ale také podívat na [publikovanou verzi](https://stage.docs.microsoft.com/en-us/rights-management/template), abyste viděli, jak se ukázkové soubory Markdown vykreslují.

Při vytváření souboru markdownu byste měli zkopírovat soubor šablonu do nového souboru, vyplnit metadata níže popsaným způsobem, nastavit nadpis H1 výše na název článku a odstranit obsah. 


## Metadata 

Kompletní blok metadat je uveden výše. Je rozdělený na povinná a volitelná pole. Další podrobnosti najdete v tématu [„Tahák“ k metadatům OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data). Důležité poznámky:

- **Musíte** mít mezeru mezi dvojtečkou (:) a hodnotou elementu metadat.
- Pokud volitelný element metadat nemá hodnotu, odkomentujte ho křížkem (#) (nenechávejte ho prázdný ani nepoužívejte hodnotu „na“ [není k dispozici]). Pokud přidáváte hodnotu do elementu, který je odkomentovaný, nezapomeňte znak křížku (#) odebrat.
- Použití dvojteček v hodnotě (např. pro hodnotu title) vedou k chybě analyzátoru metadat. Místo nich použijte kódování HTML &#58; (například "title: Azure Rights Management&#58; – základní informace | Azure RMS").
- **title**: Tento název (title) se zobrazí ve výsledcích vyhledávání vyhledávacího webu. Musí končit svislicí (|), za kterou následuje název služby (např. viz výše). Nemusí být (a pravděpodobně by ani neměl být) stejný jako název v nadpisu H1. Musí mít zhruba 65 znaků (včetně | NÁZEV SLUŽBY)
- **author** (autor), **manager** (vedoucí), **reviewer** (revidující): Pole author musí obsahovat **uživatelské jméno Githubu** autora, ne jeho alias.  Pole manager a reviewer musí naopak obsahovat aliasy. ms.reviewer určuje jméno projektového manažera přidruženého k článku nebo službě.
- **ms.assetid**: GUID článku velkými písmeny. Při vytváření nového souboru markdownu získáte identifikátor GUID z [https://www.guidgenerator.com](https://www.guidgenerator.com). 
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm**: Možné hodnoty pro tyto elementy najdete [tady](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## Základní Markdown a GFM

Je podporovaný jak základní markdown, tak i markdown specifický pro Github. Další informace k nim najdete tady:

- [Syntaxe základního markdownu](https://daringfireball.net/projects/markdown/syntax)
- [Dokumentace k markdownu specifickému pro Github (GFM – Github-Flavored Markdown)](https://guides.github.com/features/mastering-markdown)

## Nadpisy

Příklady nadpisů první a druhé úrovně najdete výše. 

V tématu **musíte** mít jenom jeden nadpis první úrovně. Ten se bude zobrazovat jako nadpis na stránce.  

Nadpisy druhé úrovně se používají ke generování obsahu na stránce, který se zobrazí v části V tomto článku pod názvem (title) na stránce.

### Nadpis třetí úrovně
#### Nadpis čtvrté úrovně
##### Nadpis páté úrovně
###### Nadpis šesté úrovně

## Styl textu

*Kurzíva* 

**Tučné** 

~~Přeškrtnutí~~



## Odkazy

Pokud budete chtít vytvořit odkaz na soubor markdownu ve stejném úložišti, použijte k tomu [relativní odkazy](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2). 

- Příklad: [Co je Azure Rights Management?](./understand-explore/what-is-azure-rights-management.md)

Pokud budete chtít markdown propojit s hlavičkou ve stejném souboru s markdownem, zobrazte si zdroj publikovaného článku, vyhledejte ID hlavičky (například `id="blockquote"`) a vytvořte odkaz zadáním # + ID (například `#blockquote`).

- Příklad: [Bloková citace](#blockquote)

Pokud budete chtít vytvořit odkaz na hlavičku v souboru markdownu ve stejném úložišti, použijte relativní odkaz + hashtag odkaz.

- Příklad: [Technický přehled procesu registrace](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

Pokud budete chtít vytvořit odkaz na externí soubor, použijte jako odkaz úplnou adresu URL.

- Příklad: [Github](http://www.github.com)

Pokud bude v souboru markdownu adresa URL, transformuje se na prokliknutelný odkaz.

- Příklad: http://www.github.com

## Seznamy

### Seřazené seznamy

1. Tento 
1. Seznam
1. Je
1. Seřazený
1. Seznam  


#### Seřazený seznam s vloženým seznamem

1. Tady
1. je
1. vložený
1. seznam
    1. Miss Scarlett
    1. Professor Plum
1. seřazeného
1. seznamu


### Neuspořádané seznamy

- Toto
- je
- seznam
- s odrážkami
- .


##### Neseřazený seznam s vloženými seznamy

- Tento 
- seznam 
- s odrážkami
    - Mrs. Peacock
    - Mr. Green
- obsahuje  
- jiné seznamy
    1. Colonel Mustard
    1. Mrs. White
- .


## Vodorovné pravítko

---

## Tabulky

| Tabulky        | Jsou           | Super  |
| ------------- |:-------------:| -----:|
| sloupec 3 je      | zarovnaný doprava | 1 600 Kč |
| sloupec 2 je      | zarovnaný na střed      |   12 Kč |
| sloupec 1 je ve výchozím nastavení | zarovnaný doleva     |    $1 |


## Kód

### Blok kódu

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### Vložený kód

Toto je příklad pro: `in-line code`.

## Blokové citace

> Posledních deset miliónů let už bylo suchých, vláda strašlivých ještěrů dávno skončila. Tady na rovníku, na kontinentě, který jednoho dne bude známý jako Afrika, znovu dosahoval boj o existenci vrcholu zuřivosti, a vítěz stále ještě nebyl zřejmý. V této pusté a vyprahlé krajině zůstávala naděje na život, ba na pouhé přežití, jen tvorům malým nebo rychlým.

## Bitové kopie

### Statický obrázek

![toto je alternativní text](./media/AzRMS_elements.png)

### Propojený obrázek

[![aText lt pro propojený obrázek](./media/AzRMS_elements.png)](https://azure.microsoft.com) 

### Animovaný gif

![animovaný gif](./media/hololens.gif)

## Výstrahy

### Poznámka

> [!NOTE] Toto je POZNÁMKA.

### Upozornění

> [!WARNING] Toto je UPOZORNĚNÍ.

### Tip

> [!TIP] Toto je TIP.

### Důležité

> [!IMPORTANT] Toto je část DŮLEŽITÉ.

## Videa

### Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### Youtube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## rozšíření docs.ms
Dostupná jsou tato rozšíření:

### Tlačítko

> [!div class="button"] [odkazy na tlačítka](/rights-management)

### Volič

> [!div class="op_single_selector"]
- [zástupný](/rights-management/template.md)
- [panel](/rights-management/scratch.md)

### Postup:

>[!div class="step-by-step"] [Předchozí](https://www.example.com)
[Další](https://www.example.com)

<!--HONumber=Jun16_HO1-->



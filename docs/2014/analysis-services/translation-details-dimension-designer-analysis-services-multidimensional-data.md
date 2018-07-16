---
title: Detalhes de conversão (guia traduções, Designer de dimensão) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.translations.translationpane.tranlationdetails.f1
ms.assetid: 0aa61df3-f2b0-4703-a63b-124da672dcc3
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f4051de358b2567d6473a016e7f965d15b1dd215
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306326"
---
# <a name="translation-details-translations-tab-dimension-designer-analysis-services---multidimensional-data"></a>Detalhes de conversão (guia Conversões, Designer de Dimensão) (Analysis Services - Dados multidimensionais)
  Use o painel **Detalhes da conversão** na guia **Conversões** do Designer de Dimensão para definir e gerenciar conversões da dimensão atualmente selecionada.  
  
 **Para exibir o painel de detalhes da conversão**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e então abra a dimensão desejada.  
  
2.  Clique na guia **Conversões** .  
  
## <a name="options"></a>Opções  
 **Idioma Padrão**  
 Define os nomes dos objetos de dimensão no idioma padrão.  
  
 **Tipo de objeto**  
 Exibe a propriedade que será traduzida. Só podem ser convertidos objetos e propriedades para os quais foram especificados valores. As seguintes propriedades podem ser traduzidas:  
  
-   Dimensão  
  
     `Caption` e `AttributeAllMember` propriedades  
  
-   attribute  
  
     `Caption`, `AttributeHierarchyDisplayFolder`, e `NamingTemplate` propriedades  
  
    > [!NOTE]  
    >  A propriedade `NamingTemplate` só está disponível para atributos pai.  
  
-   Hierarquia  
  
     `Caption` e `AllMemberName` propriedades  
  
-   Nível  
  
     `Caption` Propriedade  
  
 **\<Idioma >**  
 Digite ou selecione o valor de propriedade do objeto de dimensão na linguagem selecionada. Clicar no botão de reticências (**...**) abre caixas de diálogo adicionais, dependendo da propriedade que está sendo editada:  
  
-   `NamingTemplate` Propriedade  
  
     Exibe a [Caixa de diálogo Modelo de Nomeação de Nível &#40;Analysis Services - Dados Multidimensionais&#41;](level-naming-template-dialog-box-analysis-services-multidimensional-data.md).  
  
-   `Caption` propriedade (para atributos)  
  
     Exibe a [Caixa de diálogo Tradução de Dados de Atributo &#40;Analysis Services - Dados Multidimensionais&#41;](attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="shortcut-menu"></a>Menu de atalho  
 As opções seguintes estão disponíveis no menu de atalho exibido ao clicar com o botão direito do mouse em uma conversão no painel **Detalhes de Conversão** :  
  
 **Nova tradução**  
 Selecione para exibir a caixa de diálogo **Selecionar Idioma** e criar uma nova tradução. A conversão aparecerá como uma coluna nova na grade **Detalhes de Conversão** .  
  
 **Excluir tradução**  
 Selecione para excluir a tradução selecionada.  
  
> [!NOTE]  
>  A opção só está habilitada se você clicou com o botão direito do mouse em uma célula para excluir a conversão.  
  
 **Nova coluna de legendas**  
 Selecione para exibir a caixa de diálogo **Conversão de Dados de Atributo** e definir uma nova coluna de legendas quando você modificar um atributo na grade **Detalhes de Conversão** . Para habilitar esta opção, é preciso selecionar uma célula na coluna de conversão de um atributo na grade **Detalhes de Conversão** .  
  
> [!NOTE]  
>  A opção só está habilitada se você clicou com o botão direito do mouse em uma célula para excluir a coluna de conversão de um atributo.  
  
 **Editar coluna de legendas**  
 Selecione para exibir a caixa de diálogo **Conversão de Dados de Atributo** e modificar uma coluna de legendas existente quando você modificar um atributo na grade **Detalhes de Conversão** .  
  
> [!NOTE]  
>  A opção só será habilitada se uma célula em uma coluna de conversão que contém a coluna de legendas de um atributo tiver que ser selecionada na grade **Detalhes de Conversão** .  
  
 **Excluir coluna de legendas**  
 Selecione para excluir a coluna de legendas para o atributo selecionado na grade **Detalhes de Conversão** .  
  
> [!NOTE]  
>  A opção só está habilitada se você clicou com o botão direito em uma célula em uma coluna de conversão que contém uma coluna de legendas para um atributo.  
  
 **Mostrar todos os atributos**  
 Selecione para alternar a exibição de todos os atributos definidos para a dimensão selecionada, inclusive atributos para os quais as hierarquias de atributo estão desabilitadas.  
  
## <a name="see-also"></a>Consulte também  
 [Traduções &#40;Designer de dimensão&#41; &#40;Analysis Services - dados multidimensionais&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  

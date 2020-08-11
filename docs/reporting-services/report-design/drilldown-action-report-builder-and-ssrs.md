---
title: Ação de drill down (Construtor de Relatórios) | Microsoft Docs
description: Permita que usuários com a Ação de drill down ocultem e exibam itens interativamente no Construtor de Relatórios fornecendo ícones e mais e menos em uma caixa de texto.
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10249"
- "10186"
- "10092"
- "10167"
- "10174"
- sql13.rtp.rptdesigner.charttitleproperties.visibility.f1
- "10155"
- sql13.rtp.rptdesigner.chartproperties.visibility.f1
- sql13.rtp.rptdesigner.pictureproperties.visibility.f1
- sql13.rtp.rptdesigner.majorgridlineproperties.visibility.f1
- "10123"
- "10425"
- sql13.rtp.rptdesigner.axisproperties.visibility.f1
- "10217"
- "10161"
- "10215"
- sql13.rtp.rptdesigner.legendproperties.visibility.f1
- "10258"
- "10144"
- sql13.rtp.rptdesigner.subreportproperties.visibility.f1
- sql13.rtp.rptdesigner.textboxproperties.visibility.f1
- "10062"
- sql13.rtp.rptdesigner.serieslabelproperties.visibility.f1
- sql13.rtp.rptdesigner.rectangleproperties.visibility.f1
- sql13.rtp.rptdesigner.calculatedseriesproperties.visibility.f1
- sql13.rtp.rptdesigner.chartareaproperties.visibility.f1
- "10053"
- sql13.rtp.rptdesigner.minorgridlineproperties.visibility.f1
- sql13.rtp.rptdesigner.seriesproperties.visibility.f1
ms.assetid: 1f8d1ef2-0daf-40c6-9ba7-3b391249bcd4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0c917e591bf7de47c7d6084d06cf2064904f8b4a
ms.sourcegitcommit: 6c2232c4d2c1ce5710296ce97b909f5ed9787f66
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84462230"
---
# <a name="drilldown-action-report-builder-and-ssrs"></a>Ação de análise detalhada (Construtor de Relatórios e SSRS)
Ao fornecer ícones de sinal de adição ou de subtração em uma caixa de texto, você permite que os usuários ocultem ou exibam itens interativamente. Isso se chama *busca detalhada* . Para uma tabela ou matriz, você pode mostrar ou ocultar linhas e colunas estáticas ou linhas e colunas que estão associadas a grupos.  
  
 ![rs_drilldown](../../reporting-services/report-design/media/rs-drilldown.gif "rs_drilldown")  
  
 Nesta ilustração, o usuário clica nos sinais de adição (+) no relatório para mostrar dados detalhados.  
  
 Por exemplo, você pode ocultar inicialmente todas as linhas, exceto a linha de resumo do grupo externo de uma tabela com grupos de linhas. Para cada grupo interno (inclusive os grupo de detalhes), adicione um ícone de expandir/recolher à célula de agrupamento do grupo contentor. Quando o relatório for renderizado, o usuário poderá clicar na caixa de texto para expandir e recolher os dados de detalhes. Para obter mais informações, consulte [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
 Para permitir que os usuários expandam ou recolham um item, defina as propriedades de visibilidade do item.  
  
> [!NOTE]  
>  Quando você cria um relatório com uma ação de busca detalhada, as informações de visibilidade devem ser definidas no grupo, na coluna ou na linha que você deseja ocultar, não apenas uma única caixa de texto na linha ou coluna. Além disso, a caixa de texto que você usa para alternância deve estar em um escopo de contenção que controle o item que você deseja mostrar ou ocultar.  
>   
>  Por exemplo, para ocultar uma linha associada a um grupo aninhado, a caixa de texto deve estar em uma linha associada ao grupo pai ou superior na hierarquia de contenção.  
>   
>  Para obter informações sobre como definir informações de visibilidade no grupo, na coluna ou na linha, consulte [Adicionar uma ação de expandir/recolher a um item &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)  
  
 Para obter mais informações sobre como ocultar itens de relatório, consulte [Ocultar um item &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="comparing-drilldown-and-drillthrough-reports"></a>Comparando relatórios de busca detalhada com relatórios detalhados  
 Em um relatório de busca detalhada, um usuário clica em um botão de adição ou subtração para expandir ou recolher uma seção de um relatório para mostrar dados detalhados no local. Em um relatório detalhado, o usuário clica em um link para um valor resumido e isso abre um relatório relacionado separado para mostrar dados de detalhes. Os dados de detalhes só são recuperados quando o relatório de detalhes é executado. Normalmente, os relatórios detalhados exigem menos recursos do que os relatórios de busca detalhada. Para obter mais informações, consulte [Detalhamento, busca detalhada, sub-relatórios e regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md).  
  
## <a name="rendering-extension-support-for-hidden-report-items"></a>Suporte à extensão de renderização para itens de relatório ocultos  
 Só há suporte para a alternância de mostrar e ocultar itens de relatório em extensões de renderização compatíveis com a interatividade de usuário, como a extensão de renderização HTML usada quando você executa um relatório no Construtor de Relatórios e no portal da Web, por exemplo. Outras extensões de renderização exibem itens ocultos. A lista a seguir descreve suporte para itens de relatório com visibilidade condicional:  
  
-   Em HTML, se os itens estiverem ocultos, eles não serão visíveis no código-fonte HTML.  
  
-   A extensão de renderização XML exibe todos os itens do relatório, quer eles estejam ocultos ou não.  
  
-   A extensão de renderização do Excel exibe e expande linhas e colunas ocultas de uma tabela, matriz ou lista. Todas as linhas e colunas são visíveis.  
  
 Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhamento, busca detalhada, sub-relatórios e regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)   
 [Classificação interativa, mapas de documentos e links &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  

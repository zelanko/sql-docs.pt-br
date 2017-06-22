---
title: "Classificar dados em uma região de dados (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2fcb9be2-1daa-4c92-ad00-5f63cdf39f70
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 01fdabcd4005e5b3b15e6c2656daed1cff499211
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="sort-data-in-a-data-region-report-builder-and-ssrs"></a>Classificar dados em uma região de dados (Construtor de Relatórios e SSRS)
  Para alterar a ordem de classificação dos dados em uma região quando um relatório for executado pela primeira vez, defina a expressão de classificação na região de dados ou no grupo. Por padrão, a expressão de classificação de um grupo é definida automaticamente como o mesmo valor da expressão do grupo.  
  
-   Em uma região de dados tablix, defina a expressão de classificação da região de dados ou de cada grupo, inclusive o grupo detalhado. Se você tiver apenas um grupo detalhado em uma região de dados tablix, será possível definir uma expressão de classificação na consulta, na região de dados ou no grupo detalhado, e todos têm o mesmo efeito.  
  
-   Em uma região de dados do gráfico, defina a expressão de classificação dos grupos Categoria e Série para controlar a ordem de classificação de cada um. A ordem das cores em uma legenda de gráfico é determinada pela expressão de classificação dos pontos de dados no grupo Categoria.  
  
-   Em uma região de dados do medidor, você normalmente não precisa classificar dados porque o medidor exibe um único valor relativo a um intervalo. Caso precise classificar dados em um medidor, você deve primeiro definir um grupo e, em seguida, definir a expressão de classificação do grupo.  
  
 Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
 Em uma região de dados tablix, também é possível adicionar um botão de classificação interativo à parte superior do cabeçalho da coluna para permitir que o usuário altere a ordem de classificação dos grupos ou das linhas detalhadas. Para obter mais informações, consulte [Classificação interativa e &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-sort-data-in-a-tablix-data-region"></a>Para classificar dados em uma região de dados Tablix  
  
1.  Na superfície de design, clique com o botão direito do mouse em um identificador de linha e clique em **Propriedades do Tablix**.  
  
2.  Clique em **Classificar**.  
  
3.  Em cada expressão de classificação, siga estas etapas:  
  
    1.  Clique em **Adicionar**.  
  
    2.  Digite ou selecione uma expressão pela qual os dados são classificados.  
  
    3.  Na lista suspensa da coluna **Ordem** , escolha a direção de classificação de cada expressão. **A-Z** classifica a expressão em ordem crescente. **Z-A** classifica a expressão em ordem decrescente.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-values-in-a-group-including-the-details-group-for-a-tablix"></a>Para classificar valores em um grupo, inclusive o grupo detalhado, para um Tablix  
  
1.  Na superfície de design, clique na região de dados tablix para selecioná-la. O painel Agrupamento exibe os grupos de linhas e de colunas da região de dados Tablix.  
  
2.  No painel Grupos de Linhas, clique com o botão direito do mouse no nome do grupo e clique em **Editar Grupo**.  
  
3.  Na caixa de diálogo **Grupo Tablix** , clique em **Classificar**.  
  
4.  Em cada expressão de classificação, siga estas etapas:  
  
    1.  Clique em **Adicionar**.  
  
    2.  Digite ou selecione uma expressão pela qual os dados são classificados.  
  
    3.  Na lista suspensa da coluna **Ordem** , escolha a direção de classificação de cada expressão. **A-Z** classifica a expressão em ordem crescente. **Z-A** classifica a expressão em ordem decrescente.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-x-axis-labels-in-alphabetical-order-on-a-chart"></a>Para classificar rótulos do eixo x em ordem alfabética em um gráfico  
  
1.  Clique com o botão direito do mouse em um campo na área para arrastar e soltar Campo de Categoria e clique em **Propriedades do Grupo de Categorias**.  
  
2.  Na caixa de diálogo **Propriedades do Grupo de Categorias** , clique em **Classificação**.  
  
3.  Em cada expressão de classificação, siga estas etapas:  
  
    1.  Clique em **Adicionar**.  
  
    2.  Selecione a expressão correspondente ao campo de agrupamento. É possível verificar a expressão do campo de agrupamento clicando em **Agrupamento**.  
  
    3.  Na lista suspensa da coluna **Ordem** , escolha a direção de classificação de cada expressão. **A-Z** classifica a expressão em ordem alfabética crescente. **Z-A** classifica a expressão em ordem alfabética decrescente.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-the-data-points-in-ascending-or-descending-order-on-a-chart"></a>Para classificar os pontos de dados em ordem crescente ou decrescente em um gráfico  
  
1.  Clique com o botão direito do mouse em um campo na área para arrastar e soltar Campo de Categoria e clique em **Propriedades do Grupo de Categorias**.  
  
2.  Na caixa de diálogo **Propriedades do Grupo de Categorias** , clique em **Classificação**.  
  
3.  Em cada expressão de classificação, siga estas etapas:  
  
    1.  Clique em **Adicionar**.  
  
    2.  Selecione a expressão correspondente ao campo de dados. Na maior parte dos casos, trata-se de um valor agregado como, por exemplo, `=Sum(Fields!Quantity.Value)`.  
  
    3.  Na lista suspensa da coluna **Ordem** , escolha a direção de classificação de cada expressão. **A-Z** classifica a expressão em ordem crescente. **Z-A** classifica a expressão em ordem decrescente.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-data-in-ascending-or-descending-order-for-display-on-a-gauge"></a>Para classificar dados em ordem crescente ou decrescente a serem exibidos em um medidor  
  
1.  Clique com o botão direito do mouse no medidor e clique em **Adicionar Grupo de Dados**.  
  
2.  Na caixa de diálogo **Propriedades do Grupo do Painel do Medidor** , clique em **Geral** , se necessário.  
  
3.  Em **Expressões de grupo**, clique em **Adicionar**.  
  
4.  Em **Agrupar em**, digite ou selecione uma expressão pela qual agrupar os dados.  
  
5.  Repita as etapas 3 e 4 até que todas as expressões de grupo que deseja usar sejam adicionadas.  
  
6.  Clique em **Classificar**.  
  
7.  Em cada expressão de classificação, siga estas etapas:  
  
    1.  Clique em **Adicionar**.  
  
    2.  Selecione a expressão correspondente ao campo de agrupamento. É possível verificar a expressão do campo de agrupamento clicando em **Agrupamento**.  
  
    3.  Na lista suspensa da coluna **Ordem** , escolha a direção de classificação de cada expressão. **A-Z** classifica a expressão em ordem crescente. **Z-A** classifica a expressão em ordem decrescente.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Para obter mais informações sobre como os dados são agrupados em um medidor, consulte [Medidores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda do Construtor de Relatórios para caixas de diálogo, painéis e assistentes](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Formatando rótulos dos eixos de um gráfico #40;Construtor de Relatórios e SSRS#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Especificar cores consistentes em gráficos com várias formas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
  

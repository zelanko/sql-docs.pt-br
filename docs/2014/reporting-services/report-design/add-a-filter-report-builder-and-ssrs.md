---
title: Adicionar um filtro (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 10ae54e7-0e8a-4dff-995d-05516c51d076
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: d258a21fe4e6e0be3f0cf33230d6e8c5928780b1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516556"
---
# <a name="add-a-filter-report-builder-and-ssrs"></a>Adicionar um filtro (Construtor de Relatórios e SSRS)
  Adicione um filtro a um conjunto de dados, região de dados ou grupo quando quiser incluir ou excluir valores específicos para cálculos ou exibição. Os filtros são aplicados em tempo de execução, primeiro, no conjunto de dados, depois, na região de dados e, em seguida, no grupo, de cima para baixo nas hierarquias de grupo. Em uma tabela, matriz ou lista, os filtros para grupos de linha, grupos de coluna e grupos adjacentes são aplicados de forma independente. Em um gráfico, os filtros para grupos de categoria e grupos de série são aplicados de forma independente.  
  
 Para adicionar um filtro, é necessário especificar uma ou mais equações de filtro. Uma equação de filtro é composta por uma expressão que identifica os dados que você deseja filtrar, um operador, e o valor para comparação. Os tipos de dados dos dados filtrados e o valor devem coincidir. Não há suporte para filtragem de valores de agregação para um conjunto de dados ou região de dados.  
  
 Para filtrar pontos de dados em um gráfico, você pode definir um filtro em um grupo de categoria ou um grupo de série. Por padrão, o gráfico usa a função interna Sum para agregar valores que pertencem ao mesmo grupo em um ponto de dados individual na série. Se você alterar a função de agregação de uma série, deverá alterar a função de agregação na expressão de filtro.  
  
 Para obter mais informações sobre como filtrar conjuntos de dados inseridos e compartilhados, consulte [Adicionar um filtro a um conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-filter-on-a-data-region"></a>Para definir um filtro em uma região de dados  
  
1.  Abra um relatório no modo de exibição de **Design** .  
  
2.  Selecione a região de dados na superfície de design e, em seguida, clique com o botão direito do mouse em  _\<data region>_**Propriedades**. Para um medidor, selecione **Propriedades do Painel de Medidores**. A caixa de diálogo **Propriedades** da _\<data region>_ será aberta.  
  
    > [!NOTE]  
    >  Em uma região de dados do Tablix, clique com o botão direito do mouse na alça de canto da célula, linha ou coluna e clique em **Propriedades do Tablix**.  
  
3.  Clique em **Filtros**. Isso exibirá a lista atual de equações de filtros. Por padrão, a lista está vazia.  
  
4.  Clique em **Adicionar**. Uma nova equação de filtro em branco é exibida.  
  
5.  Em **Expressão**, digite ou selecione a expressão do campo a ser filtrada. Para editar a expressão, clique no botão de expressão (*fx*).  
  
6.  Na caixa suspensa, selecione o tipo de dados que coincide com o tipo de dados da expressão criada na etapa 5.  
  
7.  Na caixa **Operador** , selecione o operador que você deseja que o filtro use para comparar os valores nas caixas **Expressão** e **Valor** . O operador escolhido determinará o número de valores que serão usados na próxima etapa.  
  
8.  Na caixa **Valor** , digite a expressão ou o valor em relação ao qual você deseja que o filtro avalie o valor em **Expressão**.  
  
     Para obter exemplos de equações de filtro, consulte [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md).  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-tablix-row-or-column-group"></a>Para definir um filtro em um grupo de colunas ou linhas Tablix  
  
1.  Abra um relatório no modo de exibição de **Design** .  
  
2.  Clique com o botão direito do mouse na região de dados da tabela, matriz ou lista na superfície de design para selecioná-la. O painel Agrupamento exibe os grupos do item selecionado.  
  
3.  No painel Agrupamento, clique com o botão direito do mouse no grupo e clique em **Editar Grupo**. A caixa de diálogo **Grupo Tablix** é aberta.  
  
4.  Clique em **Filtros**. Isso exibirá a lista atual de equações de filtros. Por padrão, a lista está vazia.  
  
5.  Clique em **Adicionar**. Uma nova equação de filtro em branco é exibida.  
  
6.  Em **Expressão**, digite ou selecione a expressão do campo a ser filtrada. Para editar a expressão, clique no botão de expressão (*fx*).  
  
7.  Na caixa suspensa, selecione o tipo de dados que coincide com o tipo de dados da expressão criada na etapa 5.  
  
8.  Na caixa **Operador** , selecione o operador que você deseja que o filtro use para comparar os valores nas caixas **Expressão** e **Valor** . O operador escolhido determinará o número de valores que serão usados na próxima etapa.  
  
9. Na caixa **Valor** , digite a expressão ou o valor em relação ao qual você deseja que o filtro avalie o valor em **Expressão**.  
  
     Para obter exemplos de equações de filtro, consulte [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-chart-category-group"></a>Para definir um filtro em um grupo de categoria de Gráfico  
  
1.  Abra um relatório no modo de exibição de **Design** .  
  
2.  Na superfície do design, clique duas vezes no gráfico para chamar as zonas de descarte de campo de dados, série e categoria.  
  
3.  Clique com o botão direito do mouse em um campo contido na área para arrastar e soltar do campo de categoria e selecione **Propriedades do Grupo de Categoria**.  
  
4.  Clique em **Filtros**. Isso exibirá a lista atual de equações de filtros. Por padrão, a lista está vazia.  
  
5.  Clique em **Adicionar**. Uma nova equação de filtro em branco é exibida.  
  
6.  Em **Expressão**, digite ou selecione a expressão do campo a ser filtrada. Para editar a expressão, clique no botão de expressão (*fx*).  
  
7.  Na caixa suspensa, selecione o tipo de dados que coincide com o tipo de dados da expressão criada na etapa 5.  
  
8.  Na caixa **Operador** , selecione o operador que você deseja que o filtro use para comparar os valores nas caixas **Expressão** e **Valor** . O operador escolhido determinará o número de valores que serão usados na próxima etapa.  
  
9. Na caixa **Valor** , digite a expressão ou o valor em relação ao qual você deseja que o filtro avalie o valor em **Expressão**.  
  
     Para obter exemplos de equações de filtro, consulte [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-chart-series-group"></a>Para definir um filtro em um grupo de série de Gráfico  
  
1.  Abra um relatório no modo de exibição de **Design** .  
  
2.  Na superfície do design, clique duas vezes no gráfico para chamar as zonas de descarte de campo de dados, série e categoria.  
  
3.  Clique com o botão direito do mouse em um campo contido na área para arrastar e soltar do campo de série e selecione **Propriedades do Grupo de Série**.  
  
4.  Clique em **Filtros**. Isso exibirá a lista atual de equações de filtros. Por padrão, a lista está vazia.  
  
5.  Clique em **Adicionar**. Uma nova equação de filtro em branco é exibida.  
  
6.  Em **Expressão**, digite ou selecione a expressão do campo a ser filtrada. Para editar a expressão, clique no botão de expressão (*fx*).  
  
7.  Na caixa suspensa, selecione o tipo de dados que coincide com o tipo de dados da expressão criada na etapa 5.  
  
8.  Na caixa **Operador** , selecione o operador que você deseja que o filtro use para comparar os valores nas caixas **Expressão** e **Valor** . O operador escolhido determinará o número de valores que serão usados na próxima etapa.  
  
9. Na caixa **Valor** , digite a expressão ou o valor em relação ao qual você deseja que o filtro avalie o valor em **Expressão**.  
  
     Para obter exemplos de equações de filtro, consulte [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](gauges-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  

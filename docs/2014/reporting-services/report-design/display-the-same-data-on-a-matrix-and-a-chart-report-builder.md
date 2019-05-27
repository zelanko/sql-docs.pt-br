---
title: Exibir os mesmos dados em uma matriz e um gráfico (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1262f283-9fc2-4bc1-9c79-457f7642abc7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e3c062c241a6949921b550460488316861e54e8b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106013"
---
# <a name="display-the-same-data-on-a-matrix-and-a-chart-report-builder"></a>Exibir os mesmos dados em uma matriz e um gráfico (Construtor de Relatórios)
  Quando quiser mostrar os mesmos dados em uma matriz e em um gráfico, defina propriedades em ambas as regiões de dados para especificar o mesmo conjunto de dados, além das mesmas expressões para filtros, grupos, classificações e dados.  
  
 Como as regiões de dados terão o mesmo ancestral de dados (o conjunto de dados de relatório), você pode adicionar um botão de classificação interativo à matriz que, quando clicado, altera a ordem de classificação tanto da matriz quanto do gráfico. Para obter mais informações, consulte [Adicionar classificação interativa a uma tabela ou matriz &#40;Construtor de Relatórios e SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
 Para usar os valores do grupo de colunas da matriz como legenda do gráfico, você deve especificar as cores dos dados da série no gráfico e usar as mesmas cores como cores de preenchimento no plano de fundo das caixas de texto da célula da matriz que exibe os valores do grupo. Para obter mais informações, consulte [Especificar cores consistentes em gráficos com várias formas &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
 Em tempo de execução, o relatório pode ficar desorganizado caso haja muitos valores para as definições de grupo. Você talvez precise filtrar valores, combinar grupos ou ajustar o limite do gráfico combinar grupos. Para obter mais informações, consulte [Vinculando várias regiões de dados ao mesmo conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-matrix-and-chart-to-display-the-same-data"></a>Para adicionar uma matriz e um gráfico e exibir os mesmos dados  
  
1.  Abra um relatório no modo Design.  
  
2.  Na guia **Inserir** , no grupo **Regiões de Dados** , clique em **Matriz**e, em seguida, clique no corpo do relatório ou em um retângulo no corpo do relatório. Uma matriz será adicionada ao relatório.  
  
3.  Na guia **Inserir** , no grupo **Regiões de Dados** , clique em **Gráfico**e, em seguida, selecione o tipo de gráfico. Um gráfico será adicionado ao relatório.  
  
4.  (Opcional) Na guia **Inserir** , no grupo **Itens de Relatório** , clique em **Retângulo**e clique no relatório. Um retângulo será adicionado ao relatório. Arraste a matriz e o gráfico das etapas 2 e 3 para o retângulo.  
  
     Ao colocar várias regiões de dados no contêiner do retângulo, você ajuda a controlar como a matriz e o gráfico serão renderizados quando você exibir o relatório.  
  
     Nas próximas etapas, você escolherá o mesmo campo do conjunto de dados que será exibido na matriz e no gráfico.  
  
5.  No painel de dados do relatório, arraste um campo de conjunto de dados numérico para a célula Dados na matriz.  
  
     Por padrão, a função de agregação Sum é usada para calcular o valor do grupo. Caso altere a função de agregação na matriz, você deve alterá-la no gráfico também.  
  
6.  Na matriz, clique com o botão direito do mouse na célula com dados, clique em **Propriedades da Caixa de Texto**e em **Número**. Escolha um formato apropriado ao valor do campo de conjunto de dados.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Arraste o mesmo campo do conjunto de dados que você escolheu na etapa 3 para a área **Valores** no gráfico.  
  
9. No gráfico, clique com o botão direito do mouse no eixo Y, clique em **Propriedades do Eixo**e em **Número**. Escolha o mesmo formato dos dados escolhidos na etapa 4.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Nas próximas etapas, você definirá o grupo de linhas da matriz e o grupo de séries do gráfico usando a mesma expressão, além de definir a ordem de classificação do grupo de séries do gráfico.  
  
11. No painel de dados do relatório, arraste o campo de conjunto de dados que você deseja agrupar por linhas de matriz para o painel Grupos de Linhas.  
  
     Por padrão, o grupo de linhas da matriz adiciona uma expressão de classificação igual à expressão de grupo.  
  
12. Arraste o mesmo campo de conjunto de dados usado na etapa 9 para a área **Grupos de Séries** do gráfico.  
  
13. Clique com o botão direito do mouse na área **Grupos de Séries** e clique em **Propriedades do Grupo de Séries**.  
  
14. Clique em **Classificar**.  
  
15. Clique em **Adicionar**. Uma nova linha é exibida na grade das expressões de classificação.  
  
16. Em **Classificar por**, na lista suspensa, escolha o mesmo campo de conjunto de dados escolhido para agrupamento na etapa 9.  
  
17. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Nas próximas etapas, você definirá o grupo de colunas da matriz e o grupo de categorias do gráfico usando a mesma expressão, além de definir a ordem de classificação do grupo de categorias do gráfico.  
  
18. No painel de dados do relatório, arraste o campo de conjunto de dados que você deseja agrupar por colunas de matriz para o painel Grupos de Colunas.  
  
     Por padrão, o grupo de colunas da matriz adiciona uma expressão de classificação igual à expressão de grupo.  
  
19. Arraste o mesmo campo de conjunto de dados usado na etapa 16 para a área **Grupos de Categorias** do gráfico.  
  
20. Clique com o botão direito do mouse no grupo na área **Grupos de Categorias** e clique em **Propriedades de Grupo de Categorias**.  
  
21. Clique em **Classificar**.  
  
22. Clique em **Adicionar**. Uma nova linha é exibida na grade das expressões de classificação.  
  
23. Em **Classificar por**, na lista suspensa, escolha o mesmo campo de conjunto de dados escolhido para agrupamento na etapa 16.  
  
24. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
25. Visualize o resultado. Os grupos de linhas e de colunas da matriz exibem os mesmos dados dos grupos de séries e de categorias do gráfico.  
  
## <a name="see-also"></a>Consulte também  
 [Vinculando várias regiões de dados ao mesmo conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  

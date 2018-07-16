---
title: Explorando a flexibilidade de uma região de dados Tablix (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fef19359-a618-4d21-a7e4-e391cdefd4eb
caps.latest.revision: 4
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: d4dbdcedec7cf61b3de912bab3e3658c0267f134
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323886"
---
# <a name="exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs"></a>Explorando a flexibilidade de uma região de dados Tablix (Construtor de Relatórios e SSRS)
  Ao adicionar uma tabela, matriz ou região de dados de lista usando a guia Inserir da faixa de opções, você começa com um modelo inicial de região de dados tablix, mas não é limitado por esse modelo. É possível continuar a desenvolver a maneira como os dados são exibidos adicionando ou removendo qualquer recurso de região de dados tablix, como grupos, linhas e colunas.  
  
 Quando você exclui um grupo de linhas ou de colunas, você tem a opção de excluir as linhas e colunas que são usadas para exibir valores de grupo. Também é possível adicionar ou remover manualmente. Para entender como as linhas e colunas são usadas para exibir dados detalhados e agrupados, consulte [região de dados Tablix &#40;construtor de relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md).  
  
 Depois de alterar a estrutura da região de dados tablix, você pode definir propriedades para ajudar a controlar a maneira como o relatório renderiza a região de dados. Por exemplo, é possível repetir cabeçalhos de colunas na parte superior de todas as páginas ou manter um cabeçalho com o grupo. Para obter mais informações, consulte [Controlando a exibição da região de dados Tablix em uma página do relatório &#40;Construtor de Relatórios e SSRS&#41;](controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="changing-a-table-to-a-matrix"></a>Alterando uma tabela para uma matriz  
 Por padrão, uma tabela tem linhas de detalhes que exibem os valores do conjunto de dados do relatório. Normalmente, uma tabela inclui grupos de linhas que organizam os dados de detalhes por grupo e, em seguida, inclui valores agregados com base em cada grupo. Para alterar a tabela para uma matriz, adicione grupos de colunas. Normalmente, você deve remover os grupos de detalhes quando a região de dados tem os grupos de linhas e de colunas para que possa exibir apenas os valores de resumo dos grupos. Para obter mais informações, consulte [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
 Por definição, ao criar uma matriz, você adiciona uma célula de canto tablix. É possível mesclar células nesta área e adicionar um rótulo. Para obter mais informações, consulte [Mesclar células em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](merge-cells-in-a-data-region-report-builder-and-ssrs.md).  
  
## <a name="changing-a-matrix-to-a-table"></a>Alterando uma matriz para uma tabela  
 Por padrão, uma matriz tem grupos de linhas e de colunas e nenhum grupo de detalhes. Para alterar uma matriz para uma tabela, remova grupos de colunas e adicione um grupo de detalhes para exibir nas linhas de detalhes. Para obter mais informações, consulte [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) e [Adicionar um grupo de detalhes &#40;Construtor de Relatórios e SSRS&#41;](add-a-details-group-report-builder-and-ssrs.md).  
  
## <a name="changing-a-default-list-to-a-grouped-list"></a>Alterando uma lista padrão para uma lista agrupada  
 Por padrão, uma lista tem linhas de detalhes e nenhum grupo. Para alterar a lista para usar uma linha de grupo, renomeie o grupo de detalhes e especifique uma expressão de grupo. Para obter mais informações, consulte [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
## <a name="creating-stepped-displays"></a>Criando exibições de nível  
 Por padrão, quando você adiciona grupos a uma região de dados tablix, as células da área do cabeçalho do grupo de linhas exibem valores de grupos na coluna. Quando você tem grupos aninhados, cada grupo é exibido em uma coluna separada. Para criar uma exibição de nível, remova todas as colunas do grupo, exceto uma, e formate a coluna restante para exibir a hierarquia do grupo como uma exibição de texto recuada. Para obter mais informações, consulte [Criar um relatório de nível &#40;Construtor de Relatórios e SSRS&#41;](create-a-stepped-report-report-builder-and-ssrs.md).  
  
## <a name="adding-an-adjacent-details-group"></a>Adicionando um grupo de detalhes adjacente  
 Por padrão, o grupo de detalhes é o grupo filho interno em uma hierarquia de grupo. Você não pode aninhar um grupo sob o grupo de detalhes. Você pode criar grupos de detalhes adjacentes adicionais, para exibir os 5 maiores produtos e os 5 menores produtos por vendas, por exemplo. Com a possibilidade de adicionar expressões de filtro e de classificação a cada grupo, você pode mostrar duas exibições de dados detalhados do mesmo conjunto de dados em uma região de dados tablix. Para obter mais informações, consulte [Noções básicas sobre grupos &#40;Construtor de Relatórios e SSRS&#41;](understanding-groups-report-builder-and-ssrs.md), [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) e [Adicionar um filtro a um conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  

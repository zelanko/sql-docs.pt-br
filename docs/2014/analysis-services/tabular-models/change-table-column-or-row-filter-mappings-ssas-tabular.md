---
title: Alterar tabela, coluna ou mapeamentos de filtro de linha (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2124c526-5772-4f84-a019-9dd3e906e8dd
caps.latest.revision: 9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db70af7541a46fb061a3b668b61040361b261347
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241306"
---
# <a name="change-table-column-or-row-filter-mappings-ssas-tabular"></a>Alterar os mapeamentos de tabela, coluna ou filtro de linha (SSAS tabular)
  Esse tópico descreve como alterar tabela, coluna ou mapeamentos de filtro de linha usando a visualização de tabela ou editor de consulta SQL na caixa de diálogo **Editar Propriedades de Tabela** no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 As opções desta caixa de diálogo **Editar Propriedades da Tabela** são diferentes, dependendo de você ter importado os dados originalmente selecionando tabelas em uma lista ou usando uma consulta SQL. Se você importou os dados originalmente selecionando de uma lista, a caixa de diálogo **Editar Propriedades da Tabela** exibirá o modo de visualização de Tabela. Este modo exibe somente um subconjunto limitado às primeiras cinquenta linhas da tabela de origem. Se você importou os dados originalmente usando uma instrução SQL, a caixa de diálogo **Editar Propriedades da Tabela** somente exibirá uma instrução SQL. Usando uma instrução de consulta SQL, é possível recuperar um subconjunto de linhas, criando um filtro ou editando manualmente a instrução SQL.  
  
 Se você alterar a origem para uma tabela que tenha colunas diferentes das da tabela atual, uma mensagem será exibida, avisando que as colunas são diferentes. Em seguida, você deve selecionar as colunas que deseja colocar na tabela atual e clicar em **Salvar**. Você pode substituir toda a tabela marcando a caixa de seleção no lado esquerdo da tabela.  
  
> [!NOTE]  
>  Se sua tabela tiver mais de uma partição, você não poderá usar a caixa de diálogo Propriedades da Tabela de Edição para alterar os mapeamentos de filtro de linha. Para alterar os mapeamentos de filtro de linha para tabelas com várias partições, use o Gerenciador de Partições. Para obter mais informações, consulte [Partições &#40;SSAS de Tabela&#41;](partitions-ssas-tabular.md).  
  
#### <a name="to-change-table-column-or-row-filter-mappings"></a>Para alterar os mapeamentos de tabela, coluna ou filtro de linha  
  
1.  No designer de modelo, clique na tabela, clique no menu **Tabela** e, clique em **Propriedades da Tabela**.  
  
2.  Na caixa de diálogo **Editar Propriedades da Tabela** , localize a coluna que contém os critérios pelos quais você deseja filtrar e clique na seta para baixo à direita do cabeçalho da coluna.  
  
3.  No menu **AutoFiltro** , siga um destes procedimentos:  
  
    -   Na lista de valores de coluna, selecione ou limpe um ou mais valores pelos quais filtrar e clique em OK.  
  
         Se o número de valores for extremamente grande, os itens individuais poderão não ser mostrados na lista. Em vez disso, você verá a mensagem "Itens demais para mostrar".  
  
    -   Clique em **Filtros de Número** ou em **Filtros de Texto** (dependendo do tipo de coluna) e clique nos comandos de operador de comparação (como Igual a) ou clique em Filtro Personalizado. Na caixa de diálogo **Filtro Personalizado** , crie o filtro e clique em **OK**.  
  
         Se você cometer um erro e precisa recomeçar, clique em **Limpar Filtros de Linha**.  
  
## <a name="see-also"></a>Consulte também  
 [Editar caixa de diálogo de propriedades de tabela &#40;SSAS&#41;](../edit-table-properties-dialog-box-ssas.md)  
  
  

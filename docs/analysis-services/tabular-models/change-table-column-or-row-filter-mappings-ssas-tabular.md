---
title: Alterar tabela, coluna ou mapeamentos de filtro de linha | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2124c526-5772-4f84-a019-9dd3e906e8dd
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 76587faf675131cdf01bc36ad9e27ca29abcd1c8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="change-table-column-or-row-filter-mappings"></a>Alterar os mapeamentos de tabela, coluna ou filtro de linha 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve como alterar tabela, coluna ou mapeamentos de filtro de linha usando o **editar propriedades da tabela** da caixa de diálogo [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 As opções desta caixa de diálogo **Editar Propriedades da Tabela** são diferentes, dependendo de você ter importado os dados originalmente selecionando tabelas em uma lista ou usando uma consulta SQL. Se você importou os dados originalmente selecionando de uma lista, a caixa de diálogo **Editar Propriedades da Tabela** exibirá o modo de visualização de Tabela. Este modo exibe somente um subconjunto limitado às primeiras cinquenta linhas da tabela de origem. Se você importou os dados originalmente usando uma instrução SQL, a caixa de diálogo **Editar Propriedades da Tabela** somente exibirá uma instrução SQL. Usando uma instrução de consulta SQL, é possível recuperar um subconjunto de linhas, criando um filtro ou editando manualmente a instrução SQL.  
  
 Se você alterar a origem para uma tabela que tenha colunas diferentes das da tabela atual, uma mensagem será exibida, avisando que as colunas são diferentes. Em seguida, você deve selecionar as colunas que deseja colocar na tabela atual e clicar em **Salvar**. Você pode substituir toda a tabela marcando a caixa de seleção no lado esquerdo da tabela.  
  
> [!NOTE]  
>  Se sua tabela tiver mais de uma partição, você não poderá usar a caixa de diálogo Propriedades da Tabela de Edição para alterar os mapeamentos de filtro de linha. Para alterar os mapeamentos de filtro de linha para tabelas com várias partições, use o Gerenciador de Partições. Para obter mais informações, consulte [partições](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
#### <a name="to-change-table-column-or-row-filter-mappings"></a>Para alterar os mapeamentos de tabela, coluna ou filtro de linha  
  
1.  No designer de modelo, clique na tabela, clique no menu **Tabela** e, clique em **Propriedades da Tabela**.  
  
2.  Na caixa de diálogo **Editar Propriedades da Tabela** , localize a coluna que contém os critérios pelos quais você deseja filtrar e clique na seta para baixo à direita do cabeçalho da coluna.  
  
3.  No menu **AutoFiltro** , siga um destes procedimentos:  
  
    -   Na lista de valores de coluna, selecione ou limpe um ou mais valores pelos quais filtrar e clique em OK.  
  
         Se o número de valores for extremamente grande, os itens individuais poderão não ser mostrados na lista. Em vez disso, você verá a mensagem "Itens demais para mostrar".  
  
    -   Clique em **Filtros de Número** ou em **Filtros de Texto** (dependendo do tipo de coluna) e clique nos comandos de operador de comparação (como Igual a) ou clique em Filtro Personalizado. Na caixa de diálogo **Filtro Personalizado** , crie o filtro e clique em **OK**.  
  
         Se você cometer um erro e precisa recomeçar, clique em **Limpar Filtros de Linha**.  
  
  
  

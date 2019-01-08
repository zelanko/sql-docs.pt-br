---
title: Filtrar dados em uma tabela de modelo tabular do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9b1fcdda5bd49f8056a6035ec10da8fb52f1c5d1
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072115"
---
# <a name="filter-data-in-a-table"></a>Filtrar dados em uma tabela 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Ao importar dados, é possível aplicar filtros para controlar as linhas que são carregadas em uma tabela. Depois de importar os dados, não é possível excluir linhas individuais. No entanto, você pode aplicar filtros personalizados para controlar a exibição das linhas. As linhas que não atenderem aos critérios de filtragem serão ocultadas. Você pode basear um filtro em uma ou mais colunas. Os filtros são aditivos, ou seja, cada filtro adicional se baseia no filtro atual e reduz ainda mais o subconjunto de dados.  
  
> [!NOTE]  
>  A janela de visualização de filtro limita o número de valores diferentes exibidos. Se o limite for excedido, uma mensagem será exibida.  
  
### <a name="to-filter-data-based-on-column-values"></a>Para filtrar dados com base em valores de coluna  
  
1.  No designer de modelo, selecione uma tabela e clique na seta no cabeçalho da coluna pela qual deseja filtrar.  
  
2.  No menu AutoFiltro, siga um destes procedimentos:  
  
    -   Na lista de valores de coluna, selecione ou limpe um ou mais valores pelos quais filtrar e clique em **OK**.  
  
         Se o número de valores for extremamente grande, os itens individuais poderão não ser mostrados na lista. Em vez disso, você verá a mensagem "Itens demais para mostrar".  
  
    -   Clique em **Filtros de Número** ou em **Filtros de Texto** (dependendo do tipo de coluna) e clique nos comandos de operador de comparação (como **Igual a**) ou clique em **Filtro Personalizado**. Na caixa de diálogo **Filtro Personalizado** , crie o filtro e clique em **OK**.  
  
### <a name="to-clear-a-filter-for-a-column"></a>Para limpar um filtro de uma coluna  
  
1.  Clique na seta no cabeçalho da coluna da qual você deseja limpar um filtro.  
  
2.  Clique em **Limpar filtro de \<nome da coluna >**.  
  
### <a name="to-clear-all-filters-for-a-table"></a>Para desmarcar todos os filtros de uma tabela  
  
1.  No designer de modelo, selecione a tabela para a qual você deseja limpar filtros.  
  
2.  Clique no menu **Coluna** e, em seguida, clique em **Limpar Todos os Filtros**.  
  
## <a name="see-also"></a>Consulte também  
 [Filtrar e classificar dados](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)   
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  

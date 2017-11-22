---
title: Filtrar dados em uma tabela (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.notallitemsshowing.f1
- sql13.asvs.bidtoolset.autofiltermenu.f1
- sql13.asvs.bidtoolset.customfilterdb.f1
ms.assetid: 3223059d-f525-4835-bf88-ebc195d9dbdc
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8277af2c5fb41ae2ae1ad97ab05f9da7c7ce9b84
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="filter-data-in-a-table-ssas-tabular"></a>Filtrar dados em uma tabela (SSAS tabular)
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
 [Filtrar e classificar dados &#40;SSAS de Tabela&#41;](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)   
 [Perspectivas &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Funções &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  

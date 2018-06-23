---
title: Filtrar dados em uma tabela (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.customfilterdb.f1
- sql12.asvs.bidtoolset.autofiltermenu.f1
- sql12.asvs.bidtoolset.notallitemsshowing.f1
ms.assetid: 3223059d-f525-4835-bf88-ebc195d9dbdc
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d58f376d4d7fde1ccd38eab1a1662fb7ad2605cf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116222"
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
 [Filtrar e classificar dados &#40;Tabular do SSAS&#41;](../filter-and-sort-data-ssas-tabular.md)   
 [Perspectivas &#40;Tabular do SSAS&#41;](perspectives-ssas-tabular.md)   
 [Funções &#40;Tabular do SSAS&#41;](roles-ssas-tabular.md)  
  
  
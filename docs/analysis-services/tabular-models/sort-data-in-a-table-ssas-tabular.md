---
title: Classificar dados em uma tabela (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5fa6ad56-bf68-4aac-a226-52556173b7e2
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6cfced262d6b178712da538e9b678ac46357bc1a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="sort-data-in-a-table-ssas-tabular"></a>Classificar dados em uma tabela (SSAS tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Você pode classificar dados por texto (de À Z ou Z a) e números (do menor ao maior ou menor) em uma ou mais colunas.  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-text-column"></a>Para classificar os dados em uma tabela com base em uma coluna de texto  
  
1.  No designer de modelo, selecione uma coluna de dados alfanuméricos, um intervalo de células em uma coluna ou verifique se todas as células ativas estão na coluna de uma tabela que contém dados alfanuméricos e clique na seta no cabeçalho da coluna pela qual deseja filtrar.  
  
2.  No menu AutoFiltro, siga um destes procedimentos:  
  
    -   Para classificar em ordem alfanumérica crescente, clique em **Classificar de A a Z**.  
  
    -   Para classificar em ordem alfanumérica decrescente, clique em **Classificar de Z a A**.  
  
    > [!NOTE]  
    >  Em alguns casos, podem ser inseridos espaços à esquerda antes dos dados importados de outro aplicativo. Você deve remover os espaços à esquerda para classificar os dados corretamente.  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-numeric-column"></a>Para classificar os dados em uma tabela com base em uma coluna numérica  
  
1.  No designer de modelo, selecione uma coluna de dados alfanuméricos, um intervalo de células em uma coluna ou verifique se todas as células ativas estão na coluna de uma tabela que contém dados alfanuméricos e clique na seta no cabeçalho da coluna pela qual deseja filtrar.  
  
2.  No menu AutoFiltro, siga um destes procedimentos:  
  
    -   Para classificar de números baixos para números altos, clique em **Classificar do Menor ao Maior**.  
  
    -   Para classificar de números altos para números baixos, clique em **Classificar do Maior ao Menor**.  
  
    > [!NOTE]  
    >  Se os resultados não forem os esperados, a coluna poderá conter números armazenados como texto e não como números. Por exemplo, os números negativos importados de alguns sistemas de contabilidade ou um número inserido com um ' (apóstrofo) à esquerda são armazenados como texto.  
  
## <a name="see-also"></a>Consulte também  
 [Filtrar e classificar dados &#40;SSAS de Tabela&#41;](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)   
 [Perspectivas &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Funções &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  

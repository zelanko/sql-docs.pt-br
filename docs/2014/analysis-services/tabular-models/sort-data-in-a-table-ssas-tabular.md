---
title: Classificar dados em uma tabela (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5fa6ad56-bf68-4aac-a226-52556173b7e2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc53b6ccc800e2986bf7a6bfdd01c0ef3c3208df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066659"
---
# <a name="sort-data-in-a-table-ssas-tabular"></a>Classificar dados em uma tabela (SSAS tabular)
  É possível classificar dados por texto (de A a Z ou de Z a A) e por números (do menor para o maior ou vice-versa) em uma ou mais colunas.  
  
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
 [Filtrar e classificar dados &#40;SSAS de Tabela&#41;](../filter-and-sort-data-ssas-tabular.md)   
 [Perspectivas &#40;SSAS de Tabela&#41;](perspectives-ssas-tabular.md)   
 [Funções &#40;SSAS de Tabela&#41;](roles-ssas-tabular.md)  
  
  

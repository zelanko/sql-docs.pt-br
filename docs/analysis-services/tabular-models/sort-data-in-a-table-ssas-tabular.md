---
title: Classificar dados em uma tabela | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cdc3e61405c480cbe98810409f20c3ae493c937f
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
---
# <a name="sort-data-in-a-table"></a>Classificar dados em uma tabela 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
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
 [Filtrar e classificar dados](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)   
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  

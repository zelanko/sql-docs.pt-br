---
title: FORMA (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e5c86484252d45c8c7edbd79690159e116d9b3a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37985289"
---
# <a name="ltsource-data-querygt---shape"></a>&lt;consulta de fonte de dados&gt; -forma
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Combina consultas de várias fontes de dados em uma tabela hierárquica única (ou seja, uma tabela com tabelas aninhadas), que se torna a tabela de caso do modelo de mineração.  
  
 A sintaxe completa da **forma** comando está documentado no [!INCLUDE[msCoName](../includes/msconame-md.md)] Data Access Components (MDAC) Software Development Kit (SDK).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SHAPE {<master query>}  
APPEND ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS <column table name>  
[  
     ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS < column table name>  
...  
]       
```  
  
## <a name="arguments"></a>Argumentos  
 *consulta mestre*  
 Consulta que retorna a tabela pai.  
  
 *consulta de tabela filho*  
 Consulta que retorna a tabela aninhada.  
  
 *coluna mestre*  
 Coluna da tabela pai para identificar linhas filho no resultado de uma consulta de tabela filho.  
  
 *coluna filho*  
 Coluna da tabela filho para identificar linhas pai no resultado de uma consulta mestre.  
  
 *nome da tabela de coluna*  
 Nome de coluna recentemente adicionada à tabela pai da tabela aninhada.  
  
## <a name="remarks"></a>Remarks  
 É preciso classificar as consultas pela coluna que relaciona a tabela pai à tabela filho.  
  
## <a name="examples"></a>Exemplos  
 Você pode usar o exemplo a seguir dentro de um [INSERT INTO &#40;DMX&#41; ](../dmx/insert-into-dmx.md) instrução para treinar um modelo que contém uma tabela aninhada. As duas tabelas do **forma** instrução são relacionadas por meio de **OrderNumber** coluna.  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## <a name="see-also"></a>Consulte também  
 [&#60;consulta de fonte de dados&#62;](../dmx/source-data-query.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

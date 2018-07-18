---
title: ATUALIZAÇÃO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4049c6052a4aabcfe7207086db1db19961354eb0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37989688"
---
# <a name="update-dmx"></a>UPDATE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  As alterações a **NODE_CAPTION** coluna no modelo de mineração de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UPDATE <model>.CONTENT  
SET NODE_CAPTION='new caption'  
[WHERE <condition expression>]  
```  
  
## <a name="arguments"></a>Argumentos  
 *modelo*  
 Identificador de modelo.  
  
 *nova legenda*  
 Uma cadeia de caracteres que contém o novo nome para o **NODE_CAPTION** coluna.  
  
 *expressão de condição*  
 Opcional. Uma condição para restringir os valores retornados da lista de colunas.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, o **atualização** instrução altera o nome padrão, `Cluster 1`, para cluster `001` para o nome mais descritivo, `Likely Customers`.  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

---
title: SELECT FROM &lt;modelo&gt;. SAMPLE_CASES (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0838c688b0518bf1fc7ed6c5d65c3ef03d0a7aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928319"
---
# <a name="select-from-ltmodelgtsamplecases-dmx"></a>SELECT FROM &lt;modelo&gt;. SAMPLE_CASES (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna casos de exemplo que representam os casos utilizados para treinar o modelo de mineração de dados.  
  
 Para usar essa instrução é preciso ativar o detalhamento durante a criação do modelo de mineração. Para obter mais informações sobre como habilitar o detalhamento, consulte [criar um modelo de MINERAÇÃO &#40;DMX&#41;](../dmx/create-mining-model-dmx.md), [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md), e [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.SAMPLE_CASES  
[WHERE <condition list>] ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Um inteiro que especifica quantas linhas serão retornadas.  
  
 *lista de expressões*  
 Lista separada por vírgula de identificadores de coluna relacionados.  
  
 *modelo*  
 Identificador de modelo.  
  
 *lista de condições*  
 Opcional. Condições para restringir os valores retornados da lista de colunas.  
  
 *Expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Comentários  
 Casos de exemplo podem ser gerados e podem não existir de fato nos dados de treinamento. O caso retornado é representativo do nó de conteúdo especificado.  
  
 Embora o [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering é a única [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo dá suporte ao uso de SELECT FROM \<modelo >. SAMPLE_CASES, algoritmos de terceiros podem também dar suporte a ele.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna casos de exemplo utilizados para treinar o modelo de mineração de Correio de destino. Usando o [IsInNode &#40;DMX&#41; ](../dmx/isinnode-dmx.md) funcionar a **onde** cláusula retorna apenas casos que estão associados com o nó 000000003'. A cadeia de caracteres de nó pode se encontrar na coluna de NODE_UNIQUE_NAME do conjunto de linhas de esquema.  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>Consulte também  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

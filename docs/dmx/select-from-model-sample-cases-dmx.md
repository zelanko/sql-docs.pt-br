---
title: Selecione do &lt;modelo&gt;. SAMPLE_CASES (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0838c688b0518bf1fc7ed6c5d65c3ef03d0a7aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928319"
---
# <a name="select-from-ltmodelgtsample_cases-dmx"></a>Selecione do &lt;modelo&gt;. SAMPLE_CASES (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna casos de exemplo que representam os casos utilizados para treinar o modelo de mineração de dados.  
  
 Para usar essa instrução é preciso ativar o detalhamento durante a criação do modelo de mineração. Para obter mais informações sobre como habilitar o detalhamento, consulte [criar modelo de mineração &#40;&#41;DMX ](../dmx/create-mining-model-dmx.md), [Selecione em &#40;DMX&#41;](../dmx/select-into-dmx.md)e [alterar estrutura de mineração &#40;&#41;DMX ](../dmx/alter-mining-structure-dmx.md).  
  
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
  
 *expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Comentários  
 Casos de exemplo podem ser gerados e podem não existir de fato nos dados de treinamento. O caso retornado é representativo do nó de conteúdo especificado.  
  
 Embora o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo clustering de sequências seja [!INCLUDE[msCoName](../includes/msconame-md.md)] o único algoritmo que dá suporte \<ao uso de SELECT do modelo>. SAMPLE_CASES, os algoritmos de terceiros também podem oferecer suporte a ele.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna casos de exemplo utilizados para treinar o modelo de mineração de Correio de destino. Usar a função [IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md) na cláusula **Where** retorna apenas os casos associados ao nó ' 000000003 '. A cadeia de caracteres de nó pode se encontrar na coluna de NODE_UNIQUE_NAME do conjunto de linhas de esquema.  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SELECIONAR&#41;&#40;DMX](../dmx/select-dmx.md)   
 [&#40;&#41; instruções de definição de dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

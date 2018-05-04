---
title: SELECT FROM &lt;modelo&gt;. SAMPLE_CASES (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SAMPLE_CASES
- SELECT
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- SELECT FROM <model>.SAMPLE_CASES statement
- mining models [Analysis Services], sample cases
- sample cases [DMX]
- training mining models
ms.assetid: e7a34b9b-3562-4503-bfa7-dd9b12db480a
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 61057143a92c54dbe89342f5d9c666f38e194546
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="select-from-ltmodelgtsamplecases-dmx"></a>SELECT FROM &lt;modelo&gt;. SAMPLE_CASES (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna casos de exemplo que representam os casos utilizados para treinar o modelo de mineração de dados.  
  
 Para usar essa instrução é preciso ativar o detalhamento durante a criação do modelo de mineração. Para obter mais informações sobre como habilitar o detalhamento, consulte [CREATE MINING MODEL &#40;DMX&#41;](../dmx/create-mining-model-dmx.md), [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md), e [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
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
  
## <a name="remarks"></a>Remarks  
 Casos de exemplo podem ser gerados e podem não existir de fato nos dados de treinamento. O caso retornado é representativo do nó de conteúdo especificado.  
  
 Embora o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo msc é o único [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo oferece suporte ao uso de SELECT FROM \<modelo >. SAMPLE_CASES, algoritmos de terceiros podem também dar suporte a ele.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna casos de exemplo utilizados para treinar o modelo de mineração de Correio de destino. Usando o [IsInNode &#40;DMX&#41; ](../dmx/isinnode-dmx.md) funcionar a **onde** cláusula retorna apenas casos que estão associados com o nó 000000003'. A cadeia de caracteres de nó pode se encontrar na coluna de NODE_UNIQUE_NAME do conjunto de linhas de esquema.  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>Consulte também  
 [SELECIONE &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados & #40; DMX & #41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

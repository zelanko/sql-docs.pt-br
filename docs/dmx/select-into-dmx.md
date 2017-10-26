---
title: SELECT INTO (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT
- SELECT_INTO
- SELECT INTO
dev_langs:
- DMX
helpviewer_keywords:
- mining models [Analysis Services], copying
- SELECT INTO statement
- mining models [Analysis Services], creating
- copying mining models
ms.assetid: 31ab9b4c-e20d-41ee-886f-6665c22c6ad5
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: db4e68e8051e1104ce9ed7ad42d8ac9f86a98274
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="select-into-dmx"></a>SELECT INTO (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um novo modelo de mineração que é criado na estrutura de mineração de um modelo de mineração existente. O **SELECT INTO** instrução cria o novo modelo de mineração copiando o esquema e outras informações que não são específicas para o algoritmo real.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT INTO <new model>   
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH[,] [FILTER(<expression>)]]  
FROM <existing model>  
```  
  
## <a name="arguments"></a>Argumentos  
 *novo modelo*  
 Nome exclusivo para o novo modelo que está sendo criado.  
  
 *algoritmo*  
 Nome definido pelo provedor para um algoritmo de mineração de dados.  
  
 *lista de parâmetros*  
 Opcional. Uma lista separada por vírgulas de parâmetros definidos pelo provedor para o algoritmo.  
  
 *expressão*  
 Uma expressão que avalia a uma condição de filtro válida nos dados de treinamento. Para obter mais informações sobre expressões que podem ser usadas como filtros, consulte [filtros para modelos de mineração &#40; Analysis Services – mineração de dados &#41; ](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 *modelo existente*  
 Nome do modelo existente, a ser copiado.  
  
## <a name="remarks"></a>Comentários  
 Se o modelo existente for treinado, o novo modelo será processado automaticamente quando uma instrução for executada. Caso contrário, o novo modelo permanecerá não processado.  
  
 O **SELECT INTO** instrução só funcionará se a estrutura do modelo existente é compatível com o algoritmo do novo modelo. Portanto, essa instrução é mais útil para criação rápida e teste de modelos que se baseiam no mesmo algoritmo. Se você alterar o tipo de algoritmo, o novo algoritmo deverá dar suporte ao tipo de dados de cada coluna no modelo existente ou um erro ocorrerá quando o modelo for processado.  
  
 O **com DETALHAMENTO** cláusula permite o detalhamento no novo modelo de mineração. O detalhamento pode ser habilitado somente durante a criação do modelo.  
  
## <a name="example-1-altering-the-parameters-of-the-model"></a>Exemplo 1: Alterando os parâmetros do modelo  
 O exemplo a seguir cria um novo modelo de mineração com base em um modelo de mineração existente, `TM_Clustering`, que você cria no [Tutorial básico de mineração de dados](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). No novo modelo, o parâmetro CLUSTER_COUNT é modificado para que no máximo cinco clusters existam no modelo. Em contraste, o modelo existente usa o valor padrão que é 10.  
  
```  
SELECT * INTO [New_Clustering]  
USING [Microsoft_Clustering] (CLUSTER_COUNT = 5)   
FROM [TM Clustering]  
```  
  
## <a name="example-2-adding-a-filter-to-the-model"></a>Exemplo 2: Adicionando um filtro ao modelo  
 O exemplo a seguir cria um novo modelo de mineração com base em um modelo de mineração existente e adiciona um filtro ao modelo. O filtro restringe os dados de treinamento a apenas aos clientes que vivem em uma região específica.  
  
```  
SELECT * INTO [Clustering Europe Region]  
USING [Microsoft_Clustering] WITH FILTER(Region='Europe')  
FROM [TM Clustering]  
```  
  
> [!NOTE]  
>  Os filtros aplicados à tabela de casos podem ser alterados com o uso da instrução SELECT INTO, conforme mostrado neste exemplo; no entanto, se o modelo original contiver um filtro em uma tabela aninhada, esse filtro não poderá ser alterado ou removido com o uso dessa sintaxe, mas será copiado sem alterações do modelo original. Para criar um modelo com um filtro diferente em uma tabela aninhada, use a sintaxe ALTER STRTUCTURE... ADD MODEL.  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40; DMX &#41; Instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)  
  
  


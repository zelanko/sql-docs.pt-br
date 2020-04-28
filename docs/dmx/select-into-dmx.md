---
title: SELECT INTO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a2e9fb0dfd3607adc1773d4a43561f32ba650ee5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68887682"
---
# <a name="select-into-dmx"></a>SELECT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Cria um novo modelo de mineração que é criado na estrutura de mineração de um modelo de mineração existente. A instrução **Select Into** cria o novo modelo de mineração copiando o esquema e outras informações que não são específicas do algoritmo real.  
  
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
 Uma expressão que avalia a uma condição de filtro válida nos dados de treinamento. Para obter mais informações sobre expressões que podem ser usadas como filtros, consulte [filtros para modelos de mineração &#40;&#41;de mineração de dados de Analysis Services ](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining).  
  
 *modelo existente*  
 Nome do modelo existente, a ser copiado.  
  
## <a name="remarks"></a>Comentários  
 Se o modelo existente for treinado, o novo modelo será processado automaticamente quando uma instrução for executada. Caso contrário, o novo modelo permanecerá não processado.  
  
 A instrução **Select Into** só funcionará se a estrutura do modelo existente for compatível com o algoritmo do novo modelo. Portanto, essa instrução é mais útil para criação rápida e teste de modelos que se baseiam no mesmo algoritmo. Se você alterar o tipo de algoritmo, o novo algoritmo deverá dar suporte ao tipo de dados de cada coluna no modelo existente ou um erro ocorrerá quando o modelo for processado.  
  
 A cláusula **WITH DRILLTHROUGH** habilita o detalhamento no novo modelo de mineração. O detalhamento pode ser habilitado somente durante a criação do modelo.  
  
## <a name="example-1-altering-the-parameters-of-the-model"></a>Exemplo 1: Alterando os parâmetros do modelo  
 O exemplo a seguir cria um novo modelo de mineração com base em um modelo `TM_Clustering`de mineração existente,, que você cria no [tutorial de mineração de dados básico](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). No novo modelo, o parâmetro CLUSTER_COUNT é modificado para que no máximo cinco clusters existam no modelo. Em contraste, o modelo existente usa o valor padrão que é 10.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#40;&#41; instruções de definição de dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

---
title: SELECT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bf4164308b0fdc9e6ba3fabb756c18214757cde5
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970607"
---
# <a name="select-dmx"></a>SELECT (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  A instrução **Select** em DMX (extensões de mineração de dados) é usada para as seguintes tarefas no Data Mining:  
  
-   Navegar o conteúdo de um modelo de mineração existente  
  
-   Criar previsões de um modelo de mineração existente  
  
-   Criar uma cópia de um modelo de mineração existente.  
  
-   Navegar a estrutura de mineração  
  
 Embora a sintaxe completa desta instrução seja complexa, a principais cláusulas para navegar um modelo e sua estrutura subjacente podem ser sumarizadas como segue:  
  
```  
SELECT [FLATTENED] [TOP <n>] <select list>  
FROM <model/structure>[.aspect]  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
## <a name="flattened"></a>FLATTENED (mesclado/nivelado)  
 Alguns clientes de mineração de dados não podem aceitar conjuntos de resultados em formato hierárquico de um provedor de mineração de dados. O cliente pode não ter a habilidade de manusear a hierarquia ou ele pode ter que armazenar os resultados em uma tabela simples não normalizada. Para converter os dados de tabelas aninhadas para tabelas mescladas, você deve requerer que os resultados da consulta sejam mesclados.  
  
 Para mesclar os resultados da consulta, use a opção **selecionar** sintaxe com o **nivelado** , conforme mostrado no exemplo a seguir:  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>SUPERIOR \<n> e ordenar por  
 Você pode ordenar os resultados de uma consulta usando uma expressão e, em seguida, pode retornar um subconjunto dos resultados usando uma combinação das cláusulas **order by** e **Top** . Isto é útil em um cenário como o de mala direta onde você deseja enviar os resultados para quem tenha mais probabilidade de responder. Você pode ordenar os resultados de uma consulta de previsão de correspondência de destino pela probabilidade de previsão e, em seguida, retornar apenas os \<n> resultados principais.  
  
## <a name="select-list"></a>Lista de seleção  
 O *\<select list>* pode incluir referências de coluna escalares, funções de previsão e expressões. As opções que estão disponíveis dependem do algoritmo e dos contextos seguintes:  
  
-   Se você está consultando uma estrutura de mineração ou um modelo de mineração  
  
-   Se você está consultando conteúdo ou casos  
  
-   Se dados de origem são uma tabela relacional ou um cubo  
  
-   Se você esta fazendo previsões  
  
 Em muitos casos, você pode usar aliases ou criar expressões simples com base nos itens da lista de seleção. Por exemplo, uma expressão simples em colunas de modelo:  
  
```  
SELECT [CustomerID], [Last Name] + ', ' + [FirstName] AS FullName  
FROM <model>.CASES  
```  
  
 O exemplo seguinte cria um alias para uma coluna que contém os resultados de uma função de previsão:  
  
```  
SELECT Predict([Column1], 'Value') as Column1Prediction  
FROM MyModel  
JOIN <source data query>  
```  
  
## <a name="where"></a>WHERE  
 Você pode limitar os casos retornados pela consulta usando uma cláusula **Where** . A cláusula **Where** especifica que as referências de coluna na expressão **Where** devem ter a mesma semântica que as referências de coluna no *\<select list>* da instrução **Select** e só podem retornar uma expressão booleana. A sintaxe da cláusula **Where** é a seguinte  
  
```  
WHERE < condition expression >  
```  
  
 A lista de seleção e a cláusula **Where** de uma instrução **Select** devem seguir as seguintes regras:  
  
-   A lista de seleção deve conter uma expressão que não retorna um resultado Booliano. É possível modificar a expressão, mas ela deve retornar resultados não Boolianos.  
  
-   A cláusula **Where** deve conter uma expressão que retorne um resultado booliano. Você pode modificar a cláusula, mas ela deve retornar um resultado Booliano.  
  
## <a name="predictions"></a>Previsões  
 Há dois tipos de sintaxe que você pode usar para criar previsões:  
  
-   [Selecione o modelo de &#60;&#62; junção de previsão &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [SELECIONAR do modelo de &#60;&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 O primeiro tipo de previsão permite criar previsões complexas em tempo real ou como um lote.  
  
 O segundo tipo de previsão cria uma junção de previsão vazia em uma coluna previsível no modelo de mineração e retorna o estado mais provável da coluna. Os resultados desta consulta estão completamente baseados no conteúdo do modelo de mineração.  
  
 Você pode inserir uma instrução SELECT na consulta de origem de uma instrução SELECT FROM predição JOIN usando a sintaxe a seguir.  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 Para obter mais informações sobre como criar consultas de previsão, consulte [estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md).  
  
## <a name="clause-syntax"></a>Sintaxe da cláusula  
 Devido à complexidade da navegação com a instrução **Select** , os elementos e argumentos de sintaxe detalhados são descritos pela cláusula. Para obter mais informações sobre cada cláusula, clique em um tópico na lista seguinte:  
  
 [SELECIONAR DISTINCT do modelo de &#60;&#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [Selecione do modelo de &#60;&#62;.&#41;DE CONTEÚDO &#40;DMX](../dmx/select-from-model-content-dmx.md)  
  
 [Selecione do modelo de &#60;&#62;. CASOS &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [Selecione do modelo de &#60;&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [Selecione do modelo de &#60;&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [Selecione o modelo de &#60;&#62; junção de previsão &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [SELECIONAR do modelo de &#60;&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 [Selecione &#60;&#62; de estrutura. BOLSAS](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;&#41; instruções de definição de dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)  
  
  

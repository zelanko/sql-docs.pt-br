---
title: SELECT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: def96304f13f57095679056e6eab0a004b5c47d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62658753"
---
# <a name="select-dmx"></a>SELECT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  O **selecionar** instrução em extensões DMX (Data Mining) é usada para as seguintes tarefas em mineração de dados:  
  
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
  
 Para mesclar os resultados da consulta, use o **selecionar** sintaxe com o **FLATTENED** opção, conforme mostrado no exemplo a seguir:  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>Parte superior \<n > e ORDER BY  
 Você pode ordenar os resultados de uma consulta usando uma expressão e, em seguida, pode retornar um subconjunto dos resultados, usando uma combinação da **ORDER BY** e **superior** cláusulas. Isto é útil em um cenário como o de mala direta onde você deseja enviar os resultados para quem tenha mais probabilidade de responder. Você pode ordenar os resultados de um consulta de previsão de endereçamento pela previsão de probabilidade de destino e, em seguida, retornar apenas as principais \<n > resultados.  
  
## <a name="select-list"></a>Lista de seleção  
 O  *\<lista de seleção >* podem incluir referências de coluna escalar, funções de previsão e expressões. As opções que estão disponíveis dependem do algoritmo e dos contextos seguintes:  
  
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
 Você pode limitar os casos que são retornados pela consulta usando um **onde** cláusula. O **onde** cláusula Especifica que a coluna referenciada na **onde** expressão deve ter a mesma semântica que referências de coluna no  *\<lista de seleção >* do **selecione** instrução e pode somente retornar uma expressão booliana. A sintaxe para o **onde** cláusula é da seguinte maneira  
  
```  
WHERE < condition expression >  
```  
  
 A lista de seleção e **onde** cláusula de uma **selecione** instrução deve seguir as regras a seguir:  
  
-   A lista de seleção deve conter uma expressão que não retorna um resultado Booliano. É possível modificar a expressão, mas ela deve retornar resultados não Boolianos.  
  
-   O **onde** cláusula deve conter uma expressão que retorna um resultado booliano. Você pode modificar a cláusula, mas ela deve retornar um resultado Booliano.  
  
## <a name="predictions"></a>Previsões  
 Há dois tipos de sintaxe que você pode usar para criar previsões:  
  
-   [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [SELECT FROM &#60;model&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 O primeiro tipo de previsão permite criar previsões complexas em tempo real ou como um lote.  
  
 O segundo tipo de previsão cria uma junção de previsão vazia em uma coluna previsível no modelo de mineração e retorna o estado mais provável da coluna. Os resultados desta consulta estão completamente baseados no conteúdo do modelo de mineração.  
  
 Você pode inserir uma instrução select na consulta de fonte de uma instrução SELECT FROM PREDICTION JOIN, usando a sintaxe a seguir.  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 Para obter mais informações sobre como criar consultas de previsão, consulte [estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md).  
  
## <a name="clause-syntax"></a>Sintaxe da cláusula  
 Devido à complexidade de navegar com o **selecionar** instrução, elementos de sintaxe detalhados e argumentos são descritos por cláusula. Para obter mais informações sobre cada cláusula, clique em um tópico na lista seguinte:  
  
 [SELECT DISTINCT FROM &#60;model &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [SELECT FROM &#60;model&#62;.CONTENT &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
 [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [SELECT FROM &#60;model&#62;.SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [SELECT FROM &#60;model&#62;.DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [SELECT FROM &#60;model&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 [SELECT FROM &#60;estrutura&#62;. CASOS](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)  
  
  

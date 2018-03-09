---
title: "Estrutura e o uso de consultas de previsão DMX | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- prediction joins [DMX]
- empty prediction joins [DMX]
- natural prediction joins [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- queries [DMX], prediction queries
- singleton query predictions [DMX]
- Data Mining Extensions [Analysis Services], prediction queries
ms.assetid: 098bdaa6-9e7d-4e13-a9aa-eb17ce1750e6
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5f25d8ecd230ca4d2e7aa6a694536e71f5dd0f4e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>Estrutura e uso de consultas de previsão DMX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Em [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você pode usar a consulta de previsão em extensões DMX (Data Mining) para prever valores de coluna desconhecido em um novo conjunto de dados, com base nos resultados de um modelo de mineração.  
  
 O tipo de consulta a ser usado depende de quais informações você quer obter de um modelo. Para criar predições simples em tempo real; por exemplo, e saber se o cliente potencial em um site se encaixa na persona de um comprador de bicicleta, uma consulta singleton seria usada. Para criar um lote de previsões de um conjunto de casos contidos em uma fonte de dados, uma consulta de previsão normal seria usada.  
  
## <a name="prediction-types"></a>Tipos de previsão  
 Use DMX para criar os tipos de previsões a seguir:  
  
 Junção de previsão  
 Use para criar previsões em dados de entrada fundamentados nos padrões que existem no modelo de mineração. Essa instrução de consulta deve ser seguida por um **ON** cláusula que fornece as condições de junção entre as colunas do modelo de mineração e as colunas de entrada.  
  
 Junção de previsão natural  
 Use para criar previsões fundamentadas nos nomes das colunas do modelo de mineração que correspondam exatamente aos nomes das colunas da tabela na qual a consulta é executada. Essa instrução de consulta não requer um **ON** cláusula, porque a condição de junção é gerada automaticamente com base nos nomes correspondentes entre as colunas do modelo de mineração e as colunas de entrada.  
  
 Junção de previsão vazia  
 Use para descobrir a previsão mais provável, sem ter que fornecer dados de entrada. Isto retorna uma previsão que se baseia apenas no conteúdo do modelo de mineração.  
  
 Consulta singleton  
 Use para criar uma previsão através de alimentação de dados na consulta. Essa instrução é útil porque possibilita alimentar um único caso em uma consulta para obter rapidamente o resultado. Por exemplo, use a consulta para prever que alguém que, sendo mulher, com 35 anos de idade e casada, tem probabilidade de adquirir uma bicicleta. Essa consulta não requer uma fonte de dados externa.  
  
## <a name="query-structure"></a>Estrutura da consulta  
 Para criar uma consulta de previsão em DMX, use uma combinação dos seguintes elementos:  
  
-   **SELECIONE [SIMPLIFICADOS]**  
  
-   **TOP**  
  
-   **DE***\<modelo >***PREDICTION JOIN**   
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDENAR POR**  
  
 O **selecione** elemento de uma consulta de previsão define as colunas e expressões que aparecerão no resultado do conjunto e podem incluir os seguintes dados:  
  
-   **Prever** ou **PredictOnly** colunas do modelo de mineração.  
  
-   Qualquer coluna de dados de entrada que seja usada para criar as previsões.  
  
-   Funções que retornam uma coluna de dados.  
  
 O **FROM**  *\<modelo >* **PREDICTION JOIN** elemento define os dados de origem a ser usado para criar a previsão. Para uma consulta singleton, essa é uma série de valores que são atribuídos a colunas. Para uma junção de previsão vazia, é deixado em branco.  
  
 O **ON** elemento mapeia as colunas que são definidas no modelo de mineração para colunas em um conjunto de dados externa. Esse elemento não precisará ser incluído quando forem criadas uma consulta de junção de previsão vazia ou uma junção de previsão natural.  
  
 Você pode usar o **onde** cláusula para filtrar os resultados de uma consulta de previsão. Você pode usar um **superior** ou **ORDER BY** cláusula para selecionar as previsões mais prováveis. Para obter mais informações sobre como usar essas cláusulas, consulte [SELECT &#40; DMX &#41;](../dmx/select-dmx.md).  
  
 Para obter mais informações sobre a sintaxe de uma instrução de previsão, consulte [SELECT FROM &#60; modelo de &#62; JUNÇÃO de previsão &#40; DMX &#41; ](../dmx/select-from-model-prediction-join-dmx.md) e [SELECT FROM &#60; modelo de &#62; &#40; DMX &#41;](../dmx/select-from-model-dmx.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão geral &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  

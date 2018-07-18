---
title: Estrutura e uso de consultas de previsão DMX | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37ff157cbddb0894880f12097c977b923d92f177
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37981908"
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>Estrutura e uso de consultas de previsão DMX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Na [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você pode usar a consulta de previsão em extensões DMX (Data Mining) para prever valores de coluna desconhecido em um novo conjunto de dados, com base nos resultados de um modelo de mineração.  
  
 O tipo de consulta a ser usado depende de quais informações você quer obter de um modelo. Para criar predições simples em tempo real; por exemplo, e saber se o cliente potencial em um site se encaixa na persona de um comprador de bicicleta, uma consulta singleton seria usada. Para criar um lote de previsões de um conjunto de casos contidos em uma fonte de dados, uma consulta de previsão normal seria usada.  
  
## <a name="prediction-types"></a>Tipos de previsão  
 Use DMX para criar os tipos de previsões a seguir:  
  
 Junção de previsão  
 Use para criar previsões em dados de entrada fundamentados nos padrões que existem no modelo de mineração. Essa instrução de consulta deve ser seguida por um **ON** cláusula que fornece as condições de junção entre as colunas do modelo de mineração e as colunas de entrada.  
  
 Junção de previsão natural  
 Use para criar previsões fundamentadas nos nomes das colunas do modelo de mineração que correspondam exatamente aos nomes das colunas da tabela na qual a consulta é executada. Essa instrução de consulta não requer uma **ON** cláusula, porque a condição de junção é gerada automaticamente com base nos nomes correspondentes entre as colunas do modelo de mineração e as colunas de entrada.  
  
 Junção de previsão vazia  
 Use para descobrir a previsão mais provável, sem ter que fornecer dados de entrada. Isto retorna uma previsão que se baseia apenas no conteúdo do modelo de mineração.  
  
 Consulta singleton  
 Use para criar uma previsão através de alimentação de dados na consulta. Essa instrução é útil porque possibilita alimentar um único caso em uma consulta para obter rapidamente o resultado. Por exemplo, use a consulta para prever que alguém que, sendo mulher, com 35 anos de idade e casada, tem probabilidade de adquirir uma bicicleta. Essa consulta não requer uma fonte de dados externa.  
  
## <a name="query-structure"></a>Estrutura da consulta  
 Para criar uma consulta de previsão em DMX, use uma combinação dos seguintes elementos:  
  
-   **SELECIONE [NIVELADOS]**  
  
-   **TOP**  
  
-   **PARTIR***\<modelo >***PREDICTION JOIN**   
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDER BY**  
  
 O **selecionar** elemento de uma consulta de previsão define as colunas e expressões que aparecerão no resultado definido e podem incluir os seguintes dados:  
  
-   **Prever** ou **PredictOnly** colunas do modelo de mineração.  
  
-   Qualquer coluna de dados de entrada que seja usada para criar as previsões.  
  
-   Funções que retornam uma coluna de dados.  
  
 O **FROM**  *\<modelo >* **PREDICTION JOIN** elemento define os dados de origem a ser usado para criar a previsão. Para uma consulta singleton, essa é uma série de valores que são atribuídos a colunas. Para uma junção de previsão vazia, é deixado em branco.  
  
 O **ON** elemento mapeia as colunas que são definidas no modelo de mineração para colunas em um conjunto de dados externo. Esse elemento não precisará ser incluído quando forem criadas uma consulta de junção de previsão vazia ou uma junção de previsão natural.  
  
 Você pode usar o **onde** cláusula para filtrar os resultados de uma consulta de previsão. Você pode usar um **superior** ou **ORDER BY** cláusula para selecionar as previsões mais prováveis. Para obter mais informações sobre como usar essas cláusulas, consulte [selecione &#40;DMX&#41;](../dmx/select-dmx.md).  
  
 Para obter mais informações sobre a sintaxe de uma instrução de previsão, consulte [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41; ](../dmx/select-from-model-prediction-join-dmx.md) e [SELECT FROM &#60;modelo&#62; &#40;DMX &#41;](../dmx/select-from-model-dmx.md).  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  

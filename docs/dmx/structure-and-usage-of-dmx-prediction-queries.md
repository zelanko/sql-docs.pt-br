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
ms.openlocfilehash: 99d8ef98ad4e86bce0e1beff819a8d140662aaf7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938065"
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>Estrutura e uso de consultas de previsão DMX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] No [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você pode usar a consulta de previsão no DMX (extensões de Data Mining) para prever valores de coluna desconhecidos em um novo conjunto de dados, com base nos resultados de um modelo de mineração.  
  
 O tipo de consulta a ser usado depende de quais informações você quer obter de um modelo. Para criar predições simples em tempo real; por exemplo, e saber se o cliente potencial em um site se encaixa na persona de um comprador de bicicleta, uma consulta singleton seria usada. Para criar um lote de previsões de um conjunto de casos contidos em uma fonte de dados, uma consulta de previsão normal seria usada.  
  
## <a name="prediction-types"></a>Tipos de previsão  
 Use DMX para criar os tipos de previsões a seguir:  
  
 Junção de previsão  
 Use para criar previsões em dados de entrada fundamentados nos padrões que existem no modelo de mineração. Essa instrução de consulta deve ser seguida por uma cláusula **on** que fornece as condições de junção entre as colunas do modelo de mineração e as colunas de entrada.  
  
 Junção de previsão natural  
 Use para criar previsões fundamentadas nos nomes das colunas do modelo de mineração que correspondam exatamente aos nomes das colunas da tabela na qual a consulta é executada. Essa instrução de consulta não requer uma cláusula **on** , porque a condição de junção é gerada automaticamente com base nos nomes correspondentes entre as colunas do modelo de mineração e as colunas de entrada.  
  
 Junção de previsão vazia  
 Use para descobrir a previsão mais provável, sem ter que fornecer dados de entrada. Isto retorna uma previsão que se baseia apenas no conteúdo do modelo de mineração.  
  
 Consulta singleton  
 Use para criar uma previsão através de alimentação de dados na consulta. Essa instrução é útil porque possibilita alimentar um único caso em uma consulta para obter rapidamente o resultado. Por exemplo, use a consulta para prever que alguém que, sendo mulher, com 35 anos de idade e casada, tem probabilidade de adquirir uma bicicleta. Essa consulta não requer uma fonte de dados externa.  
  
## <a name="query-structure"></a>Estrutura da consulta  
 Para criar uma consulta de previsão em DMX, use uma combinação dos seguintes elementos:  
  
-   **SELECIONAR [ACHATADO]**  
  
-   **INÍCIO**  
  
-   **Do***\<modelo>* **junção de previsão**      
  
-   **Ligado**  
  
-   **WHERE**  
  
-   **ORDER BY**  
  
 O elemento **Select** de uma consulta de previsão define as colunas e expressões que serão exibidas no conjunto de resultados e pode incluir os seguintes dados:  
  
-   **Preveja** ou **PredictOnly** colunas do modelo de mineração.  
  
-   Qualquer coluna de dados de entrada que seja usada para criar as previsões.  
  
-   Funções que retornam uma coluna de dados.  
  
 O elemento **do** * \<modelo>* **junção de previsão** define os dados de origem a serem usados para criar a previsão. Para uma consulta singleton, essa é uma série de valores que são atribuídos a colunas. Para uma junção de previsão vazia, é deixado em branco.  
  
 O elemento **on** mapeia as colunas que são definidas no modelo de mineração para colunas em um conjunto de um DataSet externo. Esse elemento não precisará ser incluído quando forem criadas uma consulta de junção de previsão vazia ou uma junção de previsão natural.  
  
 Você pode usar a cláusula **Where** para filtrar os resultados de uma consulta de previsão. Você pode usar uma cláusula **Top** ou **order by** para selecionar previsões mais prováveis. Para obter mais informações sobre como usar essas cláusulas, consulte [SELECT &#40;DMX&#41;](../dmx/select-dmx.md).  
  
 Para obter mais informações sobre a sintaxe de uma instrução de previsão, consulte [selecionar do modelo de &#60;&#62; junção de previsão &#40;dmx&#41;](../dmx/select-from-model-prediction-join-dmx.md) e [selecione do modelo de &#60;&#62; &#40;DMX ](../dmx/select-from-model-dmx.md)&#41;.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  

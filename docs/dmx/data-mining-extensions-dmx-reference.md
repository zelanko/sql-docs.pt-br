---
title: Referência de DMX (extensões de Data Mining) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 02c7185ebbf264ebf8ed8adda4915170f888e74b
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971768"
---
# <a name="data-mining-extensions-dmx-reference"></a>Referência DMX (Data Mining Extensions)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  O DMX (Data Mining Extensions) é uma linguagem que você pode usar para criar e trabalhar com modelos de Data Mining no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . É possível usar a DMX para criar a estrutura de novos modelos de mineração de dados e, com base nesses mesmos modelos, treiná-los e realizar pesquisas, gerenciamento e previsão. A extensão DMX é composta de instruções DLL (linguagem de definição de dados), instruções DML (linguagem de manipulação de dados), funções e operadores.  
  
## <a name="microsoft-ole-db-for-data-mining-specification"></a>Especificação do Microsoft OLE DB for Data Mining  
 Os recursos de Data Mining no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] são criados para cumprir a [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para especificação de mineração de dados.  
  
 O [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para especificação de mineração de dados define o seguinte:  
  
-   Uma estrutura para reter as informações que definem um modelo de mineração de dados.  
  
-   Uma linguagem para criar e trabalhar com modelos de mineração de dados.  
  
 A especificação define a base da mineração de dados como objeto virtual do modelo de mineração de dados. O objeto do modelo de mineração de dados encapsula tudo o que é conhecido sobre um modelo particular de mineração. O modelo do objeto de mineração de dados é estruturado como uma tabela SQL, com colunas, tipos de dados e informações meta que descrevem o modelo. Essa estrutura permite o uso da linguagem DMX, que é uma extensão de SQL, para criar e trabalhar com modelos.  
  
 **Para obter mais informações:** [estruturas de mineração &#40;mineração de dados Analysis Services&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-structures-analysis-services-data-mining)  
  
##  <a name="dmx-statements"></a><a name="BKMK_DMXStatements"></a>Instruções DMX  
 As instruções DMX podem ser usadas para criar, processar, excluir, copiar, pesquisar e prever, de acordo com modelos de mineração de dados. Há dois tipos de instruções em DMX: as instruções de definição de dados e as instruções de manipulação de dados. Cada um desses tipos de instrução podem executar diferentes tipos de tarefas.  
  
 As seções a seguir fornecem mais informações sobre como trabalhar com as instruções DMX:  
  
-   [Instruções de definição de dados](#BKMK_DDL)  
  
-   [Instruções de manipulação de dados](#BKMK_DML)  
  
-   [Conceitos básicos de consulta](#BKMK_Queries)  
  
###  <a name="data-definition-statements"></a><a name="BKMK_DDL"></a>Instruções de definição de dados  
 Use as instruções de definição de dados em DMX para criar e definir novos modelos e estruturas de mineração, para importar e exportar modelos de mineração e estruturas de mineração, e para ignorar modelos existentes no banco de dados. As instruções de definição de Dados em DMX integram a DDL (data definition language).  
  
 É possível executar as tarefas a seguir com instruções de definição de dados em DMX:  
  
-   Crie uma estrutura de mineração usando a instrução [criar estrutura de mineração](../dmx/create-mining-structure-dmx.md) e adicione um modelo de mineração à estrutura de mineração usando a instrução [ALTER MINING STRUCTURE](../dmx/alter-mining-structure-dmx.md) .  
  
-   Crie um modelo de mineração e uma estrutura de mineração associada simultaneamente usando a instrução [criar modelo de mineração](../dmx/create-mining-model-dmx.md) para criar um objeto de modelo de Data Mining vazio.  
  
-   Exporte um modelo de mineração e uma estrutura de mineração associada a um arquivo usando a instrução [Export](../dmx/export-dmx.md) . Importe um modelo de mineração e uma estrutura de mineração associada de um arquivo criado pela instrução EXPORT usando a instrução [Import](../dmx/import-dmx.md) .  
  
-   Copie a estrutura de um modelo de mineração existente em um novo modelo e treine-o com os mesmos dados, usando a instrução [Select Into](../dmx/select-into-dmx.md) .  
  
-   Remova completamente um modelo de mineração de um banco de dados usando a instrução [drop Mining Model](../dmx/drop-mining-model-dmx.md) . Remova completamente uma estrutura de mineração e todos os seus modelos de mineração associados do banco de dados usando a instrução [DROP MINING STRUCTURE](../dmx/drop-mining-structure-dmx.md) .  
  
 Para saber mais sobre as tarefas de Data Mining que você pode executar usando instruções DMX, consulte [referência de instrução de&#41; de Data Mining Extensions &#40;DMX](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [De volta às instruções DMX](#BKMK_DMXStatements)  
  
###  <a name="data-manipulation-statements"></a><a name="BKMK_DML"></a>Instruções de manipulação de dados  
 Use instruções de manipulação de dados em DMX de trabalhar com modelos de mineração existentes, para pesquisar os modelos e criar previsões segundo esses modelos. As instruções de manipulação de dados em DMX integram a DML (data manipulation language).  
  
 Execute as tarefas a seguir com as instruções de manipulação de dados em DMX:  
  
-   Treine um modelo de mineração usando a instrução [INSERT INTO](../dmx/insert-into-dmx.md) . Isso não inserirá os dados de origem verdadeiros no objeto de modelo de mineração de dados. Em vez disso, criará uma abstração que descreve o modelo de mineração criado pelo algoritmo. A consulta de origem para uma instrução INSERT INTO é descrita em [\<source data query>](../dmx/source-data-query.md) .  
  
-   Estenda a instrução SELECT para procurar as informações calculadas durante o treinamento do modelo e armazenadas no modelo de Data Mining, como estatísticas dos dados de origem. A seguir estão as cláusulas que você pode incluir para estender o poder da instrução SELECT:  
  
    -   [SELECIONAR DISTINCT do modelo de &#60;&#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
    -   [Selecione do modelo de &#60;&#62;.&#41;DE CONTEÚDO &#40;DMX](../dmx/select-from-model-content-dmx.md)  
  
    -   [Selecione do modelo de &#60;&#62;. CASOS &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
    -   [Selecione do modelo de &#60;&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
    -   [Selecione do modelo de &#60;&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
-   Crie previsões que se baseiam em um modelo de mineração existente usando a cláusula de [junção de previsão](../dmx/select-from-model-prediction-join-dmx.md) da instrução SELECT. A consulta de origem para uma instrução de junção de previsão é descrita em [\<source data query>](../dmx/source-data-query.md) .  
  
-   Remova todos os dados treinados de um modelo ou de uma estrutura usando a instrução [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md) .  
  
 Para saber mais sobre as tarefas de Data Mining que você pode executar usando instruções DMX, consulte [referência de instrução de&#41; de Data Mining Extensions &#40;DMX](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [De volta às instruções DMX](#BKMK_DMXStatements)  
  
###  <a name="dmx-query-fundamentals"></a><a name="BKMK_Queries"></a>Conceitos básicos de consulta DMX  
 A instrução SELECT é a base para a maioria das consultas do DMX. Dependendo das cláusulas usadas em tais instruções, é possível pesquisar, copiar ou prever de acordo com os modelos de mineração. A consulta de previsão usa uma forma de selecionar para criar previsões com base em modelos de mineração existentes. As funções estendem sua capacidade de pesquisar e consultar os modelos de mineração além dos recursos intrínsecos do modelo de mineração de dados.  
  
 Use funções DMX para obter as informações que são descobertas durante o treinamento dos modelos e para calcular novas informações. É possível usar essas funções para várias finalidades, inclusive para retornar estatísticas que descrevem os dados subjacentes ou a precisão da previsão, ou para retornar uma explicação expandida de uma previsão.  
  
 **Para obter mais**  **informações:** [noções básicas sobre a instrução DMX SELECT](../dmx/understanding-the-dmx-select-statement.md), [funções de previsão gerais &#40;&#41;DMX ](../dmx/general-prediction-functions-dmx.md), [estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md), [extensões de Data Mining &#40;referência de função&#41; DMX](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
 [De volta às instruções DMX](#BKMK_DMXStatements)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  

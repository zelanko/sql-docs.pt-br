---
title: Referência Data Mining Extensions (DMX) | Microsoft Docs
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
dev_langs:
- DMX
helpviewer_keywords:
- DMX [Analysis Services]
- statements [DMX]
- Data Mining Extensions [Analysis Services], statements
- DMX [Analysis Services], about Data Mining Extensions
- DMX [Analysis Services], statements
- data definition statements [DMX]
- predictions [DMX]
- Data Mining Extensions [Analysis Services]
- SSAS, DMX
- queries [DMX], extensions reference
- SQL Server Analysis Services, DMX
- OLE DB for Data Mining
- data manipulation statements [DMX]
- Data Mining Extensions [Analysis Services], about Data Mining Extensions
- mining models [Analysis Services], DMX
ms.assetid: 6d85ca20-de67-4e20-b3b5-b734c6cfcece
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 19459505832734371724444b9c862351101791f0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-extensions-dmx-reference"></a>Referência DMX (Data Mining Extensions)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Extensões DMX (Data Mining) é uma linguagem que você pode usar para criar e trabalhar com modelos de mineração de dados no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. É possível usar a DMX para criar a estrutura de novos modelos de mineração de dados e, com base nesses mesmos modelos, treiná-los e realizar pesquisas, gerenciamento e previsão. A extensão DMX é composta de instruções DLL (linguagem de definição de dados), instruções DML (linguagem de manipulação de dados), funções e operadores.  
  
## <a name="microsoft-ole-db-for-data-mining-specification"></a>Especificação do Microsoft OLE DB for Data Mining  
 Os recursos de mineração de dados no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] são criados de acordo com o [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para especificação de mineração de dados.  
  
 O [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para mineração de dados define o seguinte:  
  
-   Uma estrutura para reter as informações que definem um modelo de mineração de dados.  
  
-   Uma linguagem para criar e trabalhar com modelos de mineração de dados.  
  
 A especificação define a base da mineração de dados como objeto virtual do modelo de mineração de dados. O objeto do modelo de mineração de dados encapsula tudo o que é conhecido sobre um modelo particular de mineração. O modelo do objeto de mineração de dados é estruturado como uma tabela SQL, com colunas, tipos de dados e informações meta que descrevem o modelo. Essa estrutura permite o uso da linguagem DMX, que é uma extensão de SQL, para criar e trabalhar com modelos.  
  
 **Para obter mais informações:** [estruturas de mineração &#40;Analysis Services – mineração de dados&#41;](../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
##  <a name="BKMK_DMXStatements"></a> Instruções DMX  
 As instruções DMX podem ser usadas para criar, processar, excluir, copiar, pesquisar e prever, de acordo com modelos de mineração de dados. Há dois tipos de instruções em DMX: as instruções de definição de dados e as instruções de manipulação de dados. Cada um desses tipos de instrução podem executar diferentes tipos de tarefas.  
  
 As seções a seguir fornecem mais informações sobre como trabalhar com as instruções DMX:  
  
-   [Instruções de definição de dados](#BKMK_DDL)  
  
-   [Instruções de manipulação de dados](#BKMK_DML)  
  
-   [Conceitos básicos de consulta](#BKMK_Queries)  
  
###  <a name="BKMK_DDL"></a> Instruções de definição de dados  
 Use as instruções de definição de dados em DMX para criar e definir novos modelos e estruturas de mineração, para importar e exportar modelos de mineração e estruturas de mineração, e para ignorar modelos existentes no banco de dados. As instruções de definição de Dados em DMX integram a DDL (data definition language).  
  
 É possível executar as tarefas a seguir com instruções de definição de dados em DMX:  
  
-   Criar uma estrutura de mineração usando o [criar estrutura de MINERAÇÃO](../dmx/create-mining-structure-dmx.md) instrução e adicionar um modelo de mineração à estrutura de mineração usando o [ALTER MINING STRUCTURE](../dmx/alter-mining-structure-dmx.md) instrução.  
  
-   Criar um modelo de mineração e a estrutura de mineração associada ao mesmo tempo usando o [criar modelo de MINERAÇÃO](../dmx/create-mining-model-dmx.md) instrução para criar um objeto de modelo de mineração de dados vazio.  
  
-   Exportar um modelo de mineração e a estrutura de mineração associada para um arquivo usando o [exportar](../dmx/export-dmx.md) instrução. Importar um modelo de mineração e uma estrutura de mineração associados de um arquivo que é criado pela instrução exportação usando o [importação](../dmx/import-dmx.md) instrução.  
  
-   Copiar a estrutura de um modelo de mineração existente em um novo modelo e treiná-lo com os mesmos dados, usando o [SELECT INTO](../dmx/select-into-dmx.md) instrução.  
  
-   Remover completamente um modelo de mineração de um banco de dados usando o [DROP MINING MODEL](../dmx/drop-mining-model-dmx.md) instrução. Remover completamente uma estrutura de mineração e todos os seus modelos de mineração associados do banco de dados usando o [DROP MINING STRUCTURE](../dmx/drop-mining-structure-dmx.md) instrução.  
  
 Para saber mais sobre as tarefas de mineração de dados que você pode executar usando instruções DMX, consulte [Data Mining Extensions &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [De volta às instruções DMX](#BKMK_DMXStatements)  
  
###  <a name="BKMK_DML"></a> Instruções de manipulação de dados  
 Use instruções de manipulação de dados em DMX de trabalhar com modelos de mineração existentes, para pesquisar os modelos e criar previsões segundo esses modelos. As instruções de manipulação de dados em DMX integram a DML (data manipulation language).  
  
 Execute as tarefas a seguir com as instruções de manipulação de dados em DMX:  
  
-   Treinar um modelo de mineração usando o [INSERT INTO](../dmx/insert-into-dmx.md) instrução. Isso não inserirá os dados de origem verdadeiros no objeto de modelo de mineração de dados. Em vez disso, criará uma abstração que descreve o modelo de mineração criado pelo algoritmo. A consulta de origem para uma instrução INSERT INTO é descrita em [ \<consulta de fonte de dados >](../dmx/source-data-query.md).  
  
-   Estenda a instrução SELECT para pesquisar as informações que são calculadas durante o treinamento do modelo e armazenadas no modelo de mineração de dados, como estatísticas dos dados de origem. A seguir estão as cláusulas que podem ser incluídas para estender o poder da instrução SELECT:  
  
    -   [SELECT DISTINCT FROM &#60;modelo &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
    -   [SELECT FROM &#60;modelo&#62;. CONTEÚDO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
    -   [SELECT FROM &#60;modelo&#62;. CASOS &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
    -   [SELECT FROM &#60;modelo&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
    -   [SELECT FROM &#60;modelo&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
-   Criar previsões com base em um modelo de mineração existente usando o [PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) cláusula da instrução SELECT. A consulta de origem para uma instrução PREDICTION JOIN é descrita em [ \<consulta de fonte de dados >](../dmx/source-data-query.md).  
  
-   Remover todos os dados treinados de um modelo ou uma estrutura usando a [excluir &#40;DMX&#41; ](../dmx/delete-dmx.md) instrução.  
  
 Para saber mais sobre as tarefas de mineração de dados que você pode executar usando instruções DMX, consulte [Data Mining Extensions &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [De volta às instruções DMX](#BKMK_DMXStatements)  
  
###  <a name="BKMK_Queries"></a> Conceitos básicos de consulta DMX  
 A instrução SELECT é a base para a maioria das consultas DMX. Dependendo das cláusulas usadas em tais instruções, é possível pesquisar, copiar ou prever de acordo com os modelos de mineração. A consulta de previsão usa um formulário de seleção para criar previsões com base em modelos de mineração existentes. As funções estendem sua capacidade de pesquisar e consultar os modelos de mineração além dos recursos intrínsecos do modelo de mineração de dados.  
  
 Use funções DMX para obter as informações que são descobertas durante o treinamento dos modelos e para calcular novas informações. É possível usar essas funções para várias finalidades, inclusive para retornar estatísticas que descrevem os dados subjacentes ou a precisão da previsão, ou para retornar uma explicação expandida de uma previsão.  
  
 **Para obter mais****informações:** [Noções básicas sobre o DMX instrução Select](../dmx/understanding-the-dmx-select-statement.md), [funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md), [Estrutura e o uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md), [extensões de mineração de dados &#40;DMX&#41; referência de função  ](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
 [De volta às instruções DMX](#BKMK_DMXStatements)  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados & #40; DMX & #41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e o uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  

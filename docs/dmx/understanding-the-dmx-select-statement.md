---
title: "Noções básicas sobre o DMX instrução Select | Microsoft Docs"
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
dev_langs:
- DMX
helpviewer_keywords:
- browsing mining model [Analysis Services]
- Data Mining Extensions [Analysis Services], statements
- DMX [Analysis Services], statements
- predictions [DMX]
- queries [DMX], Select statement
- SELECT statement [DMX]
- statements [DMX], SELECT statement
- copying mining models
ms.assetid: 61e97285-4a06-4434-9a40-38cde5af7c3f
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7431bc5b84d76725904fff27f63c73121e13fa48
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="understanding-the-dmx-select-statement"></a>Compreendendo a instrução DMX Select
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O [selecione](../dmx/select-dmx.md) instrução é a base para a maioria das consultas que você cria com extensões DMX (Data Mining) em [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Pode executar muitos tipos diferentes de tarefas, como pesquisar e prever com base em modelos de mineração de dados.  
  
 A seguir está as tarefas que você pode concluir usando o **selecione** instrução:  
  
-   Pesquisar um modelo de mineração de dados. O conjunto de linhas de esquema define a estrutura de um modelo.  
  
-   Descobrir os possíveis valores de uma coluna de modelo de mineração.  
  
-   Navegar pelos casos que são atribuídos a nós em um modelo de mineração ou obter um caso representativo.  
  
-   Criar previsões usando uma variedade de entradas.  
  
-   Copiar modelos de mineração.  
  
 Cada uma dessas tarefas usa um conjunto diferente de dados, que chamaremos de um *domínio de dados*. Definir o domínio de dados no **FROM** cláusula da instrução.  
  
-   Você deseja localizar os objetos no próprio modelo de mineração de dados, assim como a regra que define um conjunto de dados, ou uma fórmula usada para fazer previsões.  
  
     Nesse caso, você precisa examinar os metadados armazenados no próprio modelo. Portanto, o domínio de dados são as colunas no conjunto de linhas do esquema de mineração de dados.  
  
-   Você deseja obter informações detalhadas dos casos usados para criar o modelo.  
  
     Nesse caso, você precisa detalhar a estrutura de mineração, que é o domínio de dados, e verificar as linhas individuais em colunas como Gender, Bike Buyer e assim por diante.  
  
 **IMPORTANTE:** tudo o que está incluído na lista de expressões ou no **onde** cláusula deve vir do domínio de dados definida pelo **FROM** cláusula. Você não pode misturar domínios de dados.  
  
##  <a name="Select_Types"></a>Selecione os tipos de  
 A sintaxe de **selecione** instrução dá suporte a muitas tarefas diferentes. Use os seguintes padrões para executar essas tarefas:  
  
-   [Prevendo](#Predicting)  
  
-   [Navegação](#Browsing)  
  
-   [Copiando](#Copying)  
  
-   [Detalhamento](#Drillthrough)  
  
###  <a name="Predicting"></a>Prevendo  
 As previsões com base em um modelo de mineração podem ser executadas com os tipos de consulta a seguir.  
  
 Você pode incluir qualquer uma de pesquisa ou previsão **selecione** instruções dentro de **FROM** e **onde** cláusulas de uma junção de previsão **selecione** instrução.  
  
|Tipo de consulta|Description|  
|----------------|-----------------|  
|SELECT FROM [NATURAL] PREDICTION JOIN|Retorna uma previsão criada pela associação de colunas no modelo de mineração para as colunas de uma fonte de dados interna.<br /><br /> O domínio desse tipo de consulta são as colunas previsíveis do modelo e as colunas da fonte de dados de entrada.<br /><br /> [SELECT FROM &#60; modelo de &#62; JUNÇÃO de previsão &#40; DMX &#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [Consultas de previsão &#40; mineração de dados &#41;](../analysis-services/data-mining/prediction-queries-data-mining.md)|  
|SELECT FROM  *\<modelo >*|Retorna o estado mais provável da coluna previsível, com base apenas no modelo de mineração. Esse tipo de consulta é um atalho para criação de uma previsão com junção de previsão vazia.<br /><br /> O domínio desse tipo de consulta são as colunas previsíveis do modelo.<br /><br /> [SELECT FROM &#60; modelo de &#62; &#40; DMX &#41;](../dmx/select-from-model-dmx.md)<br /><br /> [Consultas de previsão &#40; mineração de dados &#41;](../analysis-services/data-mining/prediction-queries-data-mining.md)|  
  
 [Para selecionar tipos de](#Select_Types)  
  
###  <a name="Browsing"></a>Navegação  
 Os conteúdos de um modelo de mineração podem ser pesquisados usando-se os seguintes tipos de consultas.  
  
|Tipo de consulta|Description|  
|----------------|-----------------|  
|SELECT DISTINCT FROM  *\<modelo >*|Retorna todos os valores de estado do modelo de mineração para a coluna especificada.<br /><br /> O domínio de dados para esse tipo de consulta é o modelo de mineração de dados.<br /><br /> [SELECT DISTINCT FROM &#60; modelo de &#62; &#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [Conteúdo de consultas &#40; mineração de dados &#41;](../analysis-services/data-mining/content-queries-data-mining.md)|  
|SELECT FROM  *\<modelo >*. CONTEÚDO|Retorna o conteúdo que descreve um modelo de mineração.<br /><br /> O domínio de dados para este tipo de consulta é o conjunto de linhas do esquema de conteúdo.<br /><br /> [SELECT FROM &#60; modelo de &#62;. CONTEÚDO &#40; DMX &#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [Conteúdo de consultas &#40; mineração de dados &#41;](../analysis-services/data-mining/content-queries-data-mining.md)|  
|SELECT FROM  *\<modelo >*. DIMENSION_CONTENT|Retorna o conteúdo que descreve um modelo de mineração.<br /><br /> O domínio de dados para este tipo de consulta é o conjunto de linhas do esquema de conteúdo.<br /><br /> [SELECT FROM &#60; modelo de &#62;. DIMENSION_CONTENT &#40; DMX &#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|SELECT FROM  *\<modelo >*. PMML|Retorna a representação PMML (Predictive Model Markup Language) do modelo de mineração para os algoritmos que oferecem suporte a essa funcionalidade.<br /><br /> O domínio para este tipo de consulta é o conjunto de linhas de esquema de PMML.<br /><br /> [Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT_PMML](../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|  
  
 [Para selecionar tipos de](#Select_Types)  
  
###  <a name="Copying"></a>Copiando  
 É possível copiar um modelo de mineração e a estrutura de mineração associada em um novo modelo e, depois, renomear o modelo na instrução.  
  
|Tipo de consulta|Description|  
|----------------|-----------------|  
|SELECT INTO  *\<novo modelo >*|Cria uma cópia do modelo de mineração.<br /><br /> O domínio para esse tipo de consulta é o modelo da mineração de dados.<br /><br /> [SELECT INTO &#40; DMX &#41;](../dmx/select-into-dmx.md)|  
  
 [Para selecionar tipos de](#Select_Types)  
  
###  <a name="Drillthrough"></a>Detalhamento  
 Pesquise os casos ou a representação desses casos, que foram usados para treinar o modelo, usando os tipos de consulta a seguir.  
  
|Tipo de consulta|Description|  
|----------------|-----------------|  
|SELECT FROM  *\<modelo >*. CASOS|Retorna os casos usados para treinar o modelo de mineração.<br /><br /> O domínio para esse tipo de consulta é o modelo da mineração de dados.<br /><br /> [SELECT FROM &#60; modelo de &#62;. CASOS &#40; DMX &#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [Criar consultas de detalhamento usando DMX](../analysis-services/data-mining/create-drillthrough-queries-using-dmx.md)|  
|SELECT FROM  *\<modelo >*. SAMPLE_CASES|Retorna um caso de exemplo, representante dos casos usados para treinar o modelo de mineração.<br /><br /> O domínio para esse tipo de consulta é o modelo da mineração de dados.<br /><br /> [SELECT FROM &#60; modelo de &#62;. SAMPLE_CASES &#40; DMX &#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|SELECT FROM  *\<estrutura >*. CASOS|Retorna as linhas de dados detalhadas da estrutura de mineração subjacente, mesmo que alguns detalhes não tenham sido usados no treinamento do modelo de mineração.<br /><br /> [SELECT FROM &#60; estrutura &#62;. CASOS](../dmx/select-from-structure-cases.md)<br /><br /> [Consultas de detalhamento &#40; mineração de dados &#41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md)|  
  
 [Para selecionar tipos de](#Select_Types)  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  


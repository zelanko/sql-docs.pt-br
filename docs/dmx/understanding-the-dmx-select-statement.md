---
title: Compreendendo a instrução DMX SELECT | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8cc28e9394cabee4dd32e8e84ee02517de415a75
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893070"
---
# <a name="understanding-the-dmx-select-statement"></a>Compreendendo a instrução DMX Select
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  A instrução [Select](../dmx/select-dmx.md) é a base para a maioria das consultas que você cria com o DMX (Data Mining [!INCLUDE[msCoName](../includes/msconame-md.md)] Extensions) no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Pode executar muitos tipos diferentes de tarefas, como pesquisar e prever com base em modelos de mineração de dados.  
  
 A seguir estão as tarefas que você pode concluir usando a instrução **Select** :  
  
-   Pesquisar um modelo de mineração de dados. O conjunto de linhas de esquema define a estrutura de um modelo.  
  
-   Descobrir os possíveis valores de uma coluna de modelo de mineração.  
  
-   Navegar pelos casos que são atribuídos a nós em um modelo de mineração ou obter um caso representativo.  
  
-   Criar previsões usando uma variedade de entradas.  
  
-   Copiar modelos de mineração.  
  
 Cada uma dessas tarefas usa um conjunto diferente de dados, que chamaremos de um *domínio de dados*. Você define o domínio de dados na cláusula **from** da instrução.  
  
-   Você deseja localizar os objetos no próprio modelo de mineração de dados, assim como a regra que define um conjunto de dados, ou uma fórmula usada para fazer previsões.  
  
     Nesse caso, você precisa examinar os metadados armazenados no próprio modelo. Portanto, o domínio de dados são as colunas no conjunto de linhas do esquema de mineração de dados.  
  
-   Você deseja obter informações detalhadas dos casos usados para criar o modelo.  
  
     Nesse caso, você precisa detalhar a estrutura de mineração, que é o domínio de dados, e verificar as linhas individuais em colunas como Gender, Bike Buyer e assim por diante.  
  
 **IMPORTANTE:** Tudo o que está incluído na lista de expressões ou na cláusula **Where** deve vir do domínio de dados que é definido pela cláusula **from** . Você não pode misturar domínios de dados.  
  
##  <a name="Select_Types"></a>Selecionar tipos  
 A sintaxe da instrução **Select** dá suporte a muitas tarefas diferentes. Use os seguintes padrões para executar essas tarefas:  
  
-   [Prever](#Predicting)  
  
-   [Explora](#Browsing)  
  
-   [Copia](#Copying)  
  
-   [Drillthrough](#Drillthrough)  
  
###  <a name="Predicting"></a>Prever  
 As previsões com base em um modelo de mineração podem ser executadas com os tipos de consulta a seguir.  
  
 Você pode incluir qualquer uma das instruções de navegação ou de previsão **Select** nas cláusulas **from** e **Where** de uma instrução de **seleção** de junção de previsão.  
  
|Tipo de consulta|Descrição|  
|----------------|-----------------|  
|SELECIONAR ENTRE [NATURAL] JUNÇÃO DE PREVISÃO|Retorna uma previsão criada pela associação de colunas no modelo de mineração para as colunas de uma fonte de dados interna.<br /><br /> O domínio desse tipo de consulta são as colunas previsíveis do modelo e as colunas da fonte de dados de entrada.<br /><br /> [SELECIONAR da &#60;junção&#62; &#40;de previsão do modelo DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [Consultas de previsão &#40;Mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
|Selecionar do  *\<modelo >*|Retorna o estado mais provável da coluna previsível, com base apenas no modelo de mineração. Esse tipo de consulta é um atalho para criação de uma previsão com junção de previsão vazia.<br /><br /> O domínio desse tipo de consulta são as colunas previsíveis do modelo.<br /><br /> [Selecionar do &#60;modelo&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)<br /><br /> [Consultas de previsão &#40;Mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
  
 [Voltar para selecionar tipos](#Select_Types)  
  
###  <a name="Browsing"></a>Explora  
 Os conteúdos de um modelo de mineração podem ser pesquisados usando-se os seguintes tipos de consultas.  
  
|Tipo de consulta|Descrição|  
|----------------|-----------------|  
|Selecione DISTINCT do  *\<modelo >*|Retorna todos os valores de estado do modelo de mineração para a coluna especificada.<br /><br /> O domínio de dados para esse tipo de consulta é o modelo de mineração de dados.<br /><br /> [Selecionar DISTINCT do &#60;modelo &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [Consultas de conteúdo &#40;Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|Selecione do  *\<modelo >* . DISPUTA|Retorna o conteúdo que descreve um modelo de mineração.<br /><br /> O domínio de dados para este tipo de consulta é o conjunto de linhas do esquema de conteúdo.<br /><br /> [Selecione do &#60;modelo&#62;. DMX &#40;de conteúdo&#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [Consultas de conteúdo &#40;Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|Selecione do  *\<modelo >* . DIMENSION_CONTENT|Retorna o conteúdo que descreve um modelo de mineração.<br /><br /> O domínio de dados para este tipo de consulta é o conjunto de linhas do esquema de conteúdo.<br /><br /> [SELECT FROM &#60;model&#62;.DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|Selecione do  *\<modelo >* . PMML|Retorna a representação PMML (Predictive Model Markup Language) do modelo de mineração para os algoritmos que oferecem suporte a essa funcionalidade.<br /><br /> O domínio para este tipo de consulta é o conjunto de linhas de esquema de PMML.<br /><br /> [Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT_PMML](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset)|  
  
 [Voltar para selecionar tipos](#Select_Types)  
  
###  <a name="Copying"></a>Copia  
 É possível copiar um modelo de mineração e a estrutura de mineração associada em um novo modelo e, depois, renomear o modelo na instrução.  
  
|Tipo de consulta|Descrição|  
|----------------|-----------------|  
|Selecionar no  *\<novo modelo >*|Cria uma cópia do modelo de mineração.<br /><br /> O domínio para esse tipo de consulta é o modelo da mineração de dados.<br /><br /> [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)|  
  
 [Voltar para selecionar tipos](#Select_Types)  
  
###  <a name="Drillthrough"></a>Drillthrough  
 Pesquise os casos ou a representação desses casos, que foram usados para treinar o modelo, usando os tipos de consulta a seguir.  
  
|Tipo de consulta|Descrição|  
|----------------|-----------------|  
|Selecione do  *\<modelo >* . BOLSAS|Retorna os casos usados para treinar o modelo de mineração.<br /><br /> O domínio para esse tipo de consulta é o modelo da mineração de dados.<br /><br /> [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [Criar consultas de detalhamento usando DMX](https://docs.microsoft.com/analysis-services/data-mining/create-drillthrough-queries-using-dmx)|  
|Selecione do  *\<modelo >* . SAMPLE_CASES|Retorna um caso de exemplo, representante dos casos usados para treinar o modelo de mineração.<br /><br /> O domínio para esse tipo de consulta é o modelo da mineração de dados.<br /><br /> [SELECT FROM &#60;model&#62;.SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|Selecione de  *\<> de estrutura*. BOLSAS|Retorna as linhas de dados detalhadas da estrutura de mineração subjacente, mesmo que alguns detalhes não tenham sido usados no treinamento do modelo de mineração.<br /><br /> [Selecione da &#60;estrutura&#62;. BOLSAS](../dmx/select-from-structure-cases.md)<br /><br /> [Consultas de detalhamento &#40;Mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/drillthrough-queries-data-mining)|  
  
 [Voltar para selecionar tipos](#Select_Types)  
  
## <a name="see-also"></a>Consulte também  
 [Referência de DMX &#40;extensões DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referência de instrução &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenções de sintaxe &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  

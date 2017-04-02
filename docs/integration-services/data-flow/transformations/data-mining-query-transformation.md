---
title: "Transforma&#231;&#227;o Consulta de Minera&#231;&#227;o de Dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dataminingquerytrans.f1"
helpviewer_keywords: 
  - "Transformação Consulta de Mineração de Dados"
  - "consultas de previsão [Integration Services]"
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Transforma&#231;&#227;o Consulta de Minera&#231;&#227;o de Dados
  A transformação Consulta de Mineração de Dados executa consultas de previsão em relação a modelos de mineração de dados. Essa transformação contém um construtor de consultas para criar consultas DMX (Data Mining Extensions). O construtor de consultas permite criar instruções personalizadas para avaliar os dados de entrada de transformação em relação a um modelo de mineração existente usando a linguagem DMX. Para obter mais informações, consulte [Referência de DMX &#40;extensões DMX&#41;](../../../dmx/data-mining-extensions-dmx-reference.md).  
  
 Uma transformação pode executar várias consultas de previsão se os modelos forem criados na mesma estrutura de mineração de dados. Para obter mais informações, consulte [Ferramentas de Consulta de Mineração de Dados](../../../analysis-services/data-mining/data-mining-query-tools.md).  
  
## Configuração da transformação Consulta de Mineração de Dados  
 A transformação de consulta de mineração de dados usa um gerenciador de conexões [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para conectar-se ao projeto do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou à instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que contém a estrutura de mineração e modelos de mineração. Para obter mais informações, consulte [Analysis Services Connection Manager](../../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação de Consultas de Mineração de Dados** , clique em um dos seguintes tópicos:  
  
-   [Editor de Transformação Consultas de Mineração de Dados &#40;Guia Modelo de Mineração&#41;](../../../integration-services/data-flow/transformations/data-mining-query-transformation-editor-mining-model-tab.md)  
  
-   [Editor de Transformação Consultas de Mineração de Dados &#40;Guia Modelo de Mineração&#41;](../../../integration-services/data-flow/transformations/data-mining-query-transformation-editor-mining-model-tab.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../Topic/Common%20Properties.md)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  
---
title: Transformação Consultas de Mineração de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingquerytrans.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 278fdc3b1abd38b63f01e967e28d11983a09e682
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430773"
---
# <a name="data-mining-query-transformation"></a>Transformação Consulta de Mineração de Dados
  A transformação Consulta de Mineração de Dados executa consultas de previsão em relação a modelos de mineração de dados. Essa transformação contém um construtor de consultas para criar consultas DMX (Data Mining Extensions). O construtor de consultas permite criar instruções personalizadas para avaliar os dados de entrada de transformação em relação a um modelo de mineração existente usando a linguagem DMX. Para obter mais informações, consulte [Referência de DMX &#40;extensões DMX&#41;](/sql/dmx/data-mining-extensions-dmx-reference).  
  
 Uma transformação pode executar várias consultas de previsão se os modelos forem criados na mesma estrutura de mineração de dados. Para obter mais informações, consulte [interfaces de consulta de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools).  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>Configuração da transformação Consulta de Mineração de Dados  
 A transformação de consulta de mineração de dados usa um gerenciador de conexões [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para conectar-se ao projeto do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou à instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que contém a estrutura de mineração e modelos de mineração. Para obter mais informações, consulte [Analysis Services Connection Manager](../../connection-manager/analysis-services-connection-manager.md).  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação de Consultas de Mineração de Dados** , clique em um dos seguintes tópicos:  
  
-   [Editor de Transformação Consultas de Mineração de Dados &#40;Guia Modelo de Mineração&#41;](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
-   [Editor de Transformação Consultas de Mineração de Dados &#40;Guia Modelo de Mineração&#41;](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas da transformação](transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md).  
  
  

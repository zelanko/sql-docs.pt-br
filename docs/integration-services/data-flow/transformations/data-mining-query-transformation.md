---
title: Transformação Consultas de Mineração de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquerytrans.f1
- sql13.dts.designer.dmquerytransformation.miningmodel.f1
- sql13.dts.designer.dmquerytransformation.query.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: de863a5aeba65dded46990d94e204bb29ef6bd1c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813064"
---
# <a name="data-mining-query-transformation"></a>Transformação Consulta de Mineração de Dados
  A transformação Consulta de Mineração de Dados executa consultas de previsão em relação a modelos de mineração de dados. Essa transformação contém um construtor de consultas para criar consultas DMX (Data Mining Extensions). O construtor de consultas permite criar instruções personalizadas para avaliar os dados de entrada de transformação em relação a um modelo de mineração existente usando a linguagem DMX. Para obter mais informações, consulte [Referência de DMX &#40;extensões DMX&#41;](../../../dmx/data-mining-extensions-dmx-reference.md).  
  
 Uma transformação pode executar várias consultas de previsão se os modelos forem criados na mesma estrutura de mineração de dados. Para obter mais informações, consulte [Ferramentas de Consulta de Mineração de Dados](../../../analysis-services/data-mining/data-mining-query-tools.md).  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>Configuração da transformação Consulta de Mineração de Dados  
 A transformação de consulta de mineração de dados usa um gerenciador de conexões [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para conectar-se ao projeto do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou à instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que contém a estrutura de mineração e modelos de mineração. Para obter mais informações, consulte [Analysis Services Connection Manager](../../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="data-mining-query-transformation-editor-mining-model-tab"></a>Editor de Transformação Consultas de Mineração de Dados (guia Modelo de Mineração)
  Use a guia **Modelo de Mineração** da caixa de diálogo **Editor de Transformação Consultas de Mineração de Dados** para selecionar a estrutura e os modelos de mineração de dados.  
  
### <a name="options"></a>Opções  
 **Conexão**  
 Selecione uma conexão do Analysis Services existente usando a caixa de listagem ou crie uma nova conexão usando o botão **Novo** descrito a seguir.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Adicionar Gerenciador de Conexões do Analysis Services** .  
  
 **Estrutura de mineração**  
 Selecione na lista de estruturas de modelo de mineração disponíveis.  
  
 **Modelos de mineração**  
 Exiba a lista de modelos de mineração associada com a estrutura de mineração de dados selecionada.  
  
## <a name="data-mining-query-transformation-editor-query-tab"></a>Editor de Transformação Consultas de Mineração de Dados (Guia Consulta)
  Use a guia **Consulta** da caixa de diálogo **Editor de Transformação Consultas de Mineração de Dados** para criar uma consulta de previsão.  
  
### <a name="options"></a>Opções  
 **Consulta de mineração de dados**  
 Digite uma consulta DMX (Data Mining Extensions) diretamente na caixa de texto.  
  
 **Construir Nova Consulta**  
 Clique em **Construir Nova Consulta** para criar uma consulta DMX (extensões DMX) usando o construtor de consultas gráficas.  
  

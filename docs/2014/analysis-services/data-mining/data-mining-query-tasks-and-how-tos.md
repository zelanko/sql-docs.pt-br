---
title: Tarefas e instruções de consulta de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], how-to topics
ms.assetid: 1bc2a775-6e62-4c66-a53c-201f2ea66295
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 15adaa8227a80d04cbdbdaa379dfccc4f2f03acf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118553"
---
# <a name="data-mining-query-tasks-and-how-tos"></a>Tarefas e instruções de consulta de Data Mining
  A capacidade de criar consultas será essencial se você for utilizar seus modelos de mineração de dados. Esta seção contém links para exemplos sobre como criar consultas em um modelo de mineração de dados usando as ferramentas fornecidas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Se precisar de mais informações sobre a definição de uma consulta de mineração de dados ou sobre os diferentes tipos de consultas que você pode criar, consulte [Consultas de mineração de dados](data-mining-queries.md).  
  
## <a name="creating-queries-with-prediction-query-builder"></a>Criando consultas com o Construtor de Consultas de Previsão  
 O Construtor de Consultas de Previsão é fornecido no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] como uma maneira de criar consultas em modelos de mineração de dados de forma gráfica. Os tópicos a seguir explicam como você pode selecionar um modelo, especificar uma fonte de dados, personalizar as previsões e salvar a saída.  
  
-   [Criar uma consulta de previsão usando o Construtor de Consultas de previsão](create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [Criar uma consulta Singleton no Designer de Mineração de dados](create-a-singleton-query-in-the-data-mining-designer.md)  
  
-   [Criar uma consulta de previsão usando o Construtor de Consultas de previsão](create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [Exibir e salvar os resultados de uma consulta de previsão](view-and-save-the-results-of-a-prediction-query.md)  
  
-   [Editar manualmente uma consulta de previsão](manually-edit-a-prediction-query.md)  
  
-   [Aplicar funções de previsão a um modelo](apply-prediction-functions-to-a-model.md)  
  
-   [Escolher e mapear dados de entrada para uma consulta de previsão](choose-and-map-input-data-for-a-prediction-query.md)  
  
## <a name="using-other-data-mining-query-tools"></a>Usando outras ferramentas de consulta de mineração de dados  
 Além de usar o Construtor de Consultas de Previsão, você pode digitar uma consulta diretamente no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando o DMX ou o XMLA. Você também pode criar consultas de previsão de forma programática e enviá-las a um servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Os tópicos a seguir fornecem mais informações sobre como criar e trabalhar com consultas de previsão fora do Construtor de Consultas de Previsão.  
  
 [Criar uma consulta de previsão singleton com base em um modelo](create-a-singleton-prediction-query-from-a-template.md)  
 Descreve como usar as ferramentas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar e executar uma consulta de previsão.  
  
 [Criar uma consulta de previsão singleton com base em um modelo](create-a-singleton-prediction-query-from-a-template.md)  
 Descreve como usar os modelos fornecidos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para adicionar parâmetros a uma consulta de previsão.  
  
 [Alterar o valor do tempo limite de consultas de mineração de dados](change-the-time-out-value-for-data-mining-queries.md)  
 Descreve como definir propriedades no servidor que controlem o comportamento relacionado a consultas de mineração de dados.  
  
 [Criar uma consulta de conteúdo em um modelo de mineração](create-a-content-query-on-a-mining-model.md)  
 Descreve como criar consultas que retornam informações detalhadas armazenadas no modelo de mineração, usando conjuntos de linhas do esquema de mineração de dados.  
  
 [Create a Mineração de dados Query by Using XMLA](create-a-data-mining-query-by-using-xmla.md)  
 Descreve como criar uma consulta no conteúdo do modelo de mineração usando os modelos XMLA do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Referência de linguagem de expressão e consulta &#40;do Analysis Services&#41;](https://msdn.microsoft.com/library/gg492188(SQL.130).aspx)   
 [Procedimentos armazenados da mineração de dados &#40;Analysis Services – mineração de dados&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  

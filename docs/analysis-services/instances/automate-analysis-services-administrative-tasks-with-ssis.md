---
title: Automatizar tarefas administrativas do Analysis Services com SSIS | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Execute DDL Task [Analysis Services]
- Analysis Services Processing task
ms.assetid: e960a9a2-80b4-45da-9369-bc560ecdccac
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 308c7910d408fcb29689484eb71726a669ed6d98
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="automate-analysis-services-administrative-tasks-with-ssis"></a>Automatizar tarefas administrativas do Analysis Services com SSIS
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite automatizar a execução de scripts DDL, cubo e processamento de tarefas e tarefas de consulta de mineração de dados de modelo de mineração. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode ser considerado como uma coleção de tarefas de manutenção e de fluxo de controle, que podem ser vinculadas para formar trabalhos de processamento de dados sequenciais e paralelos.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] foi projetado para executar operações de limpeza de dados durante as tarefas de processamento de dados e reunir dados de fonte de dados diferentes. Ao trabalhar com cubos e modelos de mineração, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode transformar dados não numéricos em numéricos e garantir que os valores dos dados fiquem dentro dos limites previstos, criando assim dados limpos que serão usados para preencher tabelas de fatos e dimensões.  
  
## <a name="integration-services-tasks"></a>Tarefas do Integration Services  
 Há dois elementos principais em qualquer tarefa ou trabalho do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] : elementos de fluxo de controle e de fluxo de dados. Os elementos de fluxo de controle definem a ordenação lógica da progressão do trabalho aplicando restrições de precedência. Os elementos de fluxo de dados referem-se à conectividade entre a saída de um componente para a entrada do componente seguinte, além de qualquer transformação de dados que possa ocorrer no intermédio. Com relação à decisão sobre para onde vão os dados, as restrições de precedência contêm a lógica para especificar qual componente receberá a saída. As tarefas do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mais relevantes ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluem a Tarefa Executar DDL, a Tarefa Processamento do Analysis Services e a Tarefa Consulta de Mining de Dados. Para cada uma delas, a Tarefa Enviar Email pode ser usada para enviar ao administrador uma mensagem de email contendo os resultados da tarefa.  
  
## <a name="the-execute-ddl-task"></a>A Tarefa Executar DDL  
 A Tarefa Executar DDL do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite o envio de scripts DDL diretamente para o servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e sua execução automaticamente. Com isso, o administrador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode executar operações de backup, restauração ou sincronização a partir de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Um pacote é composto pelos elementos de fluxo de controle e de dados já descritos, devendo ser todos **run regularly**, como outras instruções DDL que podem ser adicionadas às tarefas. Como as tarefas aqui abordadas geralmente são executadas à noite, é particularmente útil ter pacotes que possam ser executados facilmente a partir de qualquer aplicativo de agendamento. Você pode agendar um pacote para ser executado a qualquer hora e usar o Agente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações sobre como implementar essa tarefa, consulte [Tarefa Executar DDL do Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md).  
  
## <a name="analysis-services-processing-task"></a>Tarefa Processamento do Analysis Services  
 A Tarefa Processamento do Analysis Services do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite o preenchimento automático de cubos com novas informações quando você faz atualizações regulares no banco de dados relacional de origem. Você pode fazer o processamento no nível da dimensão, do cubo ou da partição usando a Tarefa Processamento do Analysis Services. O próprio processamento pode ser do tipo **incremental** ou **full**, seleção feita de acordo com os requisitos do trabalho. O processamento incremental adiciona novos dados e executa os recálculos suficientes para manter o destino atualizado, enquanto o processamento completo descarta os dados existentes para recarregar e recalcular completamente os dados. O processamento completo leva mais tempo, mas é mais completo. Para obter mais informações sobre como implementar essa tarefa, consulte [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md).  
  
## <a name="data-mining-query-task"></a>Data Mining Query Task  
 A Tarefa Consulta de Mining de Dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite a extração e o armazenamento de informações de modelos de mineração. Com frequência, as informações são armazenadas em um banco de dados relacional e, por exemplo, podem ser usadas para isolar uma lista de possíveis clientes para uma campanha publicitária. A mineração de dados pode identificar o valor de um cliente e a probabilidade de esse cliente responder a um determinado apelo publicitário. Você pode usar a Tarefa Consulta de Mining de Dados para extrair dados e modificá-los para um formato de sua preferência. Para obter mais informações sobre como implementar essa tarefa, consulte [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Destino de processamento de partições](../../integration-services/data-flow/partition-processing-destination.md)   
 [Destino de processamento de dimensão](../../integration-services/data-flow/dimension-processing-destination.md)   
 [Transformação de consulta de mineração de dados](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)   
 [Processar um modelo multidimensional &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
  
  

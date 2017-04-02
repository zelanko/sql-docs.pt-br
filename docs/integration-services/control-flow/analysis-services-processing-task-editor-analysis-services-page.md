---
title: "Editor da Tarefa Processamento do Analysis Services (p&#225;gina Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.asprocessingtask.as.f1"
helpviewer_keywords: 
  - "Editor da Tarefa Processamento do Analysis Services"
ms.assetid: 5612be78-57cf-4e4e-92cf-6bfa9f971040
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# Editor da Tarefa Processamento do Analysis Services (p&#225;gina Analysis Services)
  Use a página **Analysis Services** da caixa de diálogo **Editor da Tarefa Processamento do Analysis Services** para especificar um gerenciador de conexões do Analysis Services, selecione os objetos analíticos a serem processados e defina as opções de processamento e manipulação de erros.  
  
 Lembre-se do seguinte quando for processar modelos tabulares:  
  
1.  Você não pode executar a análise de impacto em modelos tabulares.  
  
2.  Algumas opções de processamento para modo tabular não são expostas, como Processar Desfragmentação e Processar Recálculo. Você pode executar essas funções usando a tarefa Executar DDL.  
  
3.  Algumas opções de processamento fornecidas, como índices de processo, não são apropriadas para modelos tabulares e não devem ser usadas.  
  
4.  As configurações de lote para modelos tabulares são ignoradas.  
  
 Para obter informações sobre essa tarefa, consulte [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md).  
  
## Opções  
 **Gerenciador de conexões do Analysis Services**  
 Selecione na lista um gerenciador de conexões do Analysis Services existente ou clique em **Novo** para criar um novo gerenciador de conexões.  
  
 **Nova**  
 Cria um novo gerenciador de conexões do Analysis Services  
  
 **Tópicos relacionados:** [Gerenciador de conexões do Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md), [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Lista de objetos**  
 |Propriedade|Description|  
|--------------|-----------------|  
|**Nome do Objeto**|Lista os nomes de objeto especificados.|  
|**Tipo**|Lista os tipos dos objetos especificados.|  
|**Opções de Processo**|Selecione uma opção de processamento na lista.<br /><br /> **Tópicos relacionados**: [Como processar um modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)|  
|**Configurações**|Lista configurações de processamento para os objetos especificados.|  
  
 **Adicionar**  
 Adicione à lista um objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 **Remover**  
 Selecione um objeto e clique em **Excluir**.  
  
 **Análise de Impacto**  
 Execute uma análise de impacto no objeto selecionado.  
  
 **Tópicos relacionados:** [Caixa de diálogo Análise de Impacto &#40;Analysis Services – Dados Multidimensionais&#41;](../Topic/Impact%20Analysis%20Dialog%20Box%20\(Analysis%20Services%20-%20Multidimensional%20Data\).md)  
  
 **Resumo de Configurações de Lote**  
 |Propriedade|Description|  
|--------------|-----------------|  
|**Ordem de processamento**|Especifica se os objetos são processados em sequência ou em um lote; se for usado o processamento paralelo, especifica o número de objetos a serem processados simultaneamente.|  
|**Modo de transação**|Especifica o modo da transação para processamento sequencial.|  
|**Erros de dimensão**|Especifica o comportamento da tarefa quando ocorrem erros.|  
|**Caminho do log de erros da chave de dimensão**|Especifica o caminho do arquivo no qual são feitos logs de erros.|  
|**Objetos afetados pelo processo**|Indica se também são processados objetos dependentes ou afetados.|  
  
 **Alterar Configurações**  
 Altere as opções de processamento e a manipulação de erros em chaves de dimensão.  
  
 **Tópicos relacionados:** [Caixa de diálogo Alterar Configurações &#40;Analysis Services – Dados Multidimensionais&#41;](../Topic/Change%20Settings%20Dialog%20Box%20\(Analysis%20Services%20-%20Multidimensional%20Data\).md)  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa Processamento do Analysis Services &#40;Página Geral&#41;](../../integration-services/control-flow/analysis-services-processing-task-editor-general-page.md)   
 [Tarefa Executar DDL do Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
  
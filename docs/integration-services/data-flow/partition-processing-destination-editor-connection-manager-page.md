---
title: "Editor de Destino de Processamento de Parti&#231;&#245;es (p&#225;gina Gerenciador de Conex&#245;es) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.partprocessingtransformation.connection.f1"
helpviewer_keywords: 
  - "Editor de Destino de Processamento de Partições"
ms.assetid: 7add6f82-eed1-47fc-a5d7-7b91f3f24d34
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Editor de Destino de Processamento de Parti&#231;&#245;es (p&#225;gina Gerenciador de Conex&#245;es)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino de Processamento de Partições** para especificar uma conexão a um projeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para saber mais sobre o destino de Processamento de Partições, consulte [Partition Processing Destination](../../integration-services/data-flow/partition-processing-destination.md).  
  
> [!NOTE]  
>  As tarefas descritas aqui não se aplicam a modelos de tabela do Analysis Services.  Você não pode mapear colunas de entrada para as colunas de partição em modelos de tabela. Você pode usar a tarefa Executar DDL do Analysis Services [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) para processar a partição.  
  
## Opções  
 **Gerenciador de conexões**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Adicionar Gerenciador de Conexões do Analysis Services**.  
  
 **Lista de partições disponíveis**  
 Selecione a partição a processar.  
  
 **Método de processamento**  
 Selecione o método de processamento. O valor padrão desta opção é **Completo**.  
  
|Value|Description|  
|-----------|-----------------|  
|Adicionar (incremental)|Execute um processamento com incremento da partição.|  
|Full (cheio)|Execute um processamento completo da partição.|  
|Apenas dados|Execute um processamento de atualização da partição.|  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Destino de Processamento de Partições &#40;Página Mapeamentos&#41;](../../integration-services/data-flow/partition-processing-destination-editor-mappings-page.md)   
 [Editor de Destino de Processamento de Partições &#40;Página Avançado&#41;](../../integration-services/data-flow/partition-processing-destination-editor-advanced-page.md)  
  
  
---
title: "Editor de Destino de Processamento de Dimens&#245;es (p&#225;gina Gerenciador de Conex&#245;es) | Microsoft Docs"
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
  - "sql13.dts.designer.dimprocessingtransformation.connection.f1"
helpviewer_keywords: 
  - "Editor de Destino de Processamento de Dimensões"
ms.assetid: 44aab631-d62d-4895-8fc7-7f1f3b1b68ce
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# Editor de Destino de Processamento de Dimens&#245;es (p&#225;gina Gerenciador de Conex&#245;es)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino de Processamento de Dimensões** para especificar uma conexão com um projeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou com uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para saber mais sobre o destino de Processamento de Dimensões, consulte [Dimension Processing Destination](../../integration-services/data-flow/dimension-processing-destination.md).  
  
## Opções  
 **Gerenciador de conexões**  
 Selecione um gerenciador de conexões existente na lista ou clique em **Novo** para criar um novo gerenciador de conexões.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Adicionar Gerenciador de Conexões do Analysis Services**.  
  
 **Lista de dimensões disponíveis**  
 Selecione a dimensão a processar.  
  
 **Método de processamento**  
 Selecione o método de processamento a aplicar à dimensão selecionada na lista. O valor padrão desta opção é **Completo**.  
  
|Value|Description|  
|-----------|-----------------|  
|**Adicionar (incremental)**|Execute um processamento com incremento da dimensão.|  
|**Full (cheio)**|Execute um processamento completo da dimensão.|  
|**Update (atualizar)**|Execute um processamento de atualização da dimensão.|  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Destino de Processamento de Dimensões &#40;página Mapeamentos&#41;](../../integration-services/data-flow/dimension-processing-destination-editor-mappings-page.md)   
 [Editor de Destino de Processamento de Dimensões &#40;Página Avançado&#41;](../../integration-services/data-flow/dimension-processing-destination-editor-advanced-page.md)  
  
  
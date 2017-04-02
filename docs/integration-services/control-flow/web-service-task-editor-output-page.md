---
title: "Editor da Tarefa Servi&#231;o da Web (p&#225;gina Sa&#237;da) | Microsoft Docs"
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
  - "sql13.dts.designer.webservicestask.output.f1"
helpviewer_keywords: 
  - "Editor da Tarefa Serviço da Web"
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Editor da Tarefa Servi&#231;o da Web (p&#225;gina Sa&#237;da)
  Use a página **Saída** da caixa de diálogo **Editor da Tarefa Serviço da Web** para especificar onde armazenar o resultado retornado pelo método Web.  
  
 Para saber mais sobre essa tarefa, consulte [Tarefa Serviço da Web](../../integration-services/control-flow/web-service-task.md).  
  
## Opções estáticas  
 **OutputType**  
 Selecione o tipo de armazenamento a usar para os resultados. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**File Connection**|Armazene os resultados em um arquivo. A seleção deste valor exibe a opção dinâmica **File**.|  
|**Variável**|Armazene os resultados em uma variável. A seleção deste valor exibe a opção dinâmica **Variable**.|  
  
## Opções dinâmicas de OutputType  
  
### OutputType = File Connection  
 **Arquivo**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### OutputType = Variable  
 **Variável**  
 Selecione uma variável na lista ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](../Topic/Add%20Variable.md)  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa Serviço da Web &#40;Página Geral&#41;](../../integration-services/control-flow/web-service-task-editor-general-page.md)   
 [Editor da Tarefa Serviço da Web &#40;Página Entrada&#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
  
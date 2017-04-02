---
title: "Editor do Detector de Eventos do WMI (p&#225;gina Op&#231;&#245;es do WMI) | Microsoft Docs"
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
  - "sql13.dts.designer.wmieventwatcher.wmiquery.f1"
helpviewer_keywords: 
  - "Editor da Tarefa Detector de Eventos do WMI"
ms.assetid: 525f3de7-a021-4e52-9939-3a83c88f131a
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Editor do Detector de Eventos do WMI (p&#225;gina Op&#231;&#245;es do WMI)
  Use a página **Opções do WMI** da caixa de diálogo **Editor do Detector de Eventos do WMI** para especificar a origem da consulta WQL (Instrumentação de Gerenciamento do Windows Query Language) e como a tarefa do Detector de Eventos do WMI responde aos eventos do WMI (Microsoft Windows Instrumentation).  
  
 Para obter informações sobre essa tarefa, consulte [WMI Event Watcher Task](../../integration-services/control-flow/wmi-event-watcher-task.md). Para obter mais informações sobre a linguagem WQL, consulte o tópico Instrumentação de Gerenciamento do Windows, [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045) (Consultando com WQL), na Biblioteca MSDN.  
  
## Opções estáticas  
 **WMIConnectionName**  
 Selecione um gerenciador de conexões WMI na lista ou clique em \<**Nova Conexão…**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de Conexões WMI](../../integration-services/connection-manager/wmi-connection-manager.md), [Editor do Gerenciador de Conexões WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Selecione o tipo de origem da consulta WQL que a tarefa executa. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de consultas WQL. Selecionar este valor faz com que seja exibida a opção dinâmica **WQLQuerySource**.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém a consulta WQL. Selecionar este valor faz com que seja exibida a opção dinâmica **WQLQuerySource**.|  
|**Variável**|Define a origem de uma variável que define a consulta WQL. Selecionar este valor faz com que seja exibida a opção dinâmica **WQLQuerySource**.|  
  
 **ActionAtEvent**  
 Especifique se o evento WMI efetua logon do evento e inicia uma ação do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou só efetua logon do evento.  
  
 **AfterEvent**  
 Especifique se a tarefa é bem-sucedida ou falha depois que recebe o evento WMI ou se a tarefa continua observando se o evento ocorre novamente.  
  
 **ActionAtTimeout**  
 Especifique se a tarefa registra o tempo limite excedido da consulta WMI e inicia um evento [!INCLUDE[ssIS](../../includes/ssis-md.md)] em resposta ou só registra o tempo limite excedido.  
  
 **AfterTimeout**  
 Especifique se a tarefa é bem-sucedida ou falha em resposta ao tempo limite excedido ou se a tarefa continua observando se o tempo limite é excedido novamente.  
  
 **NumberOfEvents**  
 Especifique o número de eventos a serem observados.  
  
 **Tempo Limite**  
 Especifique o número de segundos a esperar para que o evento ocorra. Um valor de 0 significa que nenhum tempo limite está em efeito.  
  
## Opções dinâmicas do WQLQuerySource  
  
### WQLQuerySource = Entrada direta  
 **WQLQuerySource**  
 Forneça uma consulta ou clique no botão de reticências (...) e digite uma consulta usando a caixa de diálogo **Consulta WQL**.  
  
### WQLQuerySource = Conexão do arquivo  
 **WQLQuerySource**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### WQLQuerySource = Variável  
 **WQLQuerySource**  
 Selecione uma variável na lista ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](../Topic/Add%20Variable.md)  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa Detector de Eventos do WMI &#40;Página Geral&#41;](../../integration-services/control-flow/wmi-event-watcher-task-editor-general-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)   
 [Tarefa Leitor de Dados do WMI](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
  
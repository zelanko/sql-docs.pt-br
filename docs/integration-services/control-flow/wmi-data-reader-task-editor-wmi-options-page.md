---
title: "O Editor da tarefa de leitor de dados do WMI (página de opções do WMI) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WMI Data Reader Task Editor
ms.assetid: 4b8d4716-882d-41b0-b77e-e0e2741a2cd5
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2d87bb0cfa2ca6a0ad103ac803e6fac662a9d385
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="wmi-data-reader-task-editor-wmi-options-page"></a>Editor da Tarefa Leitor de Dados do WMI (página Opções do WMI)
  Use a página **Opções do WMI** da caixa de diálogo **Editor da Tarefa Leitor de Dados do WMI** para especificar a origem da consulta da linguagem WQL e o destino do resultado da consulta.  
  
 Para obter informações sobre essa tarefa, consulte [WMI Data Reader Task](../../integration-services/control-flow/wmi-data-reader-task.md). Para obter mais informações sobre a linguagem WQL, consulte o tópico Instrumentação de Gerenciamento do Windows, [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045)(Consultando com WQL), na Biblioteca MSDN.  
  
## <a name="static-options"></a>Opções estáticas  
 **WMIConnectionName**  
 Selecione um Gerenciador de conexão WMI na lista ou clique em \< **nova Conexão de WMI...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [Gerenciador de Conexões WMI](../../integration-services/connection-manager/wmi-connection-manager.md), [Editor do Gerenciador de Conexões WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Selecione o tipo de origem da consulta WQL que a tarefa executa. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de consultas WQL. Ao selecionar esse valor, a opção dinâmica **WQLQuerySourceType**será exibida.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém a consulta WQL. Ao selecionar esse valor, a opção dinâmica **WQLQuerySourceType**será exibida.|  
|**Variável**|Defina a origem de uma variável que defina a consulta WQL. Ao selecionar esse valor, a opção dinâmica **WQLQuerySourceType**será exibida.|  
  
 **OutputType**  
 Especifique se a saída deve ser uma tabela de dados, valor de propriedade ou nome e valor de propriedade.  
  
 **OverwriteDestination**  
 Especifique se é necessário manter, substituir ou adicionar aos dados originais no arquivo ou variável de destino.  
  
 **DestinationType**  
 Selecione o tipo de destino da consulta WQL que a tarefa executa. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo no qual salvar os resultados da consulta WQL. A seleção desse valor exibe a opção dinâmica **DestinationType**.|  
|**Variável**|Defina a variável na qual armazenar os resultados da consulta WQL. A seleção desse valor exibe a opção dinâmica **DestinationType**.|  
  
## <a name="wqlquerysourcetype-dynamic-options"></a>Opções dinâmicas de WQLQuerySourceType  
  
### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = Entrada direta  
 **WQLQuerySource**  
 Forneça uma consulta ou clique nas reticências (...) e digite uma consulta, usando a caixa de diálogo **Consulta WQL** .  
  
### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = Conexão do arquivo  
 **WQLQuerySource**  
 Selecione um Gerenciador de conexão de arquivo na lista ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = Variável  
 **WQLQuerySource**  
 Selecione uma variável na lista ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="destinationtype-dynamic-options"></a>Opções dinâmicas de DestinationType  
  
### <a name="destinationtype--file-connection"></a>DestinationType = Conexão do arquivo  
 **Destino**  
 Selecione um Gerenciador de conexão de arquivo na lista ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="destinationtype--variable"></a>DestinationType = Variável  
 **Destino**  
 Selecione uma variável na lista ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa leitor de dados WMI &#40; Página geral &#41;](../../integration-services/control-flow/wmi-data-reader-task-editor-general-page.md)   
 [Página expressões](../../integration-services/expressions/expressions-page.md)   
 [Tarefa do detector de eventos WMI](../../integration-services/control-flow/wmi-event-watcher-task.md)  
  
  

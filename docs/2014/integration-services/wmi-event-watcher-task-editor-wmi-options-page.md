---
title: O Editor da tarefa de observador de eventos do WMI (página Opções do WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmieventwatcher.wmiquery.f1
helpviewer_keywords:
- WMI Event Watcher Task Editor
ms.assetid: 525f3de7-a021-4e52-9939-3a83c88f131a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8c3286d1246efb8b5ae2e17cf8df5d38d865a9f9
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374174"
---
# <a name="wmi-event-watcher-task-editor-wmi-options-page"></a>Editor do Detector de Eventos do WMI (página Opções do WMI)
  Use a página **Opções do WMI** da caixa de diálogo **Editor do Detector de Eventos do WMI** para especificar a origem da consulta WQL (Instrumentação de Gerenciamento do Windows Query Language) e como a tarefa do Detector de Eventos do WMI responde aos eventos do WMI (Microsoft Windows Instrumentation).  
  
 Para obter informações sobre essa tarefa, consulte [WMI Event Watcher Task](control-flow/wmi-event-watcher-task.md). Para obter mais informações sobre a linguagem WQL, consulte o tópico Instrumentação de Gerenciamento do Windows, [Querying with WQL](https://go.microsoft.com/fwlink/?LinkId=79045)(Consultando com WQL), na Biblioteca MSDN.  
  
## <a name="static-options"></a>Opções estáticas  
 **WMIConnectionName**  
 Selecione um gerenciador de conexões WMI na lista ou clique em \<**Nova Conexão WMI...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de Conexão do WMI](connection-manager/wmi-connection-manager.md), [Editor do Gerenciador de Conexão de WMI](../../2014/integration-services/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Selecione o tipo de origem da consulta WQL que a tarefa executa. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de consultas WQL. Selecionar este valor faz com que seja exibida a opção dinâmica **WQLQuerySource**.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém a consulta WQL. Selecionar este valor faz com que seja exibida a opção dinâmica **WQLQuerySource**.|  
|**Variável**|Define a origem de uma variável que define a consulta WQL. Selecionar este valor faz com que seja exibida a opção dinâmica **WQLQuerySource**.|  
  
 **ActionAtEvent**  
 Especifique se o evento WMI efetua logon do evento e inicia uma ação do [!INCLUDE[ssIS](../includes/ssis-md.md)] ou só efetua logon do evento.  
  
 **AfterEvent**  
 Especifique se a tarefa é bem-sucedida ou falha depois que recebe o evento WMI ou se a tarefa continua observando se o evento ocorre novamente.  
  
 **ActionAtTimeout**  
 Especifique se a tarefa registra o tempo limite excedido da consulta WMI e inicia um evento [!INCLUDE[ssIS](../includes/ssis-md.md)] em resposta ou só registra o tempo limite excedido.  
  
 **AfterTimeout**  
 Especifique se a tarefa é bem-sucedida ou falha em resposta ao tempo limite excedido ou se a tarefa continua observando se o tempo limite é excedido novamente.  
  
 **NumberOfEvents**  
 Especifique o número de eventos a serem observados.  
  
 **Tempo Limite**  
 Especifique o número de segundos a esperar para que o evento ocorra. Um valor de 0 significa que nenhum tempo limite está em efeito.  
  
## <a name="wqlquerysource-dynamic-options"></a>Opções dinâmicas do WQLQuerySource  
  
### <a name="wqlquerysource--direct-input"></a>WQLQuerySource = Entrada direta  
 **WQLQuerySource**  
 Forneça uma consulta ou clique no botão de reticências (...) e digite uma consulta usando a caixa de diálogo **Consulta WQL**.  
  
### <a name="wqlquerysource--file-connection"></a>WQLQuerySource = Conexão do arquivo  
 **WQLQuerySource**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de Conexão de arquivos](connection-manager/file-connection-manager.md), [Editor do Gerenciador de Conexão de arquivos](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="wqlquerysource--variable"></a>WQLQuerySource = Variável  
 **WQLQuerySource**  
 Selecione uma variável na lista ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Serviços de integração &#40;SSIS&#41; variáveis](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa Detector de Eventos do WMI &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Página Expressões](expressions/expressions-page.md)   
 [Tarefa Leitor de Dados do WMI](control-flow/wmi-data-reader-task.md)  
  
  

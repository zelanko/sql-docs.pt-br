---
title: Editor da tarefa leitor de dados do WMI (página Opções do WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WMI Data Reader Task Editor
ms.assetid: 4b8d4716-882d-41b0-b77e-e0e2741a2cd5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8367f0ae57df5333808e4dfde25c5676a3bcf1d4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054354"
---
# <a name="wmi-data-reader-task-editor-wmi-options-page"></a>Editor da Tarefa Leitor de Dados do WMI (página Opções do WMI)
  Use a página **Opções do WMI** da caixa de diálogo **Editor da Tarefa Leitor de Dados do WMI** para especificar a origem da consulta da linguagem WQL e o destino do resultado da consulta.  
  
 Para obter informações sobre essa tarefa, consulte [WMI Data Reader Task](control-flow/wmi-data-reader-task.md). Para obter mais informações sobre a linguagem WQL, consulte o tópico Instrumentação de Gerenciamento do Windows, [Querying with WQL](https://go.microsoft.com/fwlink/?LinkId=79045)(Consultando com WQL), na Biblioteca MSDN.  
  
## <a name="static-options"></a>Opções estáticas  
 **WMIConnectionName**  
 Selecione um gerenciador de conexões WMI na lista ou clique em \<**Nova Conexão WMI...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de conexões WMI](connection-manager/wmi-connection-manager.md), [Editor do Gerenciador de conexões WMI](../../2014/integration-services/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Selecione o tipo de origem da consulta WQL que a tarefa executa. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Entrada direta**|Defina a origem de consultas WQL. Ao selecionar esse valor, a opção dinâmica **WQLQuerySourceType**será exibida.|  
|**Conexão de arquivo**|Selecione um arquivo que contém a consulta WQL. Ao selecionar esse valor, a opção dinâmica **WQLQuerySourceType**será exibida.|  
|**Variável**|Defina a origem de uma variável que defina a consulta WQL. Ao selecionar esse valor, a opção dinâmica **WQLQuerySourceType**será exibida.|  
  
 **OutputType**  
 Especifique se a saída deve ser uma tabela de dados, valor de propriedade ou nome e valor de propriedade.  
  
 **OverwriteDestination**  
 Especifique se é necessário manter, substituir ou adicionar aos dados originais no arquivo ou variável de destino.  
  
 **DestinationType**  
 Selecione o tipo de destino da consulta WQL que a tarefa executa. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Conexão de arquivo**|Selecione um arquivo no qual salvar os resultados da consulta WQL. A seleção desse valor exibe a opção dinâmica **DestinationType**.|  
|**Variável**|Defina a variável na qual armazenar os resultados da consulta WQL. A seleção desse valor exibe a opção dinâmica **DestinationType**.|  
  
## <a name="wqlquerysourcetype-dynamic-options"></a>Opções dinâmicas de WQLQuerySourceType  
  
### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = Entrada direta  
 **WQLQuerySource**  
 Forneça uma consulta ou clique nas reticências (...) e digite uma consulta, usando a caixa de diálogo **Consulta WQL**.  
  
### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = Conexão do arquivo  
 **WQLQuerySource**  
 Selecione um Gerenciador de conexões de arquivo na lista ou clique \<em **nova conexão...**> para criar um novo Gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = Variável  
 **WQLQuerySource**  
 Selecione uma variável na lista ou clique em \< **nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
## <a name="destinationtype-dynamic-options"></a>Opções dinâmicas de DestinationType  
  
### <a name="destinationtype--file-connection"></a>DestinationType = Conexão do arquivo  
 **Destino**  
 Selecione um Gerenciador de conexões de arquivo na lista ou clique \<em **nova conexão...**> para criar um novo Gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="destinationtype--variable"></a>DestinationType = Variável  
 **Destino**  
 Selecione uma variável na lista ou clique em \< **nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa leitor de dados do WMI &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Página Expressões](expressions/expressions-page.md)   
 [Tarefa Detector de Eventos do WMI](control-flow/wmi-event-watcher-task.md)  
  
  

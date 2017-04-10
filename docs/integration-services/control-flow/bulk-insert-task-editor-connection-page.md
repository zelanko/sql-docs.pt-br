---
title: "Editor da Tarefa Inser&#231;&#227;o em Massa (p&#225;gina Conex&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.bulkinserttask.connection.f1"
helpviewer_keywords: 
  - "Editor da Tarefa Inserção em Massa"
ms.assetid: 51252c20-8865-4ede-a3fd-bd73a968f47d
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Editor da Tarefa Inser&#231;&#227;o em Massa (p&#225;gina Conex&#227;o)
  Use a página **Conexão** da caixa de diálogo **Editor da Tarefa Inserção em Massa** para especificar a origem e o destino da operação de inserção em massa e o formato a ser usado.  
  
 Para saber mais sobre como trabalhar com inserções em massa, consulte [Tarefa Inserção em Massa](../../integration-services/control-flow/bulk-insert-task.md) e [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
## Opções  
 **Conexão**  
 Selecione um gerenciador de conexões do OLE DB na lista ou clique em \<**Nova conexão…**> para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Gerenciador de conexões OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md), [Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)  
  
 **Tabela de Destino**  
 Digite o nome da tabela ou exibição de destino ou selecione uma tabela ou exibição na lista.  
  
 **Formato**  
 Selecione a fonte do formato para a inserção em massa. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Usar Arquivo**|Selecione um arquivo que contém a especificação de formato. Selecionar esta opção faz com que seja exibida a opção dinâmica **Arquivo de Formato**.|  
|**Especificar**|Especifique o formato. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas **RowDelimiter** e **ColumnDelimiter**.|  
  
 **Arquivo**  
 Selecione um gerenciador de conexões de Arquivo Simples na lista ou clique em \<**Nova conexão…**> para criar uma nova conexão.  
  
 O local do arquivo está relacionado ao Mecanismo de Banco de Dados do SQL Server especificado no gerenciador de conexões para esta tarefa. O arquivo de texto deve ser acessível pelo Mecanismo de Banco de Dados do SQL Server em um disco rígido local no servidor, por um compartilhamento ou unidade mapeada para o SQL Server. O arquivo não pode ser acessado pelo Tempo de Execução do SSIS.  
  
 Se você acessa o arquivo de origem usando um gerenciador de conexões de Arquivo Simples, a tarefa de Inserção em Massa não usa o formato especificado no gerenciador de conexões de Arquivos Simples. Em vez disso, a tarefa de Inserção em massa usa o formato especificado em um arquivo de formato ou os valores das propriedades RowDelimiter e ColumnDelimiter da tarefa.  
  
 **Tópicos relacionados:** [Gerenciador de Conexões de Arquivo](../../integration-services/connection-manager/file-connection-manager.md), [Editor do Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md), [Editor do Gerenciador de Conexões de Arquivos Simples](../../integration-services/connection-manager/flat-file-connection-manager.md), [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md), [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Colunas&#41](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md), [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Avançado&#41](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)  
  
 **Atualizar Tabelas**  
 Atualize a lista de tabelas e exibições.  
  
## Opções Dinâmicas de Formato  
  
### Formato = Usar Arquivo  
 **FormatFile**  
 Digite o caminho do arquivo de formato ou clique no botão de reticências **(…)** para localizar o arquivo.  
  
### Formato = Especificar  
 **RowDelimiter**  
 Especifique o delimitador de linhas no arquivo de origem. O valor padrão é **{CR}{LF}**.  
  
 **ColumnDelimiter**  
 Especifique o delimitador de colunas no arquivo de origem. O padrão é **Tab**.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa Inserção em Massa &#40;Página Geral&#41;](../../integration-services/control-flow/bulk-insert-task-editor-general-page.md)   
 [Editor da Tarefa Inserção em Massa &#40;Página Opções&#41;](../../integration-services/control-flow/bulk-insert-task-editor-options-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
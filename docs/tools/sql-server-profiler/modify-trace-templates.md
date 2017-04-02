---
title: "Modificar modelos de rastreamento | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modelos [SQL Server], SQL Server Profiler"
  - "Profiler [SQL Server Profiler], modelos"
  - "modelos de rastreamento [SQL Server]"
  - "modificando modelos de rastreamento"
  - "SQL Server Profiler, modelos"
ms.assetid: 75b62a54-8d16-4599-bd2d-c42cfcc209f4
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Modificar modelos de rastreamento
  Você pode modificar os modelos salvos em um arquivo no computador local em que é executado o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Você também pode modificar modelos derivados desses arquivos. Ao modificar modelos existentes, edite as propriedades do modelo, como classes de evento e colunas de dados, na mesma ordem em que essas propriedades foram definidas originalmente, na guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Rastreamento**. As classes de evento e colunas de dados podem ser adicionadas ou removidas e os filtros podem ser alterados. Depois que o modelo é modificado, um modelo específico ao usuário é criado, mantendo-se intacto o modelo do sistema original. Para obter mais informações, veja [Salvar rastreamentos e modelos de rastreamento](../../tools/sql-server-profiler/save-traces-and-trace-templates.md).  
  
 Talvez seja necessário derivar um modelo de um arquivo de rastreamento, caso você não consiga se lembrar do modelo original usado para criar o rastreamento (ou não o tenha salvado) ou se desejar executar o mesmo rastreamento em data futura. Ao trabalhar com rastreamentos existentes, você pode exibir as propriedades, mas não pode modificá-las. Para modificar as propriedades, interrompa ou pause o rastreamento. Para obter mais informações, veja [Derivar um modelo com base em um arquivo ou uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md) e [Derivar um modelo de um rastreamento em execução &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md).  
  
 **Para criar um modelo de rastreamento**  
  
 [Criar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
 **Para executar um rastreamento a partir de um modelo de rastreamento**  
  
 [Criar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 **Para modificar um modelo de rastreamento**  
  
 [Usando o SQL Server Profiler](../../tools/sql-server-profiler/modify-a-trace-template-sql-server-profiler.md)  
  
 [Usando Transact-SQL](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
 **Para adicionar ou remover eventos de um modelo ou arquivo de rastreamento**  
  
 [Usando o SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Usando Transact-SQL](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
## Consulte também  
 [Iniciar um rastreamento](../../tools/sql-server-profiler/start-a-trace.md)  
  
  
---
title: "Modificar um rastreamento existente (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "rastreamentos [SQL Server], modificando"
  - "modificando rastreamentos"
ms.assetid: 8792b43f-2510-44e3-9239-e73ad8227b89
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Modificar um rastreamento existente (Transact-SQL)
  Este tópico descreve como usar procedimentos armazenados para modificar um rastreamento existente.  
  
### Modificar um rastreamento existente  
  
1.  Se o rastreamento já estiver em execução, execute **sp_trace_setstatus** especificando **@status = 0** para parar o rastreamento.  
  
2.  Para modificar eventos de rastreamento, execute **sp_trace_setevent** especificando as alterações pelos parâmetros. Listado em ordem, os parâmetros são:  
  
    -   **@traceid** (ID do rastreamento)  
  
    -   **@eventid** (ID do evento)  
  
    -   **@columnid** (ID da coluna)  
  
    -   **@on** (ON)  
  
     Quando você modificar o parâmetro **@on**, lembre-se da interação dele com o parâmetro **@columnid**:  
  
    |ON|ID da coluna|Resultado|  
    |--------|---------------|------------|  
    |ON (**1**)|NULL|O evento é ativado. Todas as colunas são limpas.|  
    ||NOT NULL|A coluna é ativada para o evento especificado.|  
    |OFF (**0**)|NULL|Evento é desativado. Todas as colunas são limpas.|  
    ||NOT NULL|A coluna é desativada para o evento especificado.|  
  
> [!IMPORTANT]  
>  Ao contrário dos procedimentos armazenados comuns, os parâmetros de todos os procedimentos armazenados do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] (**sp_trace_*xx***) só podem ser digitados e não dão suporte à conversão automática de tipo de dados. Se esses parâmetros não forem chamados pelos tipos de dados com parâmetros de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
## Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
---
description: Modificar um rastreamento existente (Transact-SQL)
title: Modificar um rastreamento existente (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], modifying
- modifying traces
ms.assetid: 8792b43f-2510-44e3-9239-e73ad8227b89
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d6f706093032867835830d0cf98afb86c07e93f7
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88455342"
---
# <a name="modify-an-existing-trace-transact-sql"></a>Modificar um rastreamento existente (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como usar procedimentos armazenados para modificar um rastreamento existente.  
  
### <a name="to-modify-an-existing-trace"></a>Modificar um rastreamento existente  
  
1.  Se o rastreamento já estiver em execução, execute **sp_trace_setstatus** especificando **@status = 0** para parar o rastreamento.  
  
2.  Para modificar eventos de rastreamento, execute **sp_trace_setevent** especificando as alterações pelos parâmetros. Listado em ordem, os parâmetros são:  

    -   **\@traceid** (ID de rastreamento)  
  
    -   **\@eventid** (ID do evento)  
  
    -   **\@columnid** (ID da coluna)  
  
    -   **\@on** (ATIVADO)  
  
     Quando modificar o parâmetro **\@on**, tenha em mente a interação dele com o parâmetro **\@columnid**:  
  
    |ATIVADO|ID da coluna|Result|  
    |--------|---------------|------------|  
    |ON (**1**)|NULO|O evento é ativado. Todas as colunas são limpas.|  
    ||NOT NULL|A coluna é ativada para o evento especificado.|  
    |OFF (**0**)|NULO|Evento é desativado. Todas as colunas são limpas.|  
    ||NOT NULL|A coluna é desativada para o evento especificado.|  
  
> [!IMPORTANT]
>  Ao contrário dos procedimentos armazenados comuns, os parâmetros de todos os procedimentos armazenados do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] (<strong>sp_trace_ *xx*</strong>) são estritamente tipados e não são compatíveis com a conversão automática de tipo de dados. Se esses parâmetros não forem chamados pelos tipos de dados com parâmetros de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  

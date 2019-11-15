---
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
ms.openlocfilehash: 2d1f0eeb0591bd4a51b79b8e83fbbd8d6023535f
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632993"
---
# <a name="modify-an-existing-trace-transact-sql"></a>Modificar um rastreamento existente (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como usar procedimentos armazenados para modificar um rastreamento existente.  
  
### <a name="to-modify-an-existing-trace"></a>Modificar um rastreamento existente  
  
1.  Se o rastreamento já estiver em execução, execute **sp_trace_setstatus** especificando **@status = 0** para parar o rastreamento.  
  
2.  Para modificar eventos de rastreamento, execute **sp_trace_setevent** especificando as alterações pelos parâmetros. Listado em ordem, os parâmetros são:  

    -   **\@traceid** (ID de rastreamento)  
  
    -   **\@eventid** (ID do evento)  
  
    -   **\@columnid** (ID da coluna)  
  
    -   **\@on** (ATIVADO)  
  
     Quando modificar o parâmetro **\@on**, tenha em mente a interação dele com o parâmetro **\@columnid**:  
  
    |ON|ID da coluna|Resultado|  
    |--------|---------------|------------|  
    |ON (**1**)|NULL|O evento é ativado. Todas as colunas são limpas.|  
    ||NOT NULL|A coluna é ativada para o evento especificado.|  
    |OFF (**0**)|NULL|Evento é desativado. Todas as colunas são limpas.|  
    ||NOT NULL|A coluna é desativada para o evento especificado.|  
  
> [!IMPORTANT]
>  Ao contrário dos procedimentos armazenados comuns, os parâmetros de todos os procedimentos armazenados do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] (<strong>sp_trace_*xx*</strong>) são estritamente tipados e não são compatíveis com a conversão automática de tipo de dados. Se esses parâmetros não forem chamados pelos tipos de dados com parâmetros de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  

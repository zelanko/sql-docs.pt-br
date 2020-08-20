---
description: Definir um filtro de rastreamento (Transact-SQL)
title: Definir um filtro de rastreamento (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 7b976a84-7381-43a6-a828-ba83ada71cbe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 59c44a69bbe994ee7df7337213d26b4a789f5a11
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455318"
---
# <a name="set-a-trace-filter-transact-sql"></a>Definir um filtro de rastreamento (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como usar procedimentos armazenados para criar um filtro que recupera apenas as informações que você necessita em um evento que está sendo rastreado.  
  
### <a name="to-set-a-trace-filter"></a>Definir um filtro de rastreamento  
  
1.  Se o rastreamento já estiver em execução, execute **sp_trace_setstatus** especificando `@status = 0` para parar o rastreamento.  
  
2.  Execute **sp_trace_setfilter** para configurar o tipo de informações para recuperar para o evento que está sendo rastreado.  

> [!IMPORTANT]  
>  Ao contrário dos procedimentos armazenados comuns, os parâmetros de todos os procedimentos armazenados do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] (**sp_trace\__xx_**) são estritamente tipados e não são compatíveis com a conversão automática de tipo de dados. Se esses parâmetros não forem chamados com os tipos de dados com parâmetro de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Filtrar um rastreamento](../../relational-databases/sql-trace/filter-a-trace.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  

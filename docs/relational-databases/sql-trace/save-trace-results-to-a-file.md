---
title: Salvar resultados de rastreamento em um arquivo | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a5aae35c87ae1910735b06703bcc52fc87690b06
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="save-trace-results-to-a-file"></a>Salvar resultados de rastreamento em um arquivo
  Você pode salvar os resultados de rastreamentos em um arquivo. Um arquivo de rastreamento é um arquivo no qual são gravados os resultados de um rastreamento. Um arquivo de rastreamento pode estar localizado em um diretório local (como C:\\*foldername*\\*filename.trc*) ou em um diretório de rede (como \\\computername\sharename\filename.trc).  
  
 É possível usar os arquivos de rastreamento para o seguinte:  
  
-   Repetir rastreamentos  
  
-   Auditar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Conduzir análises de desempenho  
  
-   Correlacionar eventos de rastreamento com contadores de desempenho para aperfeiçoar a detecção de problemas  
  
-   Executar análises do Orientador de Otimização do Mecanismo de Banco de Dados  
  
-   Efetuar otimização de consultas  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] salva os resultados em um arquivo quando são especificados um caminho e o nome de arquivo para o argumento **@tracefile** do procedimento armazenado **sp_trace_create**.  
  
> [!NOTE]  
>  Se for especificado um caminho para que o procedimento armazenado **sp_trace_create** para salvar o arquivo de rastreamento, o diretório deverá estar acessível ao servidor. Esteja ciente, ainda, de que, se for especificado um diretório local para **sp_trace_create**, terá de ser um diretório local no computador do servidor.  
  
 Se o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] for usado, ele permitirá salvar os resultados do rastreamento em um arquivo ou em uma tabela. Salvar resultados de rastreamento em uma tabela permite o mesmo acesso que salvá-los em um arquivo, com o adicional de que a tabela poderá ser consultada quanto a eventos específicos.  
  
 Para obter mais informações sobre como salvar os resultados do rastreamento, veja [Salvar resultados de rastreamento em uma tabela &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md) e [Salvar resultados de rastreamento em um arquivo &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md).  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [Criar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  

---
title: Salvar resultados de rastreamento em um arquivo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fff72c4c6100bbff34005b26de30850f4c7381a5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115405"
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
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)   
 [Criar um rastreamento &#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)   
 [Criar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  

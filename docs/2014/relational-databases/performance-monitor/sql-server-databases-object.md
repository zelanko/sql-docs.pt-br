---
title: SQL Server, objeto Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Databases object
- SQLServer:Databases
- Availability Groups [SQL Server], performance counters
ms.assetid: a7f9e7d4-fff4-4c72-8b3e-3f18dffc8919
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b4c0c7a5626f3eb48509d7a4cfbf239f7cb931da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250649"
---
# <a name="sql-server-databases-object"></a>SQL Server, objeto Databases
  O objeto **SQLServer:Databases** no SQL Server fornece contadores para monitorar a taxa de transferência de operações de cópia em massa, backup e restauração, e atividades de log de transações. Ele monitora as transações e o log de transações para determinar quanta atividade de usuário está ocorrendo no banco de dados e o quanto o log de transações está ficando completo. A quantidade de atividade de usuário pode determinar o desempenho do banco de dados e pode afetar o tamanho de log, o bloqueio e a replicação. O monitoramento da atividade de log de baixo nível para medir a atividade de usuário e uso de recursos pode ajudá-lo a identificar gargalos no desempenho.  
  
 Diversas instâncias do objeto **Databases** , cada uma representando um único banco de dados, podem ser monitoradas ao mesmo tempo.  
  
 Esta tabela descreve os contadores **Databases** do SQL Server.  
  
|Contadores de bancos de dados do SQL Server|Descrição|  
|-----------------------------------|-----------------|  
|**Active Transactions**|Número de transações ativas do banco de dados.|  
|**Taxa de transferência de backup/restauração/s**|Taxa de transferência de leitura/gravação para operações de backup e restauração de um banco de dados por segundo. Por exemplo, você pode medir como o desempenho da operação de backup do banco de dados é alterado quando mais dispositivos de backup são usados em paralelo ou quando dispositivos mais rápidos são usados. A taxa de transferência de uma operação de backup ou restauração de banco de dados permite determinar o progresso e desempenho de suas operações de backup e restaurações.|  
|**Linhas de cópia em massa/s**|Número de linhas copiadas em massa por segundo.|  
|**Taxa de transferência de cópia em massa/s**|Quantidade de dados copiados em massa (em quilobytes) por segundo.|  
|**Confirmar entradas da tabela**|O tamanho da parte na memória da tabela de confirmação do banco de dados. Para obter mais informações, veja [sys.dm_tran_commit_table &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table).|  
|**Tamanho de arquivo (s) de dados (KB)**|Tamanho cumulativo (em quilobytes) de todos os arquivos de dados no banco de dados que inclui qualquer crescimento automático. Por exemplo, o monitoramento deste contador é útil para determinar o tamanho correto do **tempdb**.|  
|**Bytes de verificação lógica DBCC/s**|Número de bytes de verificação de leitura lógica por segundo para DBCC (comandos de console de banco de dados).|  
|**Taxa de acertos do cache de log**|Porcentagem de leituras de cache de log satisfeita do cache de log.|  
|**Leituras do cache de log/s**|Faz leituras efetuadas por segundo pelo cache do gerenciador de log.|  
|**Tamanho de arquivo (s) de log (KB)**|Tamanho cumulativo (em kilobytes) de todos os arquivos de log de transações do banco de dados.|  
|**Tamanho usado de arquivo (s) de log (KB)**|Tamanho cumulativo usado de todos os arquivos de log do banco de dados.|  
|**Tempo de espera de liberação de log**|Tempo de espera total (em milissegundos) para liberar o log. Em um banco de dados secundário AlwaysOn, esse valor indica o tempo de espera para a intensificação de registros de log em disco.|  
|**Esperas de liberação de log/s**|Número de confirmações por segundo aguardando liberação do log.|  
|**Tempo de gravação de liberação de log (MS)**|O tempo em milissegundos para execução de gravações de liberações de log que foram concluídas no último segundo.|  
|**Liberações de log/s**|Número de liberações de log por segundo.|  
|**Crescimentos de log**|Número total de vezes que o log de transações do banco de dados foi expandido.|  
|**Reduções de log**|Número total de vezes que o log de transações do banco de dados foi encolhido.|  
|**Erros de cache do pool de logs/s**|O número de solicitações para as quais o bloco de log não estava disponível no pool de logs. O *pool de logs* é um cache de memória do log de transação. Este cache é usado para otimizar a leitura do log para recuperação, replicação de transação, reversão e [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**Leituras de disco do pool de logs/s**|O número de leituras de disco que o pool de log emitiu para buscar blocos de log.|  
|**Solicitações do pool de logs/s**|O número de solicitações do bloco de log processadas pelo pool de log.|  
|**Truncamentos de log**|O número de vezes que o log de transações foi reduzido.|  
|**Percentual de log usado**|Porcentagem de espaço no log que está em uso.|  
|**Transações de repl. Pending**|Número de transações no log de transações do banco de dados de publicação marcado para replicação, mas ainda não enviadas ao banco de dados de distribuição.|  
|**Taxa de repl. trans.**|Número de transações por segundo de leitura do log de transações do banco de dados de publicação enviadas ao banco de dados de distribuição.|  
|**Bytes de movimentação de dados de redução/s**|Quantidade de dados movidos por segundo por operações de encolhimento automático ou de instruções DBCC SHRINKDATABASE ou DBCC SHRINKFILE.|  
|**Transações rastreadas/s**|O número de transações confirmadas registradas na tabela de confirmação do banco de dados.|  
|**Transações/s**|Número de transações iniciadas para o banco de dados por segundo.<br /><br /> **Transações/s** não conta transações somente XTP (transações iniciadas por um procedimento armazenado compilado nativamente)..|  
|**Transações de gravação/s**|Número de transações gravadas e confirmadas ao banco de dados, no último segundo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server, Réplica de banco de dados](sql-server-database-replica.md)  
  
  

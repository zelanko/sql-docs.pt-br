---
title: SQL Server, objeto Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
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
ms.openlocfilehash: 554e582d23afa6ef62b8bc1fd5ab7c8f0c704f4c
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158905"
---
# <a name="sql-server-databases-object"></a>SQL Server, objeto Databases
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto **SQLServer:Databases** no SQL Server fornece contadores para monitorar a taxa de transferência de operações de cópia em massa, backup e restauração, e atividades de log de transações. Ele monitora as transações e o log de transações para determinar quanta atividade de usuário está ocorrendo no banco de dados e o quanto o log de transações está ficando completo. A quantidade de atividade de usuário pode determinar o desempenho do banco de dados e pode afetar o tamanho de log, o bloqueio e a replicação. O monitoramento da atividade de log de baixo nível para medir a atividade de usuário e uso de recursos pode ajudá-lo a identificar gargalos no desempenho.  
  
 Diversas instâncias do objeto **Databases** , cada uma representando um único banco de dados, podem ser monitoradas ao mesmo tempo.  
  
 Esta tabela descreve os contadores **Databases** do SQL Server.  
  
|Contadores de bancos de dados do SQL Server|Descrição|  
|-----------------------------------|-----------------|  
|**Active Transactions**|Número de transações ativas do banco de dados.|  
|**Dist Méd de EOL/Solicit. de LP**|Distância média em bytes até o fim do log por solicitação de pool de logs para solicitações no último VLF.| 
|**Backup/Restore Throughput/sec**|Taxa de transferência de leitura/gravação para operações de backup e restauração de um banco de dados por segundo. Por exemplo, você pode medir como o desempenho da operação de backup do banco de dados é alterado quando mais dispositivos de backup são usados em paralelo ou quando dispositivos mais rápidos são usados. A taxa de transferência de uma operação de backup ou restauração de banco de dados permite determinar o progresso e desempenho de suas operações de backup e restaurações.|  
|**Bulk Copy Rows/sec**|Número de linhas copiadas em massa por segundo.|  
|**Taxa de Transferência de Cópia em Massa/s**|Quantidade de dados copiados em massa (em quilobytes) por segundo.|  
|**Confirmar entradas da tabela**|O tamanho da parte na memória da tabela de confirmação do banco de dados. Para obter mais informações, veja [sys.dm_tran_commit_table &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table.md).|  
|**Tamanho de Arquivo(s) de Dados (KB)**|Tamanho cumulativo (em quilobytes) de todos os arquivos de dados no banco de dados que inclui qualquer crescimento automático. Por exemplo, o monitoramento deste contador é útil para determinar o tamanho correto do **tempdb**.|  
|**DBCC Logical Scan Bytes/sec**|Número de bytes de verificação de leitura lógica por segundo para DBCC (comandos de console de banco de dados).|  
|**Hora da Confirmação do Grupo/s**|Tempo de parada do grupo (em microssegundos) por segundo.|
|**Bytes de Log Liberados/s**|Número total de bytes de log liberados.|  
|**Base da Taxa de Acertos do Cache de Log**|Porcentagem de leituras de cache de log satisfeita do cache de log.|  
|**Base da Taxa de Acertos do Cache de Log**|Somente para uso interno.| 
|**Log Cache Reads/sec**|Faz leituras efetuadas por segundo pelo cache do gerenciador de log.|  
|**Log File(s) Size (KB)**|Tamanho cumulativo (em kilobytes) de todos os arquivos de log de transações do banco de dados.|  
|**Log File(s) Used Size (KB)**|Tamanho cumulativo usado de todos os arquivos de log do banco de dados.|  
|**Tempo de Espera de Liberação de Log**|Tempo de espera total (em milissegundos) para liberar o log. Em um banco de dados secundário AlwaysOn, esse valor indica o tempo de espera para a proteção dos registros de log em disco.|  
|**Esperas de Liberação de Log/s**|Número de confirmações por segundo aguardando liberação do log.|  
|**Tempo de Gravação de Liberação de Log (ms)**|O tempo em milissegundos para execução de gravações de liberações de log que foram concluídas no último segundo.|  
|**Liberações de Log/s**|Número de liberações de log por segundo.|  
|**Crescimentos de Log**|Número total de vezes que o log de transações do banco de dados foi expandido.|  
|**Erros de Cache do Pool de Logs/s**|O número de solicitações para as quais o bloco de log não estava disponível no pool de logs. O *pool de logs* é um cache de memória do log de transação. Este cache é usado para otimizar a leitura do log para recuperação, replicação de transação, reversão e [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**Leituras de Disco do Pool de Logs/s**|O número de leituras de disco que o pool de log emitiu para buscar blocos de log.|  
|**Exclusões de Hash do Pool do Log/seg**|Taxa de exclusões de entrada de hash bruto no Pool do Log.|
|**Inserções de Hash do Pool do Log/seg**|Taxa de inserções de entrada de hash bruto no Pool do Lot.|
|**Entrada Inválida de Hash do Pool do Log/seg**|Taxa de pesquisas de hash com falha por ser inválida.|
|**Verificações de Rastreamento de Log do Pool do Log/seg**|Taxa de verificações em bloco do Log por varreduras do log, que podem vir do disco ou da memória.|
|**Verificações LogWriter do Pool do Log/seg**|Taxa de verificações em bloco do Log por thread de gravação do log.|
|**Push do Pool de Logs vazio para Pool Livre/s**|A taxa de push de bloco de Logs falha devido ao pool livre vazio.|
|**Memória baixa por push no Pool de Logs/s**|A taxa de push de bloco de Logs falha devido a estar com memória insuficiente.|
|**Push do Pool de Logs não tem Buffer Livre/s**|Taxa de push de bloco de Logs falha devido à indisponibilidade do buffer livre.|
|**Registrar Pool de Logs Por trás do Trunc/seg**|Registrar falhas no cache do pool devido ao bloco solicitado estar por trás da truncagem LSN.|
|**Base de Solicitações do Pool de Logs**|Somente para uso interno.| 
|**Solicitações de VLF Antigo do pool de Logs/seg**|Solicitações do Pool de Logs que não estavam no último VLF do log.|  
|**Solicitações do Pool de Logs/s**|O número de solicitações do bloco de log processadas pelo pool de log.|  
|**Tamanho de Logs ativos totais no Pool de Logs**|Logs ativos atuais totais armazenados no gerenciador de buffer em cache compartilhado em bytes.|
|**Tamanho do Pool compartilhado total no Pool de Logs**|Uso total de memória atual do gerenciador do buffer em cache compartilhado em bytes.|
|**Log Shrinks**|Número total de reduções de log para este banco de dados.|  
|**Truncamentos de Log**|O número de vezes que o log de transações foi reduzido.|  
|**Percent Log Used**|Porcentagem de espaço no log que está em uso.|  
|**Repl. Xacts pendentes**|Número de transações no log de transações do banco de dados de publicação marcado para replicação, mas ainda não enviadas ao banco de dados de distribuição.|  
|**Repl. Trans. Taxa**|Número de transações por segundo de leitura do log de transações do banco de dados de publicação enviadas ao banco de dados de distribuição.|  
|**Shrink Data Movement Bytes/sec**|Quantidade de dados movidos por segundo por operações de encolhimento automático ou de instruções DBCC SHRINKDATABASE ou DBCC SHRINKFILE.|  
|**Transações acompanhadas/s**|O número de transações confirmadas registradas na tabela de confirmação do banco de dados.|  
|**Transações/s**|Número de transações iniciadas para o banco de dados por segundo.<br /><br /> **Transações/s** não conta transações somente XTP (transações iniciadas por um procedimento armazenado compilado de modo nativo).|  
|**Write Transactions/sec**|Número de transações gravadas e confirmadas ao banco de dados, no último segundo.|  
|**Base de Latência de DLC do Controlador de XTP**|Somente para uso interno.| 
|**Latência de DLC do Controlador de XTP/Busca**|Latência média em microssegundos entre blocos de log sendo inseridos no Consumidor de Log Direto e sendo recuperados pelo controlador de XTP, por segundo.|
|**Latência de Pico de DLC do Controlador de XTP**|A maior latência registrada, em microssegundos, de uma busca desde um Consumidor de Log Direto e feita por um controlador de XTP.|
|**Log do Controlador de XTP Processado/seg**|A quantidade de bytes de log processados pelo thread do controlador de XTP, por segundo.|
|**Memória de XTP Usada (KB)**|A quantidade de memória usada pelo XTP no banco de dados.| 
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Réplica de banco de dados](../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
  

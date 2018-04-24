---
title: 'Solução de problemas: o grupo de disponibilidade excedeu o RPO (SQL Server) | Microsoft Docs'
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 38de1841-9c99-435a-998d-df81c7ca0f1e
caps.latest.revision: 8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ab808ad9a647ca68094ec9d46219b5a59a1c1a17
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshoot-availability-group-exceeded-rpo"></a>Solução de problemas: o grupo de disponibilidade excedeu o RPO
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Depois de executar um failover manual forçado em um grupo de disponibilidade para uma réplica secundária de confirmação assíncrona, você poderá perceber que a perda de dados foi maior que o RPO (objetivo de ponto de recuperação). Ou, ao calcular a potencial perda de dados de uma réplica secundária de confirmação assíncrona usando o método em [Monitorar desempenho de Grupos de Disponibilidade Always On](monitor-performance-for-always-on-availability-groups.md), você descobre que excedeu o RPO.  
  
 Uma réplica secundária de confirmação síncrona garante perda de dados igual a zero, mas a potencial perda de dados de uma réplica secundária de confirmação assíncrona depende da quantidade de log que ainda está aguardando para ser protegida na réplica secundária.  
  
 As seções a seguir descrevem as causas comuns para um alto potencial de perda de dados de uma réplica secundária de confirmação assíncrona, supondo que você não tem um problema de desempenho sistêmico em sua instância de servidor que não esteja relacionado aos grupos de disponibilidade.  
  
1.  [Alta latência da rede ou baixa taxa de transferência de rede causa o acúmulo de log na réplica primária](#BKMK_LATENCY)  
  
2.  [Gargalo de E/S de disco causa lentidão na proteção do log na réplica secundária](#BKMK_IO_BOTTLENECK)  
  
##  <a name="BKMK_LATENCY"></a> Alta latência da rede ou baixa taxa de transferência de rede causa o acúmulo de log na réplica primária  
 O motivo mais comum para que os bancos de dados excedam o RPO é porque não é possível enviá-los para a réplica secundária rápido o suficiente.  
  
### <a name="explanation"></a>Explicação  
 A réplica primária ativa o controle de fluxo no envio de log quando ele excede o número máximo permitido de mensagens não confirmadas enviadas para a réplica secundária. Até que algumas dessas mensagens sejam confirmadas, não será possível enviar mais logs para a réplica secundária. Como a perda de dados só pode ser evitada depois que os dados foram protegidos na réplica secundária, o acúmulo de mensagens de log não enviadas aumenta a potencial perda de dados.  
  
### <a name="diagnosis-and-resolution"></a>Diagnóstico e resolução  
 Se muitas mensagens são reenviadas para a réplica secundária, pode haver ruído e alta latência de rede. Você também pode comparar o valor DMV **log_send_rate** com o objeto de desempenho Bytes de log liberados/s. Se os logs estiverem sendo liberados para o disco mais rápido do que são enviados, a perda de dados poderá aumentar indefinidamente.  
  
 Além disso, é útil verificar os dois objetos de desempenho, `SQL Server:Availability Replica > Flow Control Time (ms/sec)` e `SQL Server:Availability Replica > Flow Control/sec`. A multiplicação desses dois valores mostra quanto tempo, no último segundo, foi gasto aguardando a limpeza do controle de fluxo. Quanto maior o tempo de espera do controle de fluxo, menor será a taxa de envio.  
  
 As métricas a seguir são úteis para diagnosticar a taxa de transferência e latência da rede. Você pode usar outras ferramentas do Windows, como **ping.exe** e [Monitor de Rede](http://www.microsoft.com/download/details.aspx?id=4865) para avaliar a utilização e a latência da rede.  
  
-   DMV `sys.dm_hadr_database_replica_states, log_send_queue_size`  
  
-   DMV `sys.dm_hadr_database_replica_states, log_send_rate`  
  
-   Contador de desempenho `SQL Server:Database > Log Bytes Flushed/sec`  
  
-   Contador de desempenho `SQL Server:Database Mirroring > Send/Receive Ack Time`  
  
-   Contador de desempenho `SQL Server:Availability Replica > Bytes Sent to Replica/sec`  
  
-   Contador de desempenho `SQL Server:Availability Replica > Bytes Sent to Transport/sec`  
  
-   Contador de desempenho `SQL Server:Availability Replica > Flow Control Time (ms/sec)`  
  
-   Contador de desempenho `SQL Server:Availability Replica > Flow Control/sec`  
  
-   Contador de desempenho `SQL Server:Availability Replica > Resent Messages/sec`  

Para corrigir esse problema, tente atualizar a largura de banda da sua rede ou remover ou reduzir o tráfego de rede desnecessário.  


##  <a name="BKMK_IO_BOTTLENECK"></a> Gargalo de E/S de disco causa lentidão na proteção do log na réplica secundária  
 Dependendo da implantação do arquivo de banco de dados, a proteção de log poderá causar lentidão devido à contenção de E/S com a carga de trabalho de relatório.  
  
### <a name="explanation"></a>Explicação  
 A perda de dados é evitada assim que o bloco de log é protegido no arquivo de log. Portanto, é fundamental isolar o arquivo de log do arquivo de dados. Se o arquivo de log e o arquivo de dados forem mapeados para o mesmo disco rígido, a carga de trabalho de relatório, com leituras intensivas no arquivo de dados, consumirá os mesmos recursos de E/S necessários para a operação de proteção de log. A proteção de log lenta pode se transformar em confirmação lenta na réplica primária, o que poderá causar a ativação excessiva do controle de fluxo e de tempos de espera longos de controle de fluxo.  
  
### <a name="diagnosis-and-resolution"></a>Diagnóstico e resolução  
 Se você verificou que a rede não está apresentando problemas de alta latência ou de baixa taxa de transferência, será necessário investigar contenções de E/S na réplica secundária. As consultas em [SQL Server: minimizar E/S de disco](http://technet.microsoft.com/magazine/jj643251.aspx) são úteis na identificação de contenções. Os exemplos desse artigo são derivados abaixo para sua conveniência.  
  
 O script a seguir permite que você veja o número de leituras e gravações em cada arquivo de dados e de log para cada banco de dados de disponibilidade em execução em uma instância do SQL Server. Ele está classificado por tempo médio de parada de E/S, em milissegundos. Observe que os números são cumulativos desde a última vez em que a instância do servidor foi iniciada. Então, você deve calcular a diferença entre as duas medidas após algum tempo decorrido.  
  
```sql  
SELECT DB_NAME(database_id) AS   
   [Database Name] ,   
   file_id ,   
   io_stall_read_ms ,   
   num_of_reads ,   
   CAST(io_stall_read_ms / ( 1.0 + num_of_reads ) AS NUMERIC(10, 1)) AS [avg_read_stall_ms] ,   
   io_stall_write_ms ,   
   num_of_writes ,  
   CAST(io_stall_write_ms / ( 1.0 + num_of_writes ) AS NUMERIC(10, 1)) AS [avg_write_stall_ms] ,   
   io_stall_read_ms + io_stall_write_ms AS [io_stalls] ,   
   num_of_reads + num_of_writes AS [total_io] ,   
   CAST(( io_stall_read_ms + io_stall_write_ms ) / ( 1.0 + num_of_reads  
+ num_of_writes) AS NUMERIC(10,1)) AS [avg_io_stall_ms]  
FROM sys.dm_io_virtual_file_stats(NULL, NULL)  
WHERE DB_NAME(database_id) IN (SELECT DISTINCT database_name FROM sys.dm_hadr_database_replica_cluster_states)  
ORDER BY avg_io_stall_ms DESC;  
```  
  
 A seguinte consulta fornece um instantâneo (não cumulativo) pontual de solicitações de E/S pendentes no seu sistema.  
  
```sql  
SELECT DB_NAME(mf.database_id) AS [Database] ,   
   mf.physical_name ,  
   r.io_pending ,   
   r.io_pending_ms_ticks ,   
   r.io_type ,   
   fs.num_of_reads ,   
   fs.num_of_writes  
FROM sys.dm_io_pending_io_requests AS r   
INNER JOIN sys.dm_io_virtual_file_stats(NULL, NULL) AS fs ON r.io_handle = fs.file_handle   
INNER JOIN sys.master_files AS mf ON fs.database_id = mf.database_id  
AND fs.file_id = mf.file_id  
ORDER BY r.io_pending , r.io_pending_ms_ticks DESC;  
```  
  
 Você pode comparar como a E/S de leitura e E/S de gravação correspondem entre si para identificar a contenção de E/S.  
  
 Estes são outros contadores de desempenho que podem ajudá-lo a diagnosticar gargalos de E/S:  
  
-   **Physical Disk: all counters**  
  
-   **Physical Disk: Avg. Disk sec/Transfer**  
  
-   **SQL Server: Databases > Log Flush Wait Time**  
  
-   **SQL Server: Databases > Log Flush Waits/sec**  
  
-   **SQL Server: Databases > Log Pool Disk Reads/sec**  
  
 Se você identificou um gargalo de E/S e colocou o arquivo de log e o arquivo de dados no mesmo disco rígido, a primeira coisa a ser feita é colocar o arquivo de dados e o arquivo de log em discos separados. Essa melhor prática impede que a carga de trabalho de relatório interfira no caminho de transferência de log da réplica primária para o buffer de log e sua capacidade de proteger a transação na réplica secundária.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Solução de problemas de desempenho no SQL Server (aplica-se ao SQL Server 2012)](http://msdn.microsoft.com/library/dd672789(v=SQL.100).aspx)  
  
  
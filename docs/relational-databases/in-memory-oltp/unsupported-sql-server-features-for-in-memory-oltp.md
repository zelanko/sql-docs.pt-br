---
title: Recursos do SQL Server sem suporte para OLTP in-memory | Microsoft Docs
ms.custom: 
ms.date: 10/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
caps.latest.revision: 55
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e1b1d4a26616fe83a241267bc87b9e799d883e26
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="unsupported-sql-server-features-for-in-memory-oltp"></a>Recursos do SQL Server sem suporte para OLTP na Memória
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Este tópico discute os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com ou sem suporte para uso com objetos com otimização de memória.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Recursos sem suporte para OLTP in-memory  
 Os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a seguir não têm suporte em um banco de dados que possui objetos com otimização de memória (incluindo o grupo de arquivos de dados com otimização de memória).  
  
|Recurso sem suporte|Descrição do recurso|  
|-------------------------|-------------------------|  
|Compactação de dados para tabelas com otimização de memória.|Você pode usar o recurso de compactação de dados para ajudar a compactar os dados dentro de um banco de dados e ajudar reduzir o tamanho do banco de dados. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|Particionamento de tabelas com otimização de memória e índices de HASH, bem como índices não clusterizados.|Os dados de tabelas e índices particionados são divididos em unidades que podem ser difundidas por mais de um grupo de arquivos em um banco de dados. Para saber mais, confira [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).|  
|Replicação|As configurações de replicação diferentes de replicação transacional para tabelas com otimização de memória em assinantes são incompatíveis com tabelas ou exibições que referenciam tabelas com otimização de memória. A replicação que usa o sync_mode='database snapshot' não terá suporte se houver um grupo de arquivos com otimização de memória. Para obter mais informações, veja [Replicação para assinantes de tabela com otimização de memória](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).|  
|Espelhamento|Não há suporte para o espelhamento de banco de dados para bancos de dados com um grupo de arquivos MEMORY_OPTIMIZED_DATA. Para obter mais informações sobre espelhamento, veja [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|Recompilar log|A recriação do log, tanto ao anexar quanto ao ALTERAR O BANCO DE DADOS, não tem suporte para bancos de dados com um grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Servidor vinculado|Você não pode acessar servidores vinculados na mesma consulta ou transação como tabelas com otimização de memória. Para obter mais informações, veja [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md).|  
|Registro em massa|Independentemente do modelo de recuperação do banco de dados, todas as operações nas tabelas duráveis com otimização de memória sempre são completamente registradas.|  
|Log mínimo|O log mínimo não tem suporte para tabelas com otimização de memória. Para obter mais informações sobre log mínimo, veja [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) e [Pré-requisitos para log mínimo na importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).|  
|Controle de alterações|O controle de alterações pode ser habilitado em um banco de dados com objetos OLTP na memória. No entanto, as alterações em tabelas com otimização de memória não são rastreadas.|  
|gatilhos DDL|Os gatilhos DDL no nível de servidor e de banco de dados não têm suporte com tabelas OLTP na Memória e módulos compilados nativamente.|  
|Change Data Capture (CDC)|O CDC não pode ser usado com um banco de dados que tenha tabelas com otimização de memória, pois ele usa um gatilho DDL para DROP TABLE nos bastidores.|  
|Modo fibra|O modo fibra não tem suporte em tabelas com otimização de memória:<br /><br /> Se o modo fibra estiver ativo, você não poderá criar bancos de dados com grupos de arquivos com otimização de memória ou adicionar grupos de arquivos com otimização de memória para bancos de dados existentes.<br /><br /> Você pode habilitar o modo fibra se houver bancos de dados com grupos de arquivos com otimização de memória. No entanto, habilitar o modo fibra exige a reinicialização do servidor. Nessa situação, os bancos de dados com grupos de arquivos com otimização de memória não seriam recuperados e você verá uma mensagem de erro sugerindo que você desabilite o modo fibra para usar bancos de dados com grupos de arquivos com otimização de memória.<br /><br /> Anexar e restaurar bancos de dados com grupos de arquivos com otimização de memória falhará se o modo fibra estiver ativo. O banco de dados será marcado como suspeito.<br /><br /> <br /><br /> Para saber mais, veja [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).|  
|Limitação do Service Broker|Não é possível acessar uma fila de um procedimento armazenado originalmente compilado.<br /><br /> Não é possível acessar uma fila em um banco de dados remoto em uma transação que acessa tabelas com otimização de memória.|  
|Replicação em assinantes|A replicação transacional para tabelas com otimização de memória em assinantes tem suporte, mas com algumas restrições. Para obter mais informações, veja [Replicação para assinantes de tabela com otimização de memória](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)|  
  
 Com algumas exceções, as transações entre bancos de dados não têm suporte. A tabela a seguir descreve os casos que têm suporte e as limitações correspondentes. (Veja também [Consultas de bancos de dados](../../relational-databases/in-memory-oltp/cross-database-queries.md).)  
  
|Bancos de dados|Allowed (permitido)|Descrição|  
|---------------|-------------|-----------------|  
|Bancos de dados de usuário, modelo e msdb.|Não|Não há suporte para consultas e transações entre bancos de dados.<br /><br /> As consultas e transações que acessam tabelas com otimização de memória ou procedimentos armazenados compilados nativamente não podem acessar outros bancos de dados, com exceção dos bancos de dados do sistema mestre (acesso somente leitura) e tempdb.|  
|Banco de dados de recursos, tempdb|Sim|Não há nenhuma limitação em transações entre bancos de dados que, salvo um banco de dados de usuário único, usam somente banco de dados de recursos e o tempdb.|  
|mestre|somente leitura|As transações entre bancos de dados que tocam o OLTP na memória e o banco de dados mestre falharão na confirmação se incluírem gravações no banco de dados mestre. As transações entre bancos de dados que leem apenas no mestre e usam somente um banco de dados de usuário são permitidas.|  
  
## <a name="scenarios-not-supported"></a>Cenários sem suporte  
  
-   Não há suporte para a contenção de banco de dados ([Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)) no OLTP in-memory. Há suporte para autenticação de banco de dados independente. No entanto, todos os objetos OLTP na memória são marcados como "contenção recente" em dm_db_uncontained_entities do DMV.  
  
-   Acesso a tabelas com otimização de memória usando a conexão de contexto nos procedimentos armazenados CLR.  
  
-   Cursores dinâmicos e de conjunto de chaves em consultas que acessam tabelas com otimização de memória. Esses cursores são degradados para estático e somente leitura.  
  
-   O uso de **MERGE INTO***target* com *target* é uma tabela com otimização de memória. **MERGE USING***source* em tabelas com otimização de memória.  
  
-   Não há suporte para o tipo de dados ROWVERSION (TIMESTAMP). Veja [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md) para obter mais informações.  
  
-   O fechamento automático não tem suporte nos bancos de dados com um grupo de arquivos MEMORY_OPTIMIZED_DATA.  
  
-   Os instantâneos de banco de dados não têm suporte nos bancos de dados com um grupo de arquivos MEMORY_OPTIMIZED_DATA.  
  
-   DDL transacional. Não há suporte para CREATE/ALTER/DROP de objetos OLTP na Memória em transações do usuário.  
  
-   Notificação de eventos.  
  
-   PBM (gerenciamento baseado em política). Não há suporte para impedir e registrar somente modos do PBM. A existência dessas políticas no servidor pode impedir que a DDL do OLTP na memória seja executada com êxito. Há suporte para os modos sob demanda e ao agendar.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao SQL Server para OLTP na memória](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)  
  
  


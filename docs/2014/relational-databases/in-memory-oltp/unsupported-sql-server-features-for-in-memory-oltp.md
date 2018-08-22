---
title: Suporte para recursos do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
caps.latest.revision: 48
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d46187b7f92fb9bb02bb693b51bd13bcd12da1f6
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392685"
---
# <a name="supported-sql-server-features"></a>Recursos do SQL Server com suporte
  Este tópico aborda os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com ou sem suporte para uso com objetos com otimização de memória.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Recursos com suporte para OLTP na memória  
 Os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a seguir têm suporte em um banco de dados que possui objetos com otimização de memória, incluindo o grupo de arquivos com otimização de memória.  
  
 Para obter mais informações sobre tipos de dados com suporte, consulte [Supported Data Types](supported-data-types-for-in-memory-oltp.md).  
  
-   Opções e operações com suporte nas tabelas com otimização de memória. Para obter mais informações, consulte [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).  
  
-   Opções e operações com suporte nos procedimentos armazenados compilados nativamente. Para obter mais informações, consulte [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql).  
  
-   Capacidade de acessar tabelas com otimização de memória usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado. O [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado fornece a área da superfície equivalente para acessar tabelas que não têm otimização de memória usando procedimentos armazenados que não são compilados nativamente e usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Para obter mais informações, consulte [Acessando tabelas com otimização de memória usando Transact-SQL interpretado](accessing-memory-optimized-tables-using-interpreted-transact-sql.md).  
  
-   Controle de simultaneidade otimista e várias versões. Para obter mais informações, consulte [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md).  
  
-   Backup e restauração de um banco de dados que contém grupo de arquivos de dados com otimização de memória. Para obter mais informações, consulte [Back Up and Restore of SQL Server Databases](../backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
-   Exibições de catálogo, exibições de gerenciamento dinâmico e eventos estendidos para capacidade de suporte. Para obter mais informações, consulte [Exibições do sistema, procedimentos armazenados, tipos de espera e DMVs para OLTP na memória](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects. Para obter mais informações, consulte [Suporte ao SQL Server Management Objects para OLTP na memória](sql-server-management-objects-support-for-in-memory-oltp.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Suporte ao SQL Server Management Studio para OLTP na memória](sql-server-management-studio-support-for-in-memory-oltp.md).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Visão geral do SQL Server PowerShell](http://msdn.microsoft.com/library/cc281954\(SQL.105\).aspx).  
  
-   Importar e exportar dados em massa usando o utilitário bcp. Para obter mais informações, consulte [Importar e exportar dados em massa usando o utilitário bcp &#40;SQL Server&#41;](../import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md).  
  
-   Recuperação de pane.  
  
-   Vários contêineres em um grupo de arquivos de dados com otimização de memória para armazenar objetos OLTP na memória e reduzir o RTO (objetivo de tempo de recuperação).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] blocos de log de transação calculam a soma de verificação e validam.  
  
-   A nova dica de tabela SNAPSHOT. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table).  
  
-   Nível de DB COMPAT.  
  
-   Banco de dados parcialmente independente. Há suporte para autenticação de banco de dados independente. No entanto, todos os objetos OLTP na memória são marcados como "contenção recente" em dm_db_uncontained_entities do DMV.  
  
-   Service broker, com limitações. Não é possível acessar uma fila de um procedimento armazenado originalmente compilado. Não é possível acessar uma fila em um banco de dados remoto em uma transação que acessa tabelas com otimização de memória.  
  
-   Clustering de failover: como parte da oferta AlwaysOn do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as Instâncias de Cluster de Failover do AlwaysOn aproveitam a funcionalidade WSFC (Windows Server Failover Clustering) para fornecer alta disponibilidade local por meio de redundância no nível de instância de servidor - uma FCI (instância de cluster de failover). Para obter mais informações, consulte [Instâncias do Cluster de Failover do AlwaysOn (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
-   Integração com AlwaysOn: o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece várias opções para a criação de alta disponibilidade de um servidor ou banco de dados, inclusive o AlwaysOn. Para obter mais informações, consulte [Soluções de alta disponibilidade &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md).  
  
-   Envio de logs: o envio de logs do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite o envio automático de backups do log de transações de um banco de dados primário em uma instância do servidor primário para um ou mais bancos de dados secundários em outras instâncias de servidor secundário. Para obter mais informações, consulte [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
-   A replicação transacional para tabelas com otimização de memória em assinantes tem suporte com algumas restrições. Para obter mais informações, veja [Replicação para assinantes de tabela com otimização de memória](../replication/replication-to-memory-optimized-table-subscribers.md).  
  
-   Administrador de Recursos: o Administrador de Recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um recurso que você pode usar para gerenciar a carga de trabalho e o consumo de recursos do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O Administrador de Recursos permite que você especifique os limites de quantidade de CPU, E/S física e memória que as solicitações recebidas de aplicativos podem usar. Para obter mais informações, consulte [Managing Memory for In-Memory OLTP](../../database-engine/managing-memory-for-in-memory-oltp.md) e [Resource Governor](../resource-governor/resource-governor.md).  
  
-   A OLTP na memória tem restrições nas páginas de código com suporte para colunas (var)char em tabelas com otimização de memória e agrupamentos com suporte usados em índices e em procedimentos armazenados nativamente compilados. Para obter mais informações, consulte [Collations and Code Pages](../../database-engine/collations-and-code-pages.md).  
  
-   Suporte a BACPAC.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Recursos sem suporte para OLTP in-memory  
 Os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a seguir não têm suporte em um banco de dados que possui objetos com otimização de memória (incluindo o grupo de arquivos de dados com otimização de memória).  
  
|Recurso sem suporte|Descrição do recurso|  
|-------------------------|-------------------------|  
|Compactação de dados para tabelas com otimização de memória.|Você pode usar o recurso de compactação de dados para ajudar a compactar os dados dentro de um banco de dados e ajudar reduzir o tamanho do banco de dados. Para obter mais informações, consulte [Data Compression](../data-compression/data-compression.md).|  
|Particionamento de índices de HASH e tabelas com otimização de memória.|Os dados de tabelas e índices particionados são divididos em unidades que podem ser difundidas por mais de um grupo de arquivos em um banco de dados. Para saber mais, confira [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).|  
|TDE (Criptografia de Dados Transparente) no grupo de arquivo de dados com otimização de memória de um banco de dados.|A criptografia transparente de dados (TDE) executa criptografia de E/S em tempo real e a descriptografia de dados e arquivos de log. Para obter mais informações, veja [TDE &#40;Transparent Data Encryption&#41;](../security/encryption/transparent-data-encryption.md).<br /><br /> A TDE pode ser habilitada em um banco de dados que tenha objetos OLTP na memória. Os registros de log do OLTP na memória serão criptografados se a TDE estiver habilitada. Os arquivos de ponto de verificação para tabelas duráveis não são criptografados, mesmo se a TDE estiver habilitada no banco de dados.|  
|Replicação|As configurações de replicação diferentes de replicação transacional para tabelas com otimização de memória em assinantes são incompatíveis com tabelas ou exibições que referenciam tabelas com otimização de memória. A replicação que usa o sync_mode='database snapshot' não terá suporte se houver um grupo de arquivos com otimização de memória. Para obter mais informações, consulte [Replication to Memory-Optimized Table Subscribers](../replication/replication-to-memory-optimized-table-subscribers.md).|  
|MARS (Vários Conjuntos de Resultados Ativos)|O MARS (Vários Conjuntos de Resultados Ativos) não tem suporte com tabelas com otimização de memória. Esse erro também pode indicar uso de servidor vinculado. O servidor vinculado pode usar MARS. Os servidores vinculados não têm suporte com tabelas com otimização de memória. Conecte-se diretamente ao servidor e ao banco de dados que hospeda as tabelas com otimização de memória.|  
|Espelhamento|O espelhamento de banco de dados é uma solução para aumentar a disponibilidade de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|Recompilar log|A recompilação do log, tanto ao anexar quanto ao ALTERAR O BANCO DE DADOS, não tem suporte para bancos de dados com um grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Servidor vinculado|Para obter mais informações, veja [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../linked-servers/linked-servers-database-engine.md).|  
|Registro em massa|Independentemente do modelo de recuperação do banco de dados, todas as operações nas tabelas duráveis com otimização de memória sempre são completamente registradas.|  
|Log mínimo|O log mínimo não tem suporte para tabelas com otimização de memória. Para obter mais informações sobre log mínimo, veja [O log de transações &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md) e [Pré-requisitos para log mínimo na importação em massa](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md).|  
|controle de alterações|O controle de alterações pode ser habilitado em um banco de dados com objetos OLTP na memória. No entanto, as alterações em tabelas com otimização de memória não são rastreadas.|  
|gatilhos DDL|Os gatilhos DDL no nível de servidor e de banco de dados não têm suporte com tabelas OLTP na memória e procedimentos armazenados compilados nativamente.|  
|Change Data Capture (CDC)|O CDC não deve ser habilitado em um banco de dados que tenha objetos OLTP na memória, pois isso impede determinadas operações, como DROP.|  
|Contenção do banco de dados|A contenção de banco de dados não é suportada em um banco de dados com procedimentos armazenados compilados nativamente e tabelas com otimização de memória. Para obter mais informações, consulte [Contained Databases](../databases/contained-databases.md).|  
|Conexões de contexto|Não é suportado o acesso a tabelas com otimização de memória usando a conexão de contexto nos procedimentos armazenados CLR.|  
|Cursores|Cursores dinâmicos e de conjunto de chaves em consultas que acessam tabelas com otimização de memória. Essas consultas são degradadas para estáticas, tornando-se somente leitura.|  
|TABLESTAMP|Não há suporte para TABLESTAMP. Veja [FROM &#40;Transact-SQL&#41;](/sql/t-sql/queries/from-transact-sql) para obter mais informações.|  
|AUTO_CLOSE|AUTO_CLOSE não suportado. Para obter mais informações, consulte [Set the AUTO_CLOSE Database Option to OFF](../policy-based-management/set-the-auto-close-database-option-to-off.md).|  
|Instantâneos do banco de dados|Não é oferecido suporte a instantâneos de banco de dados. Para obter mais informações, consulte [Instantâneos de banco de dados &#40;SQL Server&#41;](../databases/database-snapshots-sql-server.md).|  
|DDL transacional|O DDL transacional não é suportado no OLTP na memória.|  
|Notificações de eventos|Notificações de evento não são suportadas. Para obter mais informações, consulte [Event Notifications](../service-broker/event-notifications.md).|  
|Modo fibra|O modo fibra não tem suporte com o OLTP na memória.|  
|PBM (gerenciamento baseado em política).|Não há suporte para impedir e registrar somente modos do PBM. A existência dessas políticas no servidor pode impedir que a DDL do OLTP na memória seja executada com êxito. Há suporte para os modos sob demanda e ao agendar.|  
|Implantação/extração de DACFX|A implantação/extração da Estrutura DAC não é suportada no OLTP na memória.|  
  
 Com algumas exceções, as transações entre bancos de dados não têm suporte. A tabela a seguir descreve os casos que têm suporte e as limitações correspondentes. (Veja também [Consultas de bancos de dados](cross-database-queries.md).)  
  
|Bancos de dados|Allowed (permitido)|Description|  
|---------------|-------------|-----------------|  
|Bancos de dados de usuário, modelo e msdb|não|Não há suporte para consultas e transações entre bancos de dados.<br /><br /> As consultas e transações que acessam tabelas com otimização de memória ou procedimentos armazenados compilados nativamente não podem acessar outros bancos de dados, com exceção dos bancos de dados do sistema mestre (acesso somente leitura) e tempdb.|  
|Banco de dados de recursos e tempdb|Sim|Não há nenhuma limitação em transações entre bancos de dados que, salvo um banco de dados de usuário único, usam somente banco de dados de recursos e o tempdb.|  
|master|somente leitura|As transações entre bancos de dados que tocam o OLTP na memória e o banco de dados mestre falharão na confirmação se incluírem gravações no banco de dados mestre. As transações entre bancos de dados que leem apenas no mestre e usam somente um banco de dados de usuário são permitidas.|  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao SQL Server para OLTP na memória](sql-server-support-for-in-memory-oltp.md)  
  
  

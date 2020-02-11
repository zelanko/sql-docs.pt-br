---
title: O que&#39;s New (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5e51cda61bb44d1f143cab50901276b927cca73a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70176072"
---
# <a name="what39s-new-database-engine"></a>O que&#39;s New (Mecanismo de Banco de Dados)
  Esta versão mais recente do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] apresenta novos recursos e aprimoramentos que aumentam o poder e a produtividade de arquitetos, desenvolvedores e administradores que criam, desenvolvem e mantêm sistemas de armazenamento de dados. Estas são as áreas nas quais o [!INCLUDE[ssDE](../includes/ssde-md.md)] foi aprimorado.  
  
##  <a name="Feature"></a>Aprimoramentos de recursos do Mecanismo de Banco de Dados  
  
###  <a name="MemoryOpt"></a>Tabelas com otimização de memória  
 O OLTP em Memória é um mecanismo de banco de dados com otimização de memória integrado ao mecanismo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . OLTP em Memória é otimizado para OLTP. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
 
  
###  <a name="DataFiles"></a>SQL Server arquivos de dados no Azure  
 [SQL Server arquivos de dados no Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) habilita o suporte [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nativo para arquivos de banco de dado armazenados como BLOBs do Azure. Esse recurso permite que você crie um banco de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dados em execução no local ou em uma máquina virtual no Azure com um local de armazenamento dedicado para seus dados no armazenamento de BLOBs do Azure.  
  
  
###  <a name="AzureVM"></a>Hospedar um banco de dados SQL Server em uma máquina virtual do Azure  
 Use o assistente para [implantar um banco de dados SQL Server em uma máquina virtual do Azure](https://msdn.microsoft.com/library/dn195938\(v=sql.120\).aspx) para hospedar um banco [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de dados de uma instância do em uma máquina virtual do Azure.  
  
  
###  <a name="Backup"></a>Aprimoramentos de backup e restauração  
 O [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] contém os seguintes aperfeiçoamentos para o backup e restauração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   **Backup do SQL Server para URL**  
  
     O backup do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para URL foi introduzido no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP1 CU2 com suporte somente pelo [!INCLUDE[tsql](../includes/tsql-md.md)], PowerShell e SMO. No [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] , você pode [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] usar o para fazer backup ou restaurar do serviço de armazenamento de BLOBs do Azure. A nova opção está disponível tanto para a tarefa de backup como para os planos de manutenção. Para obter mais informações, consulte [usando a tarefa de backup no SQL Server Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#BackupTaskSSMS), [SQL Server Backup para URL usando o assistente de plano de manutenção](../relational-databases/backup-restore/sql-server-backup-to-url.md#MaintenanceWiz)e [restaurando do armazenamento do Azure usando o SQL Server Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS).  
  
-   **Backup gerenciado do SQL Server para Azure**  
  
     Inserido no backup do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para URL, o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] é um serviço que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece para gerenciar e agendar os backups de banco de dados e log. Nesta versão, só há suporte para backup no armazenamento do Azure. O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] pode ser configurado no banco de dados e no nível de instância permitindo um controle granular no nível do banco de dados e na automação no nível de instância. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]pode ser configurado em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instâncias em execução no local e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em instâncias em execução em máquinas virtuais do Azure. É recomendável para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instâncias em execução em máquinas virtuais do Azure. Para obter mais informações, consulte [SQL Server Backup gerenciado para o Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
-   **Criptografia para backups**  
  
     Agora você pode escolher criptografar o arquivo de backup durante uma operação de backup.  Ele dá suporte a vários algoritmos de criptografia incluindo AES 128, AES 192, AES 256 e Triple DES. Você deve usar um certificado ou uma chave assimétrica para executar a criptografia durante o backup. Para obter mais informações, veja [Criptografia de backup](../relational-databases/backup-restore/backup-encryption.md).  
  
  
###  <a name="CE"></a>Novo design para estimativa de cardinalidade  
 A lógica de estimativa de cardinalidade, chamada de avaliador de cardinalidade, foi reformulada no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] para melhorar a qualidade dos planos de consulta e, consequentemente, melhorar o desempenho de consulta. O novo avaliador de cardinalidade incorpora as suposições e os algoritmos que funcionam bem em OLTP moderno e em cargas de trabalho de data warehouse. Ele se baseia na pesquisa detalhada da estimativa de cardinalidade em cargas de trabalho modernas, bem como em nosso aprendizado nos últimos 15 anos de aperfeiçoamento do avaliador de cardinalidade do SQL Server. Os comentários dos clientes mostram que, apesar de a maioria das consultas se beneficiarem da alteração ou permanecerem inalteradas, poucas mostram regressões em comparação ao avaliador de cardinalidade anterior. Para o ajuste de desempenho e recomendações de teste, consulte [estimativa de cardinalidade &#40;SQL Server&#41;](../relational-databases/performance/cardinality-estimation-sql-server.md).  
   
  
###  <a name="Durability"></a>Durabilidade atrasada  
 O [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] apresenta a capacidade de reduzir a latência designando algumas ou todas as transações como duráveis atrasadas. Uma transação durável atrasada retorna o controle para o cliente antes de o registro do log de transação ser gravado no disco. A durabilidade pode ser controlada no nível do banco de dados, nível COMMIT ou nível de bloco ATOMIC.  
  
 Para obter mais informações, consulte o tópico [controlar a durabilidade da transação](../relational-databases/logs/control-transaction-durability.md).  
  
  
###  <a name="AlwaysOn"></a>Aprimoramentos do AlwaysOn  
 O [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] contém os seguintes aprimoramentos para Instâncias de Cluster de Failover AlwaysOn e Grupos de Disponibilidade AlwaysOn:  
  
-   Um Assistente para Adicionar Réplica do Azure simplifica a criação de soluções híbridas para grupos de disponibilidade AlwaysOn. Para obter mais informações, consulte [usar o assistente para adicionar réplica do Azure &#40;SQL Server&#41;](availability-groups/windows/use-the-add-azure-replica-wizard-sql-server.md).  
  
-   O número máximo de réplicas secundárias é aumentado de 4 para 8.  
  
-   Quando desconectadas da réplica primária ou durante a perda de quorum de cluster, as réplicas secundárias legíveis agora permanecem disponíveis para cargas de trabalho de leitura.  
  
-   Agora, as instâncias de cluster de failover (FCIs) podem usar Volumes Compartilhados Clusterizados (CSVs) como discos compartilhados de cluster. Para obter mais informações, consulte [Always on instâncias de cluster de failover](../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
-   Uma nova função do sistema, [sys.fn_hadr_is_primary_replica](/sql/relational-databases/system-functions/sys-fn-hadr-is-primary-replica-transact-sql)e um novo DMV, [sys.dm_io_cluster_valid_path_names](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql), estão disponíveis.  
  
-   Os DMVs a seguir foram aprimorados e agora retornam informações sobre FCI: [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql), [sys.dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)e [sys.dm_hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql).  
  
  
###  <a name="OIR"></a>Alternância de partição e indexação  
 As partições individuais de tabelas particionadas podem agora ser recriadas. Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
   
  
###  <a name="Lock"></a>Gerenciando a prioridade de bloqueio de operações online  
 A opção `ONLINE = ON` agora contém uma opção `WAIT_AT_LOW_PRIORITY` que permite que você especifique por quanto tempo o processo de recriação deve aguardar os bloqueios necessários. A opção `WAIT_AT_LOW_PRIORITY` também permite configurar a conclusão dos processos de bloqueio relacionados à instrução REBUILD. Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql) e [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql). As informações de solução de problemas de novos tipos de Estados de bloqueio estão disponíveis em [Sys. dm_tran_locks &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql) e [sys. Dm_os_wait_stats &#40;o transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql).  
 
  
###  <a name="CCI"></a>Índices Columnstore  
 Esses novos recursos estão disponíveis para índices columnstore:  
  
-   **Índice columnstore clusterizado**  
  
     Use um índice columnstore clusterizado para melhorar a compactação de dados e o desempenho de consultas para cargas de trabalho de data warehouse que basicamente executam carregamentos em massa e consultas somente leitura. Uma vez que o índice columnstore clusterizado é atualizável, a carga de trabalho pode executar muitas operações de inserção, atualização e exclusão. Para obter mais informações, consulte [índices Columnstore descritos](../relational-databases/indexes/columnstore-indexes-described.md) e [usando índices columnstore clusterizados](../relational-databases/indexes/indexes.md).  
  
-   **SHOWPLAN**  
  
     SHOWPLAN exibe informações sobre índices columnstore. As propriedades **EstimatedExecutionMode** e **ActualExecutionMode** têm dois valores possíveis: **Batch** ou **Row**.  A propriedade **Storage** tem dois valores possíveis: **RowStore** e **ColumnStore**.  
  
-   **Compactação de dados para arquivamento**  
  
     ALTERAR ÍNDICE... Rebuild tem uma nova opção de compactação de dados COLUMNSTORE_ARCHIVE que compacta ainda mais as partições especificadas de um índice COLUMNSTORE. Use esse recurso para arquivamento ou em outras situações que exijam um tamanho menor de armazenamento de dados e possam dispensar mais tempo para armazenamento e recuperação. Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
   
  
###  <a name="Buffer"></a>Extensão do pool de buffers  
 A opção [Extensão do pool de buffers](configure-windows/buffer-pool-extension.md) proporciona integração contínua das unidades de estado sólido (SSDs) como uma memória de acesso aleatório não volátil (NvRAM) ao pool de buffers do [!INCLUDE[ssDE](../includes/ssde-md.md)] com a intenção de melhorar significativamente a taxa de transferência de E/S.  
   
  
###  <a name="Stats"></a>Estatísticas incrementais  
 CREATE STATISTICS e as instruções relacionadas de estatística agora permitem estatísticas por partição para serem criadas com a opção INCREMENTAL. As instruções relacionadas permitem ou reportam estatísticas incrementais. A sintaxe afetada inclui as opções atualizar estatísticas, sp_createstats, criar índice, ALTER INDEX, ALTER DATABASE SET, DATABASEPROPERTYEX, sys. databases e sys. stats. Para obter mais informações, consulte [Create statistics &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
  
###  <a name="RG"></a>Aprimoramentos de Resource Governor para controle de e/s físico  
 O Administrador de Recursos permite que você especifique os limites de quantidade de CPU, E/S física e memória que as solicitações recebidas de aplicativos podem usar dentro de um pool de recursos. No [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], você pode usar as novas configurações do MIN_IOPS_PER_VOLUME e MAX_IOPS_PER_VOLUME para controlar as E/S físicas emitidas para threads de usuário para um determinado pool de recursos. Para obter mais informações, consulte [resource governor pool de recursos](../relational-databases/resource-governor/resource-governor-resource-pool.md) e [criar pool de recursos &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-resource-pool-transact-sql).  
  
 A configuração MAX_OUTSTANDING_IO_PER_VOLUME do ALTER RESOURCE GOVENOR define o máximo de operações de E/S pendentes por volume de disco. Você pode usar essa configuração para ajustar o controle de recursos de E/S para as características de E/S de um volume de disco e pode ser usada para limitar o número de E/S emitida no limite de instância do SQL Server. Para obter mais informações, veja [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql).  
  
  
###  <a name="OnlineEvent"></a>Classe de evento online index Operation  
 O relatório de andamento para a classe de evento da operação de índice online agora tem duas novas colunas de dados: **PartitionId** e **PartitionNumber**. Para obter mais informações, consulte [Progress Report: Online Index Operation Event Class](../relational-databases/event-classes/progress-report-online-index-operation-event-class.md).  
  
  
###  <a name="Compat"></a>Nível de compatibilidade do banco de dados  
 O nível de compatibilidade 90 não é válido no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Para obter mais informações, consulte [nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
##  <a name="TSQL"></a>Aprimoramentos do Transact-SQL  
  
### <a name="inline-specification-of-clustered-and-nonclustered"></a>Especificação embutida de CLUSTERED e NONCLUSTERED  
 A especificação embutida dos índices `CLUSTERED` e `NONCLUSTERED` é permitida agora para tabelas baseadas em disco. Criar uma tabela com índices embutidos é equivalente a emitir uma tabela de criação seguida por instruções `CREATE INDEX` correspondentes. Não há suporte para colunas incluídas e condições de filtro nos índices embutidos.  
  
### <a name="select--into"></a>SELECIONAR... PORTA  
 A instrução `SELECT ... INTO` é aprimorada e agora pode funcionar em paralelo. O nível de compatibilidade do banco de dados deve ser pelo menos 110.  
  
### <a name="includetsqlincludestsql-mdmd-enhancements-for-in-memory-oltp"></a>
  [!INCLUDE[tsql](../includes/tsql-md.md)] Aprimoramentos para OLTP em Memória  
 Para obter informações sobre as alterações do [!INCLUDE[tsql](../includes/tsql-md.md)] para dar suporte a OLTP em Memória, consulte [Transact-SQL Support for In-Memory OLTP](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md).  
  
  
##  <a name="SystemTable"></a>Aprimoramentos de exibição do sistema  
  
### <a name="sysxml_indexes"></a>sys.xml_indexes  
 [Sys. xml_indexes &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-xml-indexes-transact-sql) tem três novas colunas: `xml_index_type`, `xml_index_type_description`e `path_id`.  
  
### <a name="sysdm_exec_query_profiles"></a>sys.dm_exec_query_profiles  
 [Sys. dm_exec_query_profiles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql) monitora o progresso da consulta em tempo real enquanto uma consulta está em execução.  
  
### <a name="syscolumn_store_row_groups"></a>sys.column_store_row_groups  
 [Sys. column_store_row_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql) fornece informações de índice columnstore clusterizado por segmento para ajudar o administrador a tomar decisões de gerenciamento do sistema.  
  
### <a name="sysdatabases"></a>sys.databases  
 [Sys. databases &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) tem três novas colunas: `is_auto_create_stats_incremental_on`, `is_query_store_on`e `resource_pool_id`.  
  
### <a name="system-view-enhancements-for-in-memory-oltp"></a>Aprimoramentos de exibição do sistema para OLTP em Memória  
 Para obter informações sobre os aprimoramentos de exibição do sistema para dar suporte ao OLTP na memória, consulte [exibições do sistema, procedimentos armazenados, DMVs e tipos de espera para OLTP na memória](../../2014/database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md).  
   
  
##  <a name="Security"></a>Aprimoramentos de segurança  
  
### <a name="connect-any-database-permission"></a>Permissão CONNECT ANY DATABASE  
 Uma nova permissão de nível de servidor. Conceda **CONNECT ANY DATABASE** a um logon que deve se conectar a todos os bancos de dados que existem atualmente e a quaisquer novos bancos de dados que possam ser criados no futuro. Não concede nenhuma permissão em qualquer banco de dados além da conexão. Combine com **selecionar todos os protegíveis** de usuário `VIEW SERVER STATE` ou para permitir que um processo de auditoria exiba todos os dados ou todos os Estados de banco [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de dado na instância do.  
  
### <a name="impersonate-any-login-permission"></a>Permissão IMPERSONATE ANY LOGIN  
 Uma nova permissão de nível de servidor. Quando concedida, permite que um processo de camada intermediária represente a conta de clientes que se conecta a ela, uma vez que ela se conecta aos bancos de dados. Quando negada, um logon com altos privilégios pode ser impedido de representar outros logons. Por exemplo, um logon com a permissão **CONTROL SERVER** pode ser impedido de representar outros logons.  
  
### <a name="select-all-user-securables-permission"></a>Permissão SELECT ALL USER SECURABLES  
 Uma nova permissão de nível de servidor. Quando concedida, um logon, como um auditor, pode exibir dados em todos os bancos de dados aos quais o usuário pode se conectar.  
  
  
##  <a name="Deployment"></a>Aprimoramentos de implantação  
### <a name="azure-vm"></a>VM do Azure
[Implantar um banco de dados SQL Server em uma máquina Virtual Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) permite a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] implantação de um banco de dados em uma VM do Azure.  

### <a name="refs"></a>ReFS
Agora há suporte para a implantação de bancos de dados em ReFS.   
  
## <a name="see-also"></a>Consulte Também  
 [Recursos compatíveis com as edições do SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
   

---
title: O que&#39;novo para s (mecanismo de banco de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
caps.latest.revision: 206
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2ebd9a1aaf1b7a6c1e9130e3587ca286b4cf910c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120637"
---
# <a name="what39s-new-database-engine"></a>O que&#39;novo para s (mecanismo de banco de dados)
  Esta versão mais recente do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] apresenta novos recursos e aprimoramentos que aumentam o poder e a produtividade de arquitetos, desenvolvedores e administradores que criam, desenvolvem e mantêm sistemas de armazenamento de dados. Estas são as áreas nas quais o [!INCLUDE[ssDE](../includes/ssde-md.md)] foi aprimorado.  
  
##  <a name="Feature"></a> Aprimoramentos do mecanismo de banco de dados  
  
###  <a name="MemoryOpt"></a> Tabelas com otimização de memória  
 O OLTP em Memória é um mecanismo de banco de dados com otimização de memória integrado ao mecanismo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. OLTP em Memória é otimizado para OLTP. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
 
  
###  <a name="DataFiles"></a> Arquivos de dados do SQL Server no Windows Azure  
 [Arquivos de dados do SQL Server no Windows Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) habilita o suporte nativo para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] arquivos armazenados como Blobs do Windows Azure do banco de dados. Esse recurso permite que você crie um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] executado localmente ou em uma máquina virtual no Windows Azure com um local de armazenamento dedicado para seus dados no Armazenamento de Blob do Windows Azure.  
  
  
###  <a name="AzureVM"></a> Hospedar um banco de dados SQL Server em uma janela de máquina Virtual do Azure  
 Use o [implantar um banco de dados do SQL Server para uma máquina Virtual Windows Azure](http://msdn.microsoft.com/library/dn195938\(v=sql.120\).aspx) Assistente para hospedar um banco de dados de uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em uma máquina Virtual Windows Azure.  
  
  
###  <a name="Backup"></a> Backup e restauração aprimoramentos  
 O [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] contém os seguintes aperfeiçoamentos para o backup e restauração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   **Backup do SQL Server para URL**  
  
     O backup do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para URL foi introduzido no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP1 CU2 com suporte somente pelo [!INCLUDE[tsql](../includes/tsql-md.md)], PowerShell e SMO. No [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], você pode usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para fazer backup ou restaurar do serviço de armazenamento de blob do Windows Azure. A nova opção está disponível tanto para a tarefa de backup como para os planos de manutenção. Para obter mais informações, consulte [usando a tarefa de Backup no SQL Server Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#BackupTaskSSMS), [SQL Server Backup to URL Using Maintenance Plan Wizard](../relational-databases/backup-restore/sql-server-backup-to-url.md#MaintenanceWiz), e [restauração do armazenamento do Windows Azure usando o SQL Server Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS).  
  
-   **Backup Gerenciado do SQL Server para Microsoft Azure**  
  
     Inserido no backup do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para URL, o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] é um serviço que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece para gerenciar e agendar os backups de banco de dados e log. Nesta versão, somente o backup ao armazenamento do Windows Azure tem suporte. O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] pode ser configurado no banco de dados e no nível de instância permitindo um controle granular no nível do banco de dados e na automação no nível de instância. O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] pode ser configurado em instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que executam instâncias locais e do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que são executadas em máquinas virtuais do Windows Azure. É recomendável para as instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que sejam executadas em máquinas virtuais do Windows Azure. Para obter mais informações, consulte [SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
-   **Criptografia para Backups**  
  
     Agora você pode escolher criptografar o arquivo de backup durante uma operação de backup.  Ele dá suporte a vários algoritmos de criptografia incluindo AES 128, AES 192, AES 256 e Triple DES. Você deve usar um certificado ou uma chave assimétrica para executar a criptografia durante o backup. Para obter mais informações, consulte [criptografia de Backup](../relational-databases/backup-restore/backup-encryption.md).  
  
  
###  <a name="CE"></a> Novo Design para a estimativa de cardinalidade  
 A lógica de estimativa de cardinalidade, chamada de avaliador de cardinalidade, foi reformulada no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] para melhorar a qualidade dos planos de consulta e, portanto, para melhorar o desempenho da consulta. O novo avaliador de cardinalidade incorpora as suposições e os algoritmos que funcionam bem em OLTP moderno e em cargas de trabalho de data warehouse. Ele se baseia na pesquisa detalhada da estimativa de cardinalidade em cargas de trabalho modernas, bem como em nosso aprendizado nos últimos 15 anos de aperfeiçoamento do avaliador de cardinalidade do SQL Server. Os comentários dos clientes mostram que, apesar de a maioria das consultas se beneficiarem da alteração ou permanecerem inalteradas, poucas mostram regressões em comparação ao avaliador de cardinalidade anterior. Para ajuste de desempenho e recomendações de teste, consulte [estimativa de cardinalidade &#40;SQL Server&#41;](../relational-databases/performance/cardinality-estimation-sql-server.md).  
   
  
###  <a name="Durability"></a> Durabilidade atrasada  
 O [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] apresenta a capacidade de reduzir a latência designando algumas ou todas as transações como duráveis atrasadas. Uma transação durável atrasada retorna o controle para o cliente antes de o registro do log de transação ser gravado no disco. A durabilidade pode ser controlada no nível do banco de dados, nível COMMIT ou nível de bloco ATOMIC.  
  
 Para obter mais informações, consulte o tópico [controlar a durabilidade da transação](../relational-databases/logs/control-transaction-durability.md).  
  
  
###  <a name="AlwaysOn"></a> Aprimoramentos do AlwaysOn  
 O [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] contém os seguintes aprimoramentos para Instâncias de Cluster de Failover AlwaysOn e Grupos de Disponibilidade AlwaysOn:  
  
-   Um Assistente para Adicionar Réplica do Azure simplifica a criação de soluções híbridas para grupos de disponibilidade AlwaysOn. Para obter mais informações, consulte [usar o Assistente para adicionar réplica Azure &#40;SQL Server&#41;](availability-groups/windows/use-the-add-azure-replica-wizard-sql-server.md).  
  
-   O número máximo de réplicas secundárias é aumentado de 4 para 8.  
  
-   Quando desconectadas da réplica primária ou durante a perda de quorum de cluster, as réplicas secundárias legíveis agora permanecem disponíveis para cargas de trabalho de leitura.  
  
-   Agora, as instâncias de cluster de failover (FCIs) podem usar Volumes Compartilhados Clusterizados (CSVs) como discos compartilhados de cluster. Para obter mais informações, consulte [sempre em Failover Cluster Instances](../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
-   Uma nova função de sistema, [sys. fn_hadr_is_primary_replica](/sql/relational-databases/system-functions/sys-fn-hadr-is-primary-replica-transact-sql)e um novo DMV, [sys.DM io_cluster_valid_path_names](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql), está disponível.  
  
-   As DMVs a seguir foram aprimoradas e agora retornam informações de FCI: [sys.DM hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql), [sys.DM hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql), e [sys.DM hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql).  
  
  
###  <a name="OIR"></a> Alternância de partição e indexação  
 As partições individuais de tabelas particionadas podem agora ser recriadas. Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
   
  
###  <a name="Lock"></a> Gerenciando a prioridade de bloqueio das operações Online  
 A opção `ONLINE = ON` agora contém uma opção `WAIT_AT_LOW_PRIORITY` que permite que você especifique por quanto tempo o processo de recriação deve aguardar os bloqueios necessários. A opção `WAIT_AT_LOW_PRIORITY` também permite configurar a conclusão dos processos de bloqueio relacionados à instrução REBUILD. Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql) e [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql). Informações sobre novos tipos de estados de bloqueio de solução de problemas está disponível em [sys.DM tran_locks &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql) e [sys.DM os_wait_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql).  
 
  
###  <a name="CCI"></a> Índices columnstore  
 Esses novos recursos estão disponíveis para índices columnstore:  
  
-   **Índices columnstore clusterizados**  
  
     Use um índice columnstore clusterizado para melhorar a compactação de dados e o desempenho de consultas para cargas de trabalho de data warehouse que basicamente executam carregamentos em massa e consultas somente leitura. Uma vez que o índice columnstore clusterizado é atualizável, a carga de trabalho pode executar muitas operações de inserção, atualização e exclusão. Para obter mais informações, consulte [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md) e [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md).  
  
-   **PLANO DE EXECUÇÃO**  
  
     SHOWPLAN exibe informações sobre índices columnstore. As propriedades **EstimatedExecutionMode** e **ActualExecutionMode** têm dois valores possíveis: **Batch** ou **Row**.  A propriedade **Storage** tem dois valores possíveis: **RowStore** e **ColumnStore**.  
  
-   **Compactação de dados de arquivamento**  
  
     ALTER INDEX … REBUILD tem uma nova opção de compactação de dados COLUMNSTORE_ARCHIVE que compacta ainda mais as partições especificadas de um índice columnstore. Use esse recurso para arquivamento ou em outras situações que exijam um tamanho menor de armazenamento de dados e possam dispensar mais tempo para armazenamento e recuperação. Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
   
  
###  <a name="Buffer"></a> Extensão do Pool de buffers  
 O [extensão do Pool de buffers](configure-windows/buffer-pool-extension.md) fornece a integração perfeita de unidades de estado sólido (SSD) como uma extensão de memória (NvRAM) de acesso aleatório não volátil para a [!INCLUDE[ssDE](../includes/ssde-md.md)] buffer pool para melhorar significativamente a taxa de transferência de e/s.  
   
  
###  <a name="Stats"></a> Estatísticas incrementais  
 CREATE STATISTICS e as instruções relacionadas de estatística agora permitem estatísticas por partição para serem criadas com a opção INCREMENTAL. As instruções relacionadas permitem ou reportam estatísticas incrementais. A sintaxe afetada inclui as opções UPDATE STATISTICS, sp_createstats, CREATE INDEX, ALTER INDEX, ALTER DATABASE SET, DATABASEPROPERTYEX, sys.databases e sys.stats. Para obter mais informações, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
  
###  <a name="RG"></a> Aprimoramentos do administrador de recursos para o controle de e/s física  
 O Administrador de Recursos permite que você especifique os limites de quantidade de CPU, E/S física e memória que as solicitações recebidas de aplicativos podem usar dentro de um pool de recursos. No [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], você pode usar as novas configurações do MIN_IOPS_PER_VOLUME e MAX_IOPS_PER_VOLUME para controlar as E/S físicas emitidas para threads de usuário para um determinado pool de recursos. Para obter mais informações, consulte [Resource Governor Resource Pool](../relational-databases/resource-governor/resource-governor-resource-pool.md) e [criar POOL de recursos &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql).  
  
 A configuração MAX_OUTSTANDING_IO_PER_VOLUME do ALTER RESOURCE GOVENOR define o máximo de operações de E/S pendentes por volume de disco. Você pode usar essa configuração para ajustar o controle de recursos de E/S para as características de E/S de um volume de disco e pode ser usada para limitar o número de E/S emitida no limite de instância do SQL Server. Para obter mais informações, veja [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql).  
  
  
###  <a name="OnlineEvent"></a> Classe de evento de operação de índice online  
 O relatório de andamento para a classe de evento da operação de índice online agora tem duas novas colunas de dados: **PartitionId** e **PartitionNumber**. Para obter mais informações, consulte [Progress Report: Online Index Operation Event Class](../relational-databases/event-classes/progress-report-online-index-operation-event-class.md).  
  
  
###  <a name="Compat"></a> Nível de compatibilidade do banco de dados  
 O nível de compatibilidade 90 não é válido no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Para obter mais informações, consulte [nível de compatibilidade do banco de dados ALTER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
##  <a name="TSQL"></a> Aprimoramentos de Transact-SQL  
  
### <a name="inline-specification-of-clustered-and-nonclustered"></a>Especificação embutida de CLUSTERED e NONCLUSTERED  
 A especificação embutida dos índices `CLUSTERED` e `NONCLUSTERED` é permitida agora para tabelas baseadas em disco. Criar uma tabela com índices embutidos é equivalente a emitir uma tabela de criação seguida por instruções `CREATE INDEX` correspondentes. Não há suporte para colunas incluídas e condições de filtro nos índices embutidos.  
  
### <a name="select--into"></a>SELECT … INTO  
 A instrução `SELECT … INTO` é aprimorada e agora pode funcionar em paralelo. O nível de compatibilidade do banco de dados deve ser pelo menos 110.  
  
### <a name="includetsqlincludestsql-mdmd-enhancements-for-in-memory-oltp"></a>[!INCLUDE[tsql](../includes/tsql-md.md)] Aprimoramentos para OLTP em Memória  
 Para obter informações sobre o [!INCLUDE[tsql](../includes/tsql-md.md)] alterações para oferecer suporte a OLTP na memória, consulte [suporte a Transact-SQL para OLTP na memória](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md).  
  
  
##  <a name="SystemTable"></a> Aprimoramentos do Modo de Exibição do Sistema  
  
### <a name="sysxmlindexes"></a>sys.xml_indexes  
 [sys. xml_indexes &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-xml-indexes-transact-sql) tem 3 colunas novas: `xml_index_type`, `xml_index_type_description`, e `path_id`.  
  
### <a name="sysdmexecqueryprofiles"></a>sys.dm_exec_query_profiles  
 [sys.DM exec_query_profiles &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql) monitora o progresso da consulta em tempo real enquanto uma consulta está em execução.  
  
### <a name="syscolumnstorerowgroups"></a>sys.column_store_row_groups  
 [column_store_row_groups &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql) fornece informações de índice columnstore clusterizado em uma base por segmento para ajudar o administrador a tomar decisões de gerenciamento de sistema.  
  
### <a name="sysdatabases"></a>sys.databases  
 [sys. Databases &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) tem 3 colunas novas: `is_auto_create_stats_incremental_on`, `is_query_store_on`, e `resource_pool_id`.  
  
### <a name="system-view-enhancements-for-in-memory-oltp"></a>Aprimoramentos de exibição do sistema para OLTP em Memória  
 Para obter informações sobre aprimoramentos da exibição do sistema para dar suporte a OLTP na memória, consulte [exibições do sistema, procedimentos armazenados, DMVs e tipos de espera para OLTP na memória](../../2014/database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md).  
   
  
##  <a name="Security"></a> Aprimoramentos de segurança  
  
### <a name="connect-any-database-permission"></a>Permissão CONNECT ANY DATABASE  
 Uma nova permissão de nível de servidor. Conceda **CONNECT ANY DATABASE** a um logon que deve se conectar a todos os bancos de dados que existem atualmente e a quaisquer novos bancos de dados que possam ser criados no futuro. Não concede nenhuma permissão em qualquer banco de dados além da conexão. Combinar com **SELECT ALL USER SECURABLES** ou `VIEW SERVER STATE` para permitir que um processo de auditoria exibir todos os dados ou todos os estados de banco de dados na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
### <a name="impersonate-any-login-permission"></a>Permissão IMPERSONATE ANY LOGIN  
 Uma nova permissão de nível de servidor. Quando concedida, permite que um processo de camada intermediária represente a conta de clientes que se conecta a ela, uma vez que ela se conecta aos bancos de dados. Quando negada, um logon com altos privilégios pode ser impedido de representar outros logons. Por exemplo, um logon com a permissão **CONTROL SERVER** pode ser impedido de representar outros logons.  
  
### <a name="select-all-user-securables-permission"></a>Permissão SELECT ALL USER SECURABLES  
 Uma nova permissão de nível de servidor. Quando concedida, um logon, como um auditor, pode exibir dados em todos os bancos de dados aos quais o usuário pode se conectar.  
  
  
##  <a name="Deployment"></a> Aprimoramentos de implantação  
### <a name="azure-vm"></a>VM do Azure
[Implantar um banco de dados do SQL Server para uma máquina Virtual Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) permite a implantação de um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] banco de dados para uma VM do Windows Azure.  

### <a name="refs"></a>ReFS
Agora há suporte para a implantação de bancos de dados ReFS.   
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
   

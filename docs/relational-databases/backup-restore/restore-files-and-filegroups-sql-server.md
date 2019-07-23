---
title: Restaurar arquivos e grupos de arquivos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restorefilesandfilegrps.general.f1
- sql13.swb.bselectfilegrpsfiles.f1
- sql13.swb.restorefilesandfilegrps.options.f1
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], restoring files and filegroups
- restoring [SQL Server], files
ms.assetid: 72603b21-3065-4b56-8b01-11b707911b05
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 81a832b4372dc2b35893c329d0b7ca909224fb9f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041512"
---
# <a name="restore-files-and-filegroups-sql-server"></a>Restaurar arquivos e grupos de arquivos (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como restaurar arquivos e grupos de arquivos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   [Segurança](#Security)  
  
-   **Para restaurar arquivos e grupos de arquivos usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O administrador do sistema que restaura os arquivos e grupos de arquivos deve ser a única pessoa que atualmente esteja usando o banco de dados a ser restaurado.  
  
-   RESTORE não é permitido em uma transação explícita ou implícita.  
  
-   No modelo de recuperação simples, o arquivo deve pertencer a um grupo de arquivos somente leitura.  
  
-   No modelo de recuperação completa ou bulk-logged, antes de poder restaurar arquivos, você deve fazer backup do log de transações ativas (conhecido como a parte final do log). Para obter mais informações, veja [Back Up a Transaction Log &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).  
  
-   Para restaurar um banco de dados criptografado, é necessário ter acesso ao certificado ou à chave assimétrica usada para criptografar o banco de dados. Sem o certificado ou a chave assimétrica, o banco de dados não pode ser restaurado. Como resultado, o certificado usado para criptografar a chave de criptografia do banco de dados deverá ser retido enquanto o backup for necessário. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Se o banco de dados que está sendo restaurado não existir, o usuário deverá ter permissões CREATE DATABASE para poder executar o comando RESTORE. Se o banco de dados existir, as permissões RESTORE usarão como padrão os membros das funções de servidor fixas **sysadmin** e **dbcreator** e o proprietário (**dbo**) do banco de dados (para a opção FROM DATABASE_SNAPSHOT, o banco de dados sempre existe).  
  
 As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-restore-files-and-filegroups"></a>Para restaurar arquivos e grupos de arquivos  
  
1.  Depois de se conectar à instância adequada do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore de servidores.  
  
2.  Expanda os **Bancos de dados**. Dependendo do banco de dados, selecione um banco de dados de usuário ou expanda os **Bancos de dados do sistema**e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Restaurar**.  
  
4.  Clique em **Arquivos e Grupos de Arquivos**, que abre a caixa de diálogo **Restaurar Arquivos e Grupos de Arquivos** .  
  
5.  Na página **Geral** , na caixa de listagem **Banco de dados de destino** , digite o banco de dados a ser restaurado. Você pode digitar um novo banco de dados ou escolher um banco de dados existente na lista suspensa. A lista inclui todos os bancos de dados do servidor, excluindo os bancos de dados do sistema **mestre** e **tempdb**.  
  
6.  Para especificar a origem e o local dos conjuntos de backup a serem restaurados, clique em uma das seguintes opções:  
  
    -   **Do Banco de Dados**  
  
         Digite um nome de banco de dados na caixa de listagem. Essa lista contém apenas os bancos de dados em que foi feito backup segundo o histórico de backups do **msdb** .  
  
    -   **Do Dispositivo**  
  
         Clique no botão Procurar. Na caixa de diálogo **Especificar dispositivos de backup** , selecione um dos tipos de dispositivos listados na caixa de listagem **Tipo de mídia de backup** . Para selecionar um ou mais dispositivos para a caixa de listagem **Mídia de backup** , clique em **Adicionar**.  
  
         Após adicionar os dispositivos desejados à caixa de listagem **Mídia de backup** , clique em **OK** para voltar à página **Geral** .  
  
7.  Na grade **Selecione os conjuntos de backup a serem restaurados** , selecione os backups a serem restaurados. Essa grade exibe os backups disponíveis para o local especificado. Por padrão, um plano de recuperação é sugerido. Para substituir o plano de recuperação sugerido, você pode alterar as seleções na grade. Todos os backups que dependem de um backup não selecionado serão desmarcados automaticamente.  
  
    |Título da coluna|Valores|  
    |-----------------|------------|  
    |**Restaurar**|As caixas de seleção selecionadas indicam os conjuntos de backup a serem restaurados.|  
    |**Nome**|O nome do conjunto de backup.|  
    |**Tipo de arquivo**|Especifica o tipo dos dados na no backup: **Dados**, **Log** ou **Dados de Fluxo de Arquivos**. Dados que são contidos em tabelas estão nos arquivos **Dados** . Dados de log de transações estão nos arquivos **Log** . Dados de BLOB (objeto binário grande) armazenados no sistema de arquivos estão localizados em arquivos de **Dados do Fluxo de Arquivos** .|  
    |**Tipo**|O tipo de backup realizado: **Total**, **Diferencial** ou **Log de Transações**.|  
    |**Servidor**|Nome da instância do Mecanismo de Banco de Dados que executou a operação de backup.|  
    |**Nome Lógico do Arquivo**|O nome lógico do arquivo.|  
    |**Backup de banco de dados**|Nome do banco de dados envolvido na operação de backup.|  
    |**Data de Início**|A data e hora de início da operação de backup, apresentadas na configuração regional do cliente.|  
    |**Data de Conclusão**|A data e hora da conclusão da operação de backup, apresentadas na configuração regional do cliente.|  
    |**Tamanho**|O tamanho do conjunto de backup em bytes.|  
    |**Nome do Usuário**|O nome do usuário que realizou a operação de backup.|  
  
8.  Para exibir ou selecionar as opções avançadas, clique em **Opções** em **Painel Selecionar uma página**.  
  
9. No painel **Opções de restauração** , você pode escolher uma das seguintes opções, de acordo com sua situação.  
  
     **Restaurar um grupo de arquivos**  
     Indica que um grupo de arquivos inteiro está sendo restaurado.  
  
     **Substituir o banco de dados existente**  
     Especifica que a operação de restauração deve substituir quaisquer bancos de dados existentes e seus arquivos relacionados, mesmo se já existirem outros bancos de dados ou arquivos com o mesmo nome.  
  
     Selecionar esta opção equivale ao uso da opção REPLACE em uma declaração RESTORE [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
     **Perguntar antes de restaurar cada backup**  
     Solicita sua confirmação antes de restaurar cada conjunto de backup.  
  
     Esta opção é particularmente útil quando você precisar trocar as fitas de conjuntos de mídia diferentes, tal como quando o servidor tiver um dispositivo de fita.  
  
     **Acesso restrito ao banco de dados restaurado**  
     Disponibiliza o banco de dados restaurado apenas para os membros do **db_owner**, **dbcreator**ou **sysadmin**.  
  
     Selecionar esta opção é como usar a opção RESTRICTED_USER na declaração RESTORE [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
10. Opcionalmente, você pode restaurar o banco de dados para um novo local, especificando um novo destino de restauração para cada arquivo na grade **Restaurar os arquivos de banco de dados como** .  
  
    |Título da coluna|Valores|  
    |-----------------|------------|  
    |**Nome do arquivo original**|O caminho completo do arquivo de backup de origem.|  
    |**Tipo de arquivo**|Especifica o tipo dos dados na no backup: **Dados**, **Log** ou **Dados de Fluxo de Arquivos**. Dados que são contidos em tabelas estão nos arquivos **Dados** . Dados de log de transações estão nos arquivos **Log** . Dados de BLOB (objeto binário grande) armazenados no sistema de arquivos estão localizados em arquivos de **Dados do Fluxo de Arquivos** .|  
    |**Restaurar Como**|O caminho completo do arquivo de banco de dados a ser restaurado. Para especificar um novo arquivo de restauração, clique na caixa de texto e edite o caminho sugerido e o nome do arquivo. Alterar o caminho ou o nome do arquivo na coluna **Restaurar Como** é equivalente ao uso da opção MOVE em uma declaração RESTORE [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
  
11. O painel **Estado de recuperação** determina o estado do banco de dados após a operação de restauração.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     **Leave the database ready for use by rolling back the uncommitted transactions. Additional transaction logs cannot be restored. (RESTORE WITH RECOVERY)**  
     Recovers the database. This is the default behavior. Choose this option only if you are restoring all of the necessary backups now. This option is equivalent to specifying WITH RECOVERY in a [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE statement.  
  
     **Leave the database non-operational, and don't roll back the uncommitted transactions. Additional transaction logs can be restored. (RESTORE WITH NORECOVERY)**  
     Leaves the database in the restoring state. To recover the database, you will need to perform another restore using the preceding RESTORE WITH RECOVERY option (see above). This option is equivalent to specifying WITH NORECOVERY in a [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE statement.  
  
     If you select this option, the **Preserve replication settings** option is unavailable.  
  
     **Leave the database in read-only mode. Roll back the uncommitted transactions, but save the rollback operation in a file so the recovery effects can be undone. (RESTORE WITH STANDBY)**  
     Leaves the database in a standby state. This option is equivalent to specifying WITH STANDBY in a [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE statement.  
  
     Choosing this option requires that you specify a standby file.  
  
     **Rollback undo file**  
     Specify a standby file name in the **Rollback undo file** text box. This option is required if you leave the database in read-only mode (RESTORE WITH STANDBY).  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-restore-files-and-filegroups"></a>Para restaurar arquivos e grupos de arquivos  
  
1.  Execute a instrução RESTORE DATABASE para restaurar o backup de arquivos e grupo de arquivos, especificando:  
  
    -   O nome do banco de dados a ser restaurado.  
  
    -   O dispositivo de backup do qual o backup de banco de dados completo será restaurado.  
  
    -   A cláusula FILE para cada arquivo a restaurar.  
  
    -   A cláusula FILEGROUP para cada grupo de arquivos a restaurar.  
  
    -   A cláusula NORECOVERY. Se os arquivos não foram modificados depois que o backup foi criado, especifique a cláusula RECOVERY.  
  
2.  Se os arquivos foram modificados depois que o backup de arquivo foi criado, execute a instrução RESTORE LOG para aplicar o backup de log de transações, especificando:  
  
    -   O nome do banco de dados ao qual o log de transações será aplicado.  
  
    -   O dispositivo de backup do qual o backup de log de transações será restaurado.  
  
    -   A cláusula NORECOVERY se você tiver outro backup de log de transações para aplicar depois do atual; caso contrário, especifique a cláusula RECOVERY.  
  
         Os backups de log de transações, se aplicados, devem cobrir o tempo quando foi feito o backup dos arquivos e grupos de arquivos até o final do log (a menos que sejam restaurados TODOS os arquivos de banco de dados).  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Este exemplo restaura os arquivos e grupos de arquivos para o banco de dados `MyDatabase` . Para restaurar o banco de dados para a hora atual, dois logs de transações são aplicados.  
  
```sql  
USE master;  
GO  
-- Restore the files and filesgroups for MyDatabase.  
RESTORE DATABASE MyDatabase  
   FILE = 'MyDatabase_data_1',  
   FILEGROUP = 'new_customers',  
   FILE = 'MyDatabase_data_2',  
   FILEGROUP = 'first_qtr_sales'  
   FROM MyDatabase_1  
   WITH NORECOVERY;  
GO  
-- Apply the first transaction log backup.  
RESTORE LOG MyDatabase  
   FROM MyDatabase_log1  
   WITH NORECOVERY;  
GO  
-- Apply the last transaction log backup.  
RESTORE LOG MyDatabase  
   FROM MyDatabase_log2  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [Fazer backup de arquivos e de grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)   
 [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  

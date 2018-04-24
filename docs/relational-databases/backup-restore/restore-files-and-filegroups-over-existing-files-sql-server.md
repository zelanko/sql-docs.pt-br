---
title: Restaurar arquivos e grupos de arquivos sobre arquivos existentes (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- restoring files [SQL Server], how-to topics
- restoring files [SQL Server], steps
- file restores [SQL Server], how-to topics
- filegroups [SQL Server], restoring
- restoring filegroups [SQL Server]
- overwriting filegroups
- overwriting files
ms.assetid: 517e07eb-9685-4b06-90af-b1cc496700b7
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c683a13b3a008e3fda5047daaea0db8778f8dcf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="restore-files-and-filegroups-over-existing-files-sql-server"></a>Restaurar arquivos e grupos de arquivos sobre arquivos existentes (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como restaurar arquivos e grupos de arquivos sobre arquivos existentes no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para restaurar arquivos e grupos de arquivos sobre arquivos existentes usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O administrador do sistema que restaura os arquivos e grupos de arquivos deve ser a única pessoa usando atualmente o banco de dados a ser restaurado.  
  
-   RESTORE não é permitido em uma transação explícita ou implícita.  
  
-   No modelo de recuperação completa ou bulk-logged, antes de poder restaurar arquivos, você deve fazer backup do log de transações ativas (conhecido como a parte final do log). Para obter mais informações, veja [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)).  
  
-   Para restaurar um banco de dados criptografado, é necessário ter acesso ao certificado ou à chave assimétrica usada para criptografar o banco de dados. Sem o certificado ou a chave assimétrica, o banco de dados não pode ser restaurado. Como resultado, o certificado usado para criptografar a chave de criptografia do banco de dados deverá ser retido enquanto o backup for necessário. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Se o banco de dados que está sendo restaurado não existir, o usuário deverá ter permissões CREATE DATABASE para poder executar o comando RESTORE. Se o banco de dados existir, as permissões RESTORE usarão como padrão os membros das funções de servidor fixas **sysadmin** e **dbcreator** e o proprietário (**dbo**) do banco de dados (para a opção FROM DATABASE_SNAPSHOT, o banco de dados sempre existe).  
  
 As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-restore-files-and-filegroups-over-existing-files"></a>Para restaurar arquivos e grupos de arquivos sobre arquivos existentes  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], expanda essa instância e expanda **Bancos de Dados**.  
  
2.  Clique com o botão direito do mouse no banco de dados desejado, aponte para **Tarefas**e para **Restaurar**, e clique em **Arquivos e Grupos de Arquivos**.  
  
3.  Na página **Geral** , na caixa de listagem **Banco de dados de destino** , digite o banco de dados a ser restaurado. Você pode digitar um novo banco de dados ou escolher um banco de dados existente na lista suspensa. A lista inclui todos os bancos de dados do servidor, excluindo os bancos de dados do sistema **mestre** e **tempdb**.  
  
4.  Para especificar a origem e o local dos conjuntos de backup a serem restaurados, clique em uma das seguintes opções:  
  
    -   **Do Banco de Dados**  
  
         Digite um nome de banco de dados na caixa de listagem. Essa lista contém apenas os bancos de dados em que foi feito backup segundo o histórico de backups do **msdb** .  
  
    -   **Do Dispositivo**  
  
         Clique no botão Procurar. Na caixa de diálogo **Especificar dispositivos de backup** , selecione um dos tipos de dispositivos listados na caixa de listagem **Tipo de mídia de backup** . Para selecionar um ou mais dispositivos para a caixa de listagem **Mídia de backup** , clique em **Adicionar**.  
  
         Após adicionar os dispositivos desejados à caixa de listagem **Mídia de backup** , clique em **OK** para voltar à página **Geral** .  
  
5.  Na grade **Selecione os conjuntos de backup a serem restaurados** , selecione os backups a serem restaurados. Essa grade exibe os backups disponíveis para o local especificado. Por padrão, um plano de recuperação é sugerido. Para substituir o plano de recuperação sugerido, você pode alterar as seleções na grade. Todos os backups que dependem de um backup não selecionado serão desmarcados automaticamente.  
  
    |Título da coluna|Valores|  
    |-----------------|------------|  
    |**Restaurar**|As caixas de seleção selecionadas indicam os conjuntos de backup a serem restaurados.|  
    |**Nome**|O nome do conjunto de backup.|  
    |**Tipo de arquivo**|Especifica o tipo de dados no backup: **Dados**, **Log**ou **Filestream Data**. Dados que são contidos em tabelas estão nos arquivos **Dados** . Dados de log de transações estão nos arquivos **Log** . Dados de BLOB (objeto binário grande) armazenados no sistema de arquivos estão localizados em arquivos de **Dados do Fluxo de Arquivos** .|  
    |**Tipo**|Tipo de backup realizado: **Completo**, **Diferencial**ou **Log de Transações**.|  
    |**Servidor**|Nome da instância do Mecanismo de Banco de Dados que executou a operação de backup.|  
    |**Nome Lógico do Arquivo**|O nome lógico do arquivo.|  
    |**Backup de banco de dados**|Nome do banco de dados envolvido na operação de backup.|  
    |**Data de Início**|A data e hora de início da operação de backup, apresentadas na configuração regional do cliente.|  
    |**Data de Conclusão**|A data e hora da conclusão da operação de backup, apresentadas na configuração regional do cliente.|  
    |**Tamanho**|O tamanho do conjunto de backup em bytes.|  
    |**Nome do Usuário**|O nome do usuário que realizou a operação de backup.|  
  
6.  No painel **Selecionar uma página** , clique na página **Opções** .  
  
7.  No painel **Opções de restauração** , selecione **Substituir o banco de dados existente (WITH REPLACE)**. A operação de restauração substitui os bancos de dados existentes e seus arquivos relacionados, mesmo se já existirem outros bancos de dados ou arquivos com o mesmo nome.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-restore-files-and-filegroups-over-existing-files"></a>Para restaurar arquivos e grupos de arquivos sobre arquivos existentes  
  
1.  Execute a instrução RESTORE DATABASE para restaurar o backup de arquivos e grupo de arquivos, especificando:  
  
    -   O nome do banco de dados a ser restaurado.  
  
    -   O dispositivo de backup do qual o backup de banco de dados completo será restaurado.  
  
    -   A cláusula FILE para cada arquivo a restaurar.  
  
    -   A cláusula FILEGROUP para cada grupo de arquivos a restaurar.  
  
    -   A opção de REPLACE para especificar que cada arquivo pode ser restaurado de arquivos existentes do mesmo nome e local.  
  
        > [!CAUTION]  
        >  Use a opção de REPLACE cautelosamente. Para obter mais informações, consulte .  
  
    -   A opção de NORECOVERY. Se os arquivos não foram modificados depois que o backup foi criado, especifique a cláusula RECOVERY.  
  
2.  Se os arquivos foram modificados depois que o backup de arquivo foi criado, execute a instrução RESTORE LOG para aplicar o backup de log de transações, especificando:  
  
    -   O nome do banco de dados ao qual o log de transações será aplicado.  
  
    -   O dispositivo de backup do qual o backup de log de transações será restaurado.  
  
    -   A cláusula NORECOVERY se você tiver outro backup de log de transações para aplicar depois do atual; caso contrário, especifique a cláusula RECOVERY.  
  
         Os backups de log de transações, se aplicados, devem cobrir a hora em que os backups dos arquivos e grupos de arquivos foram feitos.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo seguinte restaura os arquivos e grupos de arquivos para o banco de dados `MyNwind` e substitui qualquer arquivo existente do mesmo nome. Também serão aplicados dois logs de transações para restaurar o banco de dados a hora atual.  
  
```sql  
USE master;  
GO  
-- Restore the files and filesgroups for MyNwind.  
RESTORE DATABASE MyNwind  
   FILE = 'MyNwind_data_1',  
   FILEGROUP = 'new_customers',  
   FILE = 'MyNwind_data_2',  
   FILEGROUP = 'first_qtr_sales'  
   FROM MyNwind_1  
   WITH NORECOVERY,  
   REPLACE;  
GO  
-- Apply the first transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log1  
   WITH NORECOVERY;  
GO  
-- Apply the last transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log2  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)   
 [Copiar bancos de dados com backup e restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)  
  
  

---
title: Restaurar arquivos para um novo local (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring files [SQL Server], how-to topics
- restoring databases [SQL Server], moving
- restoring files [SQL Server], steps
- file restores [SQL Server], how-to topics
- filegroups [SQL Server], restoring
- restoring filegroups [SQL Server]
ms.assetid: b4f4791d-646e-4632-9980-baae9cb1aade
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5d3d3ddc6d14414344e847249cb337e9f6a0d5c2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68041523"
---
# <a name="restore-files-to-a-new-location-sql-server"></a>Restaurar arquivos para um novo local (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como restaurar arquivos para um novo local no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para restaurar arquivos para um novo local, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O administrador do sistema que restaura os arquivos deve ser a única pessoa que no momento esteja usando o banco de dados a ser restaurado.  
  
-   RESTORE não é permitido em uma transação explícita ou implícita.  
  
-   No modelo de recuperação completa ou bulk-logged, antes de poder restaurar arquivos, você deve fazer backup do log de transações ativas (conhecido como a parte final do log). Para obter mais informações, veja [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)).  
  
-   Para restaurar um banco de dados criptografado, é necessário ter acesso ao certificado ou à chave assimétrica usada para criptografar o banco de dados. Sem o certificado ou a chave assimétrica, o banco de dados não pode ser restaurado. Como resultado, o certificado usado para criptografar a chave de criptografia do banco de dados deverá ser retido enquanto o backup for necessário. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Se o banco de dados que está sendo restaurado não existir, o usuário deverá ter permissões CREATE DATABASE para poder executar o comando RESTORE. Se o banco de dados existir, as permissões RESTORE usarão como padrão os membros das funções de servidor fixas **sysadmin** e **dbcreator** e o proprietário (**dbo**) do banco de dados (para a opção FROM DATABASE_SNAPSHOT, o banco de dados sempre existe).  
  
 As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-restore-files-to-a-new-location"></a>Para restaurar arquivos para um novo local  
  
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
    |**Nome de usuário**|O nome do usuário que realizou a operação de backup.|  
  
6.  No painel **Selecionar uma página** , clique na página **Opções** .  
  
7.  Na grade **Restaurar os arquivos de banco de dados como** , especifique um novo local para o arquivo ou arquivos que você quer mover.  
  
    |Título da coluna|Valores|  
    |-----------------|------------|  
    |**Nome do arquivo original**|O caminho completo do arquivo de backup de origem.|  
    |**Tipo de arquivo**|Especifica o tipo de dados no backup: **Dados**, **Log**ou **Filestream Data**. Dados que são contidos em tabelas estão nos arquivos **Dados** . Dados de log de transações estão nos arquivos **Log** . Dados de BLOB (objeto binário grande) armazenados no sistema de arquivos estão localizados em arquivos de **Dados do Fluxo de Arquivos** .|  
    |**Restaurar Como**|O caminho completo do arquivo de banco de dados a ser restaurado. Para especificar um novo arquivo de restauração, clique na caixa de texto e edite o caminho sugerido e o nome do arquivo. Alterar o caminho ou o nome do arquivo na coluna **Restaurar Como** é equivalente ao uso da opção MOVE em uma declaração RESTORE [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-restore-files-to-a-new-location"></a>Para restaurar arquivos para um novo local  
  
1.  Opcionalmente, execute a instrução RESTORE FILELISTONLY para determinar o número e os nomes dos arquivos no backup de banco de dados completo.  
  
2.  Execute a instrução RESTORE DATABASE para restaurar o backup de banco de dados completo, especificando:  
  
    -   O nome do banco de dados a ser restaurado.  
  
    -   O dispositivo de backup do qual o backup de banco de dados completo será restaurado.  
  
    -   A cláusula MOVE para cada arquivo a ser restaurado em um no local  
  
    -   A cláusula NORECOVERY.  
  
3.  Se os arquivos foram modificados depois que o backup de arquivo foi criado, execute a instrução RESTORE LOG para aplicar o backup de log de transações, especificando:  
  
    -   O nome do banco de dados ao qual o log de transações será aplicado.  
  
    -   O dispositivo de backup do qual o backup de log de transações será restaurado.  
  
    -   A cláusula NORECOVERY se você tiver outro backup de log de transações para aplicar depois do atual; caso contrário, especifique a cláusula RECOVERY.  
  
         Os backups de log de transações, se aplicados, devem cobrir a hora em que os backups dos arquivos e grupos de arquivos foram feitos.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Esse exemplo restaura dois dos arquivos para o banco de dados `MyNwind` que ficavam originalmente localizados no Drive C em novos locais no Drive D. Dois logs de transações também serão aplicados para restaurar o banco de dados para a hora atual. A instrução `RESTORE FILELISTONLY` é usada para determinar o número e os nomes lógicos e físicos dos arquivos no banco de dados que está sendo restaurado.  
  
```sql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
RESTORE FILELISTONLY  
   FROM MyNwind_1;  
-- Restore the files for MyNwind.  
RESTORE DATABASE MyNwind  
   FROM MyNwind_1  
   WITH NORECOVERY,  
   MOVE 'MyNwind_data_1' TO 'D:\MyData\MyNwind_data_1.mdf',   
   MOVE 'MyNwind_data_2' TO 'D:\MyData\MyNwind_data_2.ndf';  
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
 [Copiar bancos de dados com backup e restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
  

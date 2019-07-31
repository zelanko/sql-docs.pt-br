---
title: Restaurar um backup diferencial do banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full differential backups [SQL Server]
- restoring databases [SQL Server], full differential backups
- database backups [SQL Server], full differential backups
- database restores [SQL Server], full differential backups
- backing up databases [SQL Server], full differential backups
ms.assetid: 0dd971a4-ee38-4dd3-9f30-ef77fc58dd11
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 14e12715c3722fe3278bf535b50bc749539d57ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937502"
---
# <a name="restore-a-differential-database-backup-sql-server"></a>Restaurar um backup diferencial de banco de dados (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como restaurar um backup de banco de dados diferencial no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para restaurar um backup de banco de dados diferencial usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   RESTORE não é permitido em uma transação explícita ou implícita.  
  
-   Os backups criados por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser restaurados em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], é possível restaurar um banco de dados de usuário de um backup de banco de dados criado por meio do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou de uma versão posterior.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   No modelo de recuperação completa ou bulk-logged, antes de poder restaurar um banco de dados, é necessário fazer backup do log de transações ativas (conhecido como a parte final do log). Para obter mais informações, veja [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Se o banco de dados que está sendo restaurado não existir, o usuário deverá ter permissões CREATE DATABASE para poder executar o comando RESTORE. Se o banco de dados existir, as permissões RESTORE usarão como padrão os membros das funções de servidor fixas **sysadmin** e **dbcreator** e o proprietário (**dbo**) do banco de dados (para a opção FROM DATABASE_SNAPSHOT, o banco de dados sempre existe).  
  
 As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-restore-a-differential-database-backup"></a>Para restaurar um backup de banco de dados diferencial  
  
1.  Depois de se conectar à instância adequada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore de servidores.  
  
2.  Expanda os **Bancos de dados**. Dependendo do banco de dados, selecione um banco de dados de usuário ou expanda os **Bancos de dados do sistema**e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**, aponte para **Restaurar**e clique em **Banco de Dados**.  
  
4.  Na página **Geral** , use a seção **Origem** para especificar a origem e o local dos conjuntos de backup a serem restaurados. Selecione uma das opções a seguir:  
  
    -   **Backup de banco de dados**  
  
         Selecione o banco de dados a ser restaurado na lista suspensa. A lista contém apenas os bancos de dados dos quais foi feito um backup de acordo com o histórico de backup do **msdb** .  
  
    > [!NOTE]  
    >  Se o backup foi obtido de um servidor diferente, o servidor de destino não terá informações de histórico de backup para o banco de dados especificado. Nesse caso, selecione **Dispositivo** para especificar manualmente o arquivo ou o dispositivo a ser restaurado.  
  
    -   **Dispositivo**  
  
         Clique no botão Procurar ( **...** ) para abrir a caixa de diálogo **Selecione dispositivos de backup** . Na caixa **Tipo de mídia de backup** , selecione um dos tipos de dispositivo listados. Para selecionar um ou mais dispositivos da caixa **Mídia de backup** , clique em **Adicionar**.  
  
         Após adicionar os dispositivos desejados à caixa de listagem **Mídia de backup** , clique em **OK** para voltar à página **Geral** .  
  
         Na caixa de listagem **Fonte: Dispositivo: Banco de Dados**, selecione o nome do banco de dados que deve ser restaurado.  
  
         **Observação** Essa lista estará disponível apenas quando **Dispositivo** for selecionado. Apenas os bancos de dados que têm backups no dispositivo selecionado estarão disponíveis.  
  
5.  Na seção **Destino** , a caixa **Banco de Dados** é preenchida automaticamente com o nome do banco de dados a ser restaurado. Para alterar o nome do banco de dados, digite o novo nome na caixa **Banco de Dados** .  
  
    > [!NOTE]  
    >  Para interromper a restauração em um ponto específico, clique em **Linha do Tempo** para acessar a caixa de diálogo **Linha do Tempo de Backup** . Para obter ajuda na interrupção de uma restauração de banco de dados em um ponto específico, veja [Restaurar um Banco de Dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
6.  Na grade **Conjuntos de backup a serem restaurados** , selecione os backups que deseja restaurar através do backup diferencial.  
  
     Para obter informações sobre as colunas da grade **Selecionar os conjuntos de backup a serem restaurados**, veja [Restaurar banco de dados &#40;Página Geral&#41;](../../relational-databases/backup-restore/restore-database-general-page.md).  
  
7.  Na página **Opções** , no painel **Opções de restauração** , você pode selecionar qualquer uma das seguintes opções, de acordo com sua situação:  
  
    -   **Substituir o banco de dados existente (WITH REPLACE)**  
  
    -   **Preservar as configurações de replicação (WITH KEEP_REPLICATION)**  
  
    -   **Perguntar antes de restaurar cada backup**  
  
    -   **Acesso restrito ao banco de dados restaurado (WITH RESTRICTED_USER)**  
  
     Para obter mais informações sobre essas opções, veja [Restaurar banco de dados &#40;Página Opções&#41;](../../relational-databases/backup-restore/restore-database-options-page.md).  
  
8.  Selecione uma opção para a caixa **Estado de recuperação** . Essa caixa determina o estado do banco de dados após a operação de restauração.  
  
    -   **RESTORE WITH RECOVERY** é o comportamento padrão que deixa o banco de dados pronto para uso revertendo as transações não confirmadas. Os logs de transações adicionais não podem ser restaurados. Selecione essa opção se você estiver restaurando todos os backups necessários agora.  
  
    -   **RESTORE WITH NORECOVERY** deixa o banco de dados não operacional e não reverte as transações não confirmadas. Os logs de transações adicionais podem ser restaurados. Só é possível usar o banco de dados depois que ele é recuperado.  
  
    -   **RESTORE WITH STANDBY** deixa o banco de dados no modo somente leitura. Ele desfaz as transações não confirmadas, mas salva as ações de desfazer em um arquivo em espera para que os efeitos da recuperação possam ser revertidos.  
  
     Para ver as descrições das opções, consulte [Restaurar banco de dados &#40;Página Opções&#41;](../../relational-databases/backup-restore/restore-database-options-page.md).  
  
9. As operações de restauração falharão se houver conexões ativas com o banco de dados. Marque a opção **Fechar conexões existentes** para assegurar que todas as conexões ativas entre o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e o banco de dados sejam fechadas.  
  
10. Selecione **Perguntar antes de restaurar cada backup** para que você seja solicitado entre cada operação de restauração. Isso normalmente só é necessário quando o banco de dados é grande e você deseja monitorar o status da operação de restauração.  
  
11. Se desejar, use a página **Arquivos** para restaurar o banco de dados em um novo local. Para obter ajuda para mover um banco de dados, consulte [Restaurar um banco de dados para um novo local &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md).  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-restore-a-differential-database-backup"></a>Para restaurar um backup de banco de dados diferencial  
  
1.  Execute uma instrução RESTORE DATABASE, especificando a cláusula NORECOVERY, para restaurar o backup de banco de dados completo que vem antes do backup de banco de dados diferencial. Para obter mais informações, confira [Como restaurar um backup completo](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md).  
  
2.  Execute a instrução RESTORE DATABASE para restaurar o backup de banco de dados diferencial, especificando:  
  
    -   O nome do banco de dados para o qual o backup de banco de dados diferencial é aplicado.  
  
    -   O dispositivo de backup em que o backup de banco de dados diferencial é restaurado.  
  
    -   A cláusula NORECOVERY, se você tiver backups de log de transações para aplicar depois de o backup de banco de dados diferencial ser restaurado. Caso contrário, especifique a cláusula RECOVERY.  
  
3.  Com o modelo de recuperação completa ou bulk-logged, a restauração de um backup de banco de dados diferencial restaura o banco de dados até o ponto que o backup de banco de dados diferencial foi concluído. Para recuperar até o ponto da falha, você deve aplicar todos os backups de log de transações criados depois de o último backup de banco de dados diferencial ter sido criado. Para obter mais informações, veja [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
  
#### <a name="a-restoring-a-differential-database-backup"></a>A. Restaurando um backup de banco de dados diferencial  
 Este exemplo restaura um banco de dados e um backup de banco de dados diferencial do banco de dados `MyAdvWorks` .  
  
```sql  
-- Assume the database is lost, and restore full database,   
-- specifying the original full database backup and NORECOVERY,   
-- which allows subsequent restore operations to proceed.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH NORECOVERY;  
GO  
-- Now restore the differential database backup, the second backup on   
-- the MyAdvWorks_1 backup device.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH FILE = 2,  
   RECOVERY;  
GO  
```  
  
#### <a name="b-restoring-a-database-differential-database-and-transaction-log-backup"></a>B. Restaurando um backup de banco de dados, de banco de dados diferencial e de log de transações  
 Este exemplo restaura um banco de dados, um backup de banco de dados diferencial e um backup de log de transações do banco de dados `MyAdvWorks` .  
  
```sql  
-- Assume the database is lost at this point. Now restore the full   
-- database. Specify the original full database backup and NORECOVERY.  
-- NORECOVERY allows subsequent restore operations to proceed.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH NORECOVERY;  
GO  
-- Now restore the differential database backup, the second backup on   
-- the MyAdvWorks_1 backup device.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH FILE = 2,  
   NORECOVERY;  
GO  
-- Now restore each transaction log backup created after  
-- the differential database backup.  
RESTORE LOG MyAdvWorks  
   FROM MyAdvWorks_log1  
   WITH NORECOVERY;  
GO  
RESTORE LOG MyAdvWorks  
   FROM MyAdvWorks_log2  
   WITH RECOVERY;  
GO  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  

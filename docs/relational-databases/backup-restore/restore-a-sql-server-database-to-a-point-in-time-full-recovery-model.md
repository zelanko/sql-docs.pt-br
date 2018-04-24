---
title: Restaurar um banco de dados do SQL Server até um ponto determinado (modelo de recuperação completa) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
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
- STOPAT clause [RESTORE LOG statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
ms.assetid: 3a5daefd-08a8-4565-b54f-28ad01a47d32
caps.latest.revision: 50
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 530f2d0d47c2ef429bd284bd52af83117b4db423
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="restore-a-sql-server-database-to-a-point-in-time-full-recovery-model"></a>Restaurar um banco de dados do SQL Server até um ponto determinado (modelo de recuperação completa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como restaurar um banco de dados em um determinado ponto no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Este tópico é relevante apenas para os bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usam o modelo de recuperação completa ou bulk-logged.  
  
> [!IMPORTANT]  
>  No modelo de recuperação bulk-logged, se um backup de log contiver alterações bulk-logged, a recuperação pontual não será possível para um ponto dentro desse backup. O banco de dados deve ser recuperado até o fim do backup do log de transações.  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para restaurar um banco de dados do SQL Server em um momento determinado usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Use STANDBY para localizar um momento determinado desconhecido.  
  
-   Especificar com antecedência o momento determinado em uma sequência de restauração  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Se o banco de dados que está sendo restaurado não existir, o usuário deverá ter permissões CREATE DATABASE para poder executar o comando RESTORE. Se o banco de dados existir, as permissões RESTORE usarão como padrão os membros das funções de servidor fixas **sysadmin** e **dbcreator** e o proprietário (**dbo**) do banco de dados (para a opção FROM DATABASE_SNAPSHOT, o banco de dados sempre existe).  
  
 As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para restaurar um banco de dados para um momento determinado**  
  
1.  No Pesquisador de Objetos, conecte-se à instância adequada do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda a árvore de servidores.  
  
2.  Expanda os **Bancos de dados**. Dependendo do banco de dados, selecione um banco de dados de usuário ou expanda os **Bancos de dados do sistema**e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**, aponte para **Restaurar**e clique em **Banco de Dados**.  
  
4.  Na página **Geral** , use a seção **Origem** para especificar a origem e o local dos conjuntos de backup a serem restaurados. Selecione uma das opções a seguir:  
  
    -   **Backup de banco de dados**  
  
         Selecione o banco de dados a ser restaurado na lista suspensa. A lista contém apenas os bancos de dados dos quais foi feito um backup de acordo com o histórico de backup do **msdb** .  
  
    > [!NOTE]  
    >  Se o backup foi obtido de um servidor diferente, o servidor de destino não terá informações de histórico de backup para o banco de dados especificado. Nesse caso, selecione **Dispositivo** para especificar manualmente o arquivo ou o dispositivo a ser restaurado.  
  
    -   **Dispositivo**  
  
         Clique no botão Procurar (**...**) para abrir a caixa de diálogo **Selecione dispositivos de backup** . Na caixa **Tipo de mídia de backup** , selecione um dos tipos de dispositivo listados. Para selecionar um ou mais dispositivos da caixa **Mídia de backup** , clique em **Adicionar**.  
  
         Após adicionar os dispositivos desejados à caixa de listagem **Mídia de backup** , clique em **OK** para voltar à página **Geral** .  
  
         Na caixa de listagem **Origem: Dispositivo: Banco de Dados** , selecione o nome do banco de dados que deve ser restaurado.  
  
         **Observação** Essa lista estará disponível apenas quando **Dispositivo** for selecionado. Apenas os bancos de dados que têm backups no dispositivo selecionado estarão disponíveis.  
  
5.  Na seção **Destino** , a caixa **Banco de Dados** é preenchida automaticamente com o nome do banco de dados a ser restaurado. Para alterar o nome do banco de dados, digite o novo nome na caixa **Banco de Dados** .  
  
6.  Clique em **Linha do Tempo** para acessar a caixa de diálogo **Linha do Tempo de Backup** .  
  
7.  Na caixa de diálogo **Restaurar para** , clique em **Data e hora específicas**.  
  
8.  Use as caixas **Data** e **Hora** ou a barra de controle deslizante para especificar uma data específica e hora em que a restauração deve parar. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Use a caixa **Intervalo da Linha do Tempo** para alterar a quantidade de tempo exibida na linha do tempo.  
  
9. Depois que você especificar um momento determinado, o orientador de recuperação de banco de dados garantirá que apenas os backups necessários para restaurar até esse momento determinado sejam selecionados na coluna **Restaurar** da grade **Conjuntos de backup a serem restaurados** . Esses backups selecionados compõem o plano de restauração recomendado para a sua restauração pontual. Você deve usar apenas os backups selecionados para sua operação de restauração pontual.  
  
     Para obter informações sobre as colunas da grade **Conjuntos de backup a serem restaurados** , veja [Restaurar banco de dados &#40;página Geral&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)). Para obter informações sobre o Orientador de Recuperação de Banco de Dados, confira [Visão geral da restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
10. Na página **Opções** , no painel **Opções de restauração** , você pode selecionar qualquer uma das seguintes opções, de acordo com sua situação:  
  
    -   **Substituir o banco de dados existente (WITH REPLACE)**  
  
    -   **Preservar as configurações de replicação (WITH KEEP_REPLICATION)**  
  
    -   **Acesso restrito ao banco de dados restaurado (WITH RESTRICTED_USER)**  
  
     Para obter mais informações sobre essas opções, veja [Restaurar banco de dados &#40;Página Opções&#41;](../../relational-databases/backup-restore/restore-database-options-page.md).  
  
11. Selecione uma opção para a caixa **Estado de recuperação** . Essa caixa determina o estado do banco de dados após a operação de restauração.  
  
    -   **RESTORE WITH RECOVERY** é o comportamento padrão que deixa o banco de dados pronto para uso revertendo as transações não confirmadas. Os logs de transações adicionais não podem ser restaurados. Selecione essa opção se você estiver restaurando todos os backups necessários agora.  
  
    -   **RESTORE WITH NORECOVERY** deixa o banco de dados não operacional e não reverte as transações não confirmadas. Os logs de transações adicionais podem ser restaurados. Só é possível usar o banco de dados depois que ele é recuperado.  
  
    -   **RESTORE WITH STANDBY** deixa o banco de dados no modo somente leitura. Ele desfaz as transações não confirmadas, mas salva as ações de desfazer em um arquivo em espera para que os efeitos da recuperação possam ser revertidos.  
  
     Para ver as descrições das opções, consulte [Restaurar banco de dados &#40;Página Opções&#41;](../../relational-databases/backup-restore/restore-database-options-page.md).  
  
12. **Fazer backup da parte final do log antes da restauração** será selecionada se for necessário para o momento determinado que você selecionou. Você não precisa modificar essa configuração, mas poderá escolher o backup da parte final do log até mesmo se não for necessário.  
  
13. As operações de restauração poderão falhar se houver conexões ativas com o banco de dados. Marque a opção **Fechar conexões existentes** para assegurar que todas as conexões ativas entre o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e o banco de dados sejam fechadas. Essa caixa de seleção define o banco de dados no modo de usuário único antes de executar as operações de restauração e define o banco de dados no modo de vários usuários ao concluir.  
  
14. Selecione **Perguntar antes de restaurar cada backup** para que você seja solicitado entre cada operação de restauração. Isso normalmente só é necessário quando o banco de dados é grande e você deseja monitorar o status da operação de restauração.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Before you begin**  
  
 Um momento especificado sempre é restaurado a partir de um backup de log. Em cada instrução RESTORE LOG da sequência de restauração, especifique a transação ou o tempo de destino em uma cláusula STOPAT idêntica. Como um pré-requisito para uma restauração pontual, você deve restaurar primeiro um backup de banco de dados completo cujo ponto de extremidade seja anterior ao tempo de recuperação designado. Esse backup de banco de dados completo pode ser anterior ao backup de banco de dados completo mais recente desde que você depois restaure todos os backups de log subsequentes, até o backup de log que contém o tempo determinado.  
  
 Para ajudar a identificar qual backup de banco de dados restaurar, uma alternativa é especificar a cláusula WITH STOPAT em uma instrução RESTORE DATABASE para gerar um erro se um backup de dados for muito recente para o tempo designado especificado. O backup de dados completo será sempre restaurado, mesmo que ele contenha o tempo de destino.  
  
 **Sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] básica**  
  
 RESTORE LOG *database_name* FROM <backup_device> WITH STOPAT **=***time***,** RECOVERY…  
  
 O ponto de recuperação é a mais recente confirmação de transação ocorrida até o valor **datetime** especificado pela *hora*.  
  
 Para restaurar apenas as modificações feitas antes de um momento determinado, especifique WITH STOPAT **=** *hora* para cada backup restaurado. Isso garante que você não ultrapassará o tempo de destino.  
  
 **Para restaurar um banco de dados para um momento determinado**  
  
> [!NOTE]  
>  Para obter um exemplo desse procedimento, veja [Exemplo (Transact-SQL)](#TsqlExample), mais adiante nesta seção.  
  
1.  Conecte-se à instância de servidor na qual você deseja restaurar o banco de dados.  
  
2.  Execute a instrução RESTORE DATABASE usando a opção NORECOVERY.  
  
    > [!NOTE]  
    >  Se uma sequência de restauração parcial excluir qualquer grupo de arquivos [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md) , não haverá suporte para a restauração pontual. Você pode forçar a sequência de restauração a continuar. Contudo, os grupos de arquivos FILESTREAM omitidos de sua instrução RESTORE nunca poderão ser restaurados. Para forçar uma restauração pontual, especifique a opção CONTINUE_AFTER_ERROR juntamente com a opção STOPAT, STOPATMARK ou STOPBEFOREMARK, que você também deve especificar nas instruções RESTORE LOG subsequentes. Se você especificar CONTINUE_AFTER_ERROR, a sequência de restauração parcial terá êxito e o grupo de arquivos FILESTREAM se tornará irrecuperável.  
  
3.  Restaurar o último backup de banco de dados diferencial e, se houver, sem recuperar o banco de dados (RESTORE DATABASE *database_name* FROM *backup_device* WITH NORECOVERY).  
  
4.  Aplique cada backup de log de transações na mesma sequência em que eles foram criados, especificando a hora que você pretende parar o log de restauração (RESTORE DATABASE *database_name* FROM <backup_device> WITH STOPAT**=***time***,** RECOVERY).  
  
    > [!NOTE]  
    >  As opções RECOVERY e STOPAT. Se o backup de log de transações não contiver o tempo solicitado (por exemplo, se o tempo especificado estiver além do tempo coberto pelo log de transações), um aviso será gerado e o banco de dados permanecerá sem-recuperação.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir restaura um banco de dados para seu estado de `12:00 AM` em `April 15, 2020` e mostra uma operação de restauração que envolve vários backups de log. No dispositivo de backup, `AdventureWorksBackups`, o backup de banco de dados completo a ser restaurado é o terceiro conjunto de backup no dispositivo (`FILE = 3`), o primeiro backup de log é o quarto conjunto de backup (`FILE = 4`), e o segundo backup de log é o quinto conjunto de backup (`FILE = 5`).  
  
> [!IMPORTANT]  
>  O banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] usa o modelo de recuperação simples. Para permitir backups de log, antes de fazer um backup de banco de dados completo, o banco de dados foi definido para usar o modelo de recuperação completa, usando `ALTER DATABASE AdventureWorks SET RECOVERY FULL`.  
  
```  
RESTORE DATABASE AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=3, NORECOVERY;  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=4, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=5, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
RESTORE DATABASE AdventureWorks WITH RECOVERY;   
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Restaurar um banco de dados até o ponto de falha no modelo de recuperação completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar um banco de dados para uma transação marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Recuperar para um número de sequência de log &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ToPointInTime%2A> (SMO)  
  
## <a name="see-also"></a>Consulte Também  
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
  

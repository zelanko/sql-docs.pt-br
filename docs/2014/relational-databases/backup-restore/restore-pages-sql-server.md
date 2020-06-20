---
title: Restaurar páginas (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restorepage.general.f1
helpviewer_keywords:
- restoring pages [SQL Server]
- pages [SQL Server], restoring
- databases [SQL Server], damaged
- page restores [SQL Server]
- pages [SQL Server], damaged
- restoring [SQL Server], pages
ms.assetid: 07e40950-384e-4d84-9ac5-84da6dd27a91
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6fb008314b9cb156f1cc575bda71b6364eca6e3a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84956754"
---
# <a name="restore-pages-sql-server"></a>Restaurar páginas (SQL Server)
  Este tópico descreve como restaurar páginas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A meta da restauração de uma página é restaurar uma ou mais páginas danificadas sem restaurar todo o banco de dados. Geralmente, as páginas candidatas à restauração foram marcadas como "suspeitas" por causa de um erro encontrado durante seu acesso. Páginas suspeitas são identificadas na tabela [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) do banco de dados **msdb** .  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Quando uma restauração de página é útil?](#WhenUseful)  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para restaurar páginas usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="when-is-a-page-restore-useful"></a><a name="WhenUseful"></a> Quando uma restauração de página é útil?  
 A restauração de página é usada para restaurar páginas danificadas isoladas. A restauração e recuperação de algumas páginas individuais pode ocorrer mais rapidamente do que a restauração de arquivo, reduzindo a quantidade de dados offline durante a operação de restauração. No entanto, se for necessário restaurar mais do que algumas páginas em um arquivo, será geralmente mais eficaz restaurar todo o arquivo. Por exemplo, se várias páginas em um dispositivo indicarem uma falha de dispositivo pendente, é recomendável a restauração do arquivo, possivelmente em outro local, e a reparação do dispositivo.  
  
 Além disso, nem todos os erros de página precisam de restauração. Pode ocorrer um problema nos dados armazenados em cache, como um índice secundário, que pode ser resolvido pelo recálculo dos dados. Por exemplo, se o administrador de banco de dados cancela um índice secundário e o recria, os dados corrompidos, embora fixos, não são indicados como tal na tabela [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) .  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   A restauração de página se aplica a bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usam os modelos de recuperação completa ou bulk-logged. Só há suporte para restauração de página para grupos de arquivos de leitura/gravação.  
  
-   Somente páginas de banco de dados podem ser restauradas. A restauração de página não pode ser usada para restaurar o seguinte:  
  
    -   Log de transações  
  
    -   Páginas de alocação: páginas GAM (Global Allocation Map), páginas SGAM (Shared Global Allocation Map) e páginas PFS (Page Free Space).  
  
    -   Página 0 de todos os arquivos de dados (a página de inicialização de arquivo)  
  
    -   Página 1:9 (a página de inicialização do banco de dados)  
  
    -   Catálogo de texto completo  
  
-   Para um banco de dados que usa o modelo de recuperação bulk-logged, a restauração de página tem as seguintes condições adicionais:  
  
    -   Fazer um backup enquanto um grupo de arquivos ou dados de página estão offline é problemático para dados com log de operações em massa porque os dados offline não são registrados no log. Qualquer página offline pode impedir o backup do log. Nesses casos, considere usar DBCC REPAIR, pois isso pode causar menos perda de dados do que a restauração do backup mais recente.  
  
    -   Se um backup de log de um banco de dados com log de operações em massa encontrar uma página danificada, falhará a menos que WITH CONTINUE_AFTER_ERROR esteja especificado.  
  
    -   A restauração de página geralmente não funciona em recuperação bulk-logged.  
  
         Uma prática recomendada para executar restauração de página é definir o banco de dados como modelo de recuperação completa e tentar um backup de log. Se o backup de log funcionar, você poderá continuar com a restauração da página. Se o backup de log falhar, você perderá trabalho desde o backup de log anterior ou terá de tentar executar DBCC com a opção REPAIR_ALLOW_DATA_LOSS.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Cenários de restauração de página:  
  
     Restauração de página offline  
     Todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferecem suporte à restauração de páginas quando o banco de dados está offline. Em uma restauração de página offline, o banco de dados fica offline enquanto as páginas danificadas são restauradas. Ao término da sequência de restauração, o banco de dados fica online.  
  
     Restauração de página online  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Enterprise edition dá suporte à restaurações de página online, mesmo que use a restauração offline quando o banco de dados está offline. Na maioria dos casos, uma página danificada pode ser restaurada enquanto o banco de dados permanece online, inclusive o grupo de arquivos para o qual uma página está sendo restaurada. Quando o grupo de arquivos primário estiver online, até mesmo se um ou mais de seus grupos de arquivos secundários estiverem offline, as restaurações de página serão geralmente executadas online. No entanto, ocasionalmente uma página danificada pode precisar de uma restauração offline. Por exemplo, os danos a certas páginas importantes podem impedir a inicialização do banco de dados.  
  
    > [!WARNING]  
    >  Se páginas danificadas estiverem armazenando metadados de bancos de dados importantes, atualizações necessárias nos metadados poderão apresentar falha durante uma tentativa de restauração de página online. Nesse caso, você pode executar uma restauração de página offline, mas primeiro deve criar um [backup da parte final do log](tail-log-backups-sql-server.md) (fazendo backup do log de transações por meio de RESTORE WITH NORECOVERY).  
  
-   A restauração de página beneficia-se do relatório aprimorado de erro no nível da página (incluindo somas de verificação de página) e do rastreamento. As páginas detectadas como corrompidas por soma de verificação ou gravação interrompida, as *páginas danificadas*, podem ser restauradas por uma operação de restauração de página. Somente páginas explicitamente especificadas são restauradas. Cada página especificada é substituída pela cópia dessa página no backup de dados especificado.  
  
     Quando você restaurar os backups de log subsequentes, eles só serão aplicados a arquivos de banco de dados que contêm pelo menos uma página que está sendo recuperada. Uma cadeia uniforme de backups de log deve ser aplicada à última restauração completa ou diferencial para trazer o grupo de arquivos que contém a página até o arquivo de log atual. Assim como em uma restauração de arquivo, o conjunto de roll forward é avançado com uma única passagem de restauração de log. Para que a restauração da página tenha êxito, as páginas restauradas devem ser recuperadas para um estado consistente com o banco de dados.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Se o banco de dados que está sendo restaurado não existir, o usuário deverá ter permissões CREATE DATABASE para poder executar o comando RESTORE. Se o banco de dados existir, as permissões RESTORE usarão como padrão os membros das funções de servidor fixas **sysadmin** e **dbcreator** e o proprietário (**dbo**) do banco de dados (para a opção FROM DATABASE_SNAPSHOT, o banco de dados sempre existe).  
  
 As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Começando pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oferece suporte a restaurações de página.  
  
#### <a name="to-restore-pages"></a>Para restaurar páginas  
  
1.  Conecte-se à instância adequada do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objetos, e clique no nome do servidor para expandir a árvore de servidores.  
  
2.  Expanda os **Bancos de dados**. Dependendo do banco de dados, selecione um banco de dados de usuário ou expanda os **Bancos de dados do sistema**e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**, **Restaurar**e clique em **Página**, o que abre a caixa de diálogo **Restaurar Página** .  
  
     **Restaurar**  
     Esta seção executa a mesma função de **Restaurar em** em [Restaurar Banco de Dados (Página Geral)](../../integration-services/general-page-of-integration-services-designers-options.md).  
  
     **Backup de banco de dados**  
     Especifica o banco de dados a ser restaurado. Você pode digitar um novo banco de dados ou selecionar um banco de dados existente na lista suspensa. A lista inclui todos os bancos de dados do servidor, exceto os bancos de dados do sistema **mestre** e **tempdb**.  
  
    > [!WARNING]  
    >  Para restaurar um backup protegido por senha, você deve usar a instrução [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) .  
  
     **Backup do final do log**  
     Digite ou selecione um nome de arquivo em **Dispositivo de backup** em que o backup da parte final do log será armazenado para o banco de dados.  
  
     **Conjuntos de backup**  
     Esta seção exibe os conjuntos de backup envolvidos na restauração.  
  
    |Cabeçalho|Valores|  
    |------------|------------|  
    |**Nome**|O nome do conjunto de backup.|  
    |**Componente**|O componente de backup: banco de **dados**, **arquivo**ou **\<blank>** (para logs de transações).|  
    |**Tipo**|O tipo de backup realizado: **Total**, **Diferencial** ou **Log de Transações**.|  
    |**Servidor**|O nome da instância [!INCLUDE[ssDE](../../includes/ssde-md.md)] que executou a operação de backup.|  
    |**Backup de banco de dados**|Nome do banco de dados envolvido na operação de backup.|  
    |**Posição**|A posição do conjunto de backup no volume.|  
    |**Primeiro LSN**|Número de sequência de log (LSN) da primeira transação do conjunto de backup. Em branco para backups de arquivo.|  
    |**Último LSN**|O número de sequência de log (LSN) da última transação do conjunto de backup. Em branco para backups de arquivo.|  
    |**LSN do Ponto de Verificação**|O número de sequência de log (LSN) do ponto de verificação mais recente no momento da criação do backup.|  
    |**LSN Completo**|Número de sequência de log (LSN) do backup de banco de dados completo mais recente.|  
    |**Data de Início**|A data e hora de início da operação de backup, apresentadas na configuração regional do cliente.|  
    |**Data de Conclusão**|A data e hora da conclusão da operação de backup, apresentadas na configuração regional do cliente.|  
    |**Tamanho**|O tamanho do conjunto de backup em bytes.|  
    |**Nome de usuário**|O nome do usuário que realizou a operação de backup.|  
    |**Validade**|A data e hora de validade do conjunto de backup.|  
  
     Clique em **Verificar** para verificar a integridade dos arquivos de backup necessários para executar a operação de restauração de página.  
  
4.  Para identificar páginas corrompidas, com o banco de dados correto selecionado na caixa **Banco de Dados** , clique em **Verificar Páginas de Banco de Dados**. Essa é uma operação em execução longa.  
  
    > [!WARNING]  
    >  Para restaurar páginas específicas que não estão danificadas, clique em **Adicionar** e digite a **ID do Arquivo** e a **ID da Página** referentes às páginas que serão restauradas.  
  
5.  A grade de páginas é usada para identificar as páginas a serem restauradas. Inicialmente, essa grade é preenchida por meio da tabela de sistema [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) . Para adicionar ou remover páginas da grade, clique em **Adicionar** ou **Remover**. Para obter mais informações, veja [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](manage-the-suspect-pages-table-sql-server.md).  
  
6.  A grade **Conjuntos de backup** lista os conjuntos de backup no plano de restauração padrão. Se desejar, clique em **Verificar** para verificar se os backups são legíveis e se os conjuntos de backup são completos, sem restaurá-los. Para obter mais informações, consulte [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql).  
  
     **Páginas**  
  
7.  Para restaurar as páginas listadas na grade de páginas, clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Para especificar uma página em uma instrução RESTORE DATABASE, você precisará da ID do arquivo que contém a página e da ID da página. A sintaxe necessária é a seguinte:  
  
 `RESTORE DATABASE <database_name>`  
  
 `PAGE = '<file: page> [ ,... n ] ' [ ,... n ]`  
  
 `FROM <backup_device> [ ,... n ]`  
  
 `WITH NORECOVERY`  
  
 Para obter mais informações sobre os parâmetros da opção PAGE, consulte [Argumentos RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql). Para obter mais informações sobre a sintaxe RESTORE DATABASE, consulte [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
#### <a name="to-restore-pages"></a>Para restaurar páginas  
  
1.  Obtenha a ID das páginas a serem restauradas. Uma soma de verificação ou um erro de gravação interrompida retorna a ID da página, fornecendo as informações necessárias para especificar as páginas. Para consultar a ID de uma página danificada, use qualquer uma das origens a seguir.  
  
    |Fonte de ID de página|Tópico|  
    |-----------------------|-----------|  
    |**msdb..suspect_pages**|[Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](manage-the-suspect-pages-table-sql-server.md)|  
    |Log de erros|[Exibir o log de erros do SQL Server &#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)|  
    |Rastreamento de evento|[Monitorar e responder a eventos](../../ssms/agent/monitor-and-respond-to-events.md)|  
    |DBCC|[DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)|  
    |Provedor WMI|[Provedor WMI para conceitos de eventos de servidor](../wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)|  
  
2.  Inicie uma restauração de página com um backup completo do banco de dados, do arquivo ou do grupo de arquivos que contém a página. Na instrução RESTORE DATABASE, use a cláusula PAGE para listar as IDs de página de todas as páginas a serem restauradas.  
  
3.  Aplique os diferenciais mais recentes.  
  
4.  Aplique os backups de log subsequentes.  
  
5.  Crie um novo backup de log do banco de dados que inclui o LSN final das páginas restauradas, ou seja, o ponto no qual a última página restaurada foi colocada offline. O LSN final, que é definido como parte da primeira restauração na sequência, é o LSN refeito de destino. O roll forward Online do arquivo que contém a página pode parar no LSN refeito de destino. Para saber qual é o LSN refeito de destino de um arquivo, consulte a coluna **redo_target_lsn** de **sys.master_files**. Para obter mais informações, consulte [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql).  
  
6.  Restaure o novo backup de log. Depois que o novo backup de log é aplicado, a restauração da página está concluída e as páginas podem ser usadas.  
  
    > [!NOTE]  
    >  Essa sequência é análoga à sequência de restauração de um arquivo. Na realidade, restaurações de página e arquivo podem ser executadas como parte da mesma sequência.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir restaura quatro páginas danificadas do arquivo `B` com `NORECOVERY`. Em seguida, dois backups de log são aplicados com `NORECOVERY`, seguido pelo backup do final do log que é restaurado com `RECOVERY`. Este exemplo executa uma restauração online. No exemplo, a ID de arquivo de `B` é `1`, e as IDs de página das páginas danificadas são `57`, `202`, `916`e `1016`.  
  
```sql  
RESTORE DATABASE <database> PAGE='1:57, 1:202, 1:916, 1:1016'  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;   
BACKUP LOG <database> TO <new_log_backup>;   
RESTORE LOG <database> FROM <new_log_backup> WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](manage-the-suspect-pages-table-sql-server.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](back-up-and-restore-of-sql-server-databases.md)  
  
  

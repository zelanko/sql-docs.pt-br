---
title: Restaurar um backup de log de transações (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoretlog.options.f1
- sql12.swb.restoretlog.general.f1
helpviewer_keywords:
- restore log
- backing up transaction logs [SQL Server], restoring
- transaction log backups [SQL Server], restoring
- restoring transaction logs [SQL Server], restoring backups
- transaction log restores [SQL Server], SQL Server Management Studio
ms.assetid: 1de2b888-78a6-4fb2-a647-ba4bf097caf3
caps.latest.revision: 35
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 85c4008e1872a48126c67e47cc8d68ed0867828d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237016"
---
# <a name="restore-a-transaction-log-backup-sql-server"></a>Restaurar um backup de log de transações (SQL Server)
  Este tópico descreve como restaurar um backup de log de transação no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para restaurar um backup de log de transações, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Os backups devem ser restaurados na ordem em que foram criados. Antes de poder restaurar um backup de log de transações específico, restaure primeiro os backups anteriores seguintes sem reverter as transações não confirmadas, isto é WITH NORECOVERY:  
  
    -   O backup de banco de dados completo e o último backup diferencial, se houver, realizado antes do backup de log de transações específico. Antes do backup de banco de dados completo ou diferencial mais recente tiver sido criado, o banco de dados deverá usar o modelo de recuperação completa ou o modelo de recuperação bulk-logged.  
  
    -   Todos os backups de log de transações efetuados depois do backup de banco de dados completo ou o backup diferencial (se você o restaurar) e antes do backup de log de transações específico. Devem ser aplicados backups de log na sequência na qual eles foram criados, sem qualquer intervalo na cadeia de logs.  
  
         Para obter mais informações sobre backups de log de transações, consulte [Backups de log de transações &#40;SQL Server&#41;](transaction-log-backups-sql-server.md) e [Aplicar backups de log de transações &#40;SQL Server&#41;](apply-transaction-log-backups-sql-server.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
> [!WARNING]  
>  O processo normal de uma restauração é selecionar os backups de log na caixa de diálogo **Restaurar Banco de Dados** junto com os dados e backups diferenciais.  
  
#### <a name="to-restore-a-transaction-log-backup"></a>Para restaurar um backup de log de transações  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**, **Restaurar**e clique em **Log de Transações**, o que abre a caixa de diálogo **Restaurar Log de Transações** .  
  
    > [!NOTE]  
    >  Se a opção **Log de Transações** estiver acinzentada, talvez seja necessário restaurar um backup completo ou diferencial primeiro. Use a caixa de diálogo **Backup de banco de dados** .  
  
4.  Na página **Geral** , na caixa de listagem **Banco de Dados** , selecione o nome de um banco de dados. Só são listados bancos de dados no estado de restauração.  
  
5.  Para especificar a origem e o local dos conjuntos de backup a serem restaurados, clique em uma das seguintes opções:  
  
    -   **De backups anteriores do banco de dados**  
  
         Selecione o banco de dados a ser restaurado na lista suspensa. A lista contém apenas os bancos de dados dos quais foi feito um backup de acordo com o histórico de backup do **msdb** .  
  
    -   **Do arquivo ou fita**  
  
         Clique no botão Procurar (**...**) para abrir a caixa de diálogo **Selecione dispositivos de backup** . Na caixa **Tipo de mídia de backup** , selecione um dos tipos de dispositivo listados. Para selecionar um ou mais dispositivos da caixa **Mídia de backup** , clique em **Adicionar**.  
  
         Após adicionar os dispositivos desejados à caixa de listagem **Mídia de backup** , clique em **OK** para voltar à página **Geral** .  
  
6.  Na grade **Selecione os backups de log de transações a serem restaurados** , selecione os backups a serem restaurados. Essa grade lista os backups de log de transações disponíveis para o banco de dados selecionado. Um backup de log só estará disponível se o **Primeiro LSN** for maior do que o **Último LSN** do banco de dados. Os backups de log são listados na ordem dos números de sequência de log (LSN) que eles contêm e devem ser restaurados nessa ordem.  
  
     A tabela a seguir lista os cabeçalhos de coluna da grade e descreve seus valores.  
  
    |Cabeçalho|Valor|  
    |------------|-----------|  
    |**Restaurar**|Caixas de seleção selecionadas indicam os conjuntos de backup a serem restaurados.|  
    |**Nome**|Nome do conjunto de backup.|  
    |**Componente**|Componente com backup: **Banco de Dados**, **Arquivo** ou \<em branco> (para logs de transações).|  
    |**Backup de banco de dados**|Nome do banco de dados envolvido na operação de backup.|  
    |**Data de Início**|A data e hora do início da operação de backup, apresentadas na configuração regional do cliente.|  
    |**Data de Conclusão**|Data e hora de término da operação de backup, apresentadas na configuração regional do cliente.|  
    |**Primeiro LSN**|Número de sequência de log da primeira transação no conjunto de backup. Em branco para backups de arquivo.|  
    |**Último LSN**|Número de sequência de log da última transação no conjunto de backup. Em branco para backups de arquivo.|  
    |**LSN do Ponto de Verificação**|Número de sequência de log do ponto de verificação mais recente no momento em que o backup foi criado.|  
    |**LSN Completo**|Número de sequência de log do backup de banco de dados completo mais recente.|  
    |**Servidor**|Nome da instância do Mecanismo de Banco de Dados que executou a operação de backup.|  
    |**Nome do Usuário**|Nome do usuário que realizou a operação de backup.|  
    |**Tamanho**|Tamanho do conjunto de backup em bytes.|  
    |**Posição**|Posição do conjunto de backup no volume.|  
    |**Validade**|Data e hora de vencimento do conjunto de backup.|  
  
7.  Selecione uma destas opções:  
  
    -   **Point-in-time**  
  
         Retenha o padrão (**Mais recente possível**) ou selecione uma data e hora específicas clicando no botão Procurar, que abre a caixa de diálogo **Recuperação Pontual** .  
  
    -   **Transação marcada**  
  
         Restaure o banco de dados a uma transação previamente marcada. Selecionar esta opção inicia a caixa de diálogo **Selecionar Transação Marcada** que exibe uma grade com uma lista das transações marcadas disponíveis nos backups de log de transações selecionados.  
  
         Por padrão, a restauração vai até a transação marcada, mas a exclui. Para restaurar também a transação marcada, selecione **Incluir transação marcada**.  
  
         A tabela a seguir lista os cabeçalhos de coluna da grade e descreve seus valores.  
  
        |Cabeçalho|Valor|  
        |------------|-----------|  
        |\<em branco>|Exibe uma caixa de seleção para selecionar a marca.|  
        |**Transaction Mark**|Nome da transação marcada especificado pelo usuário quando a transação foi confirmada.|  
        |**Date**|Data e hora de confirmação da transação. A data e hora da transação são exibidas como registradas na tabela **msdbgmarkhistory** , não a data e hora do computador cliente.|  
        |**Descrição**|Descrição da transação marcada especificada pelo usuário quando a transação foi confirmada (se houver).|  
        |**LSN**|Número de sequência de log da transação marcada.|  
        |**Backup de banco de dados**|Nome do banco de dados em que a transação marcada foi confirmada.|  
        |**Nome do Usuário**|Nome do usuário do banco de dados que confirmou a transação marcada.|  
  
8.  Para exibir ou selecionar as opções avançadas, clique em **Opções** no painel **Selecionar uma página** .  
  
9. Na seção **Opções de restauração** , as opções são:  
  
    -   **Preservar as configurações de replicação (WITH KEEP_REPLICATION)**  
  
         Preserva as configurações de replicação ao restaurar um banco de dados publicado em um servidor diferente daquele onde o banco de dados foi criado.  
  
         Essa opção só está disponível com o **deixar o banco de dados pronto para uso Revertendo as transações não confirmadas...**  opção (descrita adiante), que é equivalente a restaurar um backup com o `RECOVERY` opção.  
  
         Marcar essa opção é equivalente a usar o `KEEP_REPLICATION` opção em um [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE` instrução.  
  
    -   **Perguntar antes de restaurar cada backup**  
  
         Antes de restaurar cada conjunto de backup (depois do primeiro), essa opção traz a caixa de diálogo **Continuar Restauração** que solicita a você que indique se deseja continuar a sequência de restauração. Essa caixa de diálogo exibe o nome do próximo conjunto de mídia (se disponível), o nome do conjunto de backup e a descrição do conjunto de backup.  
  
         Essa opção é particularmente útil quando você deve trocar fitas para conjuntos de mídia diferentes. Por exemplo, você poderá usá-la quando o servidor tiver só um dispositivo de fita. Espere até estar pronto para continuar antes de clicar em **OK**.  
  
         Clicar em **Não** deixa o banco de dados em estado de restauração. Quando for conveniente, você poderá continuar a sequência de restauração depois da última restauração concluída. Se o próximo backup for um backup de dados ou diferencial, use a tarefa **Restaurar Banco de Dados** novamente. Se o backup seguinte for um backup de log, use a tarefa **Restaurar Log de Transações** .  
  
    -   **Acesso restrito ao banco de dados restaurado (WITH RESTRICTED_USER)**  
  
         Disponibiliza o banco de dados restaurado apenas para os membros do **db_owner**, **dbcreator**ou **sysadmin**.  
  
         Marcar essa opção é sinônimo de usar o `RESTRICTED_USER` opção em um [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE` instrução.  
  
10. Para as opções **Estado de recuperação** , especifique o estado do banco de dados após a operação de restauração.  
  
    -   **Deixe o banco de dados pronto para uso revertendo as transações não confirmadas. Os logs de transações adicionais não podem ser restaurados. (RESTORE WITH RECOVERY)**  
  
         Recupera o banco de dados. Essa opção é equivalente à `RECOVERY` opção em um [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE` instrução.  
  
         Só escolha essa opção se você não tiver nenhum arquivo de log que queira restaurar.  
  
    -   **Deixe o banco de dados não operacional e não reverta as transações não confirmadas. Os logs de transações adicionais podem ser restaurados. (RESTORE WITH NORECOVERY)**  
  
         Deixa o banco de dados não recuperado, no estado `RESTORING`. Essa opção é equivalente a usar o `NORECOVERY` opção em um [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE` instrução.  
  
         Quando você escolhe essa opção, a opção **Preservar configurações de replicação** fica indisponível.  
  
        > [!IMPORTANT]  
        >  Para um banco de dados espelho ou secundário, sempre selecione essa opção.  
  
    -   **Deixar o banco de dados no modo somente leitura. Desfaça as transações não confirmadas, mas salve as ações de desfazer em um arquivo, para que os efeitos da recuperação possam ser revertidos. (RESTORE WITH STANDBY)**  
  
         Deixa o banco de dados no estado de espera. Essa opção é equivalente a usar o `STANDBY` opção em um [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE` instrução.  
  
         A escolha desta opção requer que você especifique um arquivo de espera.  
  
11. Opcionalmente, especifique o nome do arquivo em espera na caixa de texto **Arquivo em espera** . Essa opção será necessária se você deixar o banco de dados no modo somente leitura. Você pode procurar o arquivo em espera ou pode digitar o nome do caminho na caixa de texto.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
> [!IMPORTANT]  
>  Nós recomendamos que você sempre especifique explicite WITH NORECOVERY ou WITH RECOVERY em toda instrução RESTORE para eliminar a ambiguidade. Isso é particularmente importante ao escrever scripts.  
  
#### <a name="to-restore-a-transaction-log-backup"></a>Para restaurar um backup de log de transações  
  
1.  Execute a instrução RESTORE para aplicar o backup de log de transações, especificando o seguinte:  
  
    -   O nome do banco de dados ao qual o log de transações será aplicado.  
  
    -   O dispositivo de backup a partir de onde o backup de log de transações será restaurado.  
  
    -   A cláusula NORECOVERY.  
  
     A sintaxe básica desta instrução é:  
  
     RESTORE LOG *database_name* FROM <backup_device> WITH NORECOVERY.  
  
     Em que *database_name* é o nome do banco de dados e <backup_device> é o nome do dispositivo que contém o backup de log que está sendo restaurado.  
  
2.  Repita a etapa 1 para cada backup de log de transações você tiver que aplicar.  
  
3.  Depois de restaurar o último backup na sua sequência de restauração, para recuperar o uso de banco de dados use uma das seguintes instruções:  
  
    -   Recuperar o banco de dados como parte da última instrução RESTORE LOG:  
  
        ```  
        RESTORE LOG <database_name> FROM <backup_device> WITH RECOVERY;  
        GO  
        ```  
  
    -   Espere para recuperar o banco de dados usando uma instrução separada RESTORE DATABASE:  
  
        ```  
        RESTORE LOG <database_name> FROM <backup_device> WITH NORECOVERY;   
        RESTORE DATABASE <database_name> WITH RECOVERY;  
        GO  
        ```  
  
         Ao esperar para recuperar o banco de dados você tem a oportunidade de verificar se restaurou todos dos backups de log necessários. Essa abordagem é aconselhável quando você estiver executando uma restauração point-in-time.  
  
    > [!IMPORTANT]  
    >  Se você estiver criando um banco de dados espelho, omita a etapa de recuperação. Um banco de dados espelho deve permanecer no estado RESTORING.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Por padrão, o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] usa o modelo de recuperação simples. Os exemplos seguintes requerem a modificação do banco de dados para usar o modelo de recuperação completa, como segue:  
  
```tsql  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
```  
  
#### <a name="a-applying-a-single-transaction-log-backup"></a>A. Aplicando um único backup de log de transações  
 O exemplo seguinte inicia restaurando o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] usando um backup de banco de dados completo que reside em um dispositivo de backup chamado `AdventureWorks2012_1`. O exemplo aplica então o primeiro backup de log de transações que reside em um dispositivo de backup chamado `AdventureWorks2012_log`. Por fim, o exemplo recupera o banco de dados.  
  
```tsql  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorks2012_1  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 1,  
   WITH NORECOVERY;  
GO  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
#### <a name="b-applying-multiple-transaction-log-backups"></a>B. Aplicando múltiplos backups de log de transações  
 O exemplo seguinte inicia restaurando o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] usando um backup de banco de dados completo que reside em um dispositivo de backup chamado `AdventureWorks2012_1`. O exemplo aplica então, um por um, os três primeiros backups de log de transações que residem em um dispositivo de backup chamado `AdventureWorks2012_log`. Por fim, o exemplo recupera o banco de dados.  
  
```tsql  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorks2012_1  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 1,  
   NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 2,  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 3,  
   WITH NORECOVERY;  
GO  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [Restaurar um Backup de banco de dados &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Restaurar um banco de dados até o ponto de falha no modelo de recuperação completa &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   [Restaurar um banco de dados para uma transação marcada &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte também  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](apply-transaction-log-backups-sql-server.md)  
  
  

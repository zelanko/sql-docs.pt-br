---
title: Definir o modelo de recuperação do banco de dados
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], recovery models
- recovery [SQL Server], recovery model
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], switching
- recovery models [SQL Server], viewing
- database restores [SQL Server], recovery models
- modifying database recovery models
ms.assetid: 94918d1d-7c10-4be7-bf9f-27e00b003a0f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4af4e8b1d0dacb5e08cdd117a14691b909050b09
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75254048"
---
# <a name="view-or-change-the-recovery-model-of-a-database-sql-server"></a>Exibir ou alterar o modelo de recuperação de um banco de dados (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como exibir ou alterar o banco de dados usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. 
  
  Um *modelo de recuperação* é uma propriedade de banco de dados que controla como as transações são registradas, se o log de transações exige (e permite) backup e que tipos de operações de restauração estão disponíveis. Existem três modelos de recuperação: simples, completo e bulk-logged. Geralmente, um banco de dados usa o modelo de recuperação completa ou o modelo de recuperação simples. É possível alternar para outro modelo de recuperação do banco de dados a qualquer momento. Os banco de dados **modelo** define o modelo de recuperação padrão de novos bancos de dados.  
  
  Confira uma explicação mais detalhada em [modelos de recuperação](recovery-models-sql-server.md).
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  

-   [Fazer backup do log de transações](back-up-a-transaction-log-sql-server.md) **antes** de mudar do [mudar de recuperação completa ou recuperação registrada em log em massa](recovery-models-sql-server.md).  
  
-   A recuperação pontual não é possível com modelo bulk-logged. A execução de transações sob o modelo de recuperação bulk-logged que exigem uma restauração do log de transações, pode sujeitá-las à perda de dados. Para maximizar a recuperabilidade de dados em um cenário de recuperação de desastres, mude para o modelo de recuperação bulk-logged somente nas seguintes condições:  
  
    -   Atualmente, não são permitidos usuários no banco de dados.  
  
    -   Todas as modificações feitas durante o processamento em massa são recuperáveis sem depender de fazer um backup de log; por exemplo, executar novamente os processos em massa.  
  
     Se você atender a estas duas condições, não será exposto a perda de dados enquanto estiver restaurando um log de transação que teve o backup feito no modelo de recuperação bulk-logged.  
  
**Observação!** Se você mudar para o modelo de recuperação completa durante uma operação em massa, o log das operações em massa mudará de registro em log mínimo para registro em log completo, e vice-versa.  
  
###  <a name="required-permissions"></a><a name="Security"></a> Permissões necessárias  
   Requer a permissão ALTER no banco de dados.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-recovery-model"></a>Para exibir ou alterar o modelo de recuperação  
  
1.  Depois de conectar-se à instância adequada do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objeto, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados e clique em **Propriedades**, o que abrirá a caixa de diálogo **Propriedades do Banco de Dados** .  
  
4.  No painel **Selecionar uma página** , clique em **Opções**.  
  
5.  O modelo de recuperação atual é exibido na caixa de listagem **Modelo de Recuperação** .  
  
6.  Opcionalmente, para alterar o modelo de recuperação, selecione uma lista de modelos diferente. As escolhas são **Completo**, **Bulk-logged**ou **Simples**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-the-recovery-model"></a>Para exibir o modelo de recuperação  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como consultar a exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) para aprender o modelo de recuperação do banco de dados **modelo** .  
  
```sql  
SELECT name, recovery_model_desc  
   FROM sys.databases  
      WHERE name = 'model' ;  
GO  
  
```  
  
#### <a name="to-change-the-recovery-model"></a>Para alterar o modelo de recuperação  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como alterar o modelo de recuperação no banco de dados `model` para `FULL` usando a opção `SET RECOVERY` da instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) .  
  
```sql  
USE [master] ;  
ALTER DATABASE [model] SET RECOVERY FULL ;  
```  
  
##  <a name="recommendations-after-you-change-the-recovery-model"></a><a name="FollowUp"></a> Recomendações: após a alteração do modelo de recuperação  
  
-   **Depois de alternar entre os modelos de recuperação completa e bulk-logged**  
  
    -   Depois de concluir as operações em massa, retorne imediatamente para o modo de recuperação completa.  
  
    -   Depois de alternar do modelo de recuperação bulk-logged novamente para o modelo de recuperação completa, faça backup do log.  
  
        >**OBSERVAÇÃO:** sua estratégia de backup permanecerá a mesma: continue executando backups periódicos do banco de dados, do log e backups diferenciais.  
  
-   **Depois de alternar do modelo de recuperação simples**  
  
    -   Imediatamente depois de alternar para a troca para o modelo de recuperação completa ou modelo de recuperação bulk-logged, faça um backup completo ou diferencial de banco de dados para iniciar a cadeia de logs.  
  
        >**OBSERVAÇÃO:** a alternância para o modelo de recuperação completa ou com log de operações em massa só entrará em vigor depois do primeiro backup de dados.  
  
    -   Agende backups de log regulares e atualize seu plano de restauração adequadamente.  
  
        > **IMPORTANTE!!!!** Faça backup dos logs!! Se você não fizer backup do log com a frequência necessária, o log de transações poderá expandir até exceder o espaço em disco!  
  
-   **Depois de alternar para o modelo de recuperação simples**  
  
    -   Descontinue os trabalhos agendados para fazer backup do log de transação.  
  
    -   Verifique se os backups periódicos de banco de dados estão agendados. Fazer backup de seu banco de dados é essencial para proteger seus dados e truncar a porção inativa do log de transações.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Related tasks  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Criar um trabalho](../../ssms/agent/create-a-job.md)  
  
-   [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Planos de manutenção de banco de dados](../maintenance-plans/maintenance-plans.md) (nos Manuais Online do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] )  
  
## <a name="see-also"></a>Consulte Também  
 [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  

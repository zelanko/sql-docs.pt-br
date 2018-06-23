---
title: Exibir ou alterar o modelo de recuperação de um banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database backups [SQL Server], recovery models
- recovery [SQL Server], recovery model
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], switching
- recovery models [SQL Server], viewing
- database restores [SQL Server], recovery models
- modifying database recovery models
ms.assetid: 94918d1d-7c10-4be7-bf9f-27e00b003a0f
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 142fa3d4dcdfabac8f8c2f3c0a7576e2046f814b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121505"
---
# <a name="view-or-change-the-recovery-model-of-a-database-sql-server"></a>Exibir ou alterar o modelo de recuperação de um banco de dados (SQL Server)
  Este tópico descreve como exibir ou alterar o modelo de recuperação de um banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. Um *modelo de recuperação* é uma propriedade de banco de dados que controla como as transações são registradas, se o log de transações exige (e permite) backup e que tipos de operações de restauração estão disponíveis. Existem três modelos de recuperação: simples, completo e bulk-logged. Geralmente, um banco de dados usa o modelo de recuperação completa ou o modelo de recuperação simples. É possível alternar para outro modelo de recuperação do banco de dados a qualquer momento. Os banco de dados **modelo** define o modelo de recuperação padrão de novos bancos de dados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para exibir ou alterar o modelo de recuperação de um banco de dados, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Recomendações de acompanhamento:**  [depois que você alterar o modelo de recuperação](#FollowUp)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Antes de mudar de modelo de recuperação completa ou de recuperação bulk-logged, faça o backup do log de transações.  
  
-   A recuperação pontual não é possível com modelo bulk-logged. Portanto, se você executar transações sob o modelo de recuperação bulk-logged que pode exigir uma restauração do log de transação, estas transações estarão sujeitas a perda de dados. Para maximizar a recuperabilidade de dados em um cenário de recuperação de desastres, recomendamos que você alterne para o modelo de recuperação bulk-logged somente nas seguintes condições:  
  
    -   Atualmente, não são permitidos usuários no banco de dados.  
  
    -   Todas as modificações feitas durante o processamento em massa são recuperáveis sem depender de fazer um backup de log; por exemplo, executar novamente os processos em massa.  
  
     Se você atender a estas duas condições, não será exposto a perda de dados enquanto estiver restaurando um log de transação que teve o backup feito no modelo de recuperação bulk-logged.  
  
> [!NOTE]  
>  Se você alternar para o modelo de recuperação completa durante uma operação em massa, o registro em log da operação em massa passará de registro em log mínimo para registro em log completo, e vice-versa.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-recovery-model"></a>Para exibir ou alterar o modelo de recuperação  
  
1.  Depois de conectar-se à instância adequada do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objeto, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados e clique em **Propriedades**, o que abrirá a caixa de diálogo **Propriedades do Banco de Dados** .  
  
4.  No painel **Selecionar uma página** , clique em **Opções**.  
  
5.  O modelo de recuperação atual é exibido na caixa de listagem **Modelo de Recuperação** .  
  
6.  Opcionalmente, para alterar o modelo de recuperação, selecione uma lista de modelos diferente. As escolhas são **Completo**, **Bulk-logged**ou **Simples**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-the-recovery-model"></a>Para exibir o modelo de recuperação  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como consultar a exibição de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) para aprender o modelo de recuperação do banco de dados **modelo** .  
  
```tsql  
SELECT name, recovery_model_desc  
   FROM sys.databases  
      WHERE name = 'model' ;  
GO  
  
```  
  
#### <a name="to-change-the-recovery-model"></a>Para alterar o modelo de recuperação  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como alterar o modelo de recuperação no banco de dados `model` para `FULL` usando a opção `SET RECOVERY` da instrução [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options) .  
  
```tsql  
USE master ;  
ALTER DATABASE model SET RECOVERY FULL ;  
```  
  
##  <a name="FollowUp"></a> Recomendações de acompanhamento: Depois de alterar o modelo de recuperação  
  
-   **Depois de alternar entre os modelos de recuperação completa e bulk-logged**  
  
    -   Depois de concluir as operações em massa, retorne imediatamente para o modo de recuperação completa.  
  
    -   Depois de alternar do modelo de recuperação bulk-logged novamente para o modelo de recuperação completa, faça backup do log.  
  
        > [!NOTE]  
        >  Sua estratégia de backup permanecerá a mesma: continue executando backups periódicos do banco de dados, do log e backups diferenciais.  
  
-   **Depois de alternar do modelo de recuperação simples**  
  
    -   Imediatamente depois de alternar para a troca para o modelo de recuperação completa ou modelo de recuperação bulk-logged, faça um backup completo ou diferencial de banco de dados para iniciar a cadeia de logs.  
  
        > [!NOTE]  
        >  A alternância para o modelo de recuperação completa ou com log de operações em massa só entrará em vigor depois do primeiro backup de dados.  
  
    -   Agende backups de log regulares e atualize seu plano de restauração adequadamente.  
  
        > [!IMPORTANT]  
        >  Se você não fizer backup do log com a frequência necessária, o log de transações poderá expandir-se até exceder o espaço em disco.  
  
-   **Depois de alternar para o modelo de recuperação simples**  
  
    -   Descontinue os trabalhos agendados para fazer backup do log de transação.  
  
    -   Verifique se os backups periódicos de banco de dados estão agendados. Fazer backup de seu banco de dados é essencial para proteger seus dados e truncar a porção inativa do log de transações.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [Criar um trabalho](../../ssms/agent/create-a-job.md)  
  
-   [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Planos de manutenção de banco de dados](http://msdn.microsoft.com/library/ms187658.aspx) (nos Manuais Online do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] )  
  
## <a name="see-also"></a>Consulte também  
 [Modelos de recuperação &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [O log de transações &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [Modelos de recuperação &#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  

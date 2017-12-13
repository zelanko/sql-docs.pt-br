---
title: Reduzir um banco de dados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.shrinkdatabase.f1
helpviewer_keywords:
- shrinking databases
- databases [SQL Server], shrinking
- decreasing database size
- database shrinking [SQL Server]
- reducing database size
ms.assetid: 83afbf74-fd50-4c39-831c-b1f473a50620
caps.latest.revision: "42"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 9f7cadab23bcbdc732dcac544d4d0f8fc90b04e5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="shrink-a-database"></a>Reduzir um banco de dados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Este tópico descreve como reduzir um banco de dados usando o Pesquisador de Objetos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 A redução de arquivos de dados recupera espaço com a movimentação de páginas de dados do final do arquivo para o espaço desocupado mais próximo à frente do arquivo. Quando espaço livre suficiente é criado no final do arquivo, as páginas de dados no final do arquivo podem ser desalocadas e retornadas para o sistema de arquivos.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para reduzir um banco de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de reduzir um banco de dados](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O banco de dados não pode se tornar menor que o tamanho mínimo do banco de dados. O tamanho mínimo é aquele especificado na criação inicial do banco de dados ou o último tamanho explicitamente configurado por meio de uma operação de alteração de tamanho de arquivo, como DBCC SHRINKFILE. Por exemplo, se um banco de dados foi criado originalmente com um tamanho de 10 MB e atingir 100 MB, a menor redução desse banco de dados será de 10 MB, mesmo se todos os dados do banco de dados forem excluídos.  
  
-   Não é possível reduzir um banco de dados enquanto ele estiver sendo armazenado em backup. Da mesma forma, não é possível fazer backup de um banco de dados enquanto houver uma operação de redução em processamento.  
  
-   DBCC SHRINKDATABASE falhará quando encontrar um índices columnstore xVelocity de memória otimizada. O trabalho concluído antes de encontrar o índice de columnstore será bem-sucedido, de modo que o banco de dados talvez seja menor. Para concluir DBCC SHRINKDATABASE, desabilite todos os índices de columnstore antes de executar DBCC SHRINKDATABASE e recrie os índices de columnstore.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Para visualizar a quantidade atual de espaço livre (não alocado) no banco de dados. Para obter mais informações, consulte [Display Data and Log Space Information for a Database](../../relational-databases/databases/display-data-and-log-space-information-for-a-database.md).  
  
-   Considere as seguintes informações ao planejar reduzir um banco de dados:  
  
    -   Uma operação de redução é mais eficiente depois de uma operação que cria muito espaço não utilizado, como operações que truncam ou excluem uma tabela.  
  
    -   A maioria dos bancos de dados exige algum espaço livre disponível para operações comuns rotineiras. Se você reduzir um banco de dados repetidamente e perceber que ele aumentou novamente, isso indica que o espaço reduzido é necessário para as operações rotineiras. Nesse caso, reduzir repetidamente um banco de dados é uma operação inútil.  
  
    -   Uma operação de redução não preserva o estado de fragmentação de índices do banco de dados e, geralmente, aumenta o nível de fragmentação. Essa é outra razão para não reduzir o banco de dados repetidamente.  
  
    -   A menos que você tenha um requisito específico, não defina a opção de banco de dados AUTO_SHRINK como ON.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-shrink-a-database"></a>Para reduzir um banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda-a.  
  
2.  Expanda **Bancos de Dados**e clique com o botão direito do mouse no banco de dados que deseja reduzir.  
  
3.  Aponte para **Tarefas**, depois **Reduzir**e clique em **Banco de dados**.  
  
     **Banco de dados**  
     Exibe o nome do banco de dados selecionado.  
  
     **Espaço alocado atual**  
     Exibe o espaço total utilizado e não utilizado para o banco de dados selecionado.  
  
     **Espaço livre disponível**  
     Exibe a soma de espaço livre no log e nos arquivos de dados do banco de dados selecionado.  
  
     **Reorganizar arquivos antes de liberar espaço não utilizado**  
     Selecionar essa opção é equivalente a executar DBCC SHRINKDATABASE especificando uma opção de porcentagem de destino. Desmarcar esta opção é o mesmo que executar DBCC SHRINKDATABASE com a opção TRUNCATEONLY. Por padrão, essa opção não é selecionada quando a caixa de diálogo está aberta. Se esta opção for selecionada, o usuário deverá especificar uma opção de porcentagem de destino.  
  
     **Máximo espaço livre em arquivos após a redução**  
     Digite a porcentagem máxima de espaço livre a ser deixado nos arquivos de banco de dados após a redução do banco de dados. Os valores permitidos estão entre 0 e 99.  
  
4.  Clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-shrink-a-database"></a>Para reduzir um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo usa [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md) para reduzir o tamanho dos arquivos de dados e de log no banco de dados `UserDB` e liberar `10` por cento de espaço livre no banco de dados.  
  
 [!code-sql[DBCC#DBCC_SHRINKDB1](../../relational-databases/databases/codesnippet/tsql/shrink-a-database_1.sql)]  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de reduzir um banco de dados  
 Os dados movidos para reduzir um arquivo podem ser espalhados para qualquer local disponível no arquivo. Isso provoca uma fragmentação do índice e pode reduzir a velocidade do desempenho de consultas que pesquisam um intervalo do índice. Para eliminar a fragmentação, considere a recompilação dos índices no arquivo após a redução.  
  
## <a name="see-also"></a>Consulte também  
 [Reduzir um arquivo](../../relational-databases/databases/shrink-a-file.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
 [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)   
 [Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  

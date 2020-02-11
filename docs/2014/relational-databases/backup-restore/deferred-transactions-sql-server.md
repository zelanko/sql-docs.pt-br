---
title: Transações adiadas (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- I/O [SQL Server], database recovery
- restoring pages [SQL Server]
- deferred transactions
- modifying transaction deferred state
ms.assetid: 6fc0f9b6-d3ea-4971-9f27-d0195d1ff718
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e36b6c114e7e5f2f95c0747d6e36e4dabc118daa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62876207"
---
# <a name="deferred-transactions-sql-server"></a>Transações adiadas (SQL Server)
  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise, uma transação corrompida poderá ser adiada se os dados necessários na reversão (desfazer) estiverem offline durante a inicialização do banco de dados. Uma *transação adiada* é uma transação que não está confirmada no término da fase de roll forward e que encontrou um erro que impede a reversão. Como a transação não pode ser revertida, é adiada.  
  
> [!NOTE]  
>  Transações corrompidas só são adiadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise. Em outras edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma transação corrompida causa falha na inicialização.  
  
 Geralmente, uma transação adiada ocorre porque, enquanto o roll forward do banco de dados estava sendo efetuado, um erro de E/S impediu a leitura de uma página exigida pela transação. Porém, um erro no arquivo também pode causar transações adiadas. Uma transação adiada também pode ocorrer quando uma sequência de restauração parcial para em um ponto em que a reversão de transação é necessária e uma transação requer dados que estão offline.  
  
 Transações de usuário que estão sendo revertidas e encontram um erro de E/S fazem com que todo o banco de dados fique offline. Quando o banco de dados volta a ficar online, essa ação faz com que ele readquira todos os bloqueios que tinha e tente reverter todas as transações não confirmadas. Todos os dados modificados por uma transação permanecem adequadamente bloqueados até que a transação possa ser revertida. Transações que não podem ser revertidas perderão seus bloqueios quando o dano for reparado e o banco de dados reinicializado ou, após uma restauração online, quando as transações adiadas são resolvidas enquanto o banco de dados permanece online. Até esse ponto, uma transação adiada pode manter bloqueios que impedem certas operações no banco de dados como um todo. Por exemplo, se uma transação adiada contiver uma instrução CREATE TABLE, nenhum usuário poderá criar uma tabela até que a transação adiada tenha sido resolvida.  
  
 Uma transação adiada também pode ocorrer quando uma restauração por etapas recupera um banco de dados em um ponto no qual uma ou mais transações ativas estejam afetando um grupo de arquivos que ainda não tenha sido restaurado e está offline. Como as transações não podem ser revertidas, são adiadas.  
  
 A tabela a seguir lista as ações que fazem com que um banco de dados execute uma recuperação e o resultado da ocorrência de um problema de E/S.  
  
|Ação|Resolução (se ocorrerem problemas de E/S ou se os dados exigidos estiverem offline)|  
|------------|-----------------------------------------------------------------------|  
|Inicialização do servidor|transação adiada|  
|Restaurar|transação adiada|  
|Anexar|Falha ao anexar|  
|Reinicialização automática|transação adiada|  
|Criar banco de dados ou instantâneo do banco de dados|Falha ao criar|  
|Refazer espelhamento de banco de dados|transação adiada|  
|O grupo de arquivos está offline|transação adiada|  
  
## <a name="moving-a-transaction-out-of-the-deferred-state"></a>Removendo uma transação do estado DEFERRED  
  
> [!IMPORTANT]  
>  As transações adiadas mantêm o log de transações ativo. Um arquivo de log virtual que contém qualquer transação adiada não pode ser truncado até que essas transações sejam removidas do estado adiado. Para obter mais informações sobre o truncamento de log, veja [O log de transações &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md).  
  
 Para remover a transação do estado adiado, o banco de dados deve ser inicializado de forma limpa sem qualquer erro de E/S. Se houver transações adiadas, será necessário reparar a origem dos erros de E/S. As soluções disponíveis, listadas na ordem em que são geralmente usadas, são as seguintes:  
  
-   Reinicialize o banco de dados. Se o problema foi temporário, o banco de dados deverá reinicializar sem transações adiadas.  
  
-   Se as transações foram adiadas porque um grupo de arquivos estava offline, coloque o grupo de arquivos online.  
  
     Para colocar um grupo de arquivos offline online, use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    RESTORE DATABASE database_name FILEGROUP=<filegroup_name>  
    ```  
  
-   Restaure o banco de dados. Após a restauração online, qualquer transação adiada estará resolvida.  
  
     No modelo de recuperação completa ou bulk-logged, se as transações adiadas foram causadas somente por algumas páginas corrompidas, uma restauração de página online poderá resolver os erros (onde houver suporte).  
  
-   Se você não precisar mais de um grupo de arquivos cujo status offline esteja causando transações adiadas, exclua o grupo de arquivos offline. Transações que foram adiadas porque o grupo de arquivos estava offline são removidas desse estado depois que o grupo de arquivos é considerado extinto.  
  
    > [!IMPORTANT]  
    >  Um grupo de arquivos extinto nunca pode ser recuperado.  
  
     Para obter mais informações, veja [Remover grupos de arquivos expirados &#40;SQL Server&#41;](remove-defunct-filegroups-sql-server.md).  
  
-   Se as transações foram adiadas por causa de uma página corrompida e se não existir um bom backup do banco de dados, use o processo a seguir para reparar o banco de dados:  
  
    -   Primeiro, coloque o banco de dados em modo de emergência executando a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
        ```  
        ALTER DATABASE <database_name> SET EMERGENCY  
        ```  
  
         Para obter informações sobre o modo de emergência, consulte [Database States](../databases/database-states.md).  
  
    -   Em seguida, repare o banco de dados usando a opção DBCC REPAIR_ALLOW_DATA_LOSS em uma das seguintes instruções DBCC: [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql), [DBCC CHECKALLOC](/sql/t-sql/database-console-commands/dbcc-checkalloc-transact-sql)ou [DBCC CHECKTABLE](/sql/t-sql/database-console-commands/dbcc-checktable-transact-sql).  
  
         Quando a DBCC encontra a página corrompida, anula sua alocação e repara qualquer erro relacionado. Essa abordagem permite que o banco de dados seja colocado novamente online, em um estado fisicamente consistente. Porém, dados adicionais também podem ser perdidos; portanto essa abordagem deve ser usada como último recurso.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [Remover grupos de arquivos expirados &#40;SQL Server&#41;](remove-defunct-filegroups-sql-server.md)   
 [Restaurações de arquivo &#40;Modelo de recuperação completa&#41;](file-restores-full-recovery-model.md)   
 [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](file-restores-simple-recovery-model.md)   
 [Restaurar páginas &#40;SQL Server&#41;](restore-pages-sql-server.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  

---
title: Severidades de erros do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- user-defined error messages [SQL Server]
- severity levels [SQL Server]
- retrieving error severity
- errors [SQL Server], severity
- TRY...CATCH [SQL Server]
ms.assetid: 3e7f5925-6edd-42e1-bf17-f7deb03993a7
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d5c5a6ddee7f8d5e9b734651fa7722df56349db
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="database-engine-error-severities"></a>Severidade dos erros do Mecanismo de Banco de Dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando um erro é gerado pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], sua severidade indica o tipo de problema encontrado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="levels-of-severity"></a>Níveis de severidade  
 A tabela a seguir lista e descreve os níveis de severidade dos erros gerados pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
|Nível de severidade|Descrição|  
|--------------------|-----------------|  
|0-9|Mensagens informativas que retornam informações de status ou reportam erros que não sejam severos. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não gera erros de sistema com severidades de 0 a 9.|  
|10|Mensagens informativas que retornam informações de status ou reportam erros que não sejam severos. Por razões de compatibilidade, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] converte a severidade 10 em severidade 0 antes de retornar as informações de erro ao aplicativo de chamada.|  
|11-16|Indica erros que podem ser corrigidos pelo usuário.|  
|11|Indica que um determinado objeto ou entidade não existe.|  
|12|Severidade especial para consultas que não usam bloqueio por causa de dicas de consulta especiais. Em alguns casos, operações de leitura executadas por essas instruções podem resultar em dados inconsistentes, pois os bloqueios não são usados para garantir a consistência.|  
|13|Indica erros de deadlock de transação.|  
|14|Indica erros relacionados à segurança, como uma permissão negada.|  
|15|Indica erros de sintaxe no comando [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|16|Indica erros gerais que podem ser corrigidos pelo usuário.|  
|17-19|Indica erros de software que não podem ser corrigidos pelo usuário. O usuário deve informar o problema ao seu administrador de sistema.|  
|17|Indica que a instrução fez o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ficar sem recursos (como memória, bloqueios ou espaço em disco para o banco de dados) ou exceder algum limite definido pelo administrador de sistema.|  
|18|Indica um problema no software [!INCLUDE[ssDE](../../includes/ssde-md.md)] , mas a instrução conclui a execução e a conexão com a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é mantida. O administrador de sistema deve ser informado sempre que uma mensagem com nível de severidade 18 ocorrer.|  
|19|Indica que um limite do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não configurável foi excedido e que o processo em lotes atual foi encerrado. Mensagens de erro com nível de severidade 19 ou maior pararam a execução do lote atual. Erros de severidade 19 são raros e devem ser corrigidos pelo administrador de sistema ou por seu principal provedor de suporte. Contate seu administrador de sistema quando uma mensagem com severidade de nível 19 ocorrer. Mensagens de erro com nível de severidade de 19 a 25 são gravadas no log de erros.|  
|20-24|Indique problemas de sistema que são erros fatais, ou seja, a tarefa do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que está executando uma instrução ou um lote que não está mais em execução. A tarefa registra informações sobre o que aconteceu e, depois, é encerrada. Na maioria dos casos, a conexão do aplicativo com a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] também pode ser encerrada. Se isso acontecer, dependendo do problema, é possível que o aplicativo não consiga se reconectar.<br /><br /> Mensagens de erro nesse intervalo podem afetar todos os processos que acessam dados no mesmo banco de dados e indicar que um banco de dados ou objeto está danificado. Mensagens de erro com nível de severidade de 19 a 24 são gravadas no log de erros.|  
|20|Indica que uma instrução encontrou um problema. Como o problema afetou apenas a tarefa atual, é improvável que o banco de dados tenha sido danificado.|  
|21|Indica que foi encontrado um problema que afeta todas as tarefas no banco de dados atual, mas é improvável que o banco de dados tenha sido danificado.|  
|22|Indica que a tabela ou o índice especificado na mensagem foi danificado por um problema de software ou hardware.<br /><br /> Erros de severidade de nível 22 raramente ocorrem. Se acontecer, execute o DBCC CHECKDB para determinar se outros objetos no banco de dados também foram danificados. O problema pode ser apenas no cache do buffer e não no próprio disco. Nesse caso, reiniciar a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] corrige o problema. Para continuar trabalhando, você deve reconectar-se à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]; caso contrário, use o DBCC para corrigir o problema. Em alguns casos, pode ser necessário restaurar o banco de dados.<br /><br /> Se a reinicialização da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não corrigir o problema, é porque o problema está no disco. Às vezes, destruir o objeto especificado na mensagem de erro pode resolver o problema. Por exemplo, se a mensagem informar que a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] encontrou uma linha com comprimento 0 em um índice não clusterizado, exclua o índice e crie-o novamente.|  
|23|Indica que a integridade do banco de dados inteiro está em risco por um problema de software ou hardware.<br /><br /> Erros de severidade de nível 23 raramente ocorrem. Se um acontecer, execute o DBCC CHECKDB para determinar a extensão do dano. O problema pode ser apenas no cache e não no próprio disco. Nesse caso, reiniciar a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] corrige o problema. Para continuar trabalhando, você deve reconectar-se à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]; caso contrário, use o DBCC para corrigir o problema. Em alguns casos, pode ser necessário restaurar o banco de dados.|  
|24|Indica uma falha de mídia. O administrador de sistema pode ter que restaurar o banco de dados. Também pode ser necessário contatar o seu fornecedor de hardware.|  
  
## <a name="user-defined-error-message-severity"></a>Severidade da mensagem de erro definida pelo usuário  
 **sp_addmessage** pode ser usado para adicionar mensagens de erro definidas pelo usuário com severidades de 1 a 25 à exibição do catálogo **sys.messages** . Essas mensagens de erro definidas pelo usuário podem ser usadas pelo RAISERROR. Para obter mais informações, veja [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
  
 O RAISERROR pode ser usado para gerar mensagens de erro definidas pelo usuário com severidade de 1 a 25. O RAISERROR pode se referir a uma mensagem de erro definida pelo usuário armazenada na exibição do catálogo **sys.messages** ou criar uma mensagem dinamicamente. Quando a mensagem de erro definida pelo usuário em **sys.messages** é usada durante a geração de um erro, a severidade especificada pelo RAISERROR substitui a severidade especificada em **sys.messages**. Para obter mais informações, consulte [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
## <a name="error-severity-and-trycatch"></a>Severidade do erro e TRY...CATCH  
 Uma construção TRY...CATCH pega todos os erros de execução com severidade acima de 10 que não encerram a conexão do banco de dados.  
  
 Erros com severidade de 0 a 10 são mensagens informativas e não fazem a execução saltar do bloco CATCH de uma construção TRY...CATCH.  
  
 Erros que encerram a conexão do banco de dados, normalmente com severidade de 20 a 25, não são controlados pelo bloco CATCH porque a execução é anulada quando a conexão é encerrada.  
  
 Para obter mais informações, veja [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md).  
  
## <a name="retrieving-error-severity"></a>recuperando a severidade dos erros  
 A função do sistema ERROR_SEVERITY pode ser usada para recuperar a severidade do erro que fez o bloco CATCH de uma construção TRY...CATCH ser executado. ERROR_SEVERITY retorna NULL se chamado de fora do escopo de um bloco CATCH. Para obter mais informações, consulte [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Compreendendo os erros do Mecanismo de Banco de Dados](../../relational-databases/errors-events/understanding-database-engine-errors.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  

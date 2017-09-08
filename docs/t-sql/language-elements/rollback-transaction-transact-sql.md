---
title: ROLLBACK TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROLLBACK TRANSACTION
- ROLLBACK
- ROLLBACK_TSQL
- ROLLBACK_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- ROLLBACK TRANSACTION statement
- erasing data modifications [SQL Server]
- rolling back transactions, ROLLBACK TRANSACTION
- roll back transactions [SQL Server]
- savepoints [SQL Server]
ms.assetid: 6882c5bc-ff74-476a-984b-164aeb036c66
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e31f62560b4061610c0d3c0ec3147110a3e84644
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="rollback-transaction-transact-sql"></a>ROLLBACK TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Reverte uma transação explícita ou implícita ao começo da transação ou a um ponto de salvamento dentro da transação. Você pode usar ROLLBACK TRANSACTION para apagar todas as modificações de dados feitas desde o começo da transação ou até um ponto de salvamento. Ela também libera recursos mantidos pela transação.  
  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ROLLBACK { TRAN | TRANSACTION }   
     [ transaction_name | @tran_name_variable  
     | savepoint_name | @savepoint_variable ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *transaction_name*  
 É o nome atribuído à transação em BEGIN TRANSACTION. *transaction_name* devem estar em conformidade com as regras para identificadores, mas somente os primeiros 32 caracteres do nome da transação são usados. Ao aninhar transações, *transaction_name* deve ser o nome da instrução BEGIN TRANSACTION externa. *transaction_name* é sempre maiusculas e minúsculas, mesmo quando a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não diferencia maiusculas de minúsculas.  
  
 **@***tran_name_variable*  
 É o nome de uma variável definida pelo usuário que contém um nome de transação válido. A variável deve ser declarada com uma **char**, **varchar**, **nchar**, ou **nvarchar** tipo de dados.  
  
 *savepoint_name*  
 É *savepoint_name* de uma instrução SAVE TRANSACTION. *savepoint_name* devem estar em conformidade com as regras para identificadores. Use *savepoint_name* quando uma reversão condicional afetar somente parte da transação.  
  
 **@***savepoint_variable*  
 É o nome de uma variável definida pelo usuário que contém um nome de ponto de salvamento válido. A variável deve ser declarada com uma **char**, **varchar**, **nchar**, ou **nvarchar** tipo de dados.  
  
## <a name="error-handling"></a>Tratamento de erros  
 Uma instrução ROLLBACK TRANSACTION não produz nenhuma mensagem para o usuário. Se forem necessários avisos em procedimentos armazenados ou disparadores, use as instruções RAISERROR ou PRINT. RAISERROR é a instrução preferida por indicar erros.  
  
## <a name="general-remarks"></a>Comentários gerais  
 ROLLBACK TRANSACTION sem um *savepoint_name* ou *transaction_name* reverte ao início da transação. Ao aninhar transações, essa mesma instrução reverte todas as transações internas para a instrução externa BEGIN TRANSACTION. Em ambos os casos, ROLLBACK TRANSACTION reduz a @@TRANCOUNT função do sistema como 0. ROLLBACK TRANSACTION *savepoint_name* não diminui@TRANCOUNT.  
  
 ROLLBACK TRANSACTION não pode referenciar um *savepoint_name* em transações distribuídas iniciadas tanto explicitamente com BEGIN DISTRIBUTED TRANSACTION ou escalonada a partir de uma transação local.  
  
 Uma transação não poderá ser revertida depois que uma instrução COMMIT TRANSACTION tiver sido executada, exceto quando COMMIT TRANSACTION estiver associada com uma transação aninhada que está contida dentro da transação que está sendo revertida. Nesta instância, a transação aninhada também será revertida, mesmo se você tiver emitido um COMMIT TRANSACTION para isto.  
  
 Em uma transação, são permitidos nomes de ponto de salvamento duplicados, mas uma ROLLBACK TRANSACTION que usa o nome de ponto de salvamento duplicado reverte-se somente à SAVE TRANSACTION mais recente usando aquele nome de ponto de salvamento.  
  
## <a name="interoperability"></a>Interoperabilidade  
 Em procedimentos armazenados, instruções ROLLBACK TRANSACTION sem um *savepoint_name* ou *transaction_name* reverter todas as instruções BEGIN TRANSACTION externa. Uma instrução ROLLBACK TRANSACTION em um procedimento armazenado que faz com que @@TRANCOUNT para ter um valor diferente de quando o procedimento armazenado é concluído que o @@TRANCOUNT valor quando o procedimento armazenado foi chamado produz uma mensagem informativa. Essa mensagem não afeta o processamento subsequente.  
  
 Se uma ROLLBACK TRANSACTION for emitida em um disparador:  
  
-   Todas as modificações de dados feitas até aquele ponto na transação atual serão revertidas, incluindo qualquer uma feita pelo disparador.  
  
-   O disparador continua executando todas as instruções restantes depois da instrução ROLLBACK. Se alguma dessas instruções modificar dados, as modificações não serão revertidas. Nenhum disparador aninhado é ativado pela execução dessas instruções restantes.  
  
-   Não são executadas as instruções no lote depois da instrução que ativou o disparador.  
  
 @@TRANCOUNT é incrementada em um quando entrar em um disparador, mesmo quando no modo de confirmação automática. (O sistema trata um disparador como uma transação aninhada implícita.)  
  
 Instruções ROLLBACK TRANSACTION em procedimentos armazenados não afetam instruções subsequentes no lote que chamou o procedimento; instruções subsequentes no lote são executadas. Instruções ROLLBACK TRANSACTION em disparadores finalizam o lote contendo a instrução que ativou o disparador; instruções subsequentes no lote são executadas.  
  
 O efeito de um ROLLBACK em cursores está definido por estas três regras:  
  
1.  Com CURSOR_CLOSE_ON_COMMIT definido como ON, ROLLBACK fecha, mas desaloca todos os cursores abertos.  
  
2.  Com CURSOR_CLOSE_ON_COMMIT definido como OFF, ROLLBACK não afeta nenhum cursor STATIC síncrono aberto ou cursores INSENSITIVE ou cursores STATIC assíncronos que foram completamente populados. Cursores abertos de qualquer outro tipo são fechados, mas não desalocados.  
  
3.  Um erro que termina um lote e gera uma reversão interna desaloca todos os cursores que foram declarados no lote que contém a instrução de erro. Todos os cursores são desalocados, independentemente de seu tipo ou da configuração de CURSOR_CLOSE_ON_COMMIT. Isso inclui cursores declarados em procedimentos armazenados chamados pelo lote com erro. Cursores declarados em um lote anterior ao lote com erro estão sujeitos às regras 1 e 2. Um erro de deadlock é um exemplo desse tipo de erro. Uma instrução ROLLBACK emitida em um disparador também gera automaticamente esse tipo de erro.  
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
 Uma instrução ROLLBACK TRANSACTION que especifica um *savepoint_name* libera qualquer bloqueio adquirido além do ponto de salvamento, exceto escalonamentos e conversões. Esses bloqueios não são liberados e não são revertidos ao modo de bloqueio anterior.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o efeito da reversão de uma transação nomeada.  
  
```  
USE tempdb;  
GO  
CREATE TABLE ValueTable ([value] int;)  
GO  
  
DECLARE @TransactionName varchar(20) = 'Transaction1';  
  
--The following statements start a named transaction,  
--insert two rows, and then roll back  
--the transaction named in the variable @TransactionName.  
--Another statement outside of the named transaction inserts two rows.  
--The query returns the results of the previous statements.  
  
BEGIN TRAN @TransactionName  
       INSERT INTO ValueTable VALUES(1), (2);  
ROLLBACK TRAN @TransactionName;  
  
INSERT INTO ValueTable VALUES(3),(4);  
  
SELECT [value] FROM ValueTable;  
  
DROP TABLE ValueTable;  
  
--Results  
--value  
-------------  
--3  
--4  
```  
  
## <a name="see-also"></a>Consulte também  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [TRABALHO de confirmação &#40; Transact-SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK WORK &#40; Transact-SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  


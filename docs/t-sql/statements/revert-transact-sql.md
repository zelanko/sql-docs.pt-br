---
title: REVERTER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REVERT_TSQL
- REVERT
dev_langs:
- TSQL
helpviewer_keywords:
- REVERT statement
- context switching [SQL Server], reverting
- reverting execution context
- REVERT WITH COOKIE statement
- execution context [SQL Server]
- COOKIE clause
ms.assetid: 4688b17a-dfd1-4f03-8db4-273a401f879f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3350f92afbb6d6ed0278a9ae41ee25f5ed4096b0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="revert-transact-sql"></a>REVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Alterna o contexto de execução de volta para o chamador da última instrução EXECUTE AS.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVERT  
    [ WITH COOKIE = @varbinary_variable ]  
```  
  
## <a name="arguments"></a>Argumentos  
 WITH COOKIE = @*varbinary_variable*  
 Especifica o cookie que foi criado no correspondente [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) instrução autônoma. *@varbinary_variable*é **varbinary(100)**.  
  
## <a name="remarks"></a>Comentários  
 REVERT pode ser especificado dentro de um módulo como um procedimento armazenado ou uma função definida pelo usuário ou como uma instrução autônoma. Quando especificado dentro de um módulo, REVERT só é aplicável às instruções EXECUTE AS definidas no módulo. Por exemplo, o procedimento armazenado a seguir emite uma instrução `EXECUTE AS` seguida por uma instrução `REVERT`.  
  
```  
CREATE PROCEDURE dbo.usp_myproc   
  WITH EXECUTE AS CALLER  
AS   
    SELECT SUSER_NAME(), USER_NAME();  
    EXECUTE AS USER = 'guest';  
    SELECT SUSER_NAME(), USER_NAME();  
    REVERT;  
    SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
 Suponha que, na sessão em que o procedimento armazenado é executado, o contexto de execução da sessão seja explicitamente alterado para `login1`, como mostra o exemplo a seguir.  
  
```  
  -- Sets the execution context of the session to 'login1'.  
EXECUTE AS LOGIN = 'login1';  
GO  
EXECUTE dbo.usp_myproc;   
```  
  
 O `REVERT` instrução que é definida dentro de `usp_myproc` alterna o contexto de execução definido dentro do módulo, mas não afeta o contexto de execução definido fora do módulo. Isto é, o contexto de execução para a sessão permanece definido como `login1`.  
  
 Quando especificado como uma instrução autônoma, REVERT se aplica às instruções EXECUTE AS definidas dentro de um lote ou de uma sessão. REVERT não tem nenhum efeito se a instrução EXECUTE AS correspondente tiver uma cláusula WITH NO REVERT. Nesse caso, o contexto de execução permanece em efeito até que a sessão seja descartada.  
  
## <a name="using-revert-with-cookie"></a>Usando REVERT WITH COOKIE  
 EXECUTE como a instrução que é usada para definir o contexto de execução de uma sessão pode incluir a cláusula opcional WITH NO REVERT COOKIE = @*varbinary_variabl*e. Quando essa instrução é executada, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] passa o cookie para @*varbinary_variabl*e. O contexto de execução definido por essa instrução só poderá ser revertida para o contexto anterior se a chamada REVERT WITH COOKIE = @*varbinary_variable* instrução contém corretas  *@varbinary_variable*  valor.  
  
 Esse mecanismo é útil em um ambiente no qual um pool de conexão é usado. O pool de conexão é a manutenção de um grupo de conexões de banco de dados para reutilização por aplicativos por vários usuários finais. Como o valor passado para  *@varbinary_variable*  é conhecido apenas pelo chamador da execução de instrução (nesse caso, o aplicativo), o chamador pode garantir que o contexto de execução estabelecido não pode ser alterado pelo usuário final que invoca o aplicativo. Depois que o contexto de execução é revertido, o aplicativo pode alterná-lo para outra entidade.  
  
## <a name="permissions"></a>Permissões  
 Nenhuma permissão é necessária.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-execute-as-and-revert-to-switch-context"></a>A. Usando EXECUTE AS e REVERT para alternar o contexto  
 O exemplo a seguir cria uma pilha de execução de contexto usando várias entidades. A instrução REVERT é usada para redefinir o contexto de execução para o chamador anterior. A instrução REVERT é executada várias vezes movendo a pilha para cima até o contexto de execução ser definido como o chamador original.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create two temporary principals.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE LOGIN login2 WITH PASSWORD = 'Uor80$23b';  
GO  
CREATE USER user1 FOR LOGIN login1;  
CREATE USER user2 FOR LOGIN login2;  
GO  
-- Give IMPERSONATE permissions on user2 to user1  
-- so that user1 can successfully set the execution context to user2.  
GRANT IMPERSONATE ON USER:: user2 TO user1;  
GO  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- Set the execution context to login1.   
EXECUTE AS LOGIN = 'login1';  
-- Verify that the execution context is now login1.  
SELECT SUSER_NAME(), USER_NAME();  
-- Login1 sets the execution context to login2.  
EXECUTE AS USER = 'user2';  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- The execution context stack now has three principals: the originating caller, login1, and login2.  
-- The following REVERT statements will reset the execution context to the previous context.  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
  
-- Remove the temporary principals.  
DROP LOGIN login1;  
DROP LOGIN login2;  
DROP USER user1;  
DROP USER user2;  
GO  
```  
  
### <a name="b-using-the-with-cookie-clause"></a>B. Usando a cláusula WITH COOKIE  
 O exemplo a seguir define o contexto de execução de uma sessão para um usuário especificado e especifica o WITH NO REVERT COOKIE = @*varbinary_variabl*cláusula. A instrução `REVERT` deve especificar o valor passado para a variável `@cookie` na instrução `EXECUTE AS` para reverter com êxito o contexto de volta para o chamador. Para executar este exemplo, o logon `login1` e o usuário `user1` criados no exemplo A devem existir.  
  
```  
DECLARE @cookie varbinary(100);  
EXECUTE AS USER = 'user1' WITH COOKIE INTO @cookie;  
-- Store the cookie somewhere safe in your application.  
-- Verify the context switch.  
SELECT SUSER_NAME(), USER_NAME();  
--Display the cookie value.  
SELECT @cookie;  
GO  
-- Use the cookie in the REVERT statement.  
DECLARE @cookie varbinary(100);  
-- Set the cookie value to the one from the SELECT @cookie statement.  
SET @cookie = <value from the SELECT @cookie statement>;  
REVERT WITH COOKIE = @cookie;  
-- Verify the context switch reverted.  
SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [EXECUTE AS &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SUSER_NAME &#40; Transact-SQL &#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [User_name &#40; Transact-SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
  

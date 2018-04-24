---
title: SET CURSOR_CLOSE_ON_COMMIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CURSOR_CLOSE_ON_COMMIT
- SET CURSOR_CLOSE_ON_COMMIT
- CURSOR_CLOSE_ON_COMMIT_TSQL
- SET_CURSOR_CLOSE_ON_COMMIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CURSOR_CLOSE_ON_COMMIT option
- transactions [SQL Server], cursors
- closing cursors
- cursors [SQL Server], closing
- SET CURSOR_CLOSE_ON_COMMIT statement
ms.assetid: 7b976154-98ce-4a06-bbae-7e59c34211f7
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab7a9211d441ace6895472a869e337ba999c7927
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="set-cursorcloseoncommit-transact-sql"></a>SET CURSOR_CLOSE_ON_COMMIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Controla o comportamento da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] COMMIT TRANSACTION. O valor padrão dessa configuração é OFF. Isso significa que o servidor não fechará os cursores quando você confirmar uma transação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 Quando SET CURSOR_CLOSE_ON_COMMIT for ON, esta configuração fecha qualquer cursor aberto em confirmação ou reversão em conformidade com a ISO. Quando SET CURSOR_CLOSE_ON_COMMIT for OFF, o cursor não será fechado quando uma transação estiver confirmada.  
  
> [!NOTE]  
>  SET CURSOR_CLOSE_ON_COMMIT como ON não fechará cursores abertos em reversão quando a reversão for aplicada a um savepoint_name de uma instrução SAVE TRANSACTION.  
  
 Quando SET CURSOR_CLOSE_ON_COMMIT for OFF, uma instrução ROLLBACK fechará apenas cursores assíncronos abertos que não estejam totalmente populados. Cursores STATIC ou INSENSITIVE abertos depois que modificações foram feitas não refletirão o estado dos dados se as modificações forem revertidas.  
  
 SET CURSOR_CLOSE_ON_COMMIT controla o mesmo comportamento que a opção de banco de dados a CURSOR_CLOSE_ON_COMMIT. Se CURSOR_CLOSE_ON_COMMIT for definido como ON ou OFF, essa configuração será usada na conexão. Se SET CURSOR_CLOSE_ON_COMMIT não for especificado, o valor na coluna **is_cursor_close_on_commit_on** na exibição do catálogo **sys.databases** será aplicado.  
  
 O Provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o driver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC definem CURSOR_CLOSE_ON_COMMIT como OFF na conexão. A biblioteca de banco de dados não define o valor de CURSOR_CLOSE_ON_COMMIT automaticamente.  
  
 Quando SET ANSI_DEFAULTS for ON, SET CURSOR_CLOSE_ON_COMMIT é habilitado.  
  
 A configuração de SET CURSOR_CLOSE_ON_COMMIT é definida no momento da execução e não no momento da análise.  
  
 Para exibir a configuração atual dessa configuração, execute a consulta a seguir.  
  
```  
DECLARE @CURSOR_CLOSE VARCHAR(3) = 'OFF';  
IF ( (4 & @@OPTIONS) = 4 ) SET @CURSOR_CLOSE = 'ON';  
SELECT @CURSOR_CLOSE AS CURSOR_CLOSE_ON_COMMIT;  
```  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define um cursor em uma transação e tentativas de usá-lo depois que a transação for confirmada.  
  
```  
-- SET CURSOR_CLOSE_ON_COMMIT  
-------------------------------------------------------------------------------  
SET NOCOUNT ON;  
  
CREATE TABLE t1 (a INT);  
GO   
  
INSERT INTO t1   
VALUES (1), (2);  
GO  
  
PRINT '-- SET CURSOR_CLOSE_ON_COMMIT ON';  
GO  
SET CURSOR_CLOSE_ON_COMMIT ON;  
GO  
PRINT '-- BEGIN TRAN';  
BEGIN TRAN;  
PRINT '-- Declare and open cursor';  
DECLARE testcursor CURSOR FOR  
    SELECT a FROM t1;  
OPEN testcursor;  
PRINT '-- Commit tran';  
COMMIT TRAN;  
PRINT '-- Try to use cursor';  
FETCH NEXT FROM testcursor;  
CLOSE testcursor;  
DEALLOCATE testcursor;  
GO  
PRINT '-- SET CURSOR_CLOSE_ON_COMMIT OFF';  
GO  
SET CURSOR_CLOSE_ON_COMMIT OFF;  
GO  
PRINT '-- BEGIN TRAN';  
BEGIN TRAN;  
PRINT '-- Declare and open cursor';  
DECLARE testcursor CURSOR FOR  
    SELECT a FROM t1;  
OPEN testcursor;  
PRINT '-- Commit tran';  
COMMIT TRAN;  
PRINT '-- Try to use cursor';  
FETCH NEXT FROM testcursor;  
CLOSE testcursor;  
DEALLOCATE testcursor;  
GO  
DROP TABLE t1;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  

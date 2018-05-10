---
title: RETURN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- RETURN_TSQL
- RETURN
dev_langs:
- TSQL
helpviewer_keywords:
- unconditionally exiting program
- stored procedures [SQL Server], exiting
- batches [SQL Server], exiting
- statement blocks [SQL Server]
- queries [SQL Server], exiting
- exiting queries [SQL Server]
- exiting procedures [SQL Server]
- RETURN statement
ms.assetid: 1d9c8247-fd89-4544-be9c-01c95b745db0
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 19363e04e6dd514a139a35c018b3785accb7f25d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="return-transact-sql"></a>RETURN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Sai incondicionalmente de uma consulta ou procedimento. RETURN é imediato e completo e pode ser usado em qualquer ponto para sair de um procedimento, lote ou bloco de instruções. As instruções posteriores a RETURN não são executadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETURN [ integer_expression ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression*  
 É o valor inteiro que é retornado. Os procedimentos armazenados podem retornar um valor inteiro a um procedimento de chamada ou um aplicativo.  
  
## <a name="return-types"></a>Tipos de retorno  
 Opcionalmente, retorna **int**.  
  
> [!NOTE]  
>  A menos que seja documentado o contrário, todos os procedimentos armazenados de sistema retornam o valor 0. Isto indica sucesso e um valor diferente de zero indica falha.  
  
## <a name="remarks"></a>Remarks  
 Quando usado com um procedimento armazenado, RETURN não pode retornar um valor nulo. Se um procedimento tentar retornar um valor nulo (por exemplo, usando @status quando @status for NULL), será gerada uma mensagem de aviso, e o valor 0 será retornado.  
  
 O valor do status de retorno pode ser incluído em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] subsequentes no lote ou no procedimento que executou o procedimento atual, mas ele deve ser inserido no seguinte formato: `EXECUTE @return_status = <procedure_name>`.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-from-a-procedure"></a>A. Retornando de um procedimento  
 O exemplo a seguir mostra que se nenhum nome de usuário estiver especificado como um parâmetro quando `findjobs` for executado, `RETURN` fará com que o procedimento seja encerrado depois que uma mensagem for enviada à tela do usuário. Se um nome de usuário for especificado, os nomes de todos os objetos criados por esse usuário no banco de dados atual serão recuperados das tabelas do sistema apropriadas.  
  
```  
CREATE PROCEDURE findjobs @nm sysname = NULL  
AS   
IF @nm IS NULL  
    BEGIN  
        PRINT 'You must give a user name'  
        RETURN  
    END  
ELSE  
    BEGIN  
        SELECT o.name, o.id, o.uid  
        FROM sysobjects o INNER JOIN master..syslogins l  
            ON o.uid = l.sid  
        WHERE l.name = @nm  
    END;  
```  
  
### <a name="b-returning-status-codes"></a>B. Retornando códigos de status  
 O exemplo a seguir verifica o estado do ID de um contato especificado. Se o estado for Washington (`WA`), um status `1` será retornado. Caso contrário, `2` será retornado para qualquer outra condição (um valor diferente de `WA` para `StateProvince` ou `ContactID` que não correspondeu a uma linha).  
  
```  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE checkstate @param varchar(11)  
AS  
IF (SELECT StateProvince FROM Person.vAdditionalContactInfo WHERE ContactID = @param) = 'WA'  
    RETURN 1  
ELSE  
    RETURN 2;  
GO  
```  
  
 Os exemplos a seguir mostram o status de retorno da execução de `checkstate`. O primeiro mostra um contato em Washington; o segundo, um contato que não é de Washington; e o terceiro, um contato que não é válido. A variável local `@return_status` deve ser declarada antes que possa ser usada.  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '2';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status 
  
 ------------- 
  
 1
 ```  
  
 Executar a consulta novamente, especificando um número de contato diferente.  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '6';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
 Executar a consulta novamente, especificando outro número de contato.  
  
```  
DECLARE @return_status int  
EXEC @return_status = checkstate '12345678901';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)   
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)  
  
  

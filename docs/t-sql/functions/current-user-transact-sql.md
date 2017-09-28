---
title: CURRENT_USER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURRENT_USER
- CURRENT_USER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- current user names
- niladic functions
- CURRENT_USER
- users [SQL Server], names
ms.assetid: 29248949-325b-4063-9f55-5a445fb35c6e
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9edbc344723da335de150f5e829820eaef1d983e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="currentuser-transact-sql"></a>CURRENT_USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna o nome do usuário atual. Esta função é equivalente a USER_NAME().
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CURRENT_USER  
```  

## <a name="return-types"></a>Tipos de retorno
**sysname**
  
## <a name="remarks"></a>Comentários  
CURRENT_USER retorna o nome do contexto de segurança atual. Se CURRENT_USER for executado depois que uma chamada para EXECUTE AS alternar o contexto, CURRENT_USER retornará o nome do contexto representado. Se uma entidade de segurança do Windows acessou o banco de dados por meio de associação em um grupo, o nome da entidade de segurança do Windows será retornado em vez do nome do grupo.
  
Para retornar o logon do usuário atual, consulte [SUSER_NAME &#40; Transact-SQL &#41; ](../../t-sql/functions/suser-name-transact-sql.md) e [SYSTEM_USER &#40; Transact-SQL &#41; ](../../t-sql/functions/system-user-transact-sql.md).
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-currentuser-to-return-the-current-user-name"></a>A. Usando CURRENT_USER para retornar o nome do usuário atual  
O exemplo a seguir retorna o nome do usuário atual.
  
```sql
SELECT CURRENT_USER;  
GO  
```  
  
### <a name="b-using-currentuser-as-a-default-constraint"></a>B. Usando CURRENT_USER como uma restrição DEFAULT  
O exemplo a seguir cria uma tabela que usa `CURRENT_USER` como uma restrição `DEFAULT` para a coluna `order_person` em uma linha de vendas.
  
```sql
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
      WHERE TABLE_NAME = 'orders22')  
   DROP TABLE orders22;  
GO  
SET NOCOUNT ON;  
CREATE TABLE orders22  
(  
order_id int IDENTITY(1000, 1) NOT NULL,
cust_id  int NOT NULL,
order_date smalldatetime NOT NULL DEFAULT GETDATE(),
order_amt money NOT NULL,
order_person char(30) NOT NULL DEFAULT CURRENT_USER
);  
GO  
```  
  
O código a seguir insere um registro na tabela. O usuário que está executando essas instruções se chama `Wanida`.
  
```sql
INSERT orders22 (cust_id, order_amt)  
VALUES (5105, 577.95);  
GO  
SET NOCOUNT OFF;  
GO  
```  
  
A consulta a seguir seleciona todas as informações da tabela `orders22`.
  
```sql
SELECT * FROM orders22;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`order_id    cust_id     order_date           order_amt    order_person`
  
`----------- ----------- -------------------- ------------ ------------`
  
`1000        5105        2005-04-03 23:34:00  577.95       Wanida`
  
`(1 row(s) affected)`
  
### <a name="c-using-currentuser-from-an-impersonated-context"></a>C. Usando CURRENT_USER em um contexto representado  
No exemplo a seguir, o usuário `Wanida` executa o seguinte código [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
```sql
SELECT CURRENT_USER;  
GO  
EXECUTE AS USER = 'Arnalfo';  
GO  
SELECT CURRENT_USER;  
GO  
REVERT;  
GO  
SELECT CURRENT_USER;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`Wanida`
  
`Arnalfo`
  
`Wanida`
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-currentuser-to-return-the-current-user-name"></a>Unidade d: usando CURRENT_USER para retornar o nome de usuário atual  
O exemplo a seguir retorna o nome do usuário atual.
  
```sql
SELECT CURRENT_USER;  
```  
  
## <a name="see-also"></a>Consulte também
[User_name &#40; Transact-SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)  
[SYSTEM_USER &#40; Transact-SQL &#41;](../../t-sql/functions/system-user-transact-sql.md)  
[sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Funções do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  



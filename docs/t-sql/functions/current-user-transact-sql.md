---
title: CURRENT_USER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 29765164d6eb5e677c307091cf37aa8623674f00
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="currentuser-transact-sql"></a>CURRENT_USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Essa função retorna o nome do usuário atual. Essa função é equivalente a `USER_NAME()`.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CURRENT_USER  
```  

## <a name="return-types"></a>Tipos de retorno
**sysname**
  
## <a name="remarks"></a>Remarks  
`CURRENT_USER` retorna o nome do contexto de segurança atual. Se `CURRENT_USER` for executado após uma chamada para o contexto de comutadores `EXECUTE AS`, `CURRENT_USER` retornará o nome do contexto representado. Se uma entidade de segurança do Windows tiver acessado o banco de dados por meio da associação em um grupo, `CURRENT_USER` retornará a entidade de segurança do Windows em vez do nome do grupo.
  
Veja [SUSER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-name-transact-sql.md) e [SYSTEM_USER &#40;Transact-SQL&#41;](../../t-sql/functions/system-user-transact-sql.md) para saber como retornar o logon do usuário atual.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-currentuser-to-return-the-current-user-name"></a>A. Usando CURRENT_USER para retornar o nome do usuário atual  
Este exemplo retorna o nome do usuário atual.
  
```sql
SELECT CURRENT_USER;  
GO  
```  
  
### <a name="b-using-currentuser-as-a-default-constraint"></a>B. Usando CURRENT_USER como uma restrição DEFAULT  
Este exemplo cria uma tabela que usa `CURRENT_USER` como uma restrição `DEFAULT` para a coluna `order_person` em uma linha de vendas.
  
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
  
Este exemplo insere um registro na tabela. O usuário chamado `Wanida` executa essas instruções.
  
```sql
INSERT orders22 (cust_id, order_amt)  
VALUES (5105, 577.95);  
GO  
SET NOCOUNT OFF;  
GO  
```  
  
Essa consulta seleciona todas as informações da tabela `orders22`.
  
```sql
SELECT * FROM orders22;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
order_id    cust_id     order_date           order_amt    order_person
----------- ----------- -------------------- ------------ ------------
1000        5105        2005-04-03 23:34:00  577.95       Wanida
  
(1 row(s) affected)
```
  
### <a name="c-using-currentuser-from-an-impersonated-context"></a>C. Usando CURRENT_USER em um contexto representado  
Neste exemplo, o usuário `Wanida` executa o seguinte código [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
```sql
SELECT CURRENT_USER;  
GO  
EXECUTE AS USER = 'Wanida';  
GO  
SELECT CURRENT_USER;  
GO  
REVERT;  
GO  
SELECT CURRENT_USER;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Wanida
Arnalfo
Wanida
```
  
## <a name="see-also"></a>Confira também
[USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)  
[SYSTEM_USER &#40;Transact-SQL&#41;](../../t-sql/functions/system-user-transact-sql.md)  
[sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  


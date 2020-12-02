---
description: APPLOCK_TEST (Transact-SQL)
title: APPLOCK_TEST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APPLOCK_TEST_TSQL
- APPLOCK_TEST
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- APPLOCK_TEST function
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- testing application locks
ms.assetid: 4ea33d04-f8e9-46ff-ae61-985bd3eaca2c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ae3fc6e47bcb375122be6e045c36b5e5f08c2cc0
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124930"
---
# <a name="applock_test-transact-sql"></a>APPLOCK_TEST (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Essa função retorna informações sobre ser possível ou não conceder um bloqueio em um recurso de aplicativo específico para um proprietário de bloqueio especificado, sem aquisição do bloqueio. Como uma função de bloqueio de aplicativo, a APPLOCK_TEST opera no banco de dados atual. O banco de dados é o escopo dos bloqueios de aplicativo.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
APPLOCK_TEST ( 'database_principal' , 'resource_name' , 'lock_mode' , 'lock_owner' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
**'** *database_principal* **'**  
O usuário, a função ou a função de aplicativo que pode receber permissões para objetos no banco de dados. Para chamar a função com êxito, o chamador da função deve ser membro de *database_principal*, dbo, ou a função de banco de dados fixa db_owner.
  
**'** *resource_name* **'**  
Um nome de recurso de bloqueio especificado pelo aplicativo cliente. O aplicativo deve garantir um nome do recurso exclusivo. O nome especificado passa internamente por hash, tornando-se um valor que o gerenciador de bloqueio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode armazenar internamente.  *resource_name* é **nvarchar(255)** , sem nenhum padrão. *resource_name* é comparado com binário comparado e diferencia maiúsculas de minúsculas, independentemente das configurações de ordenação do banco de dados atual.
  
**'** *lock_mode* **'**  
O modo de bloqueio a ser obtido para um recurso específico. *lock_mode* é **nvarchar(32)**, sem nenhum valor padrão. *lock_mode* pode ter qualquer um destes valores: **Shared**, **Update**, **IntentShared**, **IntentExclusive**, **Exclusive**.
  
**'** *lock_owner* **'**  
O proprietário do bloqueio, que é o valor de *lock_owner* quando o bloqueio foi solicitado. *lock_owner* é **nvarchar(32)** e o valor pode ser **Transaction** (o padrão) ou **Session**. Se o padrão ou **Transaction** for especificado explicitamente, APPLOCK_TEST deverá ser executado de uma transação.
  
## <a name="return-types"></a>Tipos de retorno
**smallint**
  
## <a name="return-value"></a>Valor retornado
0 se o bloqueio não puder ser concedido ao proprietário especificado, ou 1 se o bloqueio puder ser concedido.
  
## <a name="function-properties"></a>Propriedades da função
**Não determinístico**
  
**Não indexável**
  
**Não paralelizável**
  
## <a name="examples"></a>Exemplos  
Dois usuários (**Usuário A** e **Usuário B**), com sessões separadas, executam a seguinte sequência de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
**Usuário A** executa:
  
```sql
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result INT;  
EXEC @result=sp_getapplock  
    @DbPrincipal='public',  
    @Resource='Form1',  
    @LockMode='Shared',  
    @LockOwner='Transaction';  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
GO  
```  
  
O **Usuário B** então executa:
  
```sql
Use AdventureWorks2012;  
GO  
BEGIN TRAN;  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
--Result set: NoLock  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Shared', 'Transaction');  
--Result set: 1 (Lock is grantable.)  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: 0 (Lock is not grantable.)  
GO  
```  
  
Então, o **Usuário A** executa:
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
O **Usuário B** então executa:
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
**Usuário A** e **Usuário B** executam:
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>Confira também
[APPLOCK_MODE &#40;Transact-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)  
[sp_getapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)

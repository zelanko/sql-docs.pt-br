---
title: APPLOCK_TEST (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a272abaccb41653c9b1b0569738b74905e93e5c9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="applocktest-transact-sql"></a>APPLOCK_TEST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna informações sobre o fato de ser possível ou não conceder um bloqueio em um recurso de aplicativo específico para um proprietário de bloqueio especificado, sem adquirir o bloqueio. APPLOCK_TEST é uma função de bloqueio de aplicativo e opera no banco de dados atual. O escopo de bloqueios de aplicativo é o banco de dados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
APPLOCK_TEST ( 'database_principal' , 'resource_name' , 'lock_mode' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>Argumentos  
**'** *database_principal* **'**  
É o usuário, a função ou a função de aplicativo que pode receber permissões para objetos no banco de dados. O chamador da função deve ser um membro do *database_principal*, **dbo**, ou o **db_owner** função de banco de dados fixa para chamar a função com êxito.
  
**'** *resource_name* **'**  
É um nome de recurso de bloqueio especificado pelo aplicativo cliente. O aplicativo deve garantir que o recurso seja exclusivo. O nome especificado é internamente transformado em hash para um valor que pode ser armazenado no gerenciador de bloqueio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *resource_name*é **nvarchar (255)** sem nenhum padrão. *resource_name* é binário comparado e diferencia maiusculas de minúsculas, independentemente das configurações de agrupamento do banco de dados atual.
  
**'** *lock_mode* **'**  
É o modo de bloqueio a ser obtido para um recurso específico. *lock_mode* é **nvarchar (32)** e não tem valor padrão. O valor pode ser qualquer um dos seguintes: **compartilhado**, **atualização**, **IntentShared**, **IntentExclusive**, **exclusivo** .
  
**'** *lock_owner* **'**  
É o proprietário do bloqueio, que é o *lock_owner* valor quando o bloqueio foi solicitado. *lock_owner* é **nvarchar (32)**. O valor pode ser **transação** (o padrão) ou **sessão**. Se padrão ou **transação** for especificado explicitamente, APPLOCK_TEST deverá ser executado de dentro de uma transação.
  
## <a name="return-types"></a>Tipos de retorno
**smallint**
  
## <a name="return-value"></a>Valor de retorno
Retorna 0 quando o bloqueio não puder ser concedido ao proprietário especificado e retorna 1 se o bloqueio puder ser concedido.
  
## <a name="function-properties"></a>Propriedades de função
**Não determinístico**
  
**Não indexável**
  
**Não Paralelizável**
  
## <a name="examples"></a>Exemplos  
No exemplo a seguir, dois usuários (**usuário** e **usuário B**) com sessões separadas executam a seguinte sequência de [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções.
  
**O usuário A** executa:
  
```sql
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result=sp_getapplock  
    @DbPrincipal='public',  
    @Resource='Form1',  
    @LockMode='Shared',  
    @LockOwner='Transaction';  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
GO  
```  
  
**O usuário B** executa:
  
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
  
**O usuário A** executa:
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
**O usuário B** executa:
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
**O usuário A** e **usuário B** e executam a ambas:
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>Consulte também
[APPLOCK_MODE &#40; Transact-SQL &#41;](../../t-sql/functions/applock-mode-transact-sql.md)  
[sp_getapplock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  


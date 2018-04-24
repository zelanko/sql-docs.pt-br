---
title: APPLOCK_TEST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: 463c6e176cec6c0403e85bc75584e6bd890e0668
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="applocktest-transact-sql"></a>APPLOCK_TEST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Essa função retorna informações sobre ser possível ou não conceder um bloqueio em um recurso de aplicativo específico para um proprietário de bloqueio especificado, sem aquisição do bloqueio. Como uma função de bloqueio de aplicativo, a APPLOCK_TEST opera no banco de dados atual. O banco de dados é o escopo dos bloqueios de aplicativo.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
APPLOCK_TEST ( 'database_principal' , 'resource_name' , 'lock_mode' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>Argumentos  
**'** *database_principal* **'**  
O usuário, a função ou a função de aplicativo que pode receber permissões para objetos no banco de dados. Para chamar a função com êxito, o chamador da função deve ser membro de *database_principal*, dbo, ou a função de banco de dados fixa db_owner.
  
**'** *resource_name* **'**  
Um nome de recurso de bloqueio especificado pelo aplicativo cliente. O aplicativo deve garantir um nome do recurso exclusivo. O nome especificado passa internamente por hash, tornando-se um valor que o gerenciador de bloqueio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode armazenar internamente.  *resource_name* é **nvarchar(255)**, sem nenhum padrão. *resource_name* é comparado com binário comparado e diferencia maiúsculas de minúsculas, independentemente das configurações de agrupamento do banco de dados atual.
  
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
DECLARE @result int;  
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
  
  

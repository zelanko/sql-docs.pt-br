---
title: APPLOCK_MODE (Transact-SQL) | Microsoft Docs
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
- APPLOCK_MODE_TSQL
- APPLOCK_MODE
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- APPLOCK_MODE function
ms.assetid: e43d4917-77f1-45cc-b231-68ba7fee3385
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b6b5c0a0879580e5c1e084259b61ff206d49c896
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="applockmode-transact-sql"></a>APPLOCK_MODE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o modo de bloqueio mantido pelo proprietário de bloqueio em um determinado recurso de aplicativo. APPLOCK_MODE é uma função de bloqueio de aplicativo e opera no banco de dados atual. O escopo de bloqueios de aplicativo é o banco de dados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
APPLOCK_MODE( 'database_principal' , 'resource_name' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>Argumentos  
'*database_principal*'  
É o usuário, a função ou a função de aplicativo que pode receber permissões para objetos no banco de dados. O chamador da função deve ser membro da função de banco de dados fixa *database_principal*, dbo ou db_owner para chamar a função com êxito.
  
'*resource_name*'  
É um nome de recurso de bloqueio especificado pelo aplicativo cliente. O aplicativo deve garantir que o nome do recurso seja exclusivo. O nome especificado é internamente transformado em hash para um valor que pode ser armazenado no gerenciador de bloqueio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *resource_name* é **nvarchar(255)** sem nenhum padrão. *resource_name* é comparado com binário comparado e diferencia maiúsculas de minúsculas, independentemente das configurações de agrupamento do banco de dados atual.
  
'*lock_owner*'  
É o proprietário do bloqueio, que é o valor de *lock_owner* quando o bloqueio foi solicitado. *lock_owner* é **nvarchar(32)** e o valor pode ser **Transaction** (o padrão) ou **Session**.
  
## <a name="return-types"></a>Tipos de retorno
**nvarchar(32)**
  
## <a name="return-value"></a>Valor de retorno
Retorna o modo de bloqueio mantido pelo proprietário de bloqueio em um determinado recurso de aplicativo. O modo de bloqueio pode ser qualquer um destes valores:
  
||||  
|-|-|-|  
|**NoLock**|**Update (atualizar)**|**\*SharedIntentExclusive**|  
|**IntentShared**|**IntentExclusive**|**\*UpdateIntentExclusive**|  
|**Compartilhado**|**Exclusive**||  
  
*Este modo de bloqueio é uma combinação de outros modos de bloqueio e não é adquirido explicitamente usando sp_getapplock.
  
## <a name="function-properties"></a>Propriedades da função
**Não determinístico**
  
**Não indexável**
  
**Não paralelizável**
  
## <a name="examples"></a>Exemplos  
Dois usuários (Usuário A e Usuário B) com sessões separadas executam a seguinte sequência de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
Usuário A executa:
  
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
  
Usuário B executa:
  
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
  
Usuário A executa:
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
Usuário B executa:
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
O Usuário A e o Usuário B executam:
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>Consulte também
[APPLOCK_TEST &#40;Transact-SQL&#41;](../../t-sql/functions/applock-test-transact-sql.md)  
[sp_getapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  

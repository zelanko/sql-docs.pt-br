---
title: APPLOCK_MODE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d3d171d77cf3462eb68893f4ac5f6230d73b8b11
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87113179"
---
# <a name="applock_mode-transact-sql"></a>APPLOCK_MODE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Essa função retorna o modo de bloqueio mantido pelo proprietário de bloqueio em um determinado recurso de aplicativo. Como uma função de bloqueio de aplicativo, a APPLOCK_MODE opera no banco de dados atual. O banco de dados é o escopo dos bloqueios de aplicativo.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
APPLOCK_MODE( 'database_principal' , 'resource_name' , 'lock_owner' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
'*database_principal*'  
O usuário, a função ou a função de aplicativo que pode receber permissões para objetos no banco de dados. Para chamar a função com êxito, o chamador da função deve ser membro de *database_principal*, dbo, ou a função de banco de dados fixa db_owner.
  
'*resource_name*'  
Um nome de recurso de bloqueio especificado pelo aplicativo cliente. O aplicativo deve garantir um nome do recurso exclusivo. O nome especificado passa internamente por hash, tornando-se um valor que o gerenciador de bloqueio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode armazenar internamente. *resource_name* é **nvarchar(255)** , sem nenhum padrão. *resource_name* é comparado com binário comparado e diferencia maiúsculas de minúsculas, independentemente das configurações de ordenação do banco de dados atual.
  
'*lock_owner*'  
O proprietário do bloqueio, que é o valor de *lock_owner* quando o bloqueio foi solicitado. *lock_owner* é **nvarchar(32)** e o valor pode ser **Transaction** (o padrão) ou **Session**.
  
## <a name="return-types"></a>Tipos de retorno
**nvarchar(32)**
  
## <a name="return-value"></a>Valor retornado
Retorna o modo de bloqueio mantido pelo proprietário de bloqueio em um determinado recurso de aplicativo. O modo de bloqueio pode ter qualquer um destes valores:
  
||||  
|-|-|-|  
|**NoLock**|**Atualização**|**\*SharedIntentExclusive**|  
|**IntentShared**|**IntentExclusive**|**\*UpdateIntentExclusive**|  
|**Compartilhado**|**Exclusive**||  
  
*Este modo de bloqueio é uma combinação de outros modos de bloqueio e o sp_getapplock não pode adquiri-lo explicitamente.
  
## <a name="function-properties"></a>Propriedades da função
**Não determinístico**
  
**Não indexável**
  
**Não paralelizável**
  
## <a name="examples"></a>Exemplos  
Dois usuários (Usuário A e Usuário B), com sessões separadas, executam a seguinte sequência de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
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
  
## <a name="see-also"></a>Confira também
[APPLOCK_TEST &#40;Transact-SQL&#41;](../../t-sql/functions/applock-test-transact-sql.md)  
[sp_getapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  

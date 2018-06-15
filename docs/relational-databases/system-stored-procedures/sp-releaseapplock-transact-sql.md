---
title: sp_releaseapplock (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_releaseapplock_TSQL
- sp_releaseapplock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_releaseapplock
ms.assetid: 51b03c2f-0d54-40f5-9172-e747942d4a46
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6db9c114f4f3faade3334e7bf682eba197a2dbb7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33257917"
---
# <a name="spreleaseapplock-transact-sql"></a>sp_releaseapplock (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Libera um bloqueio em um recurso de aplicativo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_releaseapplock [ @Resource = ] 'resource_name'   
     [ , [ @LockOwner = ] 'lock_owner' ]  
     [ , [ @DbPrincipal = ] 'database_principal' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @Resource=] '*resource_name*'  
 É um nome de recurso de bloqueio especificado pelo aplicativo cliente. O aplicativo deve garantir que o recurso seja exclusivo. O nome especificado é internamente transformado em hash para um valor que pode ser armazenado no gerenciador de bloqueio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *resource_name* é **nvarchar (255)** sem nenhum padrão. *resource_name* é binário comparado e, portanto, diferencia maiusculas de minúsculas, independentemente das configurações de agrupamento do banco de dados atual.  
  
 [ @LockOwner=] '*lock_owner*'  
 É o proprietário do bloqueio, que é o valor de *lock_owner* quando o bloqueio foi solicitado. *lock_owner* é **nvarchar(32)**. O valor pode ser **Transaction** (o padrão) ou **Session**. Quando o *lock_owner* valor é **transação**, por padrão ou explicitamente especificado, sp_getapplock deve ser executado de dentro de uma transação.  
  
 [ @DbPrincipal=] '*database_principal*'  
 É o usuário, função ou função de aplicativo que tem permissões para um objeto em um banco de dados. O chamador da função deve ser membro da função de banco de dados fixa *database_principal*, dbo ou db_owner para chamar a função com êxito. O padrão é público.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 \>= 0 (êxito) ou < 0 (falha)  
  
|Value|Resultado|  
|-----------|------------|  
|0|O bloqueio foi liberado com êxito.|  
|-999|Indica validação de parâmetro ou outro erro de chamada.|  
  
## <a name="remarks"></a>Remarks  
 Quando um aplicativo chama sp_getapplock várias vezes para o mesmo recurso de bloqueio, sp_releaseapplock deve ser chamado o mesmo número de vezes para liberar o bloqueio.  
  
 Quando o servidor é desligado por algum motivo, os bloqueios são liberados.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir libera o bloqueio associado à transação atual no recurso `Form1` do banco de dados `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_getapplock @DbPrincipal = 'dbo', @Resource = 'Form1',   
     @LockMode = 'Shared';  
EXEC sp_releaseapplock @DbPrincipal = 'dbo', @Resource = 'Form1';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [APPLOCK_MODE &#40;Transact-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)   
 [APPLOCK_TEST &#40;Transact-SQL&#41;](../../t-sql/functions/applock-test-transact-sql.md)   
 [sp_getapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
  
  

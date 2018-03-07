---
title: DROP USER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_USER_TSQL
- DROP USER
dev_langs:
- TSQL
helpviewer_keywords:
- dropping users
- DROP USER statement
- deleting users
- database user removal [SQL Server]
- removing users
- users [SQL Server], removing
ms.assetid: d6e0e21a-7568-4321-b6d6-bcfba183a719
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0a2f7d00b12cfb69031b1dbaab8aad1f6ac0cded
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-user-transact-sql"></a>DROP USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove um usuário do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP USER [ IF EXISTS ] user_name  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP USER user_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *SE EXISTIR*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]).  
  
 Condicionalmente descarta o usuário somente se ele já existe.  
  
 *user_name*  
 Especifica o nome pelo qual o usuário é identificado nesse banco de dados.  
  
## <a name="remarks"></a>Comentários  
 Os usuários que possuem itens protegíveis não podem ser descartados do banco de dados. Antes de descartar um usuário de banco de dados que possui itens protegíveis, primeiramente descarte ou transfira a propriedade desses itens.  
  
 O usuário guest não pode ser descartado, mas o usuário guest pode ser desabilitado revogando sua permissão CONNECT com a execução de REVOKE CONNECT FROM GUEST em qualquer banco de dados que não seja master ou tempdb.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY USER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o usuário `AbolrousHazem` do banco de dados `AdventureWorks2012`.  
  
```  
DROP USER AbolrousHazem;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [ALTER USER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  

---
description: ROLLBACK WORK (Transact-SQL)
title: ROLLBACK WORK (Transact-SQL)
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ROLLBACK WORK
- ROLLBACK_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- erasing data modifications [SQL Server]
- ROLLBACK WORK statement
- roll back transactions [SQL Server]
- rolling back transactions, ROLLBACK WORK
- savepoints [SQL Server]
ms.assetid: 2071dbd3-53d5-4510-be8d-26e80f2553b4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 38388c9d697bc3f7d2fddd8d6ff162ff7b306f08
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459292"
---
# <a name="rollback-work-transact-sql"></a>ROLLBACK WORK (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Reverte uma transação especificada pelo usuário ao começo da transação.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
ROLLBACK [ WORK ]  
[ ; ]  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários  
 Essa instrução funciona identicamente a ROLLBACK TRANSACTION exceto que ROLLBACK TRANSACTION aceita um nome de transação definido pelo usuário. Com ou sem especificar a palavra-chave opcional WORK, essa sintaxe ROLLBACK é compatível com o ISO.  
  
 Ao aninhar transações, ROLLBACK WORK sempre reverte para a instrução BEGIN TRANSACTION mais distante e decrementa a função de sistema @@TRANCOUNT para 0.  
  
## <a name="permissions"></a>Permissões  
 Permissões de ROLLBACK WORK assumem como padrão qualquer usuário válido.  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  

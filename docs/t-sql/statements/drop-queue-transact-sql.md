---
title: FILA de DROP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP QUEUE
- DROP_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping queues
- queues [Service Broker], removing
- deleting queues
- DROP QUEUE statement
- removing queues
ms.assetid: fd866520-ca00-477d-b2e9-0110e9610ed4
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51920e14a3a24f9bfb48f11c07414812da1694b9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-queue-transact-sql"></a>DROP QUEUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta uma fila existente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP QUEUE <object>  
[ ; ]  
  
<object> ::=  
{  
    [ database_name . [ schema_name ] . | schema_name . ]  
        queue_name  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 O nome do banco de dados que contém a fila a ser descartada. Quando nenhum *database_name* for fornecido, o padrão é o banco de dados atual.  
  
 *schema_name (object)*  
 O nome do esquema que possui a fila a ser descartada. Quando nenhum *schema_name* for fornecido, o padrão é o esquema padrão para o usuário atual.  
  
 *nome_da_fila*  
 O nome da fila a ser descartada.  
  
## <a name="remarks"></a>Comentários  
 Não é possível descartar uma fila se qualquer serviço se referir a ela.  
  
## <a name="permissions"></a>Permissões  
 Permissão para descartar uma fila padrão é o proprietário da fila, os membros do **db_ddladmin** ou **db_owner** fixa de funções de banco de dados e os membros do **sysadmin** fixa função de servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta o **ExpenseQueue** fila do banco de dados atual.  
  
```  
DROP QUEUE ExpenseQueue ;  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

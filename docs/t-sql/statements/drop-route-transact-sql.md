---
title: DROP ROUTE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP ROUTE
- DROP_ROUTE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping routes
- DROP ROUTE statement
- deleting routes
- routes [Service Broker], removing
- removing routes
ms.assetid: d8fab0bc-d54a-46ca-9437-552db7477d40
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b11908f182037a1368b9d1fda34ebda3f1422918
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68022587"
---
# <a name="drop-route-transact-sql"></a>DROP ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta uma rota, excluindo as informações da rota da tabela de roteamento do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP ROUTE route_name  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *route_name*  
 O nome da rota a ser descartada. Os nomes de servidor, banco de dados e esquema não podem ser especificados.  
  
## <a name="remarks"></a>Comentários  
 A tabela de roteamento que armazena as rotas é uma tabela de metadados que pode ser lida por meio da exibição do catálogo **sys.routes**. A tabela de roteamento pode ser atualizada somente pelas instruções CREATE ROUTE, ALTER ROUTE e DROP ROUTE.  
  
 Você pode descartar uma rota, seja ela usa ou não por alguma conversa. No entanto, se não houver nenhuma outra rota para o serviço remoto, as mensagens para essas conversas permanecerão na fila de transmissão até que uma rota para o serviço remoto seja criada ou o tempo da conversa se esgote.  
  
## <a name="permissions"></a>Permissões  
 A permissão para descartar uma rota assume como padrão o proprietário dessa rota, os membros das funções de banco de dados fixas db_ddladmin ou db_owner e os membros da função de servidor fixa sysadmin.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exclui a rota `ExpenseRoute`.  
  
```  
DROP ROUTE ExpenseRoute ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [CREATE ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.routes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-routes-transact-sql.md)  
  
  

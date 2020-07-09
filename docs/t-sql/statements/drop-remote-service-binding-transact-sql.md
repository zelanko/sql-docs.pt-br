---
title: DROP REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP REMOTE SERVICE BINDING
- DROP_REMOTE_SERVICE_BINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping remote service bindings
- removing remote service bindings
- deleting remote service bindings
- remote service bindings [Service Broker], dropping
- DROP REMOTE SERVICE BINDING statement
ms.assetid: 377789b4-bf94-488f-8c20-687d0bae447a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 07338b22d4d0ab36265c5cf97f679b92261e67d2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895089"
---
# <a name="drop-remote-service-binding-transact-sql"></a>DROP REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Descarta uma associação de serviço remoto.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
DROP REMOTE SERVICE BINDING binding_name  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *binding_name*  
 É o nome da associação de serviço remoto a ser descartada. Os nomes de servidor, banco de dados e esquema não podem ser especificados.  
  
## <a name="permissions"></a>Permissões  
 A permissão para descartar uma associação de serviço remoto assume como padrão o proprietário dessa associação, os membros da função de banco de dados fixa db_owner e os membros da função de servidor fixa sysadmin.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exclui a associação de serviço remoto `APBinding` do banco de dados.  
  
```  
DROP REMOTE SERVICE BINDING APBinding ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [ALTER REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

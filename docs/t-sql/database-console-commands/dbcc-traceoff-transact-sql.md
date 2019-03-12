---
title: DBCC TRACEOFF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRACEOFF_TSQL
- TRACEOFF
- DBCC TRACEOFF
- DBCC_TRACEOFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- trace flags [SQL Server], disabling
- DBCC TRACEOFF statement
- disabling trace flags
ms.assetid: 1379afba-6480-454b-9c65-5e64cb4f3415
author: pmasl
ms.author: umajay
manager: craigg
ms.openlocfilehash: b66d02c4f2b480f4238b87e190d63ee2682e86a7
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685599"
---
# <a name="dbcc-traceoff-transact-sql"></a>DBCC TRACEOFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Desabilita os sinalizadores de rastreamento especificados.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC TRACEOFF ( trace# [ ,...n ] [ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
*trace#*  
É o número do sinalizador de rastreamento a ser desabilitado.  
  
**-1**  
Desabilita globalmente os sinalizadores de rastreamento especificados.  
  
WITH NO_INFOMSGS  
Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="remarks"></a>Remarks  
Indicadores de rastreamento são usados para personalizar certas características que controlam o modo como a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opera.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC TRACEOFF retorna:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** .
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir desabilita o sinalizador de rastreamento `3205`.
  
```sql
DBCC TRACEOFF (3205);   
GO  
```  
  
O exemplo a seguir desabilita primeiro o sinalizador de rastreamento `3205` globalmente.
  
```sql
DBCC TRACEOFF (3205, -1);   
GO  
```  
  
O exemplo a seguir desabilita sinalizadores de rastreamento `3205` e `260` globalmente.
  
```sql
DBCC TRACEOFF (3205, 260, -1);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[DBCC TRACESTATUS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  

---
title: DBCC TRACEOFF (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 916474620c3ee248ec94da61b65bfa15de86ffee
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-traceoff-transact-sql"></a>DBCC TRACEOFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Desabilita os sinalizadores de rastreamento especificados.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC TRACEOFF ( trace# [ ,...n ] [ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
*Trace #*  
É o número do sinalizador de rastreamento a ser desabilitado.  
  
**-1**  
Desabilita globalmente os sinalizadores de rastreamento especificados.  
  
WITH NO_INFOMSGS  
Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="remarks"></a>Comentários  
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
  
## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[DBCC TRACESTATUS &#40; Transact-SQL &#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  


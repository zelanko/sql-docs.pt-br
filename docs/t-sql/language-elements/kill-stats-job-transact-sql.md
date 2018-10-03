---
title: KILL STATS JOB (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KILL STATS JOB
- KILL_STATS_JOB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending statistics update jobs [SQL Server]
- stopping statistics update jobs
- terminating statistics update jobs
- asynchronous statistics updates [SQL Server]
- KILL STATS JOB statement
- statistics update jobs [SQL Server]
ms.assetid: 55a8f9f1-3259-45c0-8ab9-60b9c088b4b4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dd7b4165ae08bee50d8e236c91458927798c0954
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845054"
---
# <a name="kill-stats-job-transact-sql"></a>KILL STATS JOB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Encerra um trabalho de atualização de estatísticas assíncrono no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
KILL STATS JOB job_id   
```  
  
## <a name="arguments"></a>Argumentos  
 *job_id*  
 É o campo job_id retornado pela exibição de gerenciamento dinâmico sys.dm_exec_background_job_queue para o trabalho.  
  
## <a name="remarks"></a>Remarks  
 O job_id não está relacionado ao session_id nem à unidade de trabalho usados em outros formatos da instrução KILL.  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter permissão VIEW SERVER STATE para acessar informações da exibição de gerenciamento dinâmico sys.dm_exec_background_job_queue.  
  
 As permissões KILL STATS JOB usam como padrão membros das funções de banco de dados fixas sysadmin e processadmin e não podem ser transferidas.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como encerrar a atualização de estatísticas associadas a um trabalho em que *job_id* = `53`.  
  
```  
KILL STATS JOB 53;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [sys.dm_exec_background_job_queue &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md)   
 [Estatísticas](../../relational-databases/statistics/statistics.md)  
  
  

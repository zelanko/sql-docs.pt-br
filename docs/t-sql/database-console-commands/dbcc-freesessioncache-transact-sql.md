---
title: DBCC FREESESSIONCACHE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREESESSIONCACHE
- FREESESSIONCACHE_TSQL
- DBCC_FREESESSIONCACHE_TSQL
- DBCC FREESESSIONCACHE
dev_langs: TSQL
helpviewer_keywords:
- DBCC FREESESSIONCACHE statement
- distributed queries [SQL Server], cache
- clearing distributed query cache
- flushing distributed query cache
ms.assetid: a256ba63-7e11-4d5e-abc0-1fa4ed072e63
caps.latest.revision: "15"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 25690ece853aa6c4cc3564ce5adad4e9c692972e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-freesessioncache-transact-sql"></a>DBCC FREESESSIONCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Libera o cache de conexão de consulta distribuída usado por consultas distribuídas em uma instância de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
```sql
DBCC FREESESSIONCACHE [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir libera o cache de consulta distribuída.
  
```sql
USE AdventureWorks2012;  
GO  
DBCC FREESESSIONCACHE WITH NO_INFOMSGS;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

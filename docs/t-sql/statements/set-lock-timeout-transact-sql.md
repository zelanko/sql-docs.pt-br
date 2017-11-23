---
title: SET LOCK_TIMEOUT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOCK_TIMEOUT_TSQL
- SET_LOCK_TIMEOUT_TSQL
- SET LOCK_TIMEOUT
- LOCK_TIMEOUT
dev_langs: TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- releasing locks
- LOCK_TIMEOUT option
- SET LOCK_TIMEOUT statement
- locking [SQL Server], time-outs
- wait time for lock releases [SQL Server]
ms.assetid: dd0c389e-956d-435e-bf71-e16624a0a215
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0e19a9acd7378615433364ac1b30db31a1a84b3a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="set-locktimeout-transact-sql"></a>SET LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica o número de milissegundos que uma instrução espera para um bloqueio ser liberado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SET LOCK_TIMEOUT timeout_period  
```  
  
## <a name="arguments"></a>Argumentos  
 *timeout_period*  
 É o número de milissegundos que decorrerão antes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna um erro de bloqueio. Um valor de -1 (padrão) indica nenhum tempo limite (isto é, esperar indefinidamente).  
  
 Quando uma espera por um bloqueio exceder o valor limite, um erro será retornado. Um valor de 0 significa não esperar e retornar uma mensagem assim que um bloqueio for encontrado.  
  
## <a name="remarks"></a>Comentários  
 No começo de uma conexão esta configuração tem um valor de -1. Após ser alterado, a nova configuração permanece durante toda a conexão.  
  
 A configuração de SET LOCK_TIMEOU é definida no momento da execução e não no momento da análise.  
  
 A dica de bloqueio READPAST fornece uma alternativa para esta opção de SET.  
  
 Instruções CREATE DATABASE, ALTER DATABASE e DROP DATABASE não aceitam a configuração SET LOCK_TIMEOUT.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-set-the-lock-timeout-to-1800-milliseconds"></a>R: definir o tempo limite de bloqueio como 1800 milissegundos  
 O seguinte exemplo define o período de tempo limite de bloqueio para `1800` milissegundos.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-set-the-lock-timeout-to-wait-forever-for-a-lock-to-be-released"></a>B. Defina o tempo limite de bloqueio para esperar por um bloqueio seja liberado.  
 O exemplo a seguir define o tempo limite de bloqueio para esperar e nunca expirar. Esse é o comportamento padrão que já está definido no início de cada conexão.  
  
```sql  
SET LOCK_TIMEOUT -1;  
```  
  
 O seguinte exemplo define o período de tempo limite de bloqueio para `1800` milissegundos. Nesta versão, [!INCLUDE[ssDW](../../includes/ssdw-md.md)] analisará a instrução com êxito, mas irá ignorar o valor 1800 e continuar a usar o comportamento padrão.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
```  
  
## <a name="see-also"></a>Consulte também  
 [@@LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  


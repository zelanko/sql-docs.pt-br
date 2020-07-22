---
title: SET LOCK_TIMEOUT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LOCK_TIMEOUT_TSQL
- SET_LOCK_TIMEOUT_TSQL
- SET LOCK_TIMEOUT
- LOCK_TIMEOUT
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- releasing locks
- LOCK_TIMEOUT option
- SET LOCK_TIMEOUT statement
- locking [SQL Server], time-outs
- wait time for lock releases [SQL Server]
ms.assetid: dd0c389e-956d-435e-bf71-e16624a0a215
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e48ac56759f41fef0d8778b7e663582759a57ed3
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484651"
---
# <a name="set-lock_timeout-transact-sql"></a>SET LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Especifica o número de milissegundos que uma instrução espera para um bloqueio ser liberado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
SET LOCK_TIMEOUT timeout_period  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *timeout_period*  
 É o número de milissegundos que se passarão antes que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorne um erro de bloqueio. Um valor de -1 (padrão) indica nenhum tempo limite (isto é, esperar indefinidamente).  
  
 Quando uma espera por um bloqueio exceder o valor limite, um erro será retornado. Um valor de 0 significa não esperar e retornar uma mensagem assim que um bloqueio for encontrado.  
  
## <a name="remarks"></a>Comentários  
 No começo de uma conexão esta configuração tem um valor de -1. Após ser alterado, a nova configuração permanece durante toda a conexão.  
  
 A configuração de SET LOCK_TIMEOU é definida no momento da execução e não no momento da análise.  
  
 A dica de bloqueio READPAST fornece uma alternativa para esta opção de SET.  
  
 Instruções CREATE DATABASE, ALTER DATABASE e DROP DATABASE não aceitam a configuração SET LOCK_TIMEOUT.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-set-the-lock-timeout-to-1800-milliseconds"></a>A: Definir o tempo limite de bloqueio como 1.800 milissegundos  
 O seguinte exemplo define o período de tempo limite de bloqueio para `1800` milissegundos.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-set-the-lock-timeout-to-wait-forever-for-a-lock-to-be-released"></a>B. Definir o tempo limite de bloqueio para esperar por um bloqueio ser liberado.  
 O exemplo a seguir define o tempo limite de bloqueio para esperar para sempre e nunca expirar. Esse é o comportamento padrão que já está definido no início de cada conexão.  
  
```sql  
SET LOCK_TIMEOUT -1;  
```  
  
 O seguinte exemplo define o período de tempo limite de bloqueio para `1800` milissegundos. Nesta versão, [!INCLUDE[ssDW](../../includes/ssdw-md.md)] analisará a instrução com êxito, mas ignorará o valor 1.800 e continuará usando o comportamento padrão.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [@@LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  


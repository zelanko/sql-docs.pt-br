---
title: '@@CPU_BUSY (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@CPU_BUSY_TSQL'
- '@@CPU_BUSY'
dev_langs:
- TSQL
helpviewer_keywords:
- CPU [SQL Server]
- status information [SQL Server], CPU
- ticks [SQL Server]
- time [SQL Server], CPU activity
- '@@CPU_BUSY function'
- statistical information [SQL Server], CPU
- CPU [SQL Server], activity
ms.assetid: 81ae0e64-79fa-4a74-9aa5-37045c4cd211
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 337682a73ae351536af64afca77959cbe6297d7f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40cpubusy-transact-sql"></a>&#x40;&#x40;CPU_BUSY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Retorna o tempo que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gastou desde que foi iniciado pela última vez. O resultado é indicado em incrementos de tempo de CPU ou "tiques", sendo cumulativo para todas as CPUs; portanto, ele pode exceder o tempo decorrido real. Multiplique por @@TIMETICKS para converter em microssegundos.
  
> [!NOTE]  
>  Se o tempo retornado em @@CPU_BUSY ou @@IO_BUSY exceder aproximadamente 49 dias de tempo de CPU cumulativo, você receberá um aviso de estouro aritmético. Nesse caso, o valor das variáveis @@CPU_BUSY, @@IO_BUSY e @@IDLE não é preciso.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```
@@CPU_BUSY  
```  
  
## <a name="return-types"></a>Tipos de retorno
**inteiro**
  
## <a name="remarks"></a>Remarks  
Para exibir um relatório que contém várias estatísticas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo a atividade da CPU, execute [sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md).
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir mostra o retorno de atividade de CPU do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir da data e hora atuais. Para evitar estouro aritmético ao converter o valor em microssegundos, o exemplo converte um dos valores no tipo de dados `float`.
  
```sql
SELECT @@CPU_BUSY * CAST(@@TIMETICKS AS float) AS 'CPU microseconds',   
   GETDATE() AS 'As of' ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
CPU microseconds As of
---------------- -----------------------
18406250         2006-12-05 17:00:50.600
```
  
## <a name="see-also"></a>Consulte também
[sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)  
[@@IDLE &#40;Transact-SQL&#41;](../../t-sql/functions/idle-transact-sql.md)  
[@@IO_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)  
[sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)  
[Funções estatísticas do sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)
  
  

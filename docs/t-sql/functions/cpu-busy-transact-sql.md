---
title: '@@CPU_BUSY (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 9263eac53d78da42752704019d95e72431eabcc0
ms.contentlocale: pt-br
ms.lasthandoff: 10/12/2017

---
# <a name="x40x40cpubusy-transact-sql"></a>& #x 40; & #x 40. CPU_BUSY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Retorna o tempo que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gastou desde que foi iniciado pela última vez. Resultados em incrementos de tempo de CPU, ou "tiques" e é cumulativo para todas as CPUs, portanto pode exceder o tempo decorrido real. Multiplique por@TIMETICKS para converter em microssegundos.
  
> [!NOTE]  
>  Se o tempo retornado em@CPU_BUSY ou @@IO_BUSY exceder aproximadamente 49 dias de tempo de CPU cumulativo, você receberá um aviso de estouro aritmético. Nesse caso, o valor de @@CPU_BUSY, @@IO_BUSY e @@IDLE variáveis não são precisos.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```
@@CPU_BUSY  
```  
  
## <a name="return-types"></a>Tipos de retorno
**inteiro**
  
## <a name="remarks"></a>Comentários  
Para exibir um relatório que contém várias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estatísticas, inclusive a atividade da CPU, execute [sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md).
  
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
[sys.DM os_sys_info &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)  
[@@IDLE &#40;Transact-SQL&#41;](../../t-sql/functions/idle-transact-sql.md)  
[@@IO_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)  
[sp_monitor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)  
[Funções estatísticas do sistema &#40; Transact-SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)
  
  


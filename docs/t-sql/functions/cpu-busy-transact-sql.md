---
title: '@@CPU_BUSY (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5f763ac74b32fd641791a45d1805b95a99230fbb
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895813"
---
# <a name="x40x40cpu_busy-transact-sql"></a>&#x40;&#x40;CPU_BUSY (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Esta função retorna a quantidade de tempo que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gastou em operação ativa desde o início mais recente. `@@CPU_BUSY` retorna um resultado medido em incrementos de tempo de CPU, ou "tiques". Este valor é cumulativo para todas as CPUs; portanto, ele pode exceder o tempo decorrido real. Para converter em microssegundos, multiplique por [@@TIMETICKS](./timeticks-transact-sql.md).
  
> [!NOTE]  
>  Se o tempo retornado em @@CPU_BUSY ou @@IO_BUSY exceder 49 dias (aproximadamente) de tempo de CPU cumulativo, você receberá um aviso de estouro aritmético. Nesse caso, o valor das variáveis `@@CPU_BUSY`, `@@IO_BUSY` e `@@IDLE` não é preciso.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```
@@CPU_BUSY  
```  
  
## <a name="return-types"></a>Tipos de retorno
**inteiro**
  
## <a name="remarks"></a>Comentários  
Para ver um relatório que contém várias estatísticas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo a atividade da CPU, execute [sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md).
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna a atividade de CPU do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir da data e hora atuais. O exemplo converte um dos valores para o tipo de dados `float`. Isso evita problemas de estouro de capacidade aritmética ao calcular um valor em microssegundos.
  
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
  
## <a name="see-also"></a>Confira também
[sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)  
[@@IDLE &#40;Transact-SQL&#41;](../../t-sql/functions/idle-transact-sql.md)  
[@@IO_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)  
[sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)  
[Funções estatísticas do sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)
  
  

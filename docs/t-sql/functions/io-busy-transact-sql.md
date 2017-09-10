---
title: '@@IO_BUSY (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@IO_BUSY'
- '@@IO_BUSY_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- ticks [SQL Server]
- I/O [SQL Server], time spent performing operations
- '@@IO_BUSY function'
- output operations [SQL Server]
- input operations [SQL Server]
- time [SQL Server], I/O operations
ms.assetid: 3c26770c-41ae-4e34-8c82-7bef920ffbca
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ef13f65af269167eba7c8df53c35ecfd992df6e0
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="iobusy-transact-sql"></a>@@IO_BUSY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o tempo que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gastou para executar operações de entrada e saída desde que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciado pela última vez. O resultado é indicado em incrementos de tempo de CPU ("tiques"), sendo cumulativo para todas as CPUs, portanto pode exceder o tempo decorrido real. Multiplique por@TIMETICKS para converter em microssegundos.  
  
> [!NOTE]  
>  Se o tempo retornado em@CPU_BUSY, @@IO_BUSY exceder aproximadamente 49 dias de tempo de CPU cumulativo, você receberá um aviso de estouro aritmético. Nesse caso, o valor de @@CPU_BUSY, @@IO_BUSY e @@IDLE variáveis não são precisos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
@@IO_BUSY  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **inteiro**  
  
## <a name="remarks"></a>Comentários  
 Para exibir um relatório que contém várias estatísticas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute sp_monitor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o retorno do número de milissegundos que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gastou para executar operações de entrada/saída entre a hora de início e a hora atual. Para evitar estouro aritmético ao converter o valor em microssegundos, o exemplo converte um dos valores para o **float** tipo de dados.  
  
```  
SELECT @@IO_BUSY*@@TIMETICKS AS 'IO microseconds',   
   GETDATE() AS 'as of';  
```  
  
 Aqui está um conjunto de resultados típico:  
  
```  
  
IO microseconds as of                   
--------------- ----------------------  
4552312500      12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.DM os_sys_info &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [@@CPU_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Funções estatísticas do sistema &#40; Transact-SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

---
title: '@@IO_BUSY (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b874feb143f72b6cc65a59b8f08eab889ad1927b
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65944451"
---
# <a name="x40x40iobusy-transact-sql"></a>&#x40;&#x40;IO_BUSY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o tempo que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gastou para executar operações de entrada e saída desde que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciado pela última vez. O resultado é indicado em incrementos de tempo de CPU ("tiques"), sendo cumulativo para todas as CPUs, portanto pode exceder o tempo decorrido real. Multiplique por @@TIMETICKS para converter em microssegundos.  
  
> [!NOTE]  
>  Se o tempo retornado em @@CPU_BUSY ou @@IO_BUSY exceder aproximadamente 49 dias de tempo de CPU cumulativo, você receberá um aviso de estouro aritmético. Nesse caso, o valor das variáveis @@CPU_BUSY, @@IO_BUSY e @@IDLE não é preciso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@IO_BUSY  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **inteiro**  
  
## <a name="remarks"></a>Remarks  
 Para exibir um relatório que contém várias estatísticas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute sp_monitor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o retorno do número de milissegundos que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gastou para executar operações de entrada/saída entre a hora de início e a hora atual. Para evitar estouro aritmético ao converter o valor em microssegundos, o exemplo converte um dos valores no tipo de dados **float**.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [@@CPU_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Funções estatísticas do sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

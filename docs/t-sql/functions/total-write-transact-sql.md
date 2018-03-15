---
title: '@@TOTAL_WRITE (Transact-SQL) | Microsoft Docs'
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
- '@@TOTAL_WRITE'
- '@@TOTAL_WRITE_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- write activity since last started [SQL Server]
- number of disk writes
- '@@TOTAL_WRITE function'
- disks [SQL Server], numbr of disk writes
- total write [SQL Server]
ms.assetid: cd528126-51ee-4aa4-a21f-f32ce5c80fac
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e24b92f6eb47e0aa8087e9526e299f2e1e251f0f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40totalwrite-transact-sql"></a>&#x40;&#x40;TOTAL_WRITE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o número de gravações em disco do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciado pela última vez.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
@@TOTAL_WRITE  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **inteiro**  
  
## <a name="remarks"></a>Remarks  
 Para exibir um relatório que contém várias estatísticas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo a atividade de leitura e gravação, execute **sp_monitor**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o retorno do número total de leituras e gravações em disco a partir da data e hora atuais.  
  
```  
SELECT @@TOTAL_READ AS 'Reads', @@TOTAL_WRITE AS 'Writes', GETDATE() AS 'As of'  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Reads       Writes      As of                   
----------- ----------- ----------------------  
7760        97263       12/5/2006 10:23:00 PM   
```  
  
## <a name="see-also"></a>Consulte Também  
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Funções estatísticas do sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)   
 [@@TOTAL_READ &#40;Transact-SQL&#41;](../../t-sql/functions/total-read-transact-sql.md)  
  
  

---
title: sp_flush_log (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_flush_log_TSQL
- sys.sp_flush_log
- sys.sp_flush_log_TSQL
- sp_flush_log
dev_langs: TSQL
helpviewer_keywords: sys.sp_flush_log
ms.assetid: 75cc9f52-3b1f-4754-b1e7-ce0dd3323bc9
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7085d93310e0f2b5e4f4523fa96ba66b3eaadc7
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sysspflushlog-transact-sql"></a>sys.sp_flush_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Libera para disco o log de transações do banco de dados atual, protegendo, assim todas as transações duráveis atrasadas confirmadas anteriormente.  
  
 Se você escolher usar a durabilidade da transação atrasada devido aos benefícios de desempenho, mas também quiser ter um limite garantido na quantidade de dados que serão perdidos se houver falha do servidor ou failover, execute `sys.sp_flush_log` regularmente. Por exemplo, se você quiser ter certeza de não perder mais do que x segundos de dados, deverá executar `sp_flush_log` a cada x segundos.  
  
 Executar `sys.sp_flush_log` garante que todas as transações duráveis atrasadas confirmadas anteriormente tornem-se duráveis. Consulte o tópico conceitual [controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md) para obter mais informações.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```tsql  
  
sys.sp_flush_log  
  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhum.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Um código de retorno de 1 indica êxito.  Qualquer outro valor indica falha.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum.  
  
## <a name="sample-code"></a>Código de exemplo  
  
```tsql  
.  
EXECUTE sys.sp_flush_log  
  
```  
  
  

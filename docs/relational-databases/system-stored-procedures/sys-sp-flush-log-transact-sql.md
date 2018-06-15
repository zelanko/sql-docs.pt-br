---
title: sp_flush_log (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_flush_log_TSQL
- sys.sp_flush_log
- sys.sp_flush_log_TSQL
- sp_flush_log
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_flush_log
ms.assetid: 75cc9f52-3b1f-4754-b1e7-ce0dd3323bc9
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 010870b0364cd302928fd9e0cc8491133f2283b4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33253817"
---
# <a name="sysspflushlog-transact-sql"></a>sys.sp_flush_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Libera para disco o log de transações do banco de dados atual, protegendo, assim todas as transações duráveis atrasadas confirmadas anteriormente.  
  
 Se você escolher usar a durabilidade da transação atrasada devido aos benefícios de desempenho, mas também quiser ter um limite garantido na quantidade de dados que serão perdidos se houver falha do servidor ou failover, execute `sys.sp_flush_log` regularmente. Por exemplo, se você quiser ter certeza de não perder mais do que x segundos de dados, deverá executar `sp_flush_log` a cada x segundos.  
  
 Executar `sys.sp_flush_log` garante que todas as transações duráveis atrasadas confirmadas anteriormente tornem-se duráveis. Consulte o tópico conceitual [controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md) para obter mais informações.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
  
sys.sp_flush_log  
  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhuma.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Um código de retorno de 1 indica êxito.  Qualquer outro valor indica falha.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma.  
  
## <a name="sample-code"></a>Código de exemplo  
  
```sql  
.  
EXECUTE sys.sp_flush_log  
  
```  
  
  

---
description: sys.sp_flush_log (Transact-SQL)
title: sys. sp_flush_log (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 99d804cc8df3a25853abc11b2ea4403b00fec503
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489021"
---
# <a name="syssp_flush_log-transact-sql"></a>sys.sp_flush_log (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Libera para disco o log de transações do banco de dados atual, protegendo, assim todas as transações duráveis atrasadas confirmadas anteriormente.  
  
 Se você escolher usar a durabilidade da transação atrasada devido aos benefícios de desempenho, mas também quiser ter um limite garantido na quantidade de dados que serão perdidos se houver falha do servidor ou failover, execute `sys.sp_flush_log` regularmente. Por exemplo, se você quiser ter certeza de que não perderá mais de x segundos de dados, será executado a `sp_flush_log` cada x segundos.  
  
 Executar `sys.sp_flush_log` garante que todas as transações duráveis atrasadas confirmadas anteriormente tornem-se duráveis. Consulte o tópico conceitual [controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md) para obter mais informações.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
  
sys.sp_flush_log  
  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhum.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Um código de retorno de 1 indica êxito.  Qualquer outro valor indica falha.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum.  
  
## <a name="sample-code"></a>Código de exemplo  
  
```sql  
.  
EXECUTE sys.sp_flush_log  
  
```  
  
  

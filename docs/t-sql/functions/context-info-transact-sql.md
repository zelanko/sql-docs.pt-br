---
title: CONTEXT_INFO (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONTEXT_INFO_TSQL
- CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- CONTEXT_INFO function
- Multiple Active Result Sets
- context information [SQL Server]
- MARS [SQL Server]
- session context information [SQL Server]
ms.assetid: 571320f5-7228-4b0e-9d01-ab732d2d1eab
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 98a275622a809b3856b66d825cd48e2698fea51b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o valor **context_info** definido para a sessão ou o lote atual usando a instrução [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>Valor retornado
O valor de **context_info**.
  
Se **context_info** não foi definido:
-   Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], retorna NULL.  
-   Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], retorna um GUID exclusivo específico da sessão.  
  
## <a name="remarks"></a>Remarks  
MARS (Vários Conjuntos de Resultados Ativos) permite que os aplicativos sejam executados em vários lotes, ou solicitações, ao mesmo tempo na mesma conexão. Quando um dos lotes em uma conexão MARS executa SET CONTEXT_INFO, o novo valor de contexto é retornado pela função CONTEXT_INFO quando é executado no mesmo lote que a instrução SET. O novo valor não é retornado pela função CONTEXT_INFO executada em um ou mais dos outros lotes da conexão, a menos que sejam iniciados depois do lote que executou a instrução SET completa.
  
## <a name="permissions"></a>Permissões  
Não requer nenhuma permissão especial. As informações de contexto também são armazenadas nas exibições do sistema **sys.dm_exec_requests**, **sys.dm_exec_sessions** e **sys.sysprocesses**, mas a consulta direta às exibições exige as permissões SELECT e VIEW SERVER STATE.
  
## <a name="examples"></a>Exemplos  
O exemplo simples a seguir define o valor **context_info** como `0x1256698456` e, em seguida, usa a função `CONTEXT_INFO` para recuperar o valor.
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>Confira também
[SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  

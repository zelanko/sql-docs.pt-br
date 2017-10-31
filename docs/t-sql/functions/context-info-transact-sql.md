---
title: CONTEXT_INFO (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd261b2f7f1cc4234792bec66c3662d6d9b8dcd8
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o **context_info** valor que foi definido para a sessão atual ou lote usando o [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md) instrução.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>Valor de retorno
O valor de **context_info**.
  
Se **context_info** não foi definido:
-   Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna NULL.  
-   Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] retorna um GUID exclusivo de sessão específica.  
  
## <a name="remarks"></a>Comentários  
MARS (Vários Conjuntos de Resultados Ativos) permite que os aplicativos sejam executados em vários lotes, ou solicitações, ao mesmo tempo na mesma conexão. Quando um dos lotes em uma conexão MARS executa SET CONTEXT_INFO, o novo valor de contexto é retornado pela função CONTEXT_INFO quando é executado no mesmo lote que a instrução SET. O novo valor não é retornado pela função CONTEXT_INFO executada em um ou mais dos outros lotes da conexão, a menos que sejam iniciados depois do lote que executou a instrução SET completa.
  
## <a name="permissions"></a>Permissões  
Não requer nenhuma permissão especial. As informações de contexto também são armazenadas no **exec_requests**, **sys.DM exec_sessions**, e **sys. sysprocesses** exibições do sistema, mas a consulta direta às exibições requer permissões SELECT e VIEW SERVER STATE.
  
## <a name="examples"></a>Exemplos  
O exemplo simples a seguir define o **context_info** valor `0x1256698456`e, em seguida, usa o `CONTEXT_INFO` função para recuperar o valor.
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>Consulte também
[Definir CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  


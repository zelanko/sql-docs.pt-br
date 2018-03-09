---
title: DBCC DROPCLEANBUFFERS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROPCLEANBUFFERS
- DBCC_DROPCLEANBUFFERS_TSQL
- DROPCLEANBUFFERS_TSQL
- DBCC DROPCLEANBUFFERS
dev_langs:
- TSQL
helpviewer_keywords:
- clean buffers
- cold buffer cache
- buffer pools [SQL Server]
- dropping buffers
- removing buffers
- DBCC DROPCLEANBUFFERS statement
ms.assetid: a4121927-f2ce-4926-aa2c-9b1519dac048
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 94830ffc100d0be451d34055a645e124a58325b7
ms.sourcegitcommit: 03021482208259e6c67599b47df23fbbe8f3a393
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2018
---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

Remove todos os buffers limpos do pool de buffers e os objetos de columnstore do pool de objetos columnstore.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe
Sintaxe do SQL Server: 

```sql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
Sintaxe do SQL Warehouse do Azure e do Parallel Data Warehouse:

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas. As mensagens informativas sempre são suprimidas no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 COMPUTE  
 Limpar o cache de dados na memória de cada nó de computação.  
  
 ALL  
 Limpar o cache de dados na memória de cada nó de computação e do nó de controle. Esse será o padrão se você não especificar um valor.  
  
## <a name="remarks"></a>Remarks  
Use DBCC DROPCLEANBUFFERS para testar consultas com um cache de buffer a frio sem desligar e reiniciar o servidor.
Para remover buffers limpos dos objetos de columnstore e do pool de buffers do pool de objetos columnstore, primeiro use CHECKPOINT para produzir um cache de buffer frio. Isso faz com que todas as páginas de alterações para o banco de dados atual sejam gravadas no disco e limpa os buffers. Depois de fazer isso, você pode emitir o comando DBCC DROPCLEANBUFFERS para remover todos os buffers do pool de buffers.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC DROPCLEANBUFFERS no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissões  

Aplica-se a: SQL Server, Parallel Data Warehouse 

- Exige associação à função de servidor fixa **sysadmin** .  

Aplica-se a: SQL Data Warehouse do Azure

- Requer associação à função de servidor fixa DB_OWNER.  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  

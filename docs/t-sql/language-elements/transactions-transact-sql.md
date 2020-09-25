---
description: transações (Transact-SQL)
title: Transações (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Transactions
- Transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactions [SQL Server]
- transactions [SQL Server], about transactions
- UOW [SQL Server]
- unit of work [SQL Server]
ms.assetid: 1485c375-921a-42af-a871-bb333cc08d3e
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3588c21ff18120c390c6ecb4484d02bc7f83dbb9
ms.sourcegitcommit: 8f062015c2a033f5a0d805ee4adabbe15e7c8f94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91227475"
---
# <a name="transactions-transact-sql"></a>transações (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Uma transação é uma única unidade de trabalho. Se uma transação tiver êxito, todas as modificações de dados feitas durante a transação estarão confirmadas e se tornarão parte permanente do banco de dados. Se uma transação encontrar erros e precisar ser cancelada ou revertida, todas as modificações de dados serão apagadas.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opera nos seguintes modos de transação:  
  
 Transações de confirmação automática  
 Cada instrução individual é uma transação.  
  
 Transações explícitas  
 Cada transação é iniciada explicitamente com a instrução BEGIN TRANSACTION e finalizada explicitamente com uma instrução COMMIT ou ROLLBACK.  
  
 Transações implícitas  
 Uma transação nova é iniciada implicitamente quando a transação anterior é concluída, mas cada transação é explicitamente concluída com uma instrução COMMIT ou ROLLBACK.  
  
 Transações de escopo de lote  
 Aplicável apenas a MARS (Conjuntos de Resultados Ativos Múltiplos), a transação [!INCLUDE[tsql](../../includes/tsql-md.md)] explícita ou implícita iniciada em uma sessão MARS se torna uma transação de escopo de lote. A transação de escopo de lote que não é confirmada ou revertida quando um lote é concluído, será revertida automaticamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!NOTE] 
> Para considerações especiais relacionadas a produtos de Data Warehouse, confira [Transações (Azure Synapse Analytics)](transactions-sql-data-warehouse.md).   

## <a name="in-this-section"></a>Nesta seção  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece as seguintes instruções de transação:  
  
:::row:::
    :::column:::
        [BEGIN DISTRIBUTED TRANSACTION](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)
    :::column-end:::
    :::column:::
        [ROLLBACK TRANSACTION](../../t-sql/language-elements/rollback-transaction-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md)
    :::column-end:::
    :::column:::
        [ROLLBACK WORK](../../t-sql/language-elements/rollback-work-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [COMMIT TRANSACTION](../../t-sql/language-elements/commit-transaction-transact-sql.md)
    :::column-end:::
    :::column:::
        [SAVE TRANSACTION](../../t-sql/language-elements/save-transaction-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [COMMIT WORK](../../t-sql/language-elements/commit-work-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
  
## <a name="see-also"></a>Consulte Também  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  

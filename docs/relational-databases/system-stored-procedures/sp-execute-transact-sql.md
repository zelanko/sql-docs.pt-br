---
description: sp_execute (Transact-SQL)
title: sp_execute (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_execute
- sp_cursor_execute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute
ms.assetid: 2009acd3-0d92-435a-a8fb-057e50dc7146
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f4b3e0c2ca3a310406326b9bcf3dd12841707625
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548053"
---
# <a name="sp_execute-transact-sql"></a>sp_execute (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Executa uma instrução preparada [!INCLUDE[tsql](../../includes/tsql-md.md)] usando um identificador especificado e um valor de parâmetro opcional. sp_execute é invocado especificando ID = 12 em um pacote TDS (tabela de dados tabulares).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_execute handle OUTPUT  
    [,bound_param  ]  [,...n ]  ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *processamento*  
 É o valor de *identificador* retornado por sp_prepare. o *identificador* é um parâmetro necessário que chama o valor de entrada **int** .  
  
 *bound_param*  
 Significa o uso de parâmetros adicionais. *bound_param* é um parâmetro necessário que chama os valores de entrada de qualquer tipo de dados para significar parâmetros adicionais para o procedimento.  
  
> [!NOTE]  
>  *bound_param* deve corresponder às declarações feitas pelo valor de*parâmetros* de sp_prepare e pode estar no formato * @name = valor* ou *valor*.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_prepare &#40;&#41;Transact SQL ](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)  
  
  

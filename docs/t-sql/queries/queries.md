---
title: Consultas | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5ff02a32-e8d3-479c-ae8b-07581e41f5f8
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: dab62a8aae5a986bc54928208a258cab48d16247
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="queries"></a>Consultas
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Linguagem de manipulação de dados (DML) é um vocabulário usado para recuperar e trabalhar com dados em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e o banco de dados SQL. Mais também funcionam no SQL Data Warehouse e PDW (revisar cada instrução individual para obter detalhes). Use estas instruções para adicionar, modificar, consultar ou remover dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 A tabela a seguir lista as instruções DML usadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|||  
|-|-|  
|[BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)|[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|  
|[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)|  
|[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)|[UPDATETEXT &#40; Transact-SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)|  
|[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)|[WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)|  
|[READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)||  
  
 A tabela a seguir lista as cláusulas usadas em várias instruções ou cláusulas DML.  
  
|Cláusula|Pode ser usada nestas instruções|  
|------------|-------------------------------------|  
|[FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)|DELETE, SELECT, UPDATE|  
|[Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)|DELETE, INSERT, SELECT, UPDATE|  
|[OPTION Clause &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)|DELETE, SELECT, UPDATE|  
|[Cláusula OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)|DELETE, INSERT, MERGE, UPDATE|  
|[Critério de pesquisa &#40; Transact-SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md)|DELETE, MERGE, SELECT, UPDATE|  
|[Construtor de valor de tabela &#40; Transact-SQL &#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)|FROM, INSERT, MERGE|  
|[TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)|DELETE, INSERT, MERGE, SELECT, UPDATE|  
|[WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)|DELETE, SELECT, UPDATE, CORRESPONDÊNCIA|  
|[COM common_table_expression &#40; Transact-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)|DELETE, INSERT, MERGE, SELECT, UPDATE|  
  
  

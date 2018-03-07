---
title: Hints (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
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
helpviewer_keywords:
- query optimizer [SQL Server], hints
- hints [SQL Server], about hints
- SELECT statement [SQL Server], hints
- hints [SQL Server]
- INSERT statement [SQL Server], hints
- UPDATE statement [SQL Server], hints
- DELETE statement [SQL Server], hints
ms.assetid: 99412475-b0df-4264-9938-33a0b302b41a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bddb86e431c252a45e68a52a4e7192d9fcbc5006
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="hints-transact-sql"></a>dicas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Dicas são opções ou estratégias especificadas para aplicação pelo processador de consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em instruções SELECT, INSERT, UPDATE ou DELETE. As dicas substituem todos os planos de execução que o otimizador de consulta possa selecionar para uma consulta.  
  
> [!CAUTION]  
>  Porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente, o otimizador de consulta seleciona o melhor plano de execução para uma consulta, é recomendável que \<as dicas join_hint >, \<query_hint >, e \<table_hint > ser usados apenas como último recurso por experiente os desenvolvedores e administradores de banco de dados.
  
 As seguintes dicas são descritas nesta seção:  
  
-   [Dicas de junção](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [Dicas de consulta](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [Dica de tabela](../../t-sql/queries/hints-transact-sql-table.md)  
  
  

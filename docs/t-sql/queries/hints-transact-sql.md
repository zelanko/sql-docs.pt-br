---
title: Dicas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8bd2692d428012e0af4ea4f41059228178810abb
ms.sourcegitcommit: 670082cb47f7d3d82e987b549b6f8e3a8968b5db
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57334303"
---
# <a name="hints-transact-sql"></a>dicas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Dicas são opções ou estratégias especificadas para aplicação pelo processador de consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em instruções SELECT, INSERT, UPDATE ou DELETE. As dicas substituem todos os planos de execução que o otimizador de consulta possa selecionar para uma consulta.  
  
> [!CAUTION]  
>  Como o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geralmente seleciona o melhor plano de execução para uma consulta, é recomendável que \<join_hint>, \<query_hint> e \<table_hint> sejam usadas apenas como um último recurso por desenvolvedores e administradores de banco de dados experientes.
  
 As seguintes dicas são descritas nesta seção:  
  
-   [Dicas de junção](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [Dicas de consulta](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [Dica de tabela](../../t-sql/queries/hints-transact-sql-table.md)  
  
  

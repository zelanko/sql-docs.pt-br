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
ms.openlocfilehash: 7ee01e23c544ac01ee9fb85e5b59d31b73088987
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731288"
---
# <a name="hints-transact-sql"></a>dicas (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Dicas são opções ou estratégias especificadas para aplicação pelo processador de consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em instruções SELECT, INSERT, UPDATE ou DELETE. As dicas substituem todos os planos de execução que o otimizador de consulta possa selecionar para uma consulta.  
  
> [!CAUTION]  
>  Como o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente seleciona o melhor plano de execução para uma consulta, recomendamos que desenvolvedores e administradores de banco de dados experientes usem \<join_hint>, \<query_hint> e \<table_hint> apenas como um último recurso.
  
 As seguintes dicas são descritas nesta seção:  
  
-   [Dicas de junção](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [Dicas de consulta](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [Dica de tabela](../../t-sql/queries/hints-transact-sql-table.md)  
  
  

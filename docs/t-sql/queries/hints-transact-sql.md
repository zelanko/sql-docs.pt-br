---
title: Dicas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a404f015c177fe38985c07470645e9a16e2cb716
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33058543"
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
  
  

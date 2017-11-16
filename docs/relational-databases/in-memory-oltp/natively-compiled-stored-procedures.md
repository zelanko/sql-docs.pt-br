---
title: Procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
caps.latest.revision: "54"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b3fc9af2aca5914ee2074333f5621e42ac13db1d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="natively-compiled-stored-procedures"></a>procedimentos armazenados compilados nativamente
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Os procedimentos armazenados compilados nativamente são procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados no código nativo que acessam tabelas com otimização de memória. Os procedimentos armazenados compilados nativamente proporcionam a execução eficiente das consultas e da lógica de negócios no procedimento armazenado. Para obter mais detalhes sobre o processo de compilação nativo, consulte [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md). Para mais informações sobre a migração de procedimentos armazenados baseados em disco para procedimentos armazenados compilados de modo nativo, veja [Problemas de migração para procedimentos armazenados compilados de modo nativo](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md).  
  
> [!NOTE]  
>  Uma diferença entre os procedimentos armazenados interpretados (baseados em disco) e os procedimentos armazenados compilados de forma nativa é que um procedimento armazenado interpretado é compilado na primeira execução, enquanto um procedimento armazenado compilado de forma nativa é compilado quando é criado. Com os procedimentos armazenados compilados de forma nativa, muitas condições de erro podem ser detectadas no momento da criação e causarão falha na criação do procedimento armazenado compilado de forma nativa (como estouro aritmético, conversão de tipo e algumas condições de divisão por zero). Com os procedimentos armazenados interpretados, essas condições de erro, geralmente, não causam falha quando o procedimento armazenado é criado, mas todas as execuções falharão.  
  
 Tópicos desta seção:  
  
-   [Criando procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)  
  
-   [Blocos atômicos](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)  
  
-   [Recursos com suporte para módulos T-SQL compilados nativamente](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [DDL com suporte para módulos T-SQL compilados nativamente](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [Procedimentos armazenados compilados nativamente e opções de execução Set](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [Práticas recomendadas para chamar procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [Monitorando o desempenho de procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [Chamando procedimentos armazenados compilados nativamente em aplicativos de acesso a dados](../../relational-databases/in-memory-oltp/calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas com otimização de memória](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  

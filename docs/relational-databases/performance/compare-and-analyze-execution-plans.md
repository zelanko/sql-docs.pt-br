---
title: Comparar e analisar planos de execução | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan results
- execution plans [SQL Server]
- queries [SQL Server], tuning
- execution plans [SQL Server], how-to topics
- SQL Server Management Studio [SQL Server], execution plans
- tuning queries [SQL Server]
ms.assetid: bcd6f094-c613-4835-ae19-4caaadb4bb17
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 0b7a932f58fe791b6609b999f4495a42af88422d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68219447"
---
# <a name="compare-and-analyze-execution-plans"></a>Comparar e Analisar Planos de Execução
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Esta seção explica como comparar e analisar planos de execução usando o Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
Os planos de execução exibem graficamente os métodos de recuperação de dados escolhidos pelo Otimizador de Consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os planos de execução representam o custo de execução de instruções e consultas específicas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando ícones em vez da representação tabular produzida pelas instruções [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md) ou [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md). Essa abordagem gráfica é muito útil para entender as características de desempenho de uma consulta. 

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inclui a funcionalidade que permite aos usuários comparar dois planos de execução, por exemplo, entre planos bons e ruins percebidos para a mesma consulta e realizar a análise da causa raiz. Também há a funcionalidade para executar a análise de plano de consulta única, permitindo percepções sobre os cenários que podem estar afetando o desempenho de uma consulta por meio de análise de seu plano de execução.

Para obter mais informações sobre planos de execução de consulta, confira [plano de execução estimado](../../relational-databases/performance/display-the-estimated-execution-plan.md), [plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md) e [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md).
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Comparar planos de execução](../../relational-databases/performance/display-the-estimated-execution-plan.md)  
  
-   [Analisar um plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md)  
  
  

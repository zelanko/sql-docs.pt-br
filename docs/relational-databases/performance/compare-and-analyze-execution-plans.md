---
title: Comparar e analisar planos de execução | Microsoft Docs
description: Saiba como comparar e analisar planos de execução usando o SQL Server Management Studio. Os planos de execução exibem os métodos de recuperação de dados do Otimizador e Consulta.
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: wiassaf
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
ms.openlocfilehash: 9a969277322f24861e2dcd4c85e92df9e4ebb4f0
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505360"
---
# <a name="compare-and-analyze-execution-plans"></a>Comparar e Analisar Planos de Execução
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
Esta seção explica como comparar e analisar planos de execução usando o Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Este recurso está disponível a partir do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v17.4.  
  
Os planos de execução exibem graficamente os métodos de recuperação de dados escolhidos pelo Otimizador de Consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os planos de execução representam o custo de execução de instruções e consultas específicas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando ícones em vez da representação tabular produzida pelas instruções [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md) ou [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md). Essa abordagem gráfica é muito útil para entender as características de desempenho de uma consulta. 

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inclui a funcionalidade que permite aos usuários comparar dois planos de execução, por exemplo, entre planos bons e ruins percebidos para a mesma consulta e realizar a análise da causa raiz. Também há a funcionalidade para executar a análise de plano de consulta única, permitindo percepções sobre os cenários que podem estar afetando o desempenho de uma consulta por meio de análise de seu plano de execução.

Para obter mais informações sobre planos de execução de consulta, confira [plano de execução estimado](../../relational-databases/performance/display-the-estimated-execution-plan.md), [plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md) e [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md).
  
## <a name="in-this-section"></a>Nesta seção  
[Comparar planos de execução](../../relational-databases/performance/display-the-estimated-execution-plan.md)     
[Analisar um plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md)      
  

---
title: Exibir e salvar planos de execução | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2017
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
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d2d049990cd2c60db36105d3c03da36bc25b4f4b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749539"
---
# <a name="display-and-save-execution-plans"></a>Exibir e salvar planos de execução
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
Esta seção explica como exibir planos de execução e como salvá-los em um arquivo no formato XML usando o Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
Os planos de execução exibem graficamente os métodos de recuperação de dados escolhidos pelo Otimizador de Consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os planos de execução representam o custo de execução de instruções e consultas específicas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando ícones em vez da representação tabular produzida pelas instruções [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md) ou [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md). Essa abordagem gráfica é útil para entender as características de desempenho de uma consulta.  

Enquanto o Otimizador de Consulta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produz apenas um plano de execução, há o conceito de plano de execução **estimado** e de plano de execução **real**.
-  Um [plano de execução estimado](../../relational-databases/performance/display-the-estimated-execution-plan.md) retorna o plano de execução como produzido pelo Otimizador de Consulta no tempo de compilação. A produção do plano de execução estimado não executa a consulta ou o lote de fato e, portanto, não contém nenhuma informação de runtime, como avisos de métrica ou runtime de uso real do recurso. 
-  Um [plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md) retorna o plano de execução produzido pelo Otimizador de Consulta e, depois disso, as consultas ou os lotes concluem a execução. Isso inclui informações de runtime sobre as métricas de uso de recursos e os avisos de runtime.  

Para obter mais informações sobre planos de execução de consulta, confira [Guia da Arquitetura de Processamento de Consultas](../../relational-databases/query-processing-architecture-guide.md).
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Exibir o plano de execução estimado](../../relational-databases/performance/display-the-estimated-execution-plan.md)  
  
-   [Exibir um plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md)  
  
-   [Salvar um plano de execução em formato XML](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  

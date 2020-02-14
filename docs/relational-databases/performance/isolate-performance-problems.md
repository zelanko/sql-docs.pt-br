---
title: Isolar problemas de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- isolating performance problems [SQL Server]
- monitoring performance [SQL Server], isolating problems
- database monitoring [SQL Server], isolating problems
- tuning databases [SQL Server], isolating problems
- monitoring server performance [SQL Server], isolating problems
- database performance [SQL Server], isolating problems
- server performance [SQL Server], isolating problems
ms.assetid: 2eb425cb-9166-4027-ae08-c8fc2d236f44
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 643551201567ae10980c1fe3d5efca95a1bc9ded
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68051973"
---
# <a name="isolate-performance-problems"></a>Isolar problemas de desempenho
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Muitas vezes, é mais eficaz usar várias ferramentas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do Microsoft Windows juntas para isolar problemas de desempenho de banco de dados do que usar uma ferramenta de cada vez. Por exemplo, o recurso gráfico Plano de Execução ajuda a reconhecer deadlocks rapidamente em uma única consulta. No entanto, você poderá reconhecer alguns outros problemas de desempenho mais facilmente se usar os recursos de monitoramento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows juntos.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] pode ser usado para monitorar e solucionar problemas relacionados a Transact-SQL e a aplicativos. O Monitor do Sistema pode ser usado para monitorar hardware e outros problemas relacionados a sistema.  
  
 Você pode monitorar as seguintes áreas para solucionar problemas:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimentos armazenados ou lotes de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] enviados por aplicativos de usuário.  
  
-   Atividade de usuário, tal como bloqueios ou deadlocks.  
  
-   Atividade de hardware, tal como uso de disco.  
  
 Os problemas podem incluir:  
  
-   Erros de desenvolvimento de aplicativo que envolvam instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] incorretamente escritas.  
  
-   Erros de hardware, tais como erros relacionados a disco ou a rede.  
  
-   Bloqueio excessivo devido a um banco de dados incorretamente projetado.  
  
## <a name="tools-for-common-performance-problems"></a>Ferramentas para problemas de desempenho comuns  
 Igualmente importante é a seleção criteriosa do problema de desempenho que você deseja que cada ferramenta monitore ou ajuste. A ferramenta e o utilitário dependem do tipo de problema de desempenho que você queira resolver.  
  
 Os tópicos a seguir descrevem uma série de ferramentas de monitoramento e de ajuste e os problemas de que dão conta.  
  
 [Identificar afunilamentos](../../relational-databases/performance/identify-bottlenecks.md)  
  
 [Monitorar o uso de memória](../../relational-databases/performance-monitor/monitor-memory-usage.md)  
  
  

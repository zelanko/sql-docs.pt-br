---
title: Estabelecer uma linha de base de desempenho | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database performance [SQL Server], baselines
- monitoring performance [SQL Server], baselines
- tuning databases [SQL Server], baselines
- server performance [SQL Server], baselines
- performance [SQL Server], baselines
- baseline performance [SQL Server]
- measurements for baseline statistics [SQL Server]
- monitoring server performance [SQL Server], establishing baseline
- database monitoring [SQL Server], baselines
ms.assetid: dc5aa8d6-2507-448f-ad86-4196443915fc
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6d1c546387df6352a1eb59b0c0310d86a630a342
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="establish-a-performance-baseline"></a>Estabelecer uma linha de base de desempenho
  Para determinar se o sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está com desempenho ótimo, meça o desempenho a intervalos regulares, mesmo quando não houver problemas, para estabelecer uma linha de base para o desempenho do servidor. Compare cada novo de conjuntos de medidas com os anteriores.  
  
 As seguintes áreas afetam o desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Recursos do sistema (hardware)  
  
-   Arquitetura de rede  
  
-   O sistema operacional  
  
-   Aplicativos de banco de dados  
  
-   Aplicativos cliente  
  
 No mínimo, use medidas de linha de base para determinar:  
  
-   Horas de pico e fora de pico da operação.  
  
-   Tempos de resposta a consultas de produção ou comandos de lote.  
  
-   Tempos de conclusão de backup e restauração de banco de dados.  
  
 Tendo estabelecido uma linha de base para o desempenho do servidor, compare as estatísticas da linha de base com o desempenho atual do servidor. Números muito acima ou muito abaixo da linha de base são candidatos a investigação extra. Eles podem indicar áreas que necessitam de ajuste ou reconfiguração. Por exemplo, se o tempo necessário para executar um conjunto de consultas aumentar, examine as consultas para determinar se podem ser reescritas ou se devem ser adicionadas estatísticas de colunas ou novos índices.  
  
## <a name="see-also"></a>Consulte também  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

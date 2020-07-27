---
title: Estabelecer uma linha de base de desempenho | Microsoft Docs
description: Faça medidas de desempenho em intervalos regulares com o decorrer do tempo, mesmo quando não houver problemas, a fim de estabelecer uma linha de base do desempenho do servidor no SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
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
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 619e9d6ad55f17fece2a9d327d4e0d67512e4b90
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457680"
---
# <a name="establish-a-performance-baseline"></a>Estabelecer uma linha de base de desempenho
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
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
  
## <a name="see-also"></a>Consulte Também  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

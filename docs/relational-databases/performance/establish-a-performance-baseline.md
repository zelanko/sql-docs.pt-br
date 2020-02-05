---
title: Estabelecer uma linha de base de desempenho | Microsoft Docs
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
ms.openlocfilehash: a7912ca171e2bd9fb84d8f1bf7adb04dc7d8acab
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67946789"
---
# <a name="establish-a-performance-baseline"></a>Estabelecer uma linha de base de desempenho
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
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
  
  

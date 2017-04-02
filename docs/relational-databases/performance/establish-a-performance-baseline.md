---
title: "Estabelecer uma linha de base de desempenho | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "desempenho do banco de dados [SQL Server], linhas de base"
  - "monitorando desempenho [SQL Server], linhas de base"
  - "ajustando bancos de dados [SQL Server], linhas de base"
  - "desempenho do servidor [SQL Server], linhas de base"
  - "desempenho [SQL Server], linhas de base"
  - "desempenho de linha de base [SQL Server]"
  - "medidas para estatísticas de linha de base [SQL Server]"
  - "monitorando o desempenho do servidor [SQL Server], estabelecendo a linha de base"
  - "monitoramento de banco de dados [SQL Server], linhas de base"
ms.assetid: dc5aa8d6-2507-448f-ad86-4196443915fc
caps.latest.revision: 22
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 22
---
# Estabelecer uma linha de base de desempenho
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
  
## Consulte também  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
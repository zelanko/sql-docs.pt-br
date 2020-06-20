---
title: SQL Server Profiler-tabela de origem-Orientador de Otimização do Mecanismo de Banco de Dados-selecionar tabela de carga de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.tools.sourcetable.f1
helpviewer_keywords:
- Select Workload Table dialog box
- Source Table dialog box
ms.assetid: 51185be7-7092-480a-a52c-cf7786c4a0a0
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c706613c828ce579af27a8c5a6890936a31814ca
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929227"
---
# <a name="sql-server-profiler---source-table-database-engine-tuning-advisor---select-workload-table"></a>SQL Server Profiler-tabela de origem-Orientador de Otimização do Mecanismo de Banco de Dados-selecionar tabela de carga de trabalho
  O Microsoft [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] e o Orientador de Otimização do [!INCLUDE[ssDE](../includes/ssde-md.md)] usam essa caixa de diálogo para selecionar tabelas.  
  
 No [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], use a caixa de diálogo **Tabela de Origem** para especificar uma tabela de origem para uma tabela de rastreamento. Essa é uma tabela a partir da qual é carregado um rastreamento e cujo conteúdo é exibido ou usado para repetir o rastreamento.  
  
 No Orientador de Otimização do [!INCLUDE[ssDE](../includes/ssde-md.md)], use a caixa de diálogo **Selecionar Tabela de Carga de Trabalho** para selecionar uma tabela de banco de dados que contém informações de rastreamento do [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para usar como uma carga de trabalho de otimização ou para visualizar o conteúdo da tabela antes de iniciar a análise de otimização.  
  
## <a name="options"></a>Opções  
 **SQL Server**  
 Especifica a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] conectada atualmente. Esse campo é populado automaticamente e não pode ser atualizado.  
  
 **Backup de banco de dados**  
 Especifique o banco de dados onde está localizada a tabela de rastreamento.  
  
 **Proprietário**  
 Specifies the owner of the trace table. Este campo é populado automaticamente como **dbo**.  
  
 **Tabela**  
 Especifique o nome da tabela de rastreamento a partir da qual deve ser lido o rastreamento.  
  
## <a name="see-also"></a>Consulte Também  
 [Salvar resultados de rastreamento em uma tabela &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)   
 [Modelos e permissões do SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Database Engine Tuning Advisor](../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  

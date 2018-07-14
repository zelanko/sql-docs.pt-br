---
title: SQL Server Profiler - mecanismo de banco de dados de tabela fonte orientador de otimização – selecione a tabela de carga de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.tools.sourcetable.f1
helpviewer_keywords:
- Select Workload Table dialog box
- Source Table dialog box
ms.assetid: 51185be7-7092-480a-a52c-cf7786c4a0a0
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c371644630c24946b4acc50d77916fb8d0fd4a4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285682"
---
# <a name="sql-server-profiler---source-table-database-engine-tuning-advisor---select-workload-table"></a>Tabela do SQL Server Profiler - mecanismo de banco de dados de tabela fonte orientador de otimização – selecione carga de trabalho
  O Microsoft [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] e o Orientador de Otimização do [!INCLUDE[ssDE](../includes/ssde-md.md)] usam essa caixa de diálogo para selecionar tabelas.  
  
 No [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], use a caixa de diálogo **Tabela de Origem** para especificar uma tabela de origem para uma tabela de rastreamento. This is a table from which a trace is loaded, and the contents of which are viewed or used for replaying the trace.  
  
 No Orientador de Otimização do [!INCLUDE[ssDE](../includes/ssde-md.md)], use a caixa de diálogo **Selecionar Tabela de Carga de Trabalho** para selecionar uma tabela de banco de dados que contém informações de rastreamento do [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para usar como uma carga de trabalho de otimização ou para visualizar o conteúdo da tabela antes de iniciar a análise de otimização.  
  
## <a name="options"></a>Opções  
 **SQL Server**  
 Especifica a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] conectada atualmente. Esse campo é populado automaticamente e não pode ser atualizado.  
  
 **Backup de banco de dados**  
 Especifique o banco de dados onde está localizada a tabela de rastreamento.  
  
 **Proprietário**  
 Specifies the owner of the trace table. Este campo é populado automaticamente como **dbo**.  
  
 **Table**  
 Especifique o nome da tabela de rastreamento a partir da qual deve ser lido o rastreamento.  
  
## <a name="see-also"></a>Consulte também  
 [Salvar resultados de rastreamento em uma tabela &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)   
 [Modelos e permissões do SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Orientador de Otimização do Mecanismo de Banco de Dados](../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  

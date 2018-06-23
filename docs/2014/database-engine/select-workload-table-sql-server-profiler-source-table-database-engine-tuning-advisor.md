---
title: Criador de perfil do SQL Server – mecanismo de banco de dados de tabela fonte do Orientador de otimização - Selecionar tabela de carga de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.pro.replay.tools.sourcetable.f1
helpviewer_keywords:
- Select Workload Table dialog box
- Source Table dialog box
ms.assetid: 51185be7-7092-480a-a52c-cf7786c4a0a0
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8b5ccfddb032fb3833e517632290cfdf7d82e643
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007991"
---
# <a name="sql-server-profiler---source-table-database-engine-tuning-advisor---select-workload-table"></a>Tabela do SQL Server Profiler – mecanismo de banco de dados de tabela fonte do Orientador de otimização - Select de carga de trabalho
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
  
  
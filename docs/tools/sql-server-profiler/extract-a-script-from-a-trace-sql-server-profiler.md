---
title: Extrair um script de um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scripts [SQL Server], traces
- extracting script from trace [SQL Server]
ms.assetid: 431126a6-ff91-4818-8763-4442152bd571
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 80d6996f5a6ccdd9f5ada54e30800dad22c4ad20
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="extract-a-script-from-a-trace-sql-server-profiler"></a>Extrair um script de um rastreamento (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como extrair eventos do [!INCLUDE[tsql](../../includes/tsql-md.md)] de um arquivo ou de uma tabela de rastreamento e salvá-los como um arquivo de script do [!INCLUDE[tsql](../../includes/tsql-md.md)] usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-extract-a-transact-sql-script-from-a-trace-file-or-table"></a>Para extrair um script Transact-SQL de um arquivo ou tabela de rastreamento  
  
1.  Abra o arquivo ou tabela de rastreamento que contém os eventos [!INCLUDE[tsql](../../includes/tsql-md.md)] que você deseja salvar em um arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obter mais informações, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) ou do [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
2.  No menu **Arquivo**, aponte para **Exportar**, aponte para **Extrair Eventos do SQL Server** e clique em **Extrair Eventos Transact-SQL**.  
  
3.  Na caixa de diálogo **Salvar Como** , digite um nome para o arquivo [!INCLUDE[tsql](../../includes/tsql-md.md)] e clique em **Salvar**.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

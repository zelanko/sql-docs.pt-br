---
title: Extrair um script de um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scripts [SQL Server], traces
- extracting script from trace [SQL Server]
ms.assetid: 431126a6-ff91-4818-8763-4442152bd571
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 035df37fccf2507195e6576e062b7ce254dd1dba
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009874"
---
# <a name="extract-a-script-from-a-trace-sql-server-profiler"></a>Extrair um script de um rastreamento (SQL Server Profiler)
  Este tópico descreve como extrair eventos [!INCLUDE[tsql](../../includes/tsql-md.md)] de um arquivo ou tabela de rastreamento e salvá-los em um arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-extract-a-transact-sql-script-from-a-trace-file-or-table"></a>Para extrair um script Transact-SQL de um arquivo ou tabela de rastreamento  
  
1.  Abra o arquivo ou tabela de rastreamento que contém os eventos [!INCLUDE[tsql](../../includes/tsql-md.md)] que você deseja salvar em um arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obter mais informações, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) ou [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md).  
  
2.  No menu **Arquivo**, aponte para **Exportar**, aponte para **Extrair Eventos do SQL Server** e clique em **Extrair Eventos Transact-SQL**.  
  
3.  Na caixa de diálogo **Salvar Como** , digite um nome para o arquivo [!INCLUDE[tsql](../../includes/tsql-md.md)] e clique em **Salvar**.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
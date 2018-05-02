---
title: Exibir informações de filtro (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
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
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: 8d002dea-376a-452c-b3ca-3e93656ed75f
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 04c9af7d7f050918c00af72165478a59aa76e0f9
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="view-filter-information-sql-server-profiler"></a>Exibir informações de filtro (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como exibir filtros em colunas de dados para classes de evento usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-view-filter-information"></a>Para exibir informações de filtro  
  
1.  Abra um arquivo de rastreamento, tabela de rastreamento ou um script SQL e, no menu **Arquivo** , clique em **Propriedades**. Se você estiver editando um modelo de rastreamento ou criando um rastreamento novo, ignore esta etapa.  
  
2.  Na guia **Seleção de Eventos** , clique com o botão direito do mouse no nome da coluna de dados do filtro que deseja exibir e clique em **Editar Filtro de Coluna**.  
  
3.  Na caixa de diálogo **Editar Filtro** , expanda os operadores de comparação de filtro para consultar o valor atribuído ao critério especificado. Repita as Etapas 2 e 3 para todas as colunas cujas informações de filtro quiser visualizar.  
  
> [!NOTE]  
>  Operadores de comparação que já têm valores atribuídos são formatados em negrito.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

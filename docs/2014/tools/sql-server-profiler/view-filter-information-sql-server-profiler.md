---
title: Exibir informações de filtro (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: 8d002dea-376a-452c-b3ca-3e93656ed75f
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d0c040ead976dc02e8309cb65dbd615acd11ae3d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253828"
---
# <a name="view-filter-information-sql-server-profiler"></a>Exibir informações de filtro (SQL Server Profiler)
  Este tópico descreve como exibir filtros em colunas de dados de classes de evento, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-view-filter-information"></a>Para exibir informações de filtro  
  
1.  Abra um arquivo de rastreamento, tabela de rastreamento ou um script SQL e, no menu **Arquivo** , clique em **Propriedades**. Se você estiver editando um modelo de rastreamento ou criando um rastreamento novo, ignore esta etapa.  
  
2.  Na guia **Seleção de Eventos** , clique com o botão direito do mouse no nome da coluna de dados do filtro que deseja exibir e clique em **Editar Filtro de Coluna**.  
  
3.  Na caixa de diálogo **Editar Filtro** , expanda os operadores de comparação de filtro para consultar o valor atribuído ao critério especificado. Repita as Etapas 2 e 3 para todas as colunas cujas informações de filtro quiser visualizar.  
  
> [!NOTE]  
>  Operadores de comparação que já têm valores atribuídos são formatados em negrito.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  

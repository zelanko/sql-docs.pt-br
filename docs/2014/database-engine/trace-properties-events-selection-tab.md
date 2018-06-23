---
title: Propriedades de rastreamento (guia de seleção de eventos) | Microsoft Docs
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
- sql12.pro.traceproperties.eventsselection.f1
helpviewer_keywords:
- Trace Properties dialog box
ms.assetid: e1892f24-7272-4d5d-8926-6150cc82b2c3
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 627785dc9be7d6b2d270d82f1bc6797c98980779
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116208"
---
# <a name="trace-properties-events-selection-tab"></a>Propriedades do Rastreamento (guia Seleção de Eventos)
  Use a guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Rastreamento** para exibir ou especificar eventos do rastreamento e colunas de dados.  
  
## <a name="options"></a>Opções  
 Coluna**Eventos**   
 Especifique os eventos do rastreamento marcando ou desmarcando a caixa de seleção na coluna de eventos. Os**Eventos** são organizados por categoria de evento. As classes de evento especificadas no modelo são selecionadas automaticamente. Para obter mais informações, confira [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 Colunas de dados  
 Especifique as colunas de dados do rastreamento marcando a caixa correspondente ao evento e a coluna de dados necessária. Por padrão, todas as colunas de dados pertinentes são marcadas para cada evento incluído no rastreamento.  
  
 Especifique os filtros clicando no cabeçalho da coluna de dados e digitando os critérios de filtro. As colunas de dados filtrados são indicadas por um ícone de filtro à esquerda do rótulo da coluna na caixa de diálogo **Editar Filtro** . Para obter mais informações, consulte [SQL Server Profiler - Editar Filtro](../../2014/database-engine/sql-server-profiler-edit-filter.md).  
  
 **Mostrar todos os eventos**  
 Mostra todos os eventos disponíveis. Por padrão, somente as linhas selecionadas na grade **Seleção de Eventos** são exibidas. Desmarque essa caixa para ocultar todos os eventos não selecionados na grade **Seleção de Eventos** .  
  
 **Mostrar todas as colunas**  
 Mostra todas as colunas de dados disponíveis. Por padrão, somente colunas de dados selecionadas são exibidas. Desmarque essa caixa para ocultar todas as colunas de dados não selecionadas na grade **Seleção de Eventos** .  
  
 **Filtros de coluna**  
 Abre a caixa de diálogo **Editar Filtro** . Você pode usar essa caixa de diálogo para editar filtros de coluna de dados.  
  
 **Organizar Colunas**  
 Altera a ordem das colunas no rastreamento e agrupa os resultados em uma ou mais colunas.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar eventos e colunas de dados para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Organizar colunas exibidas em um rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [Filtrar eventos em um rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [Exibir informações de filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [Modificar um filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [Modelos e permissões do SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
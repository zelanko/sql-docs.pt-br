---
title: Propriedades da tabela (guia seleção de eventos) de rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracetableproperties.eventsselection.f1
helpviewer_keywords:
- Trace Table Properties dialog box
ms.assetid: fa21df6a-b6b5-4b15-9104-957385821594
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 77660e19bed6781d73efdd36e6a752ae5c3cc1fb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169136"
---
# <a name="trace-table-properties-events-selection-tab"></a>Propriedades da Tabela de Rastreamento (Guia Seleção de Eventos)
  Use a guia **Seleção de Eventos** da caixa de diálogo **Propriedades da Tabela de Rastreamento** para exibir eventos e propriedades da coluna de dados do rastreamento ou para remover eventos ou colunas do rastreamento.  
  
 Para visualizar esta janela, use o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para abrir uma tabela de rastreamento. Em seguida, no menu **Arquivo** , clique em **Propriedades**e na guia **Seleção de Eventos** .  
  
## <a name="options"></a>Opções  
 Coluna **Eventos**  
 Exiba eventos rastreados organizados por categoria de evento. Eventos podem ser selecionados marcando a caixa ou uma coluna de dados referente a um evento. Se a caixa do evento estiver marcada, todas as colunas de dados disponíveis desse evento serão selecionadas. Se a coluna de dados de um evento estiver marcada, o evento será marcado e qualquer outra coluna necessária também será automaticamente marcada. Se você estiver exibindo uma tabela ou arquivo de rastreamento, desmarcar as caixas de seleção de eventos ou colunas de dados reduzirá o total de dados visíveis na janela de rastreamento para uma análise mais fácil. Você também pode alterar os filtros de coluna para reduzir o total de dados visíveis na janela de rastreamento. Para obter mais informações sobre classes de evento, consulte [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 Outras colunas de dados  
 Exiba colunas de dados rastreadas. Todas as colunas de dados pertinentes no rastreamento são selecionadas por padrão para cada evento incluído no rastreamento.  
  
 Especifique os filtros clicando no cabeçalho da coluna de dados e digitando os critérios de filtro. As colunas de dados filtrados são indicadas por um ícone de filtro à esquerda do rótulo da coluna na caixa de diálogo **Editar Filtro** .  
  
 **Mostrar todos os eventos**  
 Mostra todos os eventos disponíveis. Por padrão, somente as linhas selecionadas na grade **Seleção de Eventos** são exibidas. Desmarque essa caixa para ocultar todos os eventos não selecionados na grade **Seleção de Eventos** . Se a opção **Mostrar todos os eventos** estiver marcada e você estiver visualizando uma tabela ou arquivo de rastreamento, todos os eventos que foram gravados no rastreamento serão exibidos na janela de rastreamento.  
  
 **Mostrar todas as colunas**  
 Mostra todas as colunas de dados disponíveis. Por padrão, somente colunas de dados selecionadas são exibidas. Desmarque essa caixa para ocultar todas as colunas de dados não selecionadas na grade **Seleção de Eventos** .  
  
 **Filtros de coluna**  
 Inicia a caixa de diálogo **Editar Filtro**, que exibe um ícone de filtro à esquerda do rótulo da coluna. Você pode usar essa caixa de diálogo para editar filtros de coluna de dados.  
  
 **Organizar Colunas**  
 Depois de selecionar **Eventos** e colunas de dados a serem rastreados, clique em **Organizar Colunas** para forçar a grade a reclassificar a coluna na janela de resultados do rastreamento.  
  
## <a name="see-also"></a>Consulte também  
 [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [Modelos e permissões do SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

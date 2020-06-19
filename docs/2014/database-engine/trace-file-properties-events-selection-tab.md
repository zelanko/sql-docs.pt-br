---
title: Propriedades do arquivo de rastreamento (guia Seleção de eventos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracefileproperties.eventsselection.f1
helpviewer_keywords:
- Trace File Properties dialog box
ms.assetid: 158d442f-2225-4173-8545-fb1cf611b4d0
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 20ec4981a7a4c7f2d09315416deddc5e0e195fda
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928353"
---
# <a name="trace-file-properties-events-selection-tab"></a>Propriedades do Arquivo de Rastreamento(Guia Seleção de Eventos)
  Use a guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Arquivo de Rastreamento** para exibir as propriedades da coluna do rastreamento ou remover colunas de dados do rastreamento.  
  
 Para exibir essa janela, abra um arquivo de rastreamento. Em seguida, no menu **Arquivo** , clique em **Propriedades**e, então, clique na guia **Seleção de Eventos** .  
  
## <a name="options"></a>Opções  
 Coluna**Eventos**  
 Exiba eventos rastreados organizados por categoria de evento. Inicialmente, todos os eventos no rastreamento são selecionados. Eventos podem ser selecionados marcando a caixa ou uma coluna de dados referente a um evento. Se a caixa do evento estiver marcada, todas as colunas de dados disponíveis desse evento serão selecionadas. Se a coluna de dados de um evento estiver marcada, o evento será marcado e qualquer outra coluna necessária também será automaticamente marcada. Se você estiver exibindo uma tabela ou arquivo de rastreamento, desmarcar as caixas de seleção de eventos ou colunas de dados reduzirá o total de dados visíveis na janela de rastreamento para uma análise mais fácil. Você também pode alterar os filtros de coluna para reduzir o total de dados visíveis na janela de rastreamento. Para obter mais informações sobre classes de evento, consulte [Referência de classe de evento do SQL Server](../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 Colunas de dados  
 Exiba colunas de dados rastreadas. Todas as colunas de dados pertinentes no rastreamento são selecionadas por padrão para cada evento incluído no rastreamento.  
  
 Especifique os filtros clicando no cabeçalho da coluna de dados e digitando os critérios de filtro. As colunas de dados filtrados são indicadas por um ícone de filtro à esquerda do rótulo da coluna na caixa de diálogo **Editar Filtro** .  
  
 **Mostrar todos os eventos**  
 Mostra todos os eventos disponíveis. Por padrão, somente as linhas selecionadas na grade **Seleção de Eventos** são exibidas. Desmarque essa caixa para ocultar todos os eventos não selecionados na grade **Seleção de Eventos** . Se a opção **Mostrar todos os eventos** estiver marcada e você estiver visualizando uma tabela ou arquivo de rastreamento, todos os eventos que foram gravados no rastreamento serão exibidos na janela de rastreamento.  
  
 **Mostrar todas as colunas**  
 Mostra todas as colunas de dados disponíveis. Por padrão, somente colunas de dados selecionadas são exibidas. Desmarque essa caixa para ocultar todas as colunas de dados não selecionadas na grade **Seleção de Eventos** .  
  
 **Filtros de coluna**  
 Inicia a caixa de diálogo **Editar Filtro** , que exibe um ícone de filtro à esquerda do rótulo da coluna para colunas de dados filtrados. Use a caixa de diálogo **Editar Filtro** para editar filtros de coluna de dados.  
  
 **Organizar colunas**  
 Depois de selecionar **Eventos** e colunas de dados a serem rastreados, clique em **Organizar Colunas** para forçar a grade a reclassificar a coluna na janela de resultados do rastreamento.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar eventos e colunas de dados para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Filtrar eventos em um &#40;de rastreamento SQL Server Profiler&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [Exibir informações de filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [Modificar um filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)   
 [Modelos e permissões do SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
  
  

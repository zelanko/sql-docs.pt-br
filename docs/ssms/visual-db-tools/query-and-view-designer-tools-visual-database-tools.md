---
title: "Ferramentas do Designer de Consulta e Exibição (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.querydesigner
- vdt.pane.diagram
- vdt.pane.grid
- vdt.dlgbox.querybuilder
- vdt.pane.sql
- vdt.pane.results
helpviewer_keywords:
- Query Designer [SQL Server], panes
- View Designer, panes
- Query Designer [SQL Server], components
- View Designer, components
ms.assetid: 12e4b5a5-b793-4b6c-a0e5-c450c49bf26f
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e5e890d0a453291ba71ab06b0489fb3d0c8c216a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="query-and-view-designer-tools-visual-database-tools"></a>Ferramentas do Designer de Consulta e Exibição (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Quando você cria uma consulta, uma exibição, uma função embutida ou um único procedimento armazenado de instrução, o designer que você usa consiste em quatro painéis: painel diagrama, painel Critérios, painel SQL e painel Resultados.  
  
![Designer de consulta](../../ssms/visual-db-tools/media/vs_queryviewdsgpanes.gif "Designer de consulta")  
  
-   O painel Diagrama exibe as tabelas e outros objetos com valores de tabela que você está consultando. Cada retângulo representa uma tabela ou um objeto com valor de tabela e mostra as colunas de dados disponíveis. Junções são indicadas por linhas entre os retângulos. Para obter mais informações, consulte [Painel Diagrama &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md).  
  
-   O painel Critérios contém uma grade do tipo planilha na qual você especifica opções, como colunas de dados para exibição, linhas a serem selecionadas, como agrupar linhas, e assim por diante. Para obter mais informações, consulte [Painel Critérios &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md).  
  
-   O painel SQL exibe a instrução SQL para a consulta ou exibição. Você pode editar a instrução SQL criada pelo Designer ou pode inserir a sua própria instrução SQL. É particularmente útil inserir instruções SQL que não possam ser criadas pelos painéis Diagrama e Critério, como consultas de união. Para obter mais informações, consulte [Painel SQL &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
-   O painel Resultados mostra uma grade com dados recuperados pela consulta ou exibição. No Designer de Consulta e Exibição, o painel mostra os resultados da consulta de SELECT executada mais recentemente. Você pode modificar o banco de dados editando valores nas células da grade e pode adicionar ou excluir linhas. Para obter mais informações, consulte [Painel de Resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md).  
  
Você pode criar uma consulta ou exibição trabalhando em qualquer painel: é possível especificar uma coluna a ser exibida, escolhendo-a no painel Diagrama, inserindo-a no painel Critérios ou tornando-a parte da instrução SQL no painel SQL.  
  
## <a name="displaying-and-hiding-panes"></a>Exibindo e ocultando painéis  
Para ocultar ou exibir um painel que não esteja visível, clique com o botão direito do mouse na superfície de design, aponte para **Painel**e clique no nome do painel. Se o Designer de Consulta e Exibição for aberto em modo Designer de Consultas, o painel de **Resultados** não estará disponível.  
  
## <a name="see-also"></a>Consulte também  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Abrir o Designer de Consulta e Exibição &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-the-query-and-view-designer-visual-database-tools.md)  
[Editor SQL &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-editor-visual-database-tools.md)  
  

---
title: Criar um modelo de rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- saving trace template
ms.assetid: 025868b0-3790-4cda-8757-5a58327bfba0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f37369821585845d63bd4d416b1868364045680f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63255774"
---
# <a name="create-a-trace-template-sql-server-profiler"></a>Criar um modelo de rastreamento (SQL Server Profiler)
  Este tópico descreve como criar um novo modelo de rastreamento usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-create-a-trace-template"></a>Para criar um modelo de rastreamento  
  
1.  No menu **Arquivo** , aponte para **Modelos**e clique em **Novo Modelo**.  
  
2.  Na caixa de diálogo **Propriedades do Modelo de Rastreamento** , selecione um tipo de servidor na lista **Selecionar tipo de servidor**.  
  
3.  Na caixa **Nome do novo modelo** , insira um nome para o modelo.  
  
4.  Opcionalmente, clique em **Basear novo modelo no existente**e selecione um modelo na lista.  
  
     Todos os eventos, colunas de dados e filtros são inicialmente definidos como especificado no modelo selecionado.  
  
5.  Opcionalmente, clique em **Usar como modelo padrão para o tipo de servidor selecionado**.  
  
6.  Na guia **Seleção de Eventos** , adicione, remova ou modifique eventos, colunas de dados ou filtros.  
  
7.  No menu **Seleção de Eventos**, use o controle da grade para adicionar ou remover eventos e colunas de dados do arquivo de rastreamento, da maneira abaixo:  
  
    -   Para adicionar um evento, expanda a categoria de evento apropriada na coluna **Eventos** e selecione o nome do evento.  
  
    -   Quando um evento é adicionado, todas as colunas de dados relevantes são incluídas, por padrão. Para remover uma coluna de dados de um evento do rastreamento, desmarque a caixa de seleção correspondente ao evento na coluna de dados.  
  
    -   Para adicionar filtros, clique no nome de coluna de dados e especifique os critérios de filtro na caixa de diálogo **Editar Filtro** . Você também pode clicar com o botão direito do mouse no nome da coluna de dados e em **Editar Filtro de Coluna** para iniciar a caixa de diálogo **Editar Filtro** . Para adicionar o filtro, clique em **OK** .  
  
8.  Clique em **Salvar**.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar eventos e colunas de dados para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Derivar um modelo de um rastreamento em execução &#40;SQL Server Profiler&#41;](derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [Derivar um modelo de um arquivo ou de uma tabela de rastreamento &#40;SQL Server Profiler&#41;](derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [Modelos e permissões do SQL Server Profiler](sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  

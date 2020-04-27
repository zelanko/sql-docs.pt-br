---
title: Modificar um modelo de rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- modifying traces
ms.assetid: b81df2a1-e202-43d8-92b0-0beb145f0116
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 64c13b9fed062b73de7ab35ef5048ae4b68e5618
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089994"
---
# <a name="modify-a-trace-template-sql-server-profiler"></a>Modificar um modelo de rastreamento (SQL Server Profiler)
  Este tópico descreve como modificar um modelo de rastreamento usando o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)].  
  
### <a name="to-modify-a-trace-template"></a>Para modificar um modelo de rastreamento  
  
1.  No menu **Arquivo** , aponte para **Modelos**e clique em **Editar Modelo**.  
  
2.  Na caixa de diálogo **Propriedades do Modelo de Rastreamento** , na guia **Geral** , você pode modificar o tipo de servidor e o nome do modelo ou optar por usar um modelo padrão para o tipo de servidor.  
  
3.  Na guia **seleção de eventos**, use o controle de grade para adicionar ou remover eventos e colunas de dados do arquivo de rastreamento da seguinte maneira.  
  
    -   Para adicionar um evento, expanda a categoria de evento apropriada na coluna **Eventos** e selecione o nome do evento.  
  
    -   Quando um evento é adicionado, todas as colunas de dados relevantes são incluídas, por padrão. Para remover uma coluna de dados de um evento do rastreamento, desmarque a caixa de seleção correspondente ao evento na coluna de dados.  
  
    -   Para adicionar filtros, clique no nome de coluna de dados e especifique os critérios de filtro na caixa de diálogo **Editar Filtro** . Você também pode clicar com o botão direito do mouse no nome da coluna de dados e em **Editar Filtro de Coluna** para iniciar a caixa de diálogo **Editar Filtro** . Para adicionar o filtro, clique em **OK** .  
  
4.  Clique em **Salvar**ou em **Salvar Como**para salvar o modelo de rastreamento com outro nome.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar eventos e colunas de dados para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Derive um modelo de um rastreamento em execução &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [Derive um modelo de um arquivo ou tabela de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [Modelos e permissões de SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

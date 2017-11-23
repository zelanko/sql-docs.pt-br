---
title: Modificar modelos de rastreamento | Microsoft Docs
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- modifying trace templates
- SQL Server Profiler, templates
ms.assetid: 75b62a54-8d16-4599-bd2d-c42cfcc209f4
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a4a1623a6b5920ae849afc17a4079da12efe450
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="modify-trace-templates"></a>Modificar modelos de rastreamento
  Você pode modificar os modelos salvos em um arquivo no computador local em que é executado o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] . Você também pode modificar modelos derivados desses arquivos. Ao modificar modelos existentes, edite as propriedades do modelo, como classes de evento e colunas de dados, na mesma ordem em que essas propriedades foram definidas originalmente, na guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Rastreamento** . As classes de evento e colunas de dados podem ser adicionadas ou removidas e os filtros podem ser alterados. Depois que o modelo é modificado, um modelo específico ao usuário é criado, mantendo-se intacto o modelo do sistema original. Para obter mais informações, veja [Salvar rastreamentos e modelos de rastreamento](../../tools/sql-server-profiler/save-traces-and-trace-templates.md).  
  
 Talvez seja necessário derivar um modelo de um arquivo de rastreamento, caso você não consiga se lembrar do modelo original usado para criar o rastreamento (ou não o tenha salvado) ou se desejar executar o mesmo rastreamento em data futura. Ao trabalhar com rastreamentos existentes, você pode exibir as propriedades, mas não pode modificá-las. Para modificar as propriedades, interrompa ou pause o rastreamento. Para obter mais informações, veja [Derivar um modelo com base em um arquivo ou uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md) e [Derivar um modelo de um rastreamento em execução &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md).  
  
## <a name="to-modify-a-trace-template"></a>Para modificar um modelo de rastreamento  
  
1.  No menu **Arquivo** , aponte para **Modelos**e clique em **Editar Modelo**.  
  
2.  Na caixa de diálogo **Propriedades do Modelo de Rastreamento** , na guia **Geral** , você pode modificar o tipo de servidor e o nome do modelo ou optar por usar um modelo padrão para o tipo de servidor.  
  
3.  Sobre o **seleção de eventos** guia, use o controle de grade para adicionar ou remover eventos e colunas de dados do arquivo de rastreamento da seguinte maneira.  
  
    -   Para adicionar um evento, expanda a categoria de evento apropriada na coluna **Eventos** e selecione o nome do evento.  
  
    -   Quando um evento é adicionado, todas as colunas de dados relevantes são incluídas, por padrão. Para remover uma coluna de dados de um evento do rastreamento, desmarque a caixa de seleção correspondente ao evento na coluna de dados.  
  
    -   Para adicionar filtros, clique no nome de coluna de dados e especifique os critérios de filtro na caixa de diálogo **Editar Filtro** . Você também pode clicar com o botão direito do mouse no nome da coluna de dados e em **Editar Filtro de Coluna** para iniciar a caixa de diálogo **Editar Filtro** . Para adicionar o filtro, clique em **OK** .  
  
4.  Clique em **salvar**, ou clique em **Salvar como** para salvar o modelo de rastreamento com outro nome.  
  
## <a name="next-steps"></a>Próximas etapas  
[Iniciar um rastreamento](../../tools/sql-server-profiler/start-a-trace.md)  
[Criar um rastreamento](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
[Modificar um rastreamento existente usando o Transact-SQL](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
[Especificar eventos e colunas de dados para um rastreamento usando o SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
[SP-rastreamento-setevent-transact-sql](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  

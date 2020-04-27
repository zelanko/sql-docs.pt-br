---
title: SQL Server Profiler-organizar colunas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.organize.columns.f1
ms.assetid: bf5674f4-da5e-43f9-aeb2-76ca37993790
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f0ad3d1204e8c27d91ecb3b586d56a27d45eeb4e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089762"
---
# <a name="sql-server-profiler---organize-columns"></a>SQL Server Profiler – Organizar Colunas
  Use a caixa de diálogo **Organizar Colunas** para selecionar colunas de dados para agrupar ou agregar eventos exibidos em um rastreamento, o que torna os arquivos ou tabelas de rastreamento grandes mais fáceis de exibir e analisar.  
  
 A agregação movimenta e recolhe todos os eventos no rastreamento em seu respectivo tipo de classe de evento. Um sinal de adição**+**() aparece à esquerda do nome da classe de evento. Clicando no sinal de mais, você expande a classe de evento para exibir todos os eventos desse tipo.  
  
 O agrupamento organiza todas as classes de evento de um tipo específico juntando-as na janela de rastreamento. Porém, os eventos não são recolhidos sob o tipo de classe de evento.  
  
 Quando você agrupa ou agrega eventos em uma janela de rastreamento, as colunas selecionadas para agrupamento ou agregação permanecem fixas na janela de exibição, mas é possível rolar para a direita ou esquerda a fim de exibir todas as outras colunas de dados.  
  
 Para acessar essa caixa de diálogo, abra um arquivo ou tabela de rastreamento existente e clique em **Propriedades** no menu [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] **Arquivo** do . Na caixa de diálogo **Propriedades do Rastreamento** , clique na guia **Seleção de Eventos** e em **Organizar Colunas**. Você também pode clicar em **Organizar Colunas** na guia **Seleção de Eventos** ao criar um rastreamento novo.  
  
## <a name="options"></a>Opções  
 **Grupos**  
 Mova os nomes da coluna de dados sob **Grupos** para agrupar ou agregar classes de evento na janela de rastreamento.  
  
 Para agregar eventos, mova uma coluna de dados para **Grupos**. Com isso, todos os eventos de um tipo específico são recolhidos abaixo do nome do tipo de classe de evento na janela de rastreamento. Um sinal de adição**+**() aparece à esquerda do nome da classe de evento. Clique no sinal de mais para expandir o tipo de classe de evento e exibir todos os eventos. Você pode ativar e desativar a agregação e o agrupamento clicando em **Exibição Agregada** ou **Exibição Agrupada** no menu **Exibição** .  
  
 Para agrupar eventos, mova mais de uma coluna de dados para **Grupos**. Com isso, todos os eventos de um tipo específico são agrupados na janela de rastreamento, mas os eventos não são recolhidos abaixo do nome de cada tipo de classe de evento. Você pode alternar entre exibições agrupadas e não agrupadas clicando em **Exibição Agrupada** no menu Exibição. Quando mais de uma coluna de dados é movida para **Grupos**, a opção de alternar para a **Exibição Agregada** fica indisponível.  
  
 **Colunas**  
 Lista de colunas de dados disponíveis para serem movidas para **Grupos**. Clique no sinal de adição**+**() à esquerda das **colunas** para expandir a lista.  
  
 **Para cima**  
 Depois de selecionar uma coluna de dados, clique em **Para Cima** para mover colunas de dados para **Grupos**. Você também pode clicar em **Acima** para reorganizar a exibição de colunas na janela de rastreamento.  
  
 **Para baixo**  
 Depois de selecionar uma coluna de dados, clique em **Para Baixo** para mover as colunas de dados para fora de **Grupos**. Você também pode clicar em **Abaixo** para reorganizar a exibição de colunas na janela de rastreamento.  
  
## <a name="see-also"></a>Consulte Também  
 [Organizar colunas exibidas em um &#40;de rastreamento SQL Server Profiler&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [Criar um &#40;de rastreamento SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [Criar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)   
 [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
  

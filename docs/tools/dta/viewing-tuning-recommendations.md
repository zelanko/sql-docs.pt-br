---
title: "Exibindo recomenda&#231;&#245;es de ajuste | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "Mecanismo de banco de dados [SQL Server], tutoriais"
ms.assetid: e4e690c9-434f-4b01-b4de-0b905323ddd6
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Exibindo recomenda&#231;&#245;es de ajuste
Esta tarefa usa a sessão de ajuste criada no [Tuning a Workload](../../tools/dta/tuning-a-workload.md). Depois que você ajusta o banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] usando o script MyScript.sql [!INCLUDE[tsql](../../includes/tsql-md.md)] , o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] exibe os resultados na guia **Recomendações** . A tarefa a seguir apresenta a guia **Recomendações** da GUI (interface gráfica do usuário) do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e explica como explorar as informações fornecidas sobre os resultados da sessão de ajuste.  
  
### Exibir recomendações de ajuste  
  
1.  Iniciar o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Consulte [Iniciando o Orientador de Otimização do Mecanismo de Banco de Dados](../../tools/dta/launching-database-engine-tuning-advisor.md). Verifique se você está conectado à mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada na prática [Ajustando uma carga de trabalho](../../tools/dta/tuning-a-workload.md).  
  
2.  Clique duas vezes em **MySession** no painel **Monitor de Sessão**. [!INCLUDE[ssDE](../../includes/ssde-md.md)] carrega a informações da sessão de ajuste anterior e exibe a guia **Recomendações** . Observe que o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não fez **Recomendações de Partição** porque você aceitou todas as opções de ajuste padrão e **Nenhum particionamento** foi selecionado na guia **Opções de Ajuste** .  
  
3.  Na guia **Recomendações** , use a barra de rolagem na parte inferior da página da guia para exibir todas as colunas de **Recomendações de Índice** . Cada linha representa um objeto de banco de dados (índices ou exibições indexadas) que o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] recomenda que sejam descartadas ou criadas. Role a tela até a coluna mais à direita e clique em **Definição**. [!INCLUDE[ssDE](../../includes/ssde-md.md)] exibe uma janela **Visualização de Script SQL** , na qual você pode exibir o script [!INCLUDE[tsql](../../includes/tsql-md.md)] que cria ou descarta o objeto de banco de dados nessa linha. Clique em **Fechar** para fechar a janela de visualização.  
  
    Se você estiver tendo dificuldades em localizar uma **Definição** que contenha um link, clique para desmarcar a caixa de seleção **Mostrar objetos existentes** na parte inferior da página da guia, o que diminuirá o número de linhas exibidas. Quando você desmarca essa caixa de seleção, o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] mostra só os objetos para os quais gerou uma recomendação. Marque a caixa de seleção **Mostrar objetos existentes** para exibir todos os objetos do banco de dados que existem atualmente no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Use a barra de rolagem à direita da página da guia para exibir todos os objetos.  
  
4.  Clique com o botão direito do mouse na grade do painel **Recomendações de Índice**. Esse menu permite marcar e desmarcar recomendações. Permite também alterar a fonte do texto da grade.  
  
5.  No menu **Ações** , clique em **Salvar Recomendações** para salvar todas as recomendações em um script [!INCLUDE[tsql](../../includes/tsql-md.md)] . Nomeie o script como **MySessionRecommendations.sql**.  
  
    Abra o script MySessionRecommendations.sql no Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibi-lo. Você poderia aplicar as recomendações ao banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] executando o script no Editor de Consultas, mas não faça isso. Feche o script no Editor de Consultas sem executá-lo.  
  
    Como uma alternativa, você também pode aplicar as recomendações clicando em **Aplicar Recomendações** no menu **Ações** do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , mas não aplique essas recomendações nesta prática.  
  
6.  Se houver mais de uma recomendação na guia **Recomendações** , desmarque algumas das linhas que listam objetos do banco de dados na grade **Recomendações de Índice** .  
  
7.  No menu **Ações** , clique em **Avaliar Recomendações**. [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria uma nova sessão de ajuste em que você pode avaliar um subconjunto das recomendações originais em MySession.  
  
8.  Digite **EvaluateMySession** para seu novo **Nome da sessão**e clique no botão **Iniciar Análise** na barra de ferramentas. Você pode repetir os passos 2 e 3 para esta nova sessão de ajuste a fim de exibir suas recomendações.  
  
## Resumo  
Você exibiu o conteúdo da guia **Recomendações** para a sessão de ajuste MySession e avaliou um subconjunto de recomendações na nova sessão de ajuste EvaluateMySession.  
  
A avaliação de um subconjunto de recomendações de ajuste poderá ser necessária se você descobrir que deve alterar as opções de ajuste depois de executar uma sessão. Por exemplo, se você pedir ao Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para considerar exibições indexadas quando você especificar as opções de ajuste para uma sessão, mas depois que a recomendação for gerada você decidir não usar as exibições indexadas. Você pode usar a opção **Avaliar Recomendações** no menu **Ações** para que o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] reavalie a sessão sem considerar as exibições indexadas. Quando você usa a opção **Avaliar Recomendações** , as recomendações geradas previamente são aplicadas hipoteticamente ao design físico atual para chegar ao design físico para a segunda sessão de ajuste.  
  
Poderão ser exibidas mais informações sobre resultados de ajuste na guia **Relatórios** , que é descrita na próxima tarefa desta lição.  
  
## Próxima tarefa da lição  
[Exibindo relatórios de ajuste](../../tools/dta/viewing-tuning-reports.md)  
  
  
  

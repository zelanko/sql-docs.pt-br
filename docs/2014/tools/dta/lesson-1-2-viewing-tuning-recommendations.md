---
title: Exibindo recomendações de ajuste | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: e4e690c9-434f-4b01-b4de-0b905323ddd6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fe8d52d898db35698155518646f074e7167687a0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66110174"
---
# <a name="viewing-tuning-recommendations"></a>Exibindo recomendações de ajuste
  Esta tarefa usa a sessão de ajuste criada no [Tuning a Workload](lesson-1-1-tuning-a-workload.md). Depois de ajustar o banco [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] de dados usando o script MyScript. [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL, [!INCLUDE[ssDE](../../includes/ssde-md.md)] o Orientador de otimização exibirá seus resultados na guia **recomendações** . A tarefa a seguir apresenta a guia **recomendações** da [!INCLUDE[ssDE](../../includes/ssde-md.md)] GUI (interface gráfica do usuário) do Orientador de otimização e orienta você a explorar as informações que ele fornece sobre os resultados da sessão de ajuste.  
  
### <a name="view-tuning-recommendations"></a>Exibir recomendações de ajuste  
  
1.  Iniciar o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Consulte [Iniciando o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md). Verifique se você está conectado à mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada na prática [Ajustando uma carga de trabalho](lesson-1-1-tuning-a-workload.md).  
  
2.  Clique duas vezes em **MySession** no painel **Monitor de Sessão** . [!INCLUDE[ssDE](../../includes/ssde-md.md)]O Orientador de otimização carrega as informações de sessão de sua sessão de **** ajuste anterior e exibe a [!INCLUDE[ssDE](../../includes/ssde-md.md)] guia recomendações. Observe que o Orientador de otimização não fez nenhuma **recomendação de partição** porque você aceitou todos os padrões de opção de ajuste e **nenhum particionamento** foi selecionado na guia **Opções de ajuste** .  
  
3.  Na guia **Recomendações** , use a barra de rolagem na parte inferior da página da guia para exibir todas as colunas de **Recomendações de Índice** . Cada linha representa um objeto de banco de dados (índices ou exibições indexadas) que o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] recomenda que sejam descartadas ou criadas. Role a tela até a coluna mais à direita e clique em **Definição**. [!INCLUDE[ssDE](../../includes/ssde-md.md)]Exibe uma janela de **visualização de script SQL** , na qual você pode [!INCLUDE[tsql](../../includes/tsql-md.md)] exibir o script que cria ou descarta o objeto de banco de dados nessa linha. Clique em **Fechar** para fechar a janela de visualização.  
  
     Se você estiver tendo dificuldades em localizar uma **Definição** que contenha um link, clique para desmarcar a caixa de seleção **Mostrar objetos existentes** na parte inferior da página da guia, o que diminuirá o número de linhas exibidas. Quando você desmarca essa caixa de seleção, o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] mostra só os objetos para os quais gerou uma recomendação. Marque a caixa de seleção **Mostrar objetos existentes** para exibir todos os objetos do banco de dados que existem atualmente no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Use a barra de rolagem à direita da página da guia para exibir todos os objetos.  
  
4.  Clique com o botão direito do mouse na grade do painel **Recomendações de Índice** . Esse menu permite marcar e desmarcar recomendações. Permite também alterar a fonte do texto da grade.  
  
5.  No menu **Ações** , clique em **Salvar Recomendações** para salvar todas as recomendações em um script [!INCLUDE[tsql](../../includes/tsql-md.md)] . Nomeie o script `MySessionRecommendations.sql`.  
  
     Abra o script MySessionRecommendations.sql no Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibi-lo. Você poderia aplicar as recomendações ao banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] executando o script no Editor de Consultas, mas não faça isso. Feche o script no Editor de Consultas sem executá-lo.  
  
     Como uma alternativa, você também pode aplicar as recomendações clicando em **Aplicar Recomendações** no menu **Ações** do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , mas não aplique essas recomendações nesta prática.  
  
6.  Se houver mais de uma recomendação na guia **Recomendações** , desmarque algumas das linhas que listam objetos do banco de dados na grade **Recomendações de Índice** .  
  
7.  No menu **Ações** , clique em **Avaliar Recomendações**. 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria uma nova sessão de ajuste em que você pode avaliar um subconjunto das recomendações originais em MySession.  
  
8.  Digite `EvaluateMySession` para o nome da nova **sessão**e clique no botão **iniciar análise** na barra de ferramentas. Você pode repetir os passos 2 e 3 para esta nova sessão de ajuste a fim de exibir suas recomendações.  
  
## <a name="summary"></a>Resumo  
 Você exibiu o conteúdo da guia **Recomendações** para a sessão de ajuste MySession e avaliou um subconjunto de recomendações na nova sessão de ajuste EvaluateMySession.  
  
 A avaliação de um subconjunto de recomendações de ajuste poderá ser necessária se você descobrir que deve alterar as opções de ajuste depois de executar uma sessão. Por exemplo, se você pedir ao Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para considerar exibições indexadas quando você especificar as opções de ajuste para uma sessão, mas depois que a recomendação for gerada você decidir não usar as exibições indexadas. Você pode usar a opção **Avaliar Recomendações** no menu **Ações** para que o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] reavalie a sessão sem considerar as exibições indexadas. Quando você usa a opção **Avaliar Recomendações** , as recomendações geradas previamente são aplicadas hipoteticamente ao design físico atual para chegar ao design físico para a segunda sessão de ajuste.  
  
 Poderão ser exibidas mais informações sobre resultados de ajuste na guia **Relatórios** , que é descrita na próxima tarefa desta lição.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Exibindo relatórios de ajuste](lesson-1-3-viewing-tuning-reports.md)  
  
  

---
title: 'Lição 2: Usando o Orientador de Otimização do Mecanismo de Banco de Dados | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 3317d4f8-ed9e-4f2e-b5f1-a6bf3a9d6c8d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9143f1d8ce6ff530ef30f7dbfcd1ca599572e5ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63001648"
---
# <a name="lesson-2-using-database-engine-tuning-advisor"></a>Lição 2: Usando o Orientador de Otimização do Mecanismo de Banco de Dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O Orientador de Otimização do Mecanismo de Banco de Dados permite gerenciar sessões de ajuste e exibir recomendações de ajuste. Usuários com conhecimento avançado de estruturas de design físico podem usar essa ferramenta para executar a análise exploratória de ajuste de banco de dados. Os iniciantes em ajuste de banco de dados também podem usar a ferramenta para encontrar a melhor configuração de estruturas de design físico para as cargas de trabalho que forem ajustar. Esta lição oferece a base prática para administradores de banco de dados que são novos usuários da interface gráfica do Orientador de Otimização do Mecanismo de Banco de Dados e para administradores de sistema que podem não ter conhecimento extenso de estruturas de design físico.  

## <a name="prerequisites"></a>Prerequisites 

Para concluir este tutorial, você precisará do SQL Server Management Studio, bem como acesso a um servidor que executa o SQL Server e um banco de dados do AdventureWorks.

- Instalar o [SQL Server Management Studio.](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)
- Instalar o [SQL Server 2017 Developer Edition.](https://www.microsoft.com/sql-server/sql-server-downloads)
- Baixar o [Banco de dados de exemplo do AdventureWorks2017.](https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017)


Instruções para restaurar bancos de dados no SSMS são encontradas em [Como restaurar um banco de dados.](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-2017)

  >[!NOTE]
  > Este tutorial destina-se um usuário familiarizado com o uso do SQL Server Management Studio e as tarefas de administração de banco de dados básico. 
  
## <a name="tuning-a-workload"></a>Como ajustar uma carga de trabalho
O Orientador de Otimização do Mecanismo de Banco de Dados pode ser usado para achar o melhor design de banco de dados físico para desempenho de consulta nos bancos de dados e tabelas que você seleciona para ajustar.  

1.  Copiar uma amostra [selecionar](../../t-sql/queries/select-examples-transact-sql.md) instrução e cole a instrução no Editor de consulta de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Salve o arquivo como **MyScript.sql** em um diretório que você possa localizar facilmente. Um exemplo que funciona no banco de dados AdventureWorks2017 foi fornecido abaixo.  

 ```sql
 Use [Adventureworks2017]; -- may need to modify database name to match database
 GO
 SELECT DISTINCT pp.LastName, pp.FirstName 
 FROM Person.Person pp JOIN HumanResources.Employee e
 ON e.BusinessEntityID = pp.BusinessEntityID WHERE pp.BusinessEntityID IN 
 (SELECT SalesPersonID 
 FROM Sales.SalesOrderHeader
 WHERE SalesOrderID IN 
 (SELECT SalesOrderID 
 FROM Sales.SalesOrderDetail
 WHERE ProductID IN 
 (SELECT ProductID 
 FROM Production.Product p 
 WHERE ProductNumber = 'BK-M68B-42')));
 GO
 ```

  ![Salvar consulta SQL](media/dta-tutorials/dta-save-query.png)
  
2.  Inicie o Orientador de Otimização do Mecanismo de Banco de Dados. Selecione **Database Tuning Advisor** da **ferramentas** menu no SQL Server Management Studio (SSMS).  Confira mais informações em [Iniciar o Orientador de Otimização do Mecanismo de Banco de Dados](lesson-1-basic-navigation-in-database-engine-tuning-advisor.md#launch-database-tuning-advisor). Conectar-se ao SQL Server no **conectar ao servidor** caixa de diálogo.  
  
3.  Na guia **Geral** do painel direito da GUI do Orientador de Otimização do Mecanismo de Banco de Dados, digite **MySession** em **Nome da sessão**. 
  
4.  Selecione **arquivo** para seu **Workload**e selecione o ícone de binóculos para **procurar um arquivo de carga de trabalho**. Localize o **Myscript** arquivo que você salvou na etapa 1.  

   ![Localize o script que foi salvo anteriormente](media/dta-tutorials/dta-script.png)
  
5.  Marque AdventureWorks2017 na lista **Banco de dados para análise de carga de trabalho**, marque AdventureWorks2017 na grade **Selecione bancos de dados e tabelas para ajuste** e marque **Salvar log de ajuste**. **Banco de dados para análise de carga de trabalho** especifica o primeiro banco de dados ao qual o Orientador de Otimização do Mecanismo de Banco de Dados se conecta ao ajustar uma carga de trabalho. Depois que a otimização começa, o Orientador de Otimização do Mecanismo de Banco de Dados se conecta aos bancos de dados especificados pelas instruções `USE DATABASE` contidas na carga de trabalho.  

  ![Opções de DTA para banco de dados](media/dta-tutorials/dta-select-db.png)
  
6.  Clique na guia **Opções de Ajuste** . Você não definirá nenhuma opção de ajuste para esta prática, mas fará a revisão as opções de ajuste padrão. Pressione F1 para exibir a Ajuda da página de guias. Clique em **Opções Avançadas** para exibir outras opções de ajuste. Clique em **Ajuda** na caixa de diálogo **Opções de Ajuste Avançadas** para obter informações sobre as opções de ajuste que são exibidas nessa caixa. Clique em **Cancelar** para fechar a caixa de diálogo **Opções de Ajuste Avançadas** , deixando as opções padrão selecionadas.  

  ![Opções de ajuste de DTA](media/dta-tutorials/dta-tuning-options.png)
  
7.  Clique no botão **Iniciar Análise** na barra de ferramentas. Enquanto o Orientador de Otimização do Mecanismo de Banco de Dados estiver analisando a carga de trabalho, você poderá monitorar o status na guia **Progresso** . Quando o ajuste foi concluído, a guia **Recomendações** será exibida.  
  
    Se você receber um erro sobre a data e hora de interrupção do ajuste, verifique a hora em **Parar em** na guia principal de **Opções de Ajuste** . Garanta que a data e a hora em **Parar em** são posteriores à data e à hora atuais e, se necessário, altere-as.  

  ![Iniciar a análise do DTA](media/dta-tutorials/dta-start-analysis.png)

  
8.  Depois que a análise for concluída, salve sua recomendação como um script [!INCLUDE[tsql](../../includes/tsql-md.md)] clicando em **Salvar Recomendações** no menu **Ações** . Na caixa de diálogo **Salvar Como** , navegue até o diretório em que você quer salvar o script de recomendações e digite o nome de arquivo **MyRecommendations**.  

  ![Salve as recomendações do DTA](media/dta-tutorials/dta-save-recommendations.png)

## <a name="view-tuning-recommendations"></a>Exibir recomendações de ajuste
  
1.  Na guia **Recomendações** , use a barra de rolagem na parte inferior da página da guia para exibir todas as colunas de **Recomendações de Índice** . Cada linha representa um objeto de banco de dados (índices ou exibições indexadas) que o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] recomenda que sejam descartadas ou criadas. Role a tela até a coluna mais à direita e clique em **Definição**. [!INCLUDE[ssDE](../../includes/ssde-md.md)] exibe uma janela **Visualização de Script SQL** , na qual você pode exibir o script [!INCLUDE[tsql](../../includes/tsql-md.md)] que cria ou descarta o objeto de banco de dados nessa linha. Clique em **Fechar** para fechar a janela de visualização.  
  
    Se você estiver tendo dificuldades em localizar uma **Definição** que contenha um link, clique para desmarcar a caixa de seleção **Mostrar objetos existentes** na parte inferior da página da guia, o que diminuirá o número de linhas exibidas. Quando você desmarca essa caixa de seleção, o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] mostra só os objetos para os quais gerou uma recomendação. Marque a caixa de seleção **Mostrar objetos existentes** para exibir todos os objetos do banco de dados que existem atualmente no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Use a barra de rolagem à direita da página da guia para exibir todos os objetos.

  ![Recomendação de índice do DTA](media/dta-tutorials/dta-recommendation.png)  
  
2.  Clique com o botão direito do mouse na grade do painel **Recomendações de Índice** . Esse menu permite marcar e desmarcar recomendações. Permite também alterar a fonte do texto da grade.  
 
   ![Menu de seleção para a recomendação de índice](media/dta-tutorials/dta-index-recommendation-options.png)
  
3.  No menu **Ações** , clique em **Salvar Recomendações** para salvar todas as recomendações em um script [!INCLUDE[tsql](../../includes/tsql-md.md)] . Nomeie o script como **MySessionRecommendations.sql**.  
  
    Abra o script MySessionRecommendations.sql no Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibi-lo. Você poderia aplicar as recomendações ao banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] executando o script no Editor de Consultas, mas não faça isso. Feche o script no Editor de Consultas sem executá-lo.  
  
    Como uma alternativa, você também pode aplicar as recomendações clicando em **Aplicar Recomendações** no menu **Ações** do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , mas não aplique essas recomendações nesta prática.  
  
4.  Se houver mais de uma recomendação na guia **Recomendações** , desmarque algumas das linhas que listam objetos do banco de dados na grade **Recomendações de Índice** .  
  
5.  No menu **Ações** , clique em **Avaliar Recomendações**. [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria uma nova sessão de ajuste em que você pode avaliar um subconjunto das recomendações originais em MySession.  
  
6.  Digite **EvaluateMySession** para seu novo **Nome da sessão**e clique no botão **Iniciar Análise** na barra de ferramentas. Você pode repetir os passos 2 e 3 para esta nova sessão de ajuste a fim de exibir suas recomendações.  
  
### <a name="summary"></a>Resumo  
A avaliação de um subconjunto de recomendações de ajuste poderá ser necessária se você descobrir que deve alterar as opções de ajuste depois de executar uma sessão. Por exemplo, se você pedir ao Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para considerar exibições indexadas quando você especificar as opções de ajuste para uma sessão, mas depois que a recomendação for gerada você decidir não usar as exibições indexadas. Você pode usar a opção **Avaliar Recomendações** no menu **Ações** para que o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] reavalie a sessão sem considerar as exibições indexadas. Quando você usa a opção **Avaliar Recomendações** , as recomendações geradas previamente são aplicadas hipoteticamente ao design físico atual para chegar ao design físico para a segunda sessão de ajuste.  
  
Poderão ser exibidas mais informações sobre resultados de ajuste na guia **Relatórios** , que é descrita na próxima tarefa desta lição.  

## <a name="view-tuning-reports"></a>Exibição de relatórios de ajuste
Além de ser útil para exibir os scripts que podem ser usados para implementar os resultados de ajuste, o Orientador de Otimização do Mecanismo de Banco de Dados fornece muitos relatórios úteis que você pode exibir. Esses relatórios fornecem informações sobre as estruturas de design físico existentes no banco de dados que você está ajustando, e sobre as estruturas recomendadas. Os relatórios de ajuste podem ser exibidos clicando na guia **Relatórios** , como descrito na prática abaixo.


1. Selecione o **relatórios** guia no orientador de otimização do banco de dados. 
2. No painel **Resumo do Ajuste** , você pode exibir informações sobre esta sessão de otimização. Use a barra de rolagem para exibir todo o conteúdo do painel. Preste atenção no **Aperfeiçoamento de percentual esperado** e no **Espaço usado por recomendação**. É possível limitar o espaço usado pela recomendação quando você define as opções de ajuste. Na guia **Opções de Ajuste** , selecione **Opções Avançadas**. Marque **Definir espaço máximo para recomendações** e especifique, em megabytes, o espaço máximo que uma configuração de recomendada pode usar. Use o botão **Voltar** em seu navegador de ajuda para voltar a este tutorial. 

    ![Resumo do ajuste de DTA](media/dta-tutorials/dta-tuning-summary.png)
  
3.  No painel **Relatórios de Ajuste** , clique em **Relatório de custo da instrução** na lista **Selecionar relatório** . Se precisar de mais espaço para exibir o relatório, arraste a borda do painel **Monitor de Sessão** para a esquerda. Cada instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] executada em uma tabela em seu banco de dados tem um custo de desempenho associado. Esse custo de desempenho pode ser reduzido criando índices efetivos em colunas acessadas frequentemente em uma tabela. Esse relatório mostra a porcentagem estimada de aperfeiçoamento entre o custo original de executar uma instrução na carga de trabalho e o custo se a recomendação de ajuste for implementada. Note que a quantidade de informações contida no relatório é baseada no tamanho e na complexidade da carga de trabalho.  

    ![Relatório DTA - custo de instrução](media/dta-tutorials/dta-statement-cost.png)
  
4.  Clique com o botão direito do mouse no painel **Relatório de custo da instrução** na área da grade e clique em **Exportar para o Arquivo**. Salve o relatório como **MyReport**. Será anexada automaticamente uma extensão .xml ao nome do arquivo. Você pode abrir MyReport.xml em seu editor de XML favorito ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibir o conteúdo do relatório.  
  
5.  Volte à guia **Relatórios** do Orientador de Otimização do Mecanismo de Banco de Dados e clique novamente com o botão direito do mouse em **Relatório de custo da instrução** . Revise as outras opções disponíveis. Note que você pode alterar a fonte do relatório que está exibindo. Alterar a fonte aqui também altera nas outras páginas de guias.  
  
6.  Clique em outros relatórios na lista **Selecionar relatório** para se familiarizar com eles.  
  
### <a name="summary"></a>Resumo  
Você explorou a guia **Relatórios** da sessão de ajuste MySession na interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados. Você pode usar esses mesmos passos para explorar os relatórios que foram gerados para a sessão de ajuste EvaluateMySession. Clique duas vezes em **EvaluateMySession** no painel **Monitor de Sessão** para começar.  


 ## <a name="next-lesson"></a>Próxima lição  
[Lição 3: como usar o utilitário de prompt de comando DTA](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
   
  
  

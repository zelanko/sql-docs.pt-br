---
title: "Li&#231;&#227;o 1: Publicando dados usando replica&#231;&#227;o de mesclagem | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "replicação [SQL Server], tutoriais"
ms.assetid: c3c6e0b6-54cd-4b7d-8efb-2cefe14fcd7f
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Li&#231;&#227;o 1: Publicando dados usando replica&#231;&#227;o de mesclagem
Nesta lição, você aprenderá a criar uma publicação de mesclagem usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para publicar um subconjunto das tabelas **Employee**, **SalesOrderHeader** e **SalesOrderDetail** no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Essas tabelas são filtradas com filtros de linha com parâmetros de modo que cada assinatura contenha uma partição exclusiva dos dados. Você também adicionará o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado pelo Agente de Mesclagem à PAL (lista de acesso à publicação). Este tutorial exige a conclusão do tutorial anterior, [Preparando o servidor para replicação](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
### Para criar uma publicação e definir artigos  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação**, clique com o botão direito do mouse em **Publicações Locais** e clique em **Nova Publicação**.  
  
    O Assistente de Configuração de Publicação é inicializado.  
  
3.  Na página Banco de Dados de Publicação, selecione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e clique em **Avançar**.  
  
4.  Na página Tipo de Publicação, selecione **Publicação de mesclagem** e clique em **Avançar**.  
  
5.  Na página Tipos de Assinante, verifique se somente o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior está selecionado e clique em **Avançar**.  
  
6.  Na página Artigos, expanda o nó **Tabelas** e selecione **SalesOrderHeader** e **SalesOrderDetail**; a seguir, expanda **Employee**, selecione **EmployeeID** ou **LoginID** e clique em **Avançar**.  
  
    > [!TIP]  
    > As colunas adicionais necessárias são selecionadas automaticamente. Selecione uma das colunas selecionadas automaticamente e exiba a observação abaixo da lista **Objetos para publicação** para obter uma explicação do porquê a coluna é necessária.  
  
7.  Na página Linhas de Tabela de Filtro, clique em **Adicionar** e em **Adicionar Filtro**.  
  
8.  Na caixa de diálogo **Adicionar Filtro**, selecione **Employee (HumanResources)** em **Selecionar a tabela a ser filtrada**, clique na coluna **LoginID**, clique na seta para a direita a fim de adicionar a coluna à cláusula WHERE da consulta de filtro e modifique a cláusula WHERE da seguinte maneira:  
  
    ```  
    WHERE [LoginID] = HOST_NAME()  
    ```  
  
9. Clique em **Uma linha desta tabela irá para apenas uma assinatura** e clique em **OK**.  
  
10. Na página **Filtrar Linhas da Tabela**, clique em **Funcionário (Recursos Humanos)**, clique em **Adicionar** e clique em **Adicionar Junção para Estender o Filtro Selecionado**.  
  
11. Na caixa de diálogo **Adicionar Junção**, selecione **Sales.SalesOrderHeader** sob **Tabela unida**, clique em **Gravar a instrução de junção manualmente** e conclua a instrução de junção da seguinte forma:  
  
    ```  
    ON Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
    ```  
  
12. Em **Especificar opções de junção**, selecione **Chave exclusiva** e clique em **OK**.  
  
13. Na página Linhas de Tabela de Filtro, clique em **SalesOrderHeader**, **Adicionar** e em **Adicionar Junção para Estender o Filtro Selecionado**.  
  
14. Na caixa de diálogo **Adicionar Junção**, selecione **Sales.SalesOrderDetail** sob **Tabela unida**.  
  
15. Clique em **Gravar a instrução de junção manualmente**.  
  
16. Em **Colunas da tabela filtrada**, selecione **BusinessEntityID** e clique no botão de seta para copiar o nome da coluna na instrução de junção.  
  
17. Na caixa **Instrução de junção**, preencha a instrução de junção da seguinte maneira:  
  
    ```  
    ON Employee.BusinessEntityID = SalesOrderHeader.SalesPersonID  
    ```  
  
18. Em **Especificar opções de junção**, selecione **Chave exclusiva** e clique em **OK**.  
  
19. Na página **Filtrar Linhas da Tabela**, clique em **SalesOrderHeader (Sales)**, **Adicionar** e em **Adicionar Junção para Estender o Filtro Selecionado**.  
  
20. Na caixa de diálogo **Adicionar Junção**, selecione **Sales.SalesOrderDetail** sob **Tabela unida**, clique em **OK** e em **Avançar**.  
  
21. Selecione **Criar um instantâneo imediatamente**, desmarque a opção **Agendar o agente de instantâneo para ser executado nos seguintes momentos** e clique em **Avançar**.  
  
22. Na página Segurança do Agente, clique em **Configurações de Segurança**, digite \<*Machine_Name>***\repl_snapshot** na caixa **Conta de processo**, forneça a senha dessa conta e clique em **OK**. Clique em **Concluir**.  
  
23. Na página Concluir o Assistente, insira **AdvWorksSalesOrdersMerge** na caixa **Nome da publicação** e clique em **Concluir**.  
  
24. Depois que a publicação for criada, clique em **Fechar**.  
  
### Para exibir o status de geração do instantâneo  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta Publicações Locais, clique com o botão direito do mouse em **AdvWorksSalesOrdersMerge** e clique em **Exibir Status do Agente de Instantâneo**.  
  
3.  O status atual do trabalho do Snapshot Agent para a publicação é exibido. Certifique-se de que o trabalho de instantâneo teve sucesso antes de passar à próxima lição.  
  
### Para adicionar o logon do Merge Agent à PAL  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta Publicações Locais, clique com o botão direito do mouse em **AdvWorksSalesOrdersMerge** e clique em **Propriedades**.  
  
    A caixa de diálogo **Propriedades da Publicação** é exibida.  
  
3.  Selecione a página **Lista de Acesso à Publicação** e clique em **Adicionar**.  
  
4.  Na caixa de diálogo Adicionar Acesso à Publicação, selecione *<Machine_Name>***\repl_merge** e clique em **OK**. Clique em **OK**.  
  
## Próximas etapas  
Você criou a publicação de mesclagem com sucesso. A seguir, você assinará essa publicação. Consulte [Lição 2: Criando uma assinatura na publicação de mesclagem](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md).  
  
## Consulte também  
[Filtrar dados publicados](../../relational-databases/replication/publish/filter-published-data.md)  
[Filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-row-filters.md)  
[Defina um Artigo](../../relational-databases/replication/publish/define-an-article.md)  
  
  
  

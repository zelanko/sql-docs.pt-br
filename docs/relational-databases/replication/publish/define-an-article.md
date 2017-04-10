---
title: "Defina um Artigo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "artigos [replicação do SQL Server], definindo"
  - "sp_addmergearticle"
  - "adicionando artigos"
  - "sp_addarticle"
  - "artigos [replicação do SQL Server], adicionando"
ms.assetid: 220584d8-b291-43ae-b036-fbba3cc07a2e
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Defina um Artigo
  Este tópico descreve como definir um artigo no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)], ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para definir um artigo, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Os nomes de artigos não podem incluir nenhum dos caracteres a seguir: % , * , [ , ] , | , : , " , ? , ' , \ , / , \< , >. Se algum objeto do banco de dados incluir qualquer um desses caracteres, para replicá-los será necessário especificar um nome de artigo que seja diferente do nome do objeto.  
  
##  <a name="Security"></a> Segurança  
 Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework do Windows.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Crie publicações e defina artigos com o Assistente para Nova Publicação. Depois que uma publicação é criada, exibir e modificar propriedades de publicação na **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter informações sobre como criar uma publicação de um banco de dados Oracle, consulte [criar uma publicação de um banco de dados Oracle](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
#### Para criar uma publicação e definir artigos  
  
1.  Conecte-se ao Publicador no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e, depois, expanda o nó do servidor.  
  
2.  Expanda o **replicação** pasta e, em seguida, clique com botão direito do **publicações locais** pasta.  
  
3.  Clique em **Nova Publicação**.  
  
4.  Siga as páginas no Assistente para Nova Publicação para:  
  
    -   Especificar um Distribuidor se a distribuição não foi configurada no servidor. Para obter mais informações sobre a configuração de distribuição, consulte [Configurar publicação e distribuição](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
         Se você especificar o **distribuidor** página que o servidor do publicador atuará como seu próprio distribuidor (um distribuidor local) e o servidor não está configurado como um distribuidor, o Assistente para nova publicação configurará o servidor. Você especificará uma pasta de instantâneo padrão para o Distribuidor na página **Pasta de Instantâneos** . A pasta de instantâneo é simplesmente um diretório que você designou como um compartilhamento, agentes que leem essa pasta e gravam nela devem ter permissões suficientes para acessá-la. Para obter mais informações sobre como proteger a pasta adequadamente, consulte [proteger a pasta de instantâneo](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
         Se você especificar que um outro servidor deverá atuar como um Distribuidor, você deverá inserir uma senha na página **Senha Administrativa** para conexões feitas do Publicador ao Distribuidor. Esta senha deve corresponder à senha especificada quando o Publicador foi habilitado no Distribuidor remoto.  
  
         Para obter mais informações, consulte [Configurar distribuição](../../../relational-databases/replication/configure-distribution.md).  
  
    -   Escolha um banco de dados de publicação.  
  
    -   Selecione um tipo de publicação. Para obter mais informações, consulte [tipos de replicação](../../../relational-databases/replication/types-of-replication.md).  
  
    -   Especifique os dados e os objetos de banco de dados para serem publicados; opcionalmente filtre as colunas de artigos de tabela e defina as propriedades dos artigos.  
  
    -   Opcionalmente filtre as linhas de artigos de tabela. Para obter mais informações, consulte [Filtrar dados publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
    -   Defina a agenda do Snapshot Agent.  
  
    -   Especifique as credenciais sob as quais os agentes de replicação a seguir executam e fazem conexões:  
  
         \- Agente de instantâneo para todas as publicações.  
  
         \- O Log Reader Agent para todas as publicações transacionais.  
  
         \- Queue Reader Agent para publicações transacionais que permitem assinaturas de atualização.  
  
         Para obter mais informações, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) e [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
    -   Opcionalmente faça o script da publicação. Para obter mais informações, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
    -   Especifique um nome para a publicação.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Após a criação da publicação, artigos poderão ser criados de forma programática, usando os procedimentos armazenados da replicação. Os procedimentos armazenados usados para criar um artigo dependem do tipo de publicação para o qual o artigo é definido. Para obter mais informações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### Para definir um artigo para um instantâneo ou publicação transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication**, um nome para o artigo para **@article**, o objeto de banco de dados que está sendo publicado para **@source_object**, e quaisquer outros parâmetros opcionais. Use **@source_owner** para especificar a propriedade do esquema do objeto, se não **dbo**. Se o artigo não é um artigo de tabela com base em log, especifique o tipo de artigo para **@type**; para obter mais informações, consulte [especificar tipos de artigo & #40. Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md).  
  
2.  Para horizontalmente filtrar linhas em uma tabela ou exibir um artigo, use [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) para definir a cláusula de filtro. Para obter mais informações, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Para verticalmente filtrar colunas em uma tabela ou exibir um artigo, use [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Para obter mais informações, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
4.  Executar [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) se o artigo é filtrado.  
  
5.  Se a publicação tiver assinaturas existentes e [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) retorna um valor de **0** no **immediate_sync** coluna, você deve chamar [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) para adicionar o artigo para cada assinatura existente.  
  
6.  Se a publicação tiver assinaturas pull existentes, execute [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) no Editor para criar um novo instantâneo para assinaturas pull existentes que contém apenas o novo artigo.  
  
    > [!NOTE]  
    >  Para assinaturas que não são inicializadas usando um instantâneo, você não precisa executar [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) conforme este procedimento é executado pelo [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
#### Para definir um artigo para uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique o nome da publicação para **@publication**, um nome para o nome do artigo para **@article**, e o objeto que está sendo publicado para **@source_object**. Para filtrar horizontalmente linhas da tabela, especifique um valor para **@subset_filterclause**. Para obter mais informações, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md) e [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md). Se o artigo não for um artigo de tabela, especifique o tipo de artigo para **@type**. Para obter mais informações, consulte [especificar tipos de artigo & #40. Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md).  
  
2.  (Opcional) No publicador do banco de dados de publicação, execute [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) para definir um filtro de junção entre dois artigos. Para obter mais informações, consulte [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
3.  (Opcional) No publicador do banco de dados de publicação, execute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) para filtrar colunas de tabela. Para obter mais informações, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo define um artigo com base na tabela `Product` para uma publicação transacional, onde o artigo é filtrado horizontal e verticalmente.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_1.sql)]  
  
 Este exemplo define artigos para uma publicação de mesclagem, onde o artigo `SalesOrderHeader` é filtrado estatisticamente com base em **SalesPersonID**, e o artigo `SalesOrderDetail` é filtrado por junção, com base em `SalesOrderHeader`.  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Defina artigos de forma programada, usando o RMO (Replication Management Objects). As classes de RMO usadas para definir um artigo dependem do tipo de publicação para a qual o artigo é definido.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 O exemplo a seguir adiciona um artigo com filtros de linha e de coluna para uma publicação transacional.  
  
 [!code-csharp[HowTo#rmo_CreateTranArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranarticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranarticles)]  
  
 O exemplo a seguir adiciona três artigos a uma publicação de mesclagem. Os artigos têm filtros de coluna, e dois filtros de função são usados para propagar o filtro de linha com parâmetros para os outros artigos.  
  
 [!code-csharp[HowTo#rmo_CreateMergeArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergearticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergeArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergearticles)]  
  
## Consulte também  
 [Crie uma publicação](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Adicionar e remover artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Filtrar dados publicados](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
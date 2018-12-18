---
title: Definir um artigo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], defining
- sp_addmergearticle
- adding articles
- sp_addarticle
- articles [SQL Server replication], adding
ms.assetid: 220584d8-b291-43ae-b036-fbba3cc07a2e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c719c6897edfa956c70b7863811ccea98bee68b9
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51672125"
---
# <a name="define-an-article"></a>Defina um Artigo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
-   Os nomes de artigos não podem incluir nenhum dos caracteres a seguir: % , * , [ , ] , | , : , " , ? , ' , \ , / , < , >. Se algum objeto do banco de dados incluir qualquer um desses caracteres, para replicá-los será necessário especificar um nome de artigo que seja diferente do nome do objeto.  
  
##  <a name="Security"></a> Segurança  
 Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](https://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework do Windows.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Crie publicações e defina artigos com o Assistente para Nova Publicação. Após a criação de uma publicação, exiba e modifique as propriedades da publicação na caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter informações sobre como criar uma publicação de um banco de dados Oracle, consulte [Criar uma publicação de um banco de dados Oracle](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
#### <a name="to-create-a-publication-and-define-articles"></a>Para criar uma publicação e definir artigos  
  
1.  Conecte-se ao Publicador no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e, depois, expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e clique com o botão direito do mouse na pasta **Publicações Locais** .  
  
3.  Clique em **Nova Publicação**.  
  
4.  Siga as páginas no Assistente para Nova Publicação para:  
  
    -   Especificar um Distribuidor se a distribuição não foi configurada no servidor. Para obter mais informações sobre a configuração de distribuição, consulte [Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md) (Configurar publicação e distribuição).  
  
         Se especificar na página do **Distribuidor** que o servidor do Publicador atuará como o seu próprio Distribuidor (um Distribuidor local) e o servidor não estiver configurado como um Distribuidor, o Assistente para Nova Publicação configurará o servidor. Você especificará uma pasta de instantâneo padrão para o Distribuidor na página **Pasta de Instantâneos** . A pasta de instantâneo é simplesmente um diretório que você designou como um compartilhamento, agentes que leem essa pasta e gravam nela devem ter permissões suficientes para acessá-la. Para obter mais informações sobre como proteger a pasta adequadamente, consulte [Secure the Snapshot Folder](../../../relational-databases/replication/security/secure-the-snapshot-folder.md) (Proteger a pasta de instantâneo).  
  
         Se você especificar que um outro servidor deverá atuar como um Distribuidor, você deverá inserir uma senha na página **Senha Administrativa** para conexões feitas do Publicador ao Distribuidor. Esta senha deve corresponder à senha especificada quando o Publicador foi habilitado no Distribuidor remoto.  
  
         Para obter mais informações, consulte [Configure Distribution](../../../relational-databases/replication/configure-distribution.md).  
  
    -   Escolha um banco de dados de publicação.  
  
    -   Selecione um tipo de publicação. Para obter mais informações, consulte [Types of Replication](../../../relational-databases/replication/types-of-replication.md) (Tipos de replicação).  
  
    -   Especifique os dados e os objetos de banco de dados para serem publicados; opcionalmente filtre as colunas de artigos de tabela e defina as propriedades dos artigos.  
  
    -   Opcionalmente filtre as linhas de artigos de tabela. Para obter mais informações, consulte [Filter Published Data](../../../relational-databases/replication/publish/filter-published-data.md) (Filtrar dados publicados).  
  
    -   Defina a agenda do Snapshot Agent.  
  
    -   Especifique as credenciais sob as quais os agentes de replicação a seguir executam e fazem conexões:  
  
         \- Snapshot Agent para todas as publicações.  
  
         \- O Agente de Leitor de Log para todas as publicações transacionais.  
  
         \- O Queue Reader Agent para as publicações transacionais que permitem atualização de assinaturas.  
  
         Para obter mais informações, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) e [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
    -   Opcionalmente faça o script da publicação. Para obter mais informações, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
    -   Especifique um nome para a publicação.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Após a criação da publicação, artigos poderão ser criados de forma programática, usando os procedimentos armazenados da replicação. Os procedimentos armazenados usados para criar um artigo dependem do tipo de publicação para o qual o artigo é definido. Para obter mais informações, consulte [Criar uma assinatura](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-define-an-article-for-a-snapshot-or-transactional-publication"></a>Para definir um artigo para um instantâneo ou publicação transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication**; um nome para o artigo para **@article**; um objeto de banco de dados sendo publicado para **@source_object**, e qualquer outro parâmetro opcional. Use **@source_owner** para especificar a propriedade de esquema do objeto; do contrário, use **dbo**. Se o artigo não for um artigo de tabela baseado em log, especifique o tipo de artigo para **@type**; para obter mais informações, consulte [Especificar tipos de artigo &#40;Programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md).  
  
2.  Para filtrar linhas horizontalmente em uma tabela ou exibir um artigo, use [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) para definir a cláusula de filtro. Para obter mais informações, consulte [Definir e modificar um filtro de linha estático](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Para filtrar colunas verticalmente em uma tabela ou exibir um artigo, use [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Para obter mais informações, consulte [Definir e modificar um filtro de colunas](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
4.  Execute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) se o artigo for filtrado.  
  
5.  Se a publicação tiver assinaturas existentes e [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) retornar um valor de **0** na coluna **immediate_sync** , será preciso chamar [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) para adicionar o artigo a cada uma das assinaturas existentes.  
  
6.  Se a publicação tiver assinaturas pull existentes, execute [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) no Publicador para criar um novo instantâneo para as assinaturas pull existentes que contêm apenas o novo artigo.  
  
    > [!NOTE]  
    >  Para assinaturas que não são iniciadas por meio de instantâneo, não há necessidade de executar [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) , uma vez que esse procedimento é executado por [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
#### <a name="to-define-an-article-for-a-merge-publication"></a>Para definir um artigo para uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute o [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique o nome da publicação para **@publication**; um nome de artigo para **@article**e o objeto sendo publicado para **@source_object**. Para filtrar horizontalmente linhas de tabelas, especifique um valor para **@subset_filterclause**. Para obter mais informações, consulte [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md) e [Definir e modificar um filtro de linha estático](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md). Se o artigo não for um artigo de tabela, especifique o tipo de artigo para **@type**. Para obter mais informações, consulte [Especificar tipos de artigo &#40;Programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md).  
  
2.  (Opcional) No Assinante do banco de dados de publicação, execute [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) para definir um filtro de junção entre dois artigos. Para obter mais informações, consulte [Definir e modificar um filtro de junção entre artigos de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
3.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) para filtrar colunas de tabela. Para obter mais informações, consulte [Definir e modificar um filtro de colunas](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo define um artigo com base na tabela `Product` para uma publicação transacional, onde o artigo é filtrado horizontal e verticalmente.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_1.sql)]  
  
 Este exemplo define artigos para uma publicação de mesclagem, onde o artigo `SalesOrderHeader` é filtrado estatisticamente com base em **SalesPersonID**, e o artigo `SalesOrderDetail` é filtrado por junção, com base em `SalesOrderHeader`.  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Defina artigos de forma programada, usando o RMO (Replication Management Objects). As classes de RMO usadas para definir um artigo dependem do tipo de publicação para a qual o artigo é definido.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 O exemplo a seguir adiciona um artigo com filtros de linha e de coluna para uma publicação transacional.  
  
 [!code-cs[HowTo#rmo_CreateTranArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranarticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranarticles)]  
  
 O exemplo a seguir adiciona três artigos a uma publicação de mesclagem. Os artigos têm filtros de coluna, e dois filtros de função são usados para propagar o filtro de linha com parâmetros para os outros artigos.  
  
 [!code-cs[HowTo#rmo_CreateMergeArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergearticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergeArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergearticles)]  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Adicionar e remover artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Filtrar os dados publicados](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  

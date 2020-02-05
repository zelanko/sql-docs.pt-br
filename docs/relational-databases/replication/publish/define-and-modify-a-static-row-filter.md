---
title: Definir e modificar um filtro de linha estático | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying filters, static row
- static row filters
- filters [SQL Server replication], static row
ms.assetid: a6ebb026-026f-4c39-b6a9-b9998c3babab
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 2f7874ecabe33f507ca471d13e00d2f48f6f8976
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287652"
---
# <a name="define-and-modify-a-static-row-filter"></a>Definir e modificar um filtro de linha estático
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Este tópico descreve como definir e modificar um filtro de linhas estático no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
-   **Para definir e modificar um filtro de linhas estático usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se você adicionar, modificar ou excluir um filtro de linhas estático após a inicialização de assinaturas na publicação, será preciso gerar um novo instantâneo e reinicializar todas as assinaturas depois de fazer a alteração. Para obter mais informações sobre os requisitos para alterações de propriedades, consulte [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
-   Se a publicação estiver habilitada para replicação transacional ponto a ponto, as tabelas não poderão ser filtradas.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Como estes filtros são estáticos, todos os assinantes receberão o mesmo subconjunto de dados. Se você precisa filtrar dinamicamente linhas em um artigo de tabela pertencente a uma publicação de mesclagem para que cada assinante receba uma partição diferente dos dados, consulte [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md). A replicação de mesclagem também permite que você filtre linhas relacionadas com base em um filtro de linha existente. Para obter mais informações, consulte [Definir e modificar um filtro de junção entre artigos de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Defina, modifique e exclua filtros de linhas estático na página **Filtrar Linhas da Tabela** no Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades da Publicação – \<Publicação>** . Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-define-a-static-row-filter"></a>Para definir um filtro de linhas estático  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades da Publicação – \<Publicação>** , a ação a ser executada depende do tipo de publicação:  
  
    -   Para um instantâneo ou publicação transacional, clique em **Adicionar**.  
  
    -   Para uma publicação de mesclagem, clique em **Adicionar**e então clique em **Adicionar filtro**.  
  
2.  Na caixa de diálogo **Adicionar Filtro** , selecione uma tabela para filtrar na caixa de listagem suspensa.  
  
3.  Crie uma instrução de filtro na área de texto **Instrução de filtro** . Você pode digitar diretamente na área de texto e também pode arrastar e soltar colunas da caixa de listagem **Colunas** .  
  
    > [!NOTE]  
    >  A cláusula WHERE deve usar nomeação de duas partes; nomeação de três partes e nomeação de quatro partes não são suportadas. Se a publicação for de um Editor Oracle, a cláusula WHERE deve estar compatível com a sintaxe do Oracle.  
  
    -   A área de texto **Instrução de filtro** inclui o texto padrão que está no formato de:  
  
        ```sql  
        SELECT <published_columns> FROM [schema].[tablename] WHERE  
        ```  
  
    -   O texto padrão não pode ser alterado; digite a cláusula de filtro depois da palavra-chave WHERE usando sintaxe padrão do SQL. A cláusula de filtro completa aparecerá como:  
  
        ```sql  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE [LoginID] = 'adventure-works\ranjit0'  
        ```  
  
    -   Um filtro de linhas estático pode incluir uma função definida pelo usuário. A cláusula de filtro completa para um filtro de linhas estático com uma função definida pelo usuário será exibida como:  
  
        ```sql  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] WHERE MyFunction([Freight]) > 100  
        ```  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , clique em **OK** para salvar e fechar a caixa de diálogo.  

#### <a name="to-modify-a-static-row-filter"></a>Para modificar um filtro de linhas estático  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione um filtro no painel **Tabelas Filtradas** e clique em **Editar**.  
  
2.  Na caixa de diálogo **Editar Filtro** , modifique o filtro.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-static-row-filter"></a>Para excluir um filtro de linhas estático  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione um filtro no painel **Tabelas Filtradas** e clique em **Excluir**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Ao criar artigos de tabela, você pode definir uma cláusula WHERE para filtrar linhas para fora de um artigo. Você também pode alterar um filtro de linha depois que ele estiver definido. Os filtros de linhas estáticos podem ser criados e modificados programaticamente usando os procedimentos armazenados de replicação.  
  
#### <a name="to-define-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>Para definir um filtro de linhas estático para um instantâneo ou publicação transacional  
  
1.  Defina o artigo a ser filtrado. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  No Publicador no banco de dados de publicação, execute o [sp_articlefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md). Especifique o nome do artigo em **\@article**, o nome da publicação em **\@publication**, um nome para o filtro em **\@filter_name** e a cláusula de filtragem em **\@filter_clause** (não incluindo `WHERE`).  
  
3.  Se um filtro de coluna ainda precisa ser definido, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md). Caso contrário, execute [sp_articleview &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Especifique o nome da publicação em **\@publication**, o nome do artigo filtrado em **\@article** e a cláusula de filtro especificada na etapa 2 em **\@filter_clause**. Isto cria os objetos de sincronização para o artigo filtrado.  
  
#### <a name="to-modify-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>Para modificar um filtro de linhas estático para um instantâneo ou publicação transacional  
  
1.  No Publicador no banco de dados de publicação, execute o [sp_articlefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md). Especifique o nome do artigo em **\@article**, o nome da publicação em **\@publication**, um nome para o novo filtro em **\@filter_name** e a nova cláusula de filtragem em **\@filter_clause** (não incluindo `WHERE`). Como essa alteração invalidará os dados nas assinaturas existentes, especifique um valor igual a **1** em **\@force_reinit_subscription**.  
  
2.  No Publicador no banco de dados de publicação, execute [sp_articleview &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Especifique o nome da publicação em **\@publication**, o nome do artigo filtrado em **\@article** e a cláusula de filtro especificada na etapa 1 em **\@filter_clause**. Isto recria a exibição que define o artigo filtrado.  
  
3.  Execute novamente o Snapshot Agent da publicação para gerar um instantâneo atualizado. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
4.  Reinicialize as assinaturas. Para obter mais informações, consulte [Reinicializar as assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### <a name="to-delete-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>Para excluir um filtro de linhas estático para um instantâneo ou publicação transacional  
  
1.  No Publicador no banco de dados de publicação, execute o [sp_articlefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md). Especifique o nome do artigo em **\@article**, o nome da publicação em **\@publication**, um valor igual a NULL em **\@filter_name** e um valor igual a NULL em **\@filter_clause**. Como essa alteração invalidará os dados nas assinaturas existentes, especifique um valor igual a **1** em **\@force_reinit_subscription**.  
  
2.  Execute novamente o Snapshot Agent da publicação para gerar um instantâneo atualizado. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
3.  Reinicialize as assinaturas. Para obter mais informações, consulte [Reinicializar as assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### <a name="to-define-a-static-row-filter-for-a-merge-publication"></a>Para definir um filtro de linhas estático para uma publicação de mesclagem  
  
1.  No Publicador no banco de dados de publicação, execute o [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique a cláusula de filtragem em **\@subset_filterclause** (não incluindo `WHERE`). Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Se um filtro de coluna ainda precisa ser definido, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
#### <a name="to-modify-a-static-row-filter-for-a-merge-publication"></a>Modificar um filtro de linhas estático para uma publicação de mesclagem  
  
1.  No Publicador no banco de dados de publicação, execute [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique o nome da publicação em **\@publication**, o nome do artigo filtrado em **\@article**, um valor igual a **subset_filterclause** em **\@property** e a nova cláusula de filtragem em **\@value** (não incluindo `WHERE`). Como essa alteração invalidará os dados nas assinaturas existentes, especifique um valor igual a 1 em **\@force_reinit_subscription**.  
  
2.  Execute novamente o Snapshot Agent da publicação para gerar um instantâneo atualizado. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
3.  Reinicialize as assinaturas. Para obter mais informações, consulte [Reinicializar as assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Neste exemplo de replicação transacional, o artigo é filtrado horizontalmente para remover todos os produtos descontinuados.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_1.sql)]  
  
 Neste exemplo de replicação de mesclagem, os artigos são filtrados horizontalmente para retornar apenas linhas que pertencem ao vendedor especificado. Um filtro de junção também é usado. Para obter mais informações, consulte [Definir e modificar um filtro de junção entre artigos de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_2.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Definir e modificar um filtro de linha parametrizado para um artigo de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtrar os dados publicados](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Filtrar dados publicados para a replicação de mesclagem](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  

---
title: Definir e modificar um filtro de junção entre artigos de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], join
- merge replication join filters [SQL Server replication]
- modifying filters, join
- join filters
ms.assetid: f7f23415-43ff-40f5-b3e0-0be1d148ee5b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bf8b3b4f00ad2e8a3b9236292ee20948c852b6ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68199551"
---
# <a name="define-and-modify-a-join-filter-between-merge-articles"></a>Definir e modificar um filtro de junção entre artigos de mesclagem
  Este tópico descreve como definir e modificar um filtro de junção entre artigos de mesclagem no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. A replicação de mesclagem dá suporte a filtros de junção, que normalmente são usados em conjunto com filtros com parâmetros para estender o particionamento de tabela a outros artigos de tabela relacionados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
-   **Para definir e modificar um filtro de junção entre artigos de mesclagem, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Para criar um filtro de junção, uma publicação deve conter pelo menos duas tabelas relacionadas. O filtro de junção estende um filtro de linha; por isso, é preciso definir o filtro de linha em uma tabela antes de poder estender o filtro de junção em outra tabela. Depois que um filtro de junção estiver definido, você poderá estender este filtro de junção com outro filtro de junção, se a publicação contiver tabelas relacionadas adicionais.  
  
-   Se você adicionar, modificar ou excluir um filtro de junção após a inicialização de assinaturas na publicação, será preciso gerar um novo instantâneo e reinicializar todas as assinaturas depois de fazer a alteração. Para obter mais informações sobre os requisitos para alterações de propriedades, consulte [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Os filtros de junção podem ser criados manualmente para um conjunto de tabelas ou a replicação pode gerar os filtros automaticamente, com base nas relações entre as chaves estrangeiras e primárias definidas nas tabelas. Para obter mais informações sobre como gerar um conjunto de filtros de junção automaticamente, consulte [Gerar automaticamente um conjunto de filtros de junção entre artigos de mesclagem &#40;SQL Server Management Studio&#41;](automatically-generate-join-filters-between-merge-articles.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Defina, modifique e exclua filtros de junção na página **Filtrar Linhas da Tabela** no Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades da Publicação – \<Publicação>** . Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](create-a-publication.md) e [Exibir e modificar as propriedades da publicação](view-and-modify-publication-properties.md).  
  
#### <a name="to-define-a-join-filter"></a>Para definir um filtro de junção  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione um filtro de linha existente ou filtro de junção no painel **Tabelas Filtradas**.  
  
2.  Clique em **Adicionar**e depois, em **Adicionar Junção para Estender o Filtro Selecionado**.  
  
3.  Crie a instrução de junção: selecione **Usar o construtor para criar a instrução** ou **Gravar a instrução de junção manualmente**.  
  
    -   Se você selecionar para usar o construtor, use as colunas na grade (**Conjunção**, **Coluna da Tabela Filtrada**, **Operador**e **Coluna da Tabela Unida**) para criar uma instrução de junção.  
  
         Cada coluna da grade contém uma caixa de combinação suspensa que permite a seleção de duas colunas e um operador ( **=** , **<>** , **<=** , **\<** , **>=** , **>** e **like**). Os resultados são exibidos na área de texto **Visualizar** . Se a junção envolver mais de um par de colunas, selecione a conjunção (AND ou OR) na coluna **Conjunção** e, depois, insira mais duas colunas e um operador.  
  
    -   Se você selecionar para gravar a instrução manualmente, grave a instrução de junção na área de texto **Instrução de Junção** . Use as caixas de listagens **Colunas da tabela filtrada** e **Colunas da tabela unida** para arrastar e soltar colunas na área de texto **Instrução de junção** .  
  
    -   A Instrução de junção completa teria a seguinte aparência:  
  
        ```  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] INNER JOIN [Sales].[SalesOrderDetail] ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID]  
        ```  
  
         A cláusula JOIN deve usar nomeação de duas partes; nomeação de três partes e nomeação de quatro partes não possuem suporte.  
  
4.  Especifique opções de junção:  
  
    -   Se a coluna de união da tabela filtrada (tabela pai) for exclusiva, selecione **Chave exclusiva**.  
  
        > [!CAUTION]  
        >  A seleção dessa opção indica que a relação entre tabelas pai e filho em um filtro de junção é de um para um ou um para muitos. Só selecione essa opção se houver uma restrição na coluna de junção na tabela filho que garanta a exclusividade. Se a opção for definida incorretamente, poderá ocorrer não convergência de dados.  
  
    -   Por padrão, os processos de replicação de mesclagem são alterados em uma base de linha por linha durante a sincronização. Para ter alterações relacionadas em linhas de tabelas filtradas e de tabelas unidas processadas como uma unidade, selecione **Registro lógico** ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou versões posteriores). Essa opção só estará disponível se os requisitos de  artigo e publicação para uso de registros lógicos forem atendidos. Para obter mais informações, consulte a seção "Considerações para uso de registros lógicos" em [Agrupar alterações a linhas relacionadas com registros lógicos](../merge/group-changes-to-related-rows-with-logical-records.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### <a name="to-modify-a-join-filter"></a>Para modificar um filtro de junção  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** de **Propriedades da Publicação – \<Publicação>** , selecione um filtro no painel **Tabelas Filtradas** e clique em **Editar**.  
  
2.  Na caixa de diálogo **Editar Junção** , modifique o filtro.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-join-filter"></a>Para excluir um filtro de junção  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** de **Propriedades da Publicação – \<Publicação>** , selecione um filtro no painel **Tabelas Filtradas** e clique em **Excluir**. Caso o próprio filtro excluído seja estendido por outras junções, essas junções também serão excluídas.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Estes procedimentos mostram um filtro com parâmetros em um artigo pai com filtros de junção entre esse artigo e artigos filho relacionados. Os filtros de junção podem ser definidos e modificados programaticamente usando procedimentos armazenados de replicação.  
  
#### <a name="to-define-a-join-filter-to-extend-an-article-filter-to-related-articles-in-a-merge-publication"></a>Para definir um filtro de junção para estender um filtro de artigo a artigos relacionados em uma publicação de mesclagem  
  
1.  Defina a filtragem para o artigo ao qual está sendo feita a junção, que é também conhecido como o artigo pai.  
  
    -   Para um artigo filtrado usando um filtro de linha com parâmetros, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
    -   Para um artigo filtrado usando um filtro de linha estático, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).  
  
2.  No Publicador no banco de dados de publicação, execute [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para definir um ou mais artigos relacionados, que também são conhecidos como artigos filho, para a publicação. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
3.  No Publicador no banco de dados de publicação, execute [sp_addmergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql). Especifique **@publication** , um nome exclusivo para esse filtro para **@filtername** , o nome do artigo filho criado na etapa 2 para **@article** ; o nome do artigo pai ao qual é feita a junção para **@join_articlename** e um dos valores a seguir para **@join_unique_key** :  
  
    -   **0** - indica uma junção muitos para um ou muitos para muitos entre os artigos pai e filho.  
  
    -   **1** - indica uma junção um para um ou um para muitos entre os artigos pai e filho.  
  
     Isso define um filtro de junção entre os dois artigos.  
  
    > [!CAUTION]  
    >  Somente defina **@join_unique_key** como **1** se você tiver uma restrição na coluna de junção na tabela subjacente para o artigo pai que garanta exclusividade. Se **@join_unique_key** for definido incorretamente como **1** , poderá ocorrer não convergência de dados.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Este exemplo define um artigo para uma publicação de mesclagem em que o artigo da tabela `SalesOrderDetail` é filtrado em relação à tabela `SalesOrderHeader` que, por sua vez, é filtrada usando um filtro de linha estático. Para obter mais informações, consulte [Definir e modificar um filtro de linha estático](define-and-modify-a-static-row-filter.md).  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergearticle)]  
  
 Este exemplo define um grupo de artigos em uma publicação de mesclagem em que os artigos são filtrados com uma série de filtros de junção na tabela `Employee` que, por sua vez, é filtrada usando um filtro de linha com parâmetros sobre o valor de [HOST_NAME](/sql/t-sql/functions/host-name-transact-sql) na coluna **LoginID** . Para obter mais informações, consulte [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubdynamic1.sql#sp_mergedynamicpub1)]  
  
## <a name="see-also"></a>Consulte também  
 [Filtros de junção](../merge/join-filters.md)   
 [Filtros de linha com parâmetros](../merge/parameterized-filters-parameterized-row-filters.md)   
 [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md)   
 [Filtrar dados publicados para a replicação de mesclagem](../merge/filter-published-data-for-merge-replication.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Definir uma relação de registro lógico entre artigos da tabela de mesclagem](define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Definir e modificar um filtro de linha parametrizado para um artigo de mesclagem](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
  

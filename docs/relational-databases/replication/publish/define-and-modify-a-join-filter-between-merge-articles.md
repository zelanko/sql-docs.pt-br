---
title: "Definir e modificar um filtro de jun&#231;&#227;o entre artigos de mesclagem | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "filtros [replicação do SQL Server], junção"
  - "filtros de junção de replicação de mesclagem [replicação do SQL Server]"
  - "modificando filtros, junção"
  - "filtros de junção"
ms.assetid: f7f23415-43ff-40f5-b3e0-0be1d148ee5b
caps.latest.revision: 46
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# Definir e modificar um filtro de jun&#231;&#227;o entre artigos de mesclagem
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
  
-   Se você adicionar, modificar ou excluir um filtro de junção após a inicialização de assinaturas na publicação, será preciso gerar um novo instantâneo e reinicializar todas as assinaturas depois de fazer a alteração. Para obter mais informações sobre os requisitos para alterações de propriedade, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Os filtros de junção podem ser criados manualmente para um conjunto de tabelas ou a replicação pode gerar os filtros automaticamente, com base nas relações entre as chaves estrangeiras e primárias definidas nas tabelas. Para obter mais informações sobre como gerar um conjunto de filtros de junção automaticamente, consulte [Gerar automaticamente um conjunto de junção filtros entre mesclar artigos e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Definir, modificar e excluir filtros de junção no **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para definir um filtro de junção  
  
1.  No **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>**, selecione um filtro de linha existente ou filtro de junção **tabelas filtradas** painel.  
  
2.  Clique em **Adicionar**e depois, em **Adicionar Junção para Estender o Filtro Selecionado**.  
  
3.  Crie a instrução de junção: selecione **Usar o construtor para criar a instrução** ou **Gravar a instrução de junção manualmente**.  
  
    -   Se você optar por usar o construtor, use as colunas na grade (**conjunto**, **coluna da tabela filtrada**, **operador**, e **coluna da tabela unida**) para criar uma instrução join.  
  
         Cada coluna na grade contém uma caixa de combinação suspensa, permitindo que você selecione duas colunas e um operador (**=**, **<>**, **<=**, **\<**, **>=**, **>**, e **como**). Os resultados são exibidos na área de texto **Visualizar** . Se a junção envolver mais de um par de colunas, selecione um conjunto (e ou ou) da **conjunto** coluna e, em seguida, insira mais duas colunas e um operador.  
  
    -   Se você selecionar para gravar a instrução manualmente, grave a instrução de junção na área de texto **Instrução de Junção** . Use as caixas de listagens **Colunas da tabela filtrada** e **Colunas da tabela unida** para arrastar e soltar colunas na área de texto **Instrução de junção** .  
  
    -   A Instrução de junção completa teria a seguinte aparência:  
  
        ```  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] INNER JOIN [Sales].[SalesOrderDetail] ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID]  
        ```  
  
         A cláusula JOIN deve usar nomeação de duas partes; nomeação de três partes e nomeação de quatro partes não possuem suporte.  
  
4.  Especifique opções de junção:  
  
    -   Se a coluna de junção na tabela filtrada (a tabela pai) for exclusiva, selecione **chave exclusiva**.  
  
        > [!CAUTION]  
        >  A seleção dessa opção indica que a relação entre tabelas pai e filho em um filtro de junção é de um para um ou um para muitos. Só selecione essa opção se houver uma restrição na coluna de junção na tabela filho que garanta a exclusividade. Se a opção for definida incorretamente, poderá ocorrer não convergência de dados.  
  
    -   Por padrão, os processos de replicação de mesclagem são alterados em uma base de linha por linha durante a sincronização. Para que as alterações nas linhas da tabela filtrada e de tabelas unidas processadas como uma unidade relacionadas, selecione **registro lógico** ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versões posteriores). Essa opção só estará disponível se os requisitos de  artigo e publicação para uso de registros lógicos forem atendidos. Para obter mais informações, consulte a seção "Considerações para usar registros lógicos" em [grupo alterações nas linhas relacionadas com registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### Para modificar um filtro de junção  
  
1.  No **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>**, selecione um filtro no **tabelas filtradas** painel e, em seguida, clique **Editar**.  
  
2.  Na caixa de diálogo **Editar Junção** , modifique o filtro.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para excluir um filtro de junção  
  
1.  No **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>**, selecione um filtro no **tabelas filtradas** painel e, em seguida, clique **Excluir**. Caso o próprio filtro excluído seja estendido por outras junções, essas junções também serão excluídas.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Estes procedimentos mostram um filtro com parâmetros em um artigo pai com filtros de junção entre esse artigo e artigos filho relacionados. Os filtros de junção podem ser definidos e modificados programaticamente usando procedimentos armazenados de replicação.  
  
#### Para definir um filtro de junção para estender um filtro de artigo a artigos relacionados em uma publicação de mesclagem  
  
1.  Defina a filtragem para o artigo ao qual está sendo feita a junção, que é também conhecido como o artigo pai.  
  
    -   Para um artigo filtrado usando um filtro de linha com parâmetros, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
    -   Para um artigo filtrado usando um filtro de linha estático, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
2.  No publicador do banco de dados de publicação, execute [sp_addmergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Para definir um ou mais artigos relacionados, que também são conhecidos como artigos filho, para a publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
3.  No publicador do banco de dados de publicação, execute [sp_addmergefilter & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md). Especifique **@publication**, um nome exclusivo para este filtro para **@filtername**, o nome do artigo filho criado na etapa 2 para **@article**, o nome do artigo pai que é adicionado para **@join_articlename**, e um dos seguintes valores para **@join_unique_key**:  
  
    -   **0** -indica uma junção muitos-para-um ou muitos-para-muitos entre os artigos pai e filho.  
  
    -   **1** -indica uma junção ou um-para-muitos entre os artigos pai e filho.  
  
     Isso define um filtro de junção entre os dois artigos.  
  
    > [!CAUTION]  
    >  Apenas defina **@join_unique_key** para **1** se você tiver uma restrição na coluna de junção na tabela subjacente para o artigo pai que garanta a exclusividade. Se **@join_unique_key** é definido como **1** incorretamente, poderá ocorrer não convergência de dados.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Este exemplo define um artigo para uma publicação de mesclagem em que o artigo da tabela `SalesOrderDetail` é filtrado em relação à tabela `SalesOrderHeader` que, por sua vez, é filtrada usando um filtro de linha estático. Para obter mais informações, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_1.sql)]  
  
 Este exemplo define um grupo de artigos em uma publicação de mesclagem onde os artigos são filtrados por uma série de filtros de junção em relação a `Employee` tabela por sua vez filtrada usando um filtro de linha com parâmetros sobre o valor de [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) no **LoginID** coluna. Para obter mais informações, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_2.sql)]  
  
## Consulte também  
 [Filtros de junção](../../../relational-databases/replication/merge/join-filters.md)   
 [Filtros de linha com parâmetros](../../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtrar dados publicados para replicação de mesclagem](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [Como definir e modificar um filtro de junção entre artigos de mesclagem (SQL Server Management Studio)](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Definir uma relação de registro lógico entre artigos da tabela de mesclagem](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
  
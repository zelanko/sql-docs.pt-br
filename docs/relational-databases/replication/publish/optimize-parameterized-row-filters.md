---
title: "Otimizar filtros de linha com par&#226;metros | Microsoft Docs"
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
  - "partições pré-computadas [replicação do SQL Server]"
  - "filtros [replicação do SQL Server], parametrizados"
  - "partições pré-computadas de replicação de mesclagem [replicação do SQL Server], SQL Server Management Studio"
  - "filtros com parâmetros [replicação do SQL Server], otimizando"
ms.assetid: 49349605-ebd0-4757-95be-c0447f30ba13
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Otimizar filtros de linha com par&#226;metros
  Este tópico descreve como otimizar filtros de linha com parâmetros no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para otimizar filtros de linha com parâmetros, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Quando você usar filtros com parâmetros, será possível controlar como os filtros serão processados pela replicação de mesclagem, especificando a opção **use partition groups** ou a opção **keep partition changes** ao criar uma publicação. Essas opções melhoram o desempenho de sincronização para publicações com artigos filtrados, armazenando metadados adicionais no banco de dados de publicação. Você pode controlar como os dados serão compartilhados entre Assinantes definindo as **opções de partição** ao criar um artigo. Para obter mais informações sobre esses requisitos, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
     Com os assinantes do [!INCLUDE[ssEW](../../../includes/ssew-md.md)] SQL Server Compact, keep_partition_changes deve ser definido como true para assegurar que as exclusões sejam propagadas corretamente. Quando definido como falso, o assinante pode ter mais linhas do que o esperado.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 As configurações seguintes podem ser usadas para aperfeiçoar filtros de linha com parâmetros:  
  
 **Opções de Partição**  
 Definir essa opção no **propriedades** página do **Propriedades do artigo - \< artigo>** caixa de diálogo ou no **Adicionar filtro** caixa de diálogo. Ambas as caixas de diálogo estão disponíveis no Assistente de nova publicação e o **Propriedades de publicação - \< publicação>** caixa de diálogo. O **Propriedades do artigo - \< artigo>** caixa de diálogo permite que você especifique valores para essa opção adicionais que não estão disponíveis na **Adicionar filtro** caixa de diálogo.  
  
 **Pré-calcular partições**  
 Essa opção é definida como **True** por padrão, se os artigos da publicação de acordo com um conjunto de requisitos. Para obter mais informações sobre esses requisitos, consulte [otimizar desempenho de filtro parametrizado com partições pré-calculadas](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md). Modificar essa opção no **Opções de assinatura** página o **Propriedades de publicação - \< publicação>** caixa de diálogo.  
  
 **Otimizar sincronização**  
 Essa opção deve ser definida como **True** somente se **pré-calcular partições** é definido como **False**. Definir essa opção no **Opções de assinatura** página o **Propriedades de publicação - \< publicação>** caixa de diálogo.  
  
 Para obter mais informações sobre como usar o Assistente para nova publicação e acessar o **Propriedades de publicação - \< publicação>** caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para definir as opções de partição na caixa de diálogo Adicionar Filtro ou Editar Filtro  
  
1.  No **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **Add**, e, em seguida, clique em **Adicionar filtro**.  
  
2.  Criar um filtro com parâmetros. Para obter mais informações, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
3.  Selecione a opção que corresponde ao modo em que os dados serão compartilhados entre Assinantes:  
  
    -   **Uma linha dessa tabela irá para múltiplas assinaturas**  
  
    -   **Uma linha dessa tabela irá para apenas uma assinatura**  
  
     Se você selecionar **Uma linha desta tabela irá para apenas uma assinatura**, a replicação de mesclagem pode otimizar o desempenho armazenando e processando uma quantia menor de metadados. No entanto, será necessário certificar-se de que os dados são particionados de forma que uma linha não seja replicada em mais de um Assinante. Para obter mais informações, consulte a seção "Configurando opções de partição" no tópico [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### Para definir opções de partição nas propriedades do artigo - \< artigo> caixa de diálogo  
  
1.  Sobre o **artigos** página do Assistente de nova publicação ou o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione uma tabela e, em seguida, clique em **Propriedades do artigo**.  
  
2.  Clique em **Definir Propriedades do Artigo Realçado na Tabela** ou **Definir as Propriedades de Todos os Artigos de Tabela**.  
  
3.  No **objeto de destino** seção o **propriedades** Guia do **Propriedades do artigo - \< artigo>** caixa de diálogo, especifique um dos valores a seguir para **Opções de partição**:  
  
    -   **Com sobreposição**  
  
    -   **Com sobreposição, não permitir alterações de dados fora da partição**  
  
    -   **Sem-sobreposição, única assinatura**  
  
    -   **Sem-sobreposição, compartilhados entre assinaturas**  
  
     Para obter mais informações sobre essas opções e sobre como estão relacionadas às opções disponíveis nas caixas de diálogo **Adicionar Filtro** e **Editar Filtro** , consulte a seção "Definindo as opções de partição'" em [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### Para definir o Pré-calcular Partições  
  
1.  No **Opções de assinatura** página o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione um valor para o **pré-calcular partições** opção. A propriedade é somente leitura se:  
  
    -   A publicação não satisfizer os requisitos para as partições pré-calculadas.  
  
    -   Um instantâneo ainda não tiver sido gerado para a publicação. Nesse caso, a opção exibe um valor de **Definir automaticamente quando um instantâneo é criado.**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para definir o Otimizar Sincronização  
  
1.  No **Opções de assinatura** página o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione um valor de **True** para o **otimizar sincronização** opção.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Para obter definições das opções de filtragem para **@keep_partition_changes** e **@use_partition_groups**, consulte [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
#### Para especificar otimizações de filtro de mesclagem ao criar uma nova publicação  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique **@publication** e um valor de **true** para um dos seguintes parâmetros:  
  
    -   **@use_partition_groups**:-a otimização de desempenho mais alta, fornecida os artigos estão em conformidade com os requisitos para partições pré-calculadas. Para obter mais informações, consulte [otimizar desempenho de filtro parametrizado com partições pré-calculadas](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md).  
  
    -   **@keep_partition_changes** -use essa otimização se partições pré-calculadas não podem ser usadas.  
  
2.  Adicione um trabalho de instantâneo para a publicação. Para obter mais informações, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md).  
  
3.  No publicador do banco de dados de publicação, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), especificando os seguintes parâmetros:  
  
    -   **@publication** -o nome da publicação da etapa 1.  
  
    -   **@article** -um nome para o artigo  
  
    -   **@source_object** - o objeto de banco de dados que está sendo publicado.  
  
    -   **@subset_filterclause** -a cláusula de filtro com parâmetros opcional usada para filtrar o artigo horizontalmente.  
  
    -   **@partition_options** -as opções de partição para o artigo filtrado.  
  
4.  Repita a etapa 3 para cada artigo na publicação.  
  
5.  (Opcional) No publicador do banco de dados de publicação, execute [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) para definir um filtro de junção entre dois artigos. Para obter mais informações, consulte [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
#### Para visualizar e modificar comportamentos de filtro de mesclagem para uma publicação existente  
  
1.  (Opcional) No publicador do banco de dados de publicação, execute [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando **@publication**. Observe o valor de **keep_partition_changes** e **use_partition_groups** no conjunto de resultados.  
  
2.  (Opcional) No publicador do banco de dados de publicação, execute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique um valor de **use_partition_groups** para **@property** e **true** ou **false** para **@value**.  
  
3.  (Opcional) No publicador do banco de dados de publicação, execute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique um valor de **keep_partition_changes** para **@property** e **true** ou **false** para **@value**.  
  
    > [!NOTE]  
    >  Ao habilitar **keep_partition_changes**, é preciso primeiro desabilitar **use_partition_groups** e especifique um valor de **1** para **@force_reinit_subscription**.  
  
4.  (Opcional) No publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor de **partition_options** para **@property** e o valor apropriado para **@value**. Consulte [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para definições destas opções de filtragem.  
  
5.  (Opcional) Iniciar o Snapshot Agent para regenerar o instantâneo se necessário. Para obter informações sobre quais alterações exigem um novo instantâneo seja gerado, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## Consulte também  
 [Gerar automaticamente um conjunto de filtros de junção entre artigos de mesclagem e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md)   
 [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Filtros de linha com parâmetros](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  
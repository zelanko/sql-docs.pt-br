---
title: "Propriedades de Publica&#231;&#227;o, Artigos | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.articles.f1"
ms.assetid: bdeea318-a153-44b8-9e51-9155f3bad18b
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Propriedades de Publica&#231;&#227;o, Artigos
  O **artigos** página de **Propriedades de publicação** caixa de diálogo: contém informações sobre os artigos contidos em uma publicação; permite adicionar e descartar artigos de publicações existentes; e permite que você altere as propriedades do artigo e filtragem de coluna.  
  
> [!NOTE]  
>  Depois que uma publicação é criada, algumas alterações de propriedade requerem um novo instantâneo. Se uma publicação tiver assinaturas, algumas alterações também exigirão que todas as assinaturas sejam reiniciadas. Para obter mais informações, consulte [alterar propriedades da publicação e artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md) e [Adicionar e descartar artigos de publicações existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 Se você estiver publicando um objeto de banco de dados que depende de outros objetos de banco de dados, terá de publicar todos os objetos referenciados. Por exemplo, se você publicar uma exibição que depende de uma tabela, terá de publicar a tabela também.  
  
 Objetos que não podem ser publicados têm um ícone vermelho próximo a eles, com uma explicação no painel de informações na parte inferior da página do assistente. Os objetos seguintes não podem ser publicados:  
  
-   Objetos criptografados.  
  
-   Exibições indexadas contendo colunas que permitem NULL.  
  
-   Tabelas sem chaves primárias não podem ser publicadas em publicações transacionais.  
  
-   Tabelas não podem ser publicadas em uma publicação de mesclagem e em uma publicação transacional habilitadas para assinaturas de atualização enfileirada. Para obter mais informações sobre como publicar um artigo em mais de uma publicação, consulte a seção "Publicando tabelas em mais de uma publicação" [publica dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
## Publicadores Oracle  
 Há considerações adicionais para Publicadores Oracle:  
  
-   Para uma lista de objetos que podem ser publicados no Oracle, consulte [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md). Não são exibidos objetos que não podem ser publicados.  
  
-   Para uma lista de tipos de dados que podem ser publicados, consulte [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md). Colunas com tipos de dados que não podem ser publicados não são exibidas.  
  
## Filtros de coluna  
 Filtrar colunas nessa página expandindo uma tabela no **objetos para publicação** painel e, em seguida, selecionando apenas as colunas necessárias (linhas podem ser filtradas no **Filtrar linhas da tabela** página desse assistente). A filtragem de colunas é útil por várias razões, incluindo segurança (impedindo que dados sensíveis sejam replicados) e desempenho (evitando replicação de colunas BLOB (objeto binário grande), por exemplo). Para obter mais informações sobre filtragem de coluna, incluindo uma lista dos tipos de coluna que não podem ser filtradas, consulte [Filtrar dados publicados](../../relational-databases/replication/publish/filter-published-data.md).  
  
## Opções  
 O painel **Objetos para publicação** permite:  
  
-   Exibir todos os objetos disponíveis para replicação.  
  
-   Incluir um objeto em uma publicação marcando a caixa de seleção próxima àquele objeto.  
  
-   Descartar um artigo de uma publicação desmarcando a caixa de seleção próximo àquele objeto. Para obter informações sobre quando os artigos podem ser descartados, consulte [Adicionar e descartar artigos de publicações existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Incluir todos os objetos de um tipo específico (como uma tabela) a publicação, marcando a caixa de seleção próxima ao tipo de objeto (como **tabelas**).  
  
-   Expandir nós de tabela para ver as colunas na tabela.  
  
-   Filtrar colunas de tabela de uma publicação, limpando a caixa de seleção próxima à coluna, ou incluir colunas não publicadas marcando a caixa de seleção.  
  
-   Clique com o botão direito do mouse em um objeto no painel para consultar um menu de comandos para aquele objeto.  
  
 **Propriedades do Artigo**  
 Clique em **Propriedades do artigo** , e, em seguida, clique em um dos seguintes:  
  
-   Clique em **definir propriedades de realçado \< ObjectType> artigo** para iniciar o **Propriedades do artigo - \< ObjectName>** caixa de diálogo; propriedade as alterações feitas nessa caixa de diálogo são aplicadas somente ao objeto que está realçado no painel do objeto no **artigos** página.  
  
-   Clique em **definir propriedades de todos os \< ObjectType> artigos**, para iniciar o **Propriedades para todos os \< ObjectType> artigos** caixa de diálogo; propriedade as alterações feitas nessa caixa de diálogo são aplicadas a todos os objetos desse tipo no painel objeto o **artigos** página, incluindo os ainda não foram selecionados para publicação.  
  
    > [!NOTE]  
    >  Alterações de propriedade feitas a **Propriedades para todos os \< ObjectType> artigos** caixa de diálogo Substituir qualquer feitas anteriormente no **Propriedades do artigo - \< ObjectName>** caixa de diálogo. Se, por exemplo, você quiser definir um número de padrões para todos os artigos de um tipo de objeto, mas também quer definir algumas propriedades para objetos individuais, defina primeiro os padrões para todos os artigos. Em seguida, defina as propriedades para os objetos individuais.  
  
 **A tabela realçada é somente para download**  
 Somente replicação de mesclagem. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Selecione para especificar que as alterações serão desabilitadas no Assinante se uma assinatura de cliente for usada. Como artigos somente para download não podem ser atualizados no Assinante, metadados de controle não são enviados aos Assinantes. Isso pode resultar em armazenamento reduzido nos Assinantes e em um benefício no desempenho, principalmente se a conexão de rede for lenta. Essa opção corresponde a um valor de **Download somente para assinante, Proibir alterações do assinante** para a opção **direção de sincronização** no **Propriedades do artigo** caixa de diálogo. Para obter mais informações, consulte [otimizar o desempenho de replicação de mesclagem com artigos Download-Only](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Mostrar somente os artigos marcados na lista**  
 Marque essa caixa de seleção para mostrar somente os artigos selecionados no painel de objeto.  
  
## Consulte também  
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizar e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Reinicializar uma assinatura](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
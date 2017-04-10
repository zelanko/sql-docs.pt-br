---
title: "Publicar dados e objetos de banco de dados | Microsoft Docs"
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
  - "tipos definidos pelo usuário [replicação do SQL Server]"
  - "artigos [replicação do SQL Server], descartando"
  - "objetos [replicação do SQL Server]"
  - "publicações [replicação do SQL Server], criando"
  - "replicação de mesclagem [replicação do SQL Server], publicações"
  - "artigos somente de esquema [replicação do SQL Server]"
  - "publicação [replicação do SQL Server], objetos de banco de dados"
  - "artigos [replicação do SQL Server], definindo"
  - "publicação [replicação do SQL Server], funções"
  - "replicação [SQL Server], publicações"
  - "publicação [replicação do SQL Server], exibições"
  - "tabelas [replica&#231;&#227;o do SQL Server]"
  - "esquemas [replica&amp;#231;&amp;#227;o do SQL Server]"
  - "publicação [replicação do SQL Server], dados"
  - "esquemas [replicação do SQL Server], publicação"
  - "artigos [replicação do SQL Server], procedimentos armazenados e"
  - "publicação [replicação do SQL Server], tabelas"
  - "tipos de dados de alias [replicação do SQL Server]"
  - "publicações [replicação do SQL Server], excluindo"
  - "replicação de instantâneo [SQL Server], publicações"
  - "artigos [replicação SQL Server], modificando"
  - "replicação transacional, publicações"
  - "publicação [replicação do SQL Server], procedimentos armazenados"
  - "publicando [replica&#231;&#227;o do SQL Server]"
  - "exibições [replicação do SQL Server]"
  - "procedimentos armazenados [replicação do SQL Server], publicação"
  - "publicações [replicação do SQL Server], opções de esquema"
  - "artigos [replicação do SQL Server], adicionando"
  - "publicações [replicação do SQL Server], modificando"
  - "fun&#231;&#245;es definidas pelo usu&#225;rio [replica&#231;&#227;o do SQL Server]"
ms.assetid: d986032c-3387-4de1-a435-3ec5e82185a2
caps.latest.revision: 83
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 83
---
# Publicar dados e objetos de banco de dados
  Ao criar uma publicação, você escolhe as tabelas e outros objetos de banco de dados que deseja publicar. Você pode publicar os objetos de banco de dados a seguir usando replicação.  
  
|Objeto de banco de dados|Replicação de instantâneo e replicação transacional|Replicação de mesclagem|  
|---------------------|--------------------------------------------------------|-----------------------|  
|Tabelas|X|X|  
|Tabelas particionadas|X|X|  
|Procedimentos armazenados – Definição ([!INCLUDE[tsql](../../../includes/tsql-md.md)] e CLR)|X|X|  
|Procedimentos armazenados – Execução ([!INCLUDE[tsql](../../../includes/tsql-md.md)] e CLR)|X|não|  
|Exibições|X|X|  
|Exibições indexadas|X|X|  
|Exibições indexadas como tabelas|X|não|  
|Tipos definidos pelo usuário (CLR)|X|X|  
|Funções definidas pelo usuário ([!INCLUDE[tsql](../../../includes/tsql-md.md)] e CLR)|X|X|  
|Tipos de dados de alias|X|X|  
|Índices de texto completo|X|X|  
|Objetos de esquema (restrições, índices, gatilhos DML de usuário, propriedades estendidas e agrupamento)|X|X|  
  
## Criando publicações  
 Para criar uma publicação, forneça as seguintes informações:  
  
-   O Distribuidor.  
  
-   A localização padrão dos arquivos de instantâneo.  
  
-   O banco de dados da publicação.  
  
-   O tipo de publicação a ser criada (instantâneo, transacional, transacional com assinaturas atualizáveis ou mesclagem).  
  
-   Os dados e objetos de banco de dados (artigos) a serem incluídos na publicação.  
  
-   Filtros de linha e filtros de coluna estáticos para todos os tipos de publicação e filtros de linha com parâmetros e filtros de junção para publicações de mesclagem.  
  
-   A agenda do Agente de Instantâneo.  
  
-   Contas sob as quais os seguintes agentes irão executar: o Agente de Instantâneo para todas as publicações; o Agente de Leitor de Log para todas as publicações transacionais; o Agente de Leitor de Fila para publicações transacionais que permitem atualização das assinaturas.  
  
-   Um nome e descrição para a publicação.  
  
 Para obter informações sobre como trabalhar com publicações, consulte os tópicos a seguir:  
  
-   [Crie uma publicação](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Defina um Artigo](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [Visualizar e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [Visualizar e modificar propriedades de artigos](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [Excluir uma publicação](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [Excluir um artigo](../../../relational-databases/replication/publish/delete-an-article.md)  
  
> [!NOTE]  
>  Excluir um artigo ou publicação não remove objetos do Assinante.  
  
## Publicando tabelas  
 O objeto publicado com maior frequência é uma tabela. Os vínculos a seguir fornecem informações adicionais sobre áreas relacionadas a publicação de tabelas:  
  
-   [Filtrar dados publicados](../../../relational-databases/replication/publish/filter-published-data.md)  
  
-   [Opções de artigo para replicação transacional](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
-   [Opções de artigo para replicação de mesclagem](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
-   [Replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
 Ao publicar uma tabela para replicação, você pode especificar quais objetos de esquema devem ser copiados para o Assinante, como integridade referencial declarada (restrições de chave primária, restrições de referência, restrições exclusivas), índices, gatilhos DML de usuário (os disparadores DDL não podem ser replicados), propriedades estendidas e agrupamento. As propriedades estendidas são replicadas apenas na sincronização inicial entre o Editor e o Assinante. Se você adicionar ou modificar uma propriedade estendida depois da sincronização inicial, a alteração não será replicada.  
  
 Para especificar opções de esquema, consulte [especificar opções de esquema](../../../relational-databases/replication/publish/specify-schema-options.md) ou <xref:Microsoft.SqlServer.Replication.Article.SchemaOption%2A>.  
  
### Tabelas e índices particionados  
 A replicação dá suporte à publicação de tabelas e índices particionados. O nível de suporte depende do tipo de replicação usado e das opções especificadas para a publicação e os artigos associados às tabelas particionadas. Para obter mais informações, consulte [replicar tabelas e índices particionados](../../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
## Publicando procedimentos armazenados  
 Todos os tipos de replicação permitem que você reproduza definições de procedimentos armazenados: o CREATE PROCEDURE é copiado para cada Assinante. No caso de procedimentos armazenados CLR (Common Language Runtime), o assembly associado também é copiado. As alterações a procedimentos são replicadas aos Assinantes; as alterações aos assemblies associados não são.  
  
 Além de replicar a definição de um procedimento armazenado, a replicação transacional permite que você replique a execução dos procedimentos armazenados. Isso é útil ao replicar os resultados de procedimentos armazenados orientados a manutenção que afetam grandes quantidades de dados. Para obter mais informações, consulte [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
## Publicando exibições  
 Todos os tipos de replicação permitem que você reproduza exibições. A exibição (e o índice correspondente, se for uma exibição indexada) pode ser copiada para o Assinante, mas a tabela base também deve ser replicada.  
  
 Para exibições indexadas, a replicação transacional também permite que você replique a exibição indexada como uma tabela em vez de uma exibição, eliminando a necessidade de replicar também a tabela base. Para fazer isso, especifique uma das opções "indexed view logbased" para o *@type* parâmetro [sp_addarticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Para obter mais informações sobre como usar o **sp_addarticle**, consulte [definir um artigo](../../../relational-databases/replication/publish/define-an-article.md).  
  
## Publicando funções definidas pelo usuário  
 As instruções CREATE FUNCTION para as funções CLR e [!INCLUDE[tsql](../../../includes/tsql-md.md)] são copiadas para cada Assinante. No caso das funções CLR, o assembly associado também é copiado. As alterações a funções são replicadas aos Assinantes; as alterações aos assemblies associados não são.  
  
## Publicando tipos definidos pelo usuário e tipos de dados de alias  
 As colunas que usam tipos definidos pelo usuário ou tipos de dados de alias são reproduzidas para Assinantes como outras colunas. O TYPEstatement criar para cada tipo replicado é executada no assinante antes da tabela é criada. No caso de tipos definidos pelo usuário, o assembly associado é copiado também para cada Assinante. As alterações nos tipos definidos pelo usuário e tipos de dados de alias não são replicadas para os Assinantes.  
  
 Se um tipo é definido em um banco de dados, mas não é referenciado em nenhuma coluna quando uma publicação é criada, o tipo não é copiado para os Assinantes. Se depois você criar uma coluna desse tipo no banco de dados e quiser replicá-la, será preciso primeiro copiar manualmente o tipo (e o assembly associado para um tipo definido pelo usuário) para cada Assinante.  
  
## Publicando índices de texto completo  
 A instrução CREATE FULLTEXT INDEX é copiada para cada Assinante e o índice de texto completo é criado para o Assinante. As alterações feitas em índices de texto completo usando ALTER FULLTEXT INDEX não são replicadas.  
  
## Fazendo alterações de esquema em objetos publicados  
 A replicação oferece suporte para um amplo intervalo de alterações de esquema para objetos publicados. Ao se fazer qualquer uma das seguintes alterações de esquema no objeto publicado adequado em um Publicador do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], essa alteração será propagada por padrão para todos os Assinantes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 Para obter mais informações, consulte [fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## Considerações ao publicar  
 Tenha em mente as seguintes questões ao publicar objetos de bancos de dados:  
  
-   O banco de dados está acessível aos usuários durante a criação da publicação e o instantâneo inicial, mas é aconselhável criar publicações em momentos de menor atividade no Publicador.  
  
-   Um banco de dados não pode ser renomeado depois que uma publicação for criada nele. Para renomeá-lo, você deve primeiro remover a replicação do banco de dados.  
  
-   Se você estiver publicando um objeto de banco de dados que depende de outros objetos de banco de dados, terá de publicar todos os objetos referenciados. Por exemplo, se você publicar uma exibição que depende de uma tabela, terá de publicar a tabela também.  
  
    > [!NOTE]  
    >  Se você adicionar um artigo a uma publicação de mesclagem e depende de um artigo existente o novo artigo, você deve especificar uma ordem de processamento para os dois artigos usando o **@processing_order** parâmetro do [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) e [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Considere o seguinte cenário: uma tabela é publicada, mas não é publicada a função que é referenciada pela tabela. Se a função não for publicada, a tabela não poderá ser criada no Assinante. Quando você adiciona a função à publicação: Especifique um valor de **1** para o **@processing_order** parâmetro do **sp_addmergearticle**; e especifique um valor de **2** para o **@processing_order** parâmetro **sp_changemergearticle**, especificando o nome da tabela para o parâmetro **@article**. Essa ordem de processamento garante a criação da função no Assinante antes da tabela que depende disso. Você pode usar números diferentes para cada artigo desde que o número para a função seja menor do que o número para a tabela.  
  
-   Os nomes de publicação não podem incluir nenhum dos seguintes caracteres: % * [ ] | : " ? \ / \< >.  
  
### Limitações na publicação de objetos  
  
-   O número máximo de artigos e colunas que podem ser publicados difere nos tipos de publicações. Para obter mais informações, consulte a seção "Objetos de replicação" [especificações de capacidade máxima para o SQL Server](../../../sql-server/maximum-capacity-specifications-for-sql-server.md).  
  
-   Procedimentos armazenados, exibições, gatilhos e funções definidas pelo usuário que tenham sido definidos como WITH ENCRYPTION não podem ser publicados como parte da replicação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   As coleções de esquema XML podem ser replicadas, mas as alterações não são replicadas depois do instantâneo inicial.  
  
-   As tabelas publicadas para replicação transacional devem ter uma chave primária. Se uma tabela estiver em uma publicação de replicação transacional, não será possível desabilitar nenhum índice associado a colunas de chave primária. Esses índices são necessários para a replicação. Para desabilitar um índice, você deve primeiramente descartar a tabela da publicação.  
  
-   Padrões associados criados com [sp_bindefault & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md) não são replicados (padrões associados são preteridos em favor de padrões criados com a palavra-chave DEFAULT de ALTER TABLE ou CREATE TABLE).  
  
-   Funções contendo a **NOEXPAND** dica em exibições indexadas não pode ser publicada na mesma publicação como as tabelas referenciadas e exibições indexadas, devido a ordem na qual o agente de distribuição as entrega. Para contornar esse problema, coloque a tabela e a criação do modo de exibição indexado em uma primeira publicação e adicione funções contendo a **NOEXPAND** Dica nas exibições indexadas para uma segunda publicação que você publica após a primeira publicação for concluído. Ou crie scripts para essas funções e fornecer o script usando o *@post_snapshot_script* parâmetro do **sp_addpublication**.  
  
### Propriedade de esquemas e objetos  
 A replicação tem o seguinte comportamento padrão no Assistente para Nova Publicação em relação à propriedade de esquemas e objetos:  
  
-   Para artigos em publicações de mesclagem com um nível de compatibilidade 90 ou superior, publicações de instantâneos e publicações transacionais: por padrão, o proprietário do objeto no Assinante é igual ao proprietário do objeto correspondente no Publicador. Caso não existam esquemas proprietários de objetos no Assinante, eles serão criados automaticamente.  
  
-   Para artigos em publicação de mesclagem com um nível de compatibilidade abaixo de 90: por padrão, o proprietário é deixado em branco e especificado como **dbo** durante a criação do objeto no Assinante.  
  
-   Para artigos em publicações Oracle: por padrão, o proprietário é especificado como **dbo**.  
  
-   Para artigos em publicações que usam instantâneos de modo de caracteres (que são usados para Assinantes não [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e Assinantes [!INCLUDE[ssEW](../../../includes/ssew-md.md)]): por padrão o proprietário é deixado em branco. O proprietário assume o padrão do proprietário associado à conta usada pelo Agente de Distribuição ou Agente de Mesclagem para se conectar ao Assinante.  
  
 O proprietário do objeto pode ser alterado por meio de **Propriedades de artigo - \<***artigo***>** caixa de diálogo e por meio dos seguintes procedimentos armazenados: **sp_addarticle**, **sp_addmergearticle**, **sp_changearticle**, e **sp_changemergearticle**. Para obter mais informações, consulte [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), [definir um artigo](../../../relational-databases/replication/publish/define-an-article.md), e [Exibir e modificar propriedades de artigo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
### Publicando dados para Assinantes que executam versões anteriores do SQL Server  
  
-   Se estiver publicando para um Assinante que executa uma versão anterior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você estará limitado à funcionalidade dessa versão, tanto em termos da funcionalidade específica à replicação quanto da funcionalidade do produto como um todo.  
  
-   As publicações de mesclagem usam um nível de compatibilidade que determina quais recursos podem ser usados em uma publicação e permitem que você forneça suporte a Assinantes que executam versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
### Publicando tabelas em mais de uma publicação  
 A replicação fornece suporte para publicação de artigos em várias publicações (inclusive a republicação de dados) com as seguintes restrições:  
  
-   Se um artigo for publicado em uma publicação transacional e uma publicação de mesclagem, certifique-se de que o *@published_in_tran_pub* propriedade é definida como TRUE para o artigo de mesclagem. Para obter mais informações sobre como configurar propriedades, consulte [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md) e [Exibir e modificar propriedades de artigo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
     Você também deve definir o *@published_in_tran_pub* propriedade se um artigo for parte de uma assinatura transacional e está incluído em uma publicação de mesclagem. Se esse for o caso, esteja ciente de que, por padrão, a replicação transacional espera que as tabelas no Assinante sejam tratadas como somente leitura; se a replicação de mesclagem alterar dados em uma tabela em uma assinatura transacional, pode haver não convergência de dados. Para evitar essa possibilidade, recomendamos que qualquer tabela desse tipo seja especificada como somente download na publicação de mesclagem. Isso impede que um Assinante de mesclagem carregue alterações de dados na tabela. Para obter mais informações, consulte [otimizar o desempenho de replicação de mesclagem com artigos Download-Only](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
-   Um artigo não pode ser publicado tanto em uma publicação de mesclagem quanto em uma publicação transacional com assinaturas de atualização enfileirada.  
  
-   Os artigos incluídos em publicações transacionais que fornecem suporte para assinaturas de atualização não podem ser republicados.  
  
-   Se um artigo for publicado em mais de uma publicação transacional que forneça suporte para assinaturas de atualização enfileiradas, as propriedades seguintes devem ter o mesmo valor para o artigo em todas as publicações:  
  
    |Propriedade|Parâmetro em sp_addarticle|  
    |--------------|---------------------------------|  
    |Gerenciamento de intervalo de identidade|**@auto_identity_range** (preterido) e **@identityrangemangementoption**|  
    |Intervalo de identidade do Publicador|**@pub_identity_range**|  
    |Intervalo de identidade|**@identity_range**|  
    |Limite de intervalo de identidade|**@threshold**|  
  
     Para obter mais informações sobre esses parâmetros, consulte [sp_addarticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
-   Se um artigo for publicado em mais de uma publicação de mesclagem, as seguintes propriedades devem ter o mesmo valor para o artigo em todas as publicações:  
  
    |Propriedade|Parâmetro em sp_addmergearticle|  
    |--------------|--------------------------------------|  
    |Rastreamento de coluna|**@column_tracking**|  
    |Opções de esquema|**@schema_option**|  
    |Filtragem de coluna|**@vertical_partition**|  
    |Opções de carregamento do assinante|**@subscriber_upload_options**|  
    |Controle de exclusão condicional|**@delete_tracking**|  
    |Compensação de erro|**@compensate_for_errors**|  
    |Gerenciamento de intervalo de identidade|**@auto_identity_range** (preterido) e **@identityrangemangementoption**|  
    |Intervalo de identidade do Publicador|**@pub_identity_range**|  
    |Intervalo de identidade|**@identity_range**|  
    |Limite de intervalo de identidade|**@threshold**|  
    |Opções de partição|**@partition_options**|  
    |Fluxo de coluna de blob|**@stream_blob_columns**|  
    |Tipo de filtro|**@filter_type** (parâmetro em **sp_addmergefilter**)|  
  
     Para obter mais informações sobre esses parâmetros, consulte [sp_addmergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) e [sp_addmergefilter & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md).  
  
-   A replicação transacional e a replicação de mesclagem não filtrada fornecem suporte à publicação de uma tabela em várias publicações e depois à assinatura dentro de uma única tabela no banco de dados de assinatura (frequentemente chamado de cenário de acúmulo). O acúmulo é usado muitas vezes para agregar subconjuntos de dados de localizações múltiplas em uma única tabela em um Assinante central. As publicações de mesclagem filtradas não fornecem suporte ao cenário de Assinante central. Para replicação de mesclagem, o acúmulo geralmente é implementado por meio de uma única publicação com filtros de linha com parâmetros. Para obter mais informações, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
## Consulte também  
 [Adicionar e remover artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Configurar a distribuição](../../../relational-databases/replication/configure-distribution.md)   
 [Inicializar uma assinatura](../../../relational-databases/replication/initialize-a-subscription.md)   
 [Replicação de script](../../../relational-databases/replication/scripting-replication.md)   
 [Proteger o Publicador](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [Assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
---
title: "Definir e modificar um filtro de linha com par&#226;metros para um artigo de mesclagem | Microsoft Docs"
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
  - "filtros com parâmetros [replicação do SQL Server], definindo"
  - "filtros com parâmetros [replicação do SQL Server], modificando"
  - "mesclar replicação [replicação do SQL Server], filtros dinâmicos"
  - "filtros com parâmetros de replicação de mesclagem [replicação do SQL Server]"
  - "filtros [replicação do SQL Server], parametrizados"
  - "modificando filtros, linha com parâmetros"
  - "filtros dinâmicos [replicação do SQL Server]"
ms.assetid: de0482a2-3cc8-4030-8a4a-14364549ac9f
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Definir e modificar um filtro de linha com par&#226;metros para um artigo de mesclagem
  Este tópico descreve como definir e modificar um filtro de linha com parâmetros no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Ao criar artigos de tabela, você pode usar filtros de linha com parâmetros. Esses filtros usam uma [onde](../../../t-sql/queries/where-transact-sql.md) cláusula para selecionar os dados apropriados a serem publicadas. Em vez de especificar um valor literal na cláusula (como você faria com um filtro de linha estático), você especifica uma ou ambas das seguintes funções do sistema: [SUSER_SNAME](../../../t-sql/functions/suser-sname-transact-sql.md) e [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md). Para obter mais informações, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para definir e modificar um filtro de linha com parâmetros, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se você adicionar, modificar ou excluir um filtro de linha com parâmetros após a inicialização de assinaturas na publicação, será preciso gerar um novo instantâneo e reinicializar todas as assinaturas depois de fazer a alteração. Para obter mais informações sobre os requisitos para alterações de propriedade, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Por motivos de desempenho, recomendamos que não sejam aplicadas funções a nomes de colunas em cláusulas de filtro de linha com parâmetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Se você usar HOST_NAME em uma cláusula de filtro e substituir o valor HOST_NAME, talvez precise converter tipos de dados usando CONVERT. Para obter mais informações sobre as práticas recomendadas para esse caso, consulte a seção "Substituindo o valor HOST_NAME ()" no tópico [filtros de linha com parâmetros](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Definir, modificar e excluir filtros de linha com parâmetros no **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para definir um filtro de linha com parâmetros  
  
1.  No **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>**, clique em **Add**, e, em seguida, clique em **Adicionar filtro**.  
  
2.  Na **Adicionar filtro** caixa de diálogo, selecione uma tabela para filtrar na caixa de listagem suspensa.  
  
3.  Crie uma instrução de filtro no **instrução de filtro** caixa de texto. Você pode digitar diretamente na área de texto e também pode arrastar e soltar colunas da caixa de listagem **Colunas** .  
  
    -   A área de texto **Instrução de filtro** inclui o texto padrão que está no formato de:  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
    -   O texto padrão não pode ser alterado; digite a cláusula de filtro depois da palavra-chave WHERE usando sintaxe padrão do SQL. Um filtro com parâmetros inclui uma chamada para a função de sistema **HOST_NAME ()** e/ou **suser_sname ()**, ou uma função definida pelo usuário que faz referência a uma ou ambas as funções. A seguir há um exemplo de uma cláusula de filtro completa para um filtro de linha com parâmetros:  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         A cláusula WHERE deve usar nomeação de duas partes; nomeação de três partes e nomeação de quatro partes não são suportadas.  
  
4.  Selecione a opção que corresponde ao modo em que os dados serão compartilhados entre Assinantes:  
  
    -   **Uma linha dessa tabela irá para múltiplas assinaturas**  
  
    -   **Uma linha dessa tabela irá para apenas uma assinatura**  
  
     Se você selecionar **Uma linha desta tabela irá para apenas uma assinatura**, a replicação de mesclagem pode otimizar o desempenho armazenando e processando uma quantia menor de metadados. No entanto, será necessário certificar-se de que os dados são particionados de forma que uma linha não seja replicada em mais de um Assinante. Para obter mais informações, consulte a seção "Configurando opções de partição" no tópico [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### Para modificar um filtro de linha com parâmetros  
  
1.  No **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>**, selecione um filtro no **tabelas filtradas** painel e, em seguida, clique **Editar**.  
  
2.  Na caixa de diálogo **Editar Filtro** , modifique o filtro.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para excluir um filtro de linha com parâmetros  
  
1.  No **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>**, selecione um filtro no **tabelas filtradas** painel e, em seguida, clique **Excluir**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Os filtros de linha com parâmetros podem ser criados e modificados de forma programada, usando os procedimentos de replicação armazenados.  
  
#### Para definir um filtro de linha com parâmetros para um artigo em uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique **@publication**, um nome para o artigo para **@article**, a tabela que está sendo publicado para **@source_object**, a cláusula WHERE que define o filtro parametrizado para **@subset_filterclause** (não incluindo `WHERE`), e um dos seguintes valores para **@partition_options**, que descreve o tipo de particionamento que resultará do filtro de linha com parâmetros:  
  
    -   **0** - a filtragem do artigo ou é estática ou não produz um único subconjunto de dados para cada partição (uma partição "sobreposta").  
  
    -   **1** - partições resultantes são sobrepostas e as atualizações feitas no assinante não podem alterar a partição à qual pertence uma linha.  
  
    -   **2** - filtragem do artigo gera partições não sobrepostas, mas vários assinantes podem receber a mesma partição.  
  
    -   **3** - a filtragem para as artigo gera partições não sobrepostas exclusivas de cada assinatura.  
  
#### Para alterar um filtro de linha com parâmetros para um artigo em uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique **@publication**, **@article**, um valor de **subset_filterclause** para **@property**, a expressão que define o filtro parametrizado para **@value** (não incluindo `WHERE`) e um valor de **1** para ambos **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
2.  Se essa alteração resulta em comportamento de particionamento diferente, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) novamente. Especifique **@publication**, **@article**, um valor de **partition_options** para **@property**, e a opção de particionamento mais adequada para **@value**, que pode ser um dos seguintes:  
  
    -   **0** - a filtragem do artigo ou é estática ou não produz um único subconjunto de dados para cada partição (uma partição "sobreposta").  
  
    -   **1** - partições resultantes são sobrepostas e as atualizações feitas no assinante não podem alterar a partição à qual pertence uma linha.  
  
    -   **2** - filtragem do artigo gera partições não sobrepostas, mas vários assinantes podem receber a mesma partição.  
  
    -   **3** - a filtragem para as artigo gera partições não sobrepostas exclusivas de cada assinatura.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Este exemplo define um grupo de artigos em uma publicação de mesclagem onde os artigos são filtrados por uma série de filtros de junção em relação a `Employee` tabela por sua vez filtrada usando um filtro de linha com parâmetros sobre o **LoginID** coluna. Durante a sincronização, o valor retornado pelo [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) função é substituída. Para obter mais informações, consulte substituindo o valor HOST_NAME () no tópico [filtros de linha com parâmetros](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-para_1.sql)]  
  
## Consulte também  
 [Definir e modificar um filtro de junção entre artigos de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtros de junção](../../../relational-databases/replication/merge/join-filters.md)   
 [Filtros de linha com parâmetros](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  
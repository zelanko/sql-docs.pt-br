---
title: Definir e modificar um filtro de linha parametrizado para um artigo de mesclagem | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameterized filters [SQL Server replication], defining
- parameterized filters [SQL Server replication], modifying
- merge replication [SQL Server replication], dynamic filters
- merge replication parameterized filters [SQL Server replication]
- filters [SQL Server replication], parameterized
- modifying filters, parameterized row
- dynamic filters [SQL Server replication]
ms.assetid: de0482a2-3cc8-4030-8a4a-14364549ac9f
caps.latest.revision: "44"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1bf6db754bdc9e0bfb9e43578ebf54cee13e082
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="define-and-modify-a-parameterized-row-filter-for-a-merge-article"></a>Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como definir e modificar um filtro de linha com parâmetros no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Ao criar artigos de tabela, você pode usar filtros de linha com parâmetros. Esses filtros usam uma cláusula [WHERE](../../../t-sql/queries/where-transact-sql.md) para selecionar os dados apropriados para serem publicados. Em vez de especificar um valor literal na cláusula (como você faria com um filtro de linha estático) você indica uma ou mais das seguintes funções do sistema: [SUSER_SNAME](../../../t-sql/functions/suser-sname-transact-sql.md) e [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md). Para obter mais informações, consulte [Filtros de linha com parâmetros](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para definir e modificar um filtro de linha com parâmetros, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se você adicionar, modificar ou excluir um filtro de linha com parâmetros após a inicialização de assinaturas na publicação, será preciso gerar um novo instantâneo e reinicializar todas as assinaturas depois de fazer a alteração. Para obter mais informações sobre os requisitos para alterações de propriedades, consulte [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Por motivos de desempenho, recomendamos que não sejam aplicadas funções a nomes de colunas em cláusulas de filtro de linha com parâmetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Se você usar HOST_NAME em uma cláusula de filtro e substituir o valor HOST_NAME, talvez precise converter tipos de dados usando CONVERT. Para obter mais informações sobre práticas recomendadas para esse caso, consulte a seção "Substituindo o valor de HOST_NAME()" no tópico [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Defina, modifique e exclua filtros de linhas com parâmetros na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-define-a-parameterized-row-filter"></a>Para definir um filtro de linha com parâmetros  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar linhas** de **Propriedades da publicação – \<Publicação>**, clique em **Adicionar** e clique em **Adicionar Filtro**.  
  
2.  Na caixa de diálogo **Adicionar Filtro** , selecione uma tabela para filtrar na caixa de listagem suspensa.  
  
3.  Crie uma instrução de filtro na caixa de texto **Instrução de filtro** . Você pode digitar diretamente na área de texto e também pode arrastar e soltar colunas da caixa de listagem **Colunas** .  
  
    -   A área de texto **Instrução de filtro** inclui o texto padrão que está no formato de:  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
    -   O texto padrão não pode ser alterado; digite a cláusula de filtro depois da palavra-chave WHERE usando sintaxe padrão do SQL. Um filtro com parâmetros inclui uma chamada para a função de sistema **HOST_NAME()** e/ou **SUSER_SNAME()**, ou uma função definida pelo usuário que referencie uma ou ambas as funções. A seguir há um exemplo de uma cláusula de filtro completa para um filtro de linha com parâmetros:  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         A cláusula WHERE deve usar nomeação de duas partes; nomeação de três partes e nomeação de quatro partes não são suportadas.  
  
4.  Selecione a opção que corresponde ao modo em que os dados serão compartilhados entre Assinantes:  
  
    -   **Uma linha dessa tabela irá para múltiplas assinaturas**  
  
    -   **Uma linha dessa tabela irá para apenas uma assinatura**  
  
     Se você selecionar **Uma linha desta tabela irá para apenas uma assinatura**, a replicação de mesclagem pode otimizar o desempenho armazenando e processando uma quantia menor de metadados. No entanto, será necessário certificar-se de que os dados são particionados de forma que uma linha não seja replicada em mais de um Assinante. Para obter mais informações, consulte a seção "Configurando opções de partição" no tópico [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>**, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### <a name="to-modify-a-parameterized-row-filter"></a>Para modificar um filtro de linha com parâmetros  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** de **Propriedades da Publicação – \<Publicação>**, selecione um filtro no painel **Tabelas Filtradas** e clique em **Editar**.  
  
2.  Na caixa de diálogo **Editar Filtro** , modifique o filtro.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-parameterized-row-filter"></a>Para excluir um filtro de linha com parâmetros  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** de **Propriedades da Publicação – \<Publicação>**, selecione um filtro no painel **Tabelas Filtradas** e clique em **Excluir**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Os filtros de linha com parâmetros podem ser criados e modificados de forma programada, usando os procedimentos de replicação armazenados.  
  
#### <a name="to-define-a-parameterized-row-filter-for-an-article-in-a-merge-publication"></a>Para definir um filtro de linha com parâmetros para um artigo em uma publicação de mesclagem  
  
1.  No Publicador no banco de dados de publicação, execute o [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique **@publication**, um nome de artigo para **@article**, a tabela sendo publicada para **@source_object**, a cláusula WHERE que define o filtro com parâmetros como **@subset_filterclause** (não incluindo `WHERE`) e um dos valores a seguir para **@partition_options**, que descreve o tipo de particionamento que resultará do filtro de linha com parâmetros:  
  
    -   **0** - A filtragem para o artigo ou é estática ou não gera um único subconjunto de dados para cada partição (uma partição “sobreposta”).  
  
    -   **1** = As partições resultantes são sobrepostas e as atualizações realizadas no Assinante não podem alterar a partição à qual uma linha pertence.  
  
    -   **2** - A filtragem para o artigo gera partições não sobrepostas, mas vários Assinantes podem receber a mesma partição.  
  
    -   **3** = A filtragem para o artigo gera partições não sobrepostas que são exclusivas para cada assinatura.  
  
#### <a name="to-change-a-parameterized-row-filter-for-an-article-in-a-merge-publication"></a>Para alterar um filtro de linha com parâmetros para um artigo em uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique **@publication**, **@article**, um valor de **subset_filterclause** para **@property**, a expressão que define o filtro com parâmetros como **@value** (não incluindo `WHERE`) e um valor de **1** para ambos, **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
2.  Se esta alteração resultar em um comportamento de particionamento diferente, execute então [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) novamente. Especifique **@publication**, **@article**, um valor de **partition_options** para **@property**e a opção de particionamento mais adequada para **@value**, que pode ser uma das seguintes:  
  
    -   **0** - A filtragem para o artigo ou é estática ou não gera um único subconjunto de dados para cada partição (uma partição “sobreposta”).  
  
    -   **1** = As partições resultantes são sobrepostas e as atualizações realizadas no Assinante não podem alterar a partição à qual uma linha pertence.  
  
    -   **2** - A filtragem para o artigo gera partições não sobrepostas, mas vários Assinantes podem receber a mesma partição.  
  
    -   **3** = A filtragem para o artigo gera partições não sobrepostas que são exclusivas para cada assinatura.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Esse exemplo define um grupo de artigos em uma publicação de mesclagem onde os artigos são filtrados por uma série de filtros de junção em relação à tabela `Employee` que, por sua vez, é filtrada usando um filtro de linha com parâmetros na coluna **LoginID** . Durante a sincronização, o valor retornado pela função [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) é substituído. Para obter mais informações, consulte Substituindo o valor do HOST_NAME () no tópico [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-para_1.sql)]  
  
## <a name="see-also"></a>Consulte também  
 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtros de junção](../../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  

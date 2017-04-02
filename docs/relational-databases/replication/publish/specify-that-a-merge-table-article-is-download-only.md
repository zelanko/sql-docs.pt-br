---
title: "Especificar que um novo artigo de tabela de mesclagem &#233; somente download | Microsoft Docs"
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
  - "replicação de mesclagem [replicação do SQL Server], artigos somente para download"
  - "artigos [replicação do SQL Server], somente para download"
  - "artigos de somente download"
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Especificar que um novo artigo de tabela de mesclagem &#233; somente download
  Este tópico descreve como especificar que um artigo de tabela de mesclagem é somente para download [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Artigos de somente download são projetados para aplicativos com dados que não são atualizados nos Assinantes. Para obter mais informações, consulte [otimizar o desempenho de replicação de mesclagem com artigos Download-Only](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para especificar que um artigo de tabela de mesclagem é somente download, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se você especificar que um artigo é somente download, após a inicialização das assinaturas, todas as assinaturas de clientes que receberem o artigo deverão ser reincializadas. As assinaturas de servidor não têm que ser reinicializadas. Para obter mais informações sobre os efeitos de alterações de propriedade, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especificar que um artigo é somente download no **artigos** página do Assistente de nova publicação ou o **propriedades** guia o **Propriedades do artigo - \< artigo>** caixa de diálogo. Essa caixa de diálogo está disponível no Assistente de nova publicação e o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar que um artigo seja somente download na página Artigos  
  
-   Sobre o **artigos** página do novo Assistente de publicação, selecione uma tabela e, em seguida, selecione a caixa de seleção **tabela realçada é somente download**.  
  
#### Para especificar que um artigo é somente download na guia Propriedades das propriedades do artigo - \< artigo> caixa de diálogo  
  
1.  Sobre o **artigos** página do Assistente de nova publicação ou o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione uma tabela e, em seguida, clique em **Propriedades do artigo**.  
  
2.  Clique em **Definir Propriedades do Artigo Realçado na Tabela** ou **Definir as Propriedades de Todos os Artigos de Tabela**.  
  
3.  No **objeto de destino** seção o **propriedades** Guia do **Propriedades do artigo - \< artigo>** caixa de diálogo, especifique um dos valores a seguir para **direção de sincronização**:  
  
    -   **Download para Assinante, proibir alterações do Assinante**  
  
    -   **Download para Assinante, permitir alterações do Assinante**  
  
4.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para especificar que um novo artigo de tabela de mesclagem é somente download  
  
1.  Executar [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), especificando um valor de **1** ou **2** para o parâmetro **@subscriber_upload_options**. Os números correspondem ao seguinte comportamento:  
  
    -   **0** -nenhuma restrição (padrão). As alterações feitas no Assinante são carregadas no Publicador.  
  
    -   **1** - as alterações são permitidas no assinante, mas não são carregadas no publicador.  
  
    -   **2** -não são permitidas alterações no assinante.  
  
        > [!NOTE]  
        >  Se a tabela de origem para um artigo já estiver publicada em outra publicação, o valor de **@subscriber_upload_options** deve ser o mesmo para os dois artigos.  
  
#### Para modificar um artigo de tabela de mesclagem existente para que seja de somente download  
  
1.  Para determinar se um artigo é somente download, execute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Observe o valor de **upload_options** para o artigo no resultado definido.  
  
2.  Se o valor retornado na etapa 1 é **0**, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando um valor de **subscriber_upload_options** para **@property**, um valor de **1** para **@force_invalidate_snapshot** e **@force_reinit_subscription**, e um valor de **1** ou **2** para **@value**, que corresponde ao seguinte comportamento:  
  
    -   **1** - as alterações são permitidas no assinante, mas não são carregadas no publicador.  
  
    -   **2** -não são permitidas alterações no assinante.  
  
        > [!NOTE]  
        >  Se a tabela de origem para um artigo já estiver publicada em outra publicação, o comportamento de somente download deve ser o mesmo para os dois artigos.  
  
## Consulte também  
 [Otimizar o desempenho de replicação de mesclagem com artigos de somente download](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Defina um Artigo](../../../relational-databases/replication/publish/define-an-article.md)   
 [Visualizar e modificar propriedades de artigos](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  
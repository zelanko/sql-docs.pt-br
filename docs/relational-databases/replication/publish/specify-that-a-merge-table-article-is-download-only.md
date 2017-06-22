---
title: "Especificar que um artigo de tabela de mesclagem é somente de download | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 83d7383aff0ccc5ab8f6716135d07c3642e6c9d6
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="specify-that-a-merge-table-article-is-download-only"></a>Especificar que um novo artigo de tabela de mesclagem é somente download
  Este tópico descreve como especificar que um artigo de tabela de mesclagem é somente para download [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Artigos de somente download são projetados para aplicativos com dados que não são atualizados nos Assinantes. Para obter mais informações, consulte [Optimize Merge Replication Performance with Download-Only Articles](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md) (Otimizar o desempenho da replicação de mesclagem com artigos somente para download).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para especificar que um artigo de tabela de mesclagem é somente download, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se você especificar que um artigo é somente download, após a inicialização das assinaturas, todas as assinaturas de clientes que receberem o artigo deverão ser reincializadas. As assinaturas de servidor não têm que ser reinicializadas. Para obter mais informações sobre os efeitos das alterações de propriedades, consulte [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especifique que um artigo seja somente para download na página **Artigos** do Assistente para Nova Publicação ou na guia **Propriedades** da caixa de diálogo **Propriedades do Artigo – \<Artigo>**. Essa caixa de diálogo está disponível no Assistente para Nova Publicação e na caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-articles-page"></a>Para especificar que um artigo seja somente download na página Artigos  
  
-   Na página **Artigos** do Assistente para Nova Publicação, selecione uma tabela, depois marque a caixa de seleção **A tabela realçada é somente para download**.  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-properties-tab-of-the-article-properties---article-dialog-box"></a>Para especificar que um artigo seja somente para download na guia Propriedades da caixa de diálogo Propriedades de Artigo – \<Artigo>  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades da Publicação – \<Publicação>**, selecione uma tabela e clique em **Propriedades do Artigo**.  
  
2.  Clique em **Definir Propriedades do Artigo Realçado na Tabela** ou **Definir as Propriedades de Todos os Artigos de Tabela**.  
  
3.  Na seção **Objeto de Destino** da guia **Propriedades** da caixa de diálogo **Propriedades do Artigo – \<Artigo>**, especifique um dos valores a seguir para **Direção de sincronização**:  
  
    -   **Download para Assinante, proibir alterações do Assinante**  
  
    -   **Download para Assinante, permitir alterações do Assinante**  
  
4.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>**, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-specify-that-a-new-merge-table-article-is-download-only"></a>Para especificar que um novo artigo de tabela de mesclagem é somente download  
  
1.  Execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), enquanto especificando um valor de **1** ou **2** para o parâmetro **@subscriber_upload_options**. Os números correspondem ao seguinte comportamento:  
  
    -   **0** - Nenhuma restrição (padrão). As alterações feitas no Assinante são carregadas no Publicador.  
  
    -   **1** - As alterações são permitidas no Assinante, mas não são carregadas no Publicador.  
  
    -   **2** - As alterações não são permitidas no Assinante.  
  
        > [!NOTE]  
        >  Se a tabela de origem para um artigo já estiver publicada em outra publicação, o valor de **@subscriber_upload_options** deve ser o mesmo para os dois artigos.  
  
#### <a name="to-modify-an-existing-merge-table-article-to-be-download-only"></a>Para modificar um artigo de tabela de mesclagem existente para que seja de somente download  
  
1.  Para determinar se um artigo é de somente download, execute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Observe o valor de **upload_options** para o artigo no conjunto de resultados.  
  
2.  Se o valor retornado na etapa 1 for **0**, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), enquanto especificando um valor de **subscriber_upload_options** para **@property**, um valor de **1** para **@force_invalidate_snapshot** e **@force_reinit_subscription**, e um valor de **1** ou **2** para **@value**, o que corresponde ao seguinte comportamento.:  
  
    -   **1** - As alterações são permitidas no Assinante, mas não são carregadas no Publicador.  
  
    -   **2** - As alterações não são permitidas no Assinante.  
  
        > [!NOTE]  
        >  Se a tabela de origem para um artigo já estiver publicada em outra publicação, o comportamento de somente download deve ser o mesmo para os dois artigos.  
  
## <a name="see-also"></a>Consulte também  
 [Otimizar o desempenho da replicação de mesclagem com artigos de somente download](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [Exibir e modificar as propriedades do artigo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  

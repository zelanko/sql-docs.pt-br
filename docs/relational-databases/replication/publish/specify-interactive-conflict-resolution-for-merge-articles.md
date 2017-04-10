---
title: "Especificar a resolu&#231;&#227;o interativa de conflitos para artigos de mesclagem | Microsoft Docs"
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
  - "resolução de conflitos de replicação de mesclagem [replicação do SQL Server], resolvedores interativos"
  - "resolução interativa de conflitos [replicação do SQL Server]"
  - "artigos [replicação do SQL Server], resolução de conflitos"
  - "resolução de conflitos [replicação do SQL Server], replicação de mesclagem"
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Especificar a resolu&#231;&#227;o interativa de conflitos para artigos de mesclagem
  Este tópico descreve como especificar a resolução interativa de conflitos para artigos de mesclagem no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a replicação fornece um resolvedor interativo, que permite que você resolva conflitos manualmente durante a sincronização sob demanda [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Gerenciador de sincronização do Windows. Depois que a resolução interativa estiver habilitada, resolva os conflitos interativamente durante a sincronização, usando o Resolvedor Interativo. O Resolvedor Interativo está disponível pelo Gerenciador de Sincronização do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Para obter mais informações, consulte [sincronizar uma assinatura usando Windows sincronização Manager & #40. O Gerenciador de sincronização do Windows & 41;](../../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para especificar a resolução interativa de conflitos para artigos de mesclagem, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Se uma sincronização for executada fora do Gerenciador de Sincronização do Windows (como sincronização agendada ou uma sincronização sob demanda no SQL Server Management Studio ou no Replication Monitor), os conflitos serão resolvidos automaticamente sem a intervenção de usuário, usando a resolução de conflitos padrão especificada para o artigo. Para obter mais informações, confira [Interactive Conflict Resolution](../../../relational-databases/replication/merge/interactive-conflict-resolution.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para habilitar a resolução interativa de conflito para um artigo  
  
1.  Sobre o **artigos** página do Assistente de nova publicação ou o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione uma tabela. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
2.  Clique em **Propriedades de Artigos**e então clique em **Definir Propriedades do Artigo Realçado da Tabela** ou **Definir Propriedades de Todos os Artigos da Tabela**.  
  
3.  Sobre o **Propriedades do artigo - \< artigo>** ou **Propriedades do artigo - \< ArticleType>** clique no **resolvedor** guia.  
  
4.  Selecione **Permitir que o assinante Resolva conflitos interativamente durante a sincronização sob demanda**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### Para especificar que uma assinatura deve usar a resolução interativa de conflito  
  
1.  No **Propriedades de assinatura - \< assinante>: \< Banco_de_dados_de_assinatura>** caixa de diálogo, especifique um valor de **True** para o **resolver conflitos interativamente** opção. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 É possível especificar de forma programada se um Assinante usará essa interface gráfica para resolver conflitos de artigos quando uma assinatura pull para uma publicação de mesclagem é criada. Só conflitos em artigos que têm suporte para esta opção serão exibidos no Resolvedor Interativo.  
  
#### Para criar uma assinatura pull de mesclagem que usa o Resolvedor Interativo  
  
1.  No publicador do banco de dados de publicação, execute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando **@publication**. Observe o valor de **allow_interactive_resolver** para cada artigo no conjunto de resultados para que o resolvedor interativo será usado.  
  
    -   Se este valor for **1**, o Resolver Interativo será usado.  
  
    -   Se este valor for **0**, você deverá primeiro habilitar o Resolvedor Interativo de cada artigo. Para fazer isso, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **@publication**, **@article**, um valor de **allow_interactive_resolver** para **@property**, e um valor de **true** para **@value**.  
  
2.  No assinante no banco de dados de assinatura, execute [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Para obter mais informações, confira [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  No assinante no banco de dados de assinatura, execute [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md), especificando os seguintes parâmetros:  
  
    -   **@publisher**, **@publisher_db** (banco de dados publicado), e **@publication**.  
  
    -   Um valor de **true** para **@enabled_for_syncmgr**.  
  
    -   Um valor de **true** para **@use_interactive_resolver**.  
  
    -   As informações da conta de segurança requerida pelo Merge Agent. Para obter mais informações, confira [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
4.  No publicador do banco de dados de publicação, execute [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md).  
  
#### Para definir um artigo que tem suporte para o Resolvedor Interativo  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication**, um nome para o artigo para **@article**, o objeto de banco de dados que está sendo publicado para **@source_object**, e um valor de **true** para **@allow_interactive_resolver**. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## Consulte também  
 [Exibir e resolver conflitos de dados para publicações de mesclagem e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/view and resolve data conflicts for merge publications.md)   
 [Resolução de conflito interativo](../../../relational-databases/replication/merge/interactive-conflict-resolution.md)  
  
  
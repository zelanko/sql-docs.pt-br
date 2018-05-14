---
title: Especificar a resolução interativa de conflitos para artigos de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], interactive resolvers
- interactive conflict resolution [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
caps.latest.revision: 40
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 96e7a808a52e72aea320726f3e56761213d800b1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="specify-interactive-conflict-resolution-for-merge-articles"></a>Especificar a resolução interativa de conflitos para artigos de mesclagem
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como especificar a resolução interativa de conflitos para artigos de mesclagem no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 A replicação do[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece um Resolvedor Interativo, que permite a resolução de conflitos de forma manual durante a sincronização sob demanda no Gerenciador de Sincronização do Windows da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] . Depois que a resolução interativa estiver habilitada, resolva os conflitos interativamente durante a sincronização, usando o Resolvedor Interativo. O Resolvedor Interativo está disponível pelo Gerenciador de Sincronização do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Para obter mais informações, consulte [Como sincronizar uma assinatura usando o Gerenciador de Sincronização do Windows &#40;Gerenciador de Sincronização do Windows&#41;](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para especificar a resolução interativa de conflitos para artigos de mesclagem, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Se uma sincronização for executada fora do Gerenciador de Sincronização do Windows (como sincronização agendada ou uma sincronização sob demanda no SQL Server Management Studio ou no Replication Monitor), os conflitos serão resolvidos automaticamente sem a intervenção de usuário, usando a resolução de conflitos padrão especificada para o artigo. Para obter mais informações, confira [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-enable-interactive-conflict-resolution-for-an-article"></a>Para habilitar a resolução interativa de conflito para um artigo  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades de Publicação – \<Publicação>**, selecione uma tabela. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
2.  Clique em **Propriedades de Artigos**e então clique em **Definir Propriedades do Artigo Realçado da Tabela** ou **Definir Propriedades de Todos os Artigos da Tabela**.  
  
3.  Na página **Propriedades do Artigo – \<Artigo>** ou **Propriedades do Artigo – \<ArticleType>**, clique na guia **Resolvedor**.  
  
4.  Selecione **Permitir que o Assinante resolva conflitos interativamente durante a sincronização sob demanda**  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>**, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### <a name="to-specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>Para especificar que uma assinatura deve usar a resolução interativa de conflito  
  
1.  Na caixa de diálogo **Propriedades da Assinatura – \<Subscriber>: \<SubscriptionDatabase>**, especifique o valor **Verdadeiro** para a opção **Resolver os conflitos interativamente**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 É possível especificar de forma programada se um Assinante usará essa interface gráfica para resolver conflitos de artigos quando uma assinatura pull para uma publicação de mesclagem é criada. Só conflitos em artigos que têm suporte para esta opção serão exibidos no Resolvedor Interativo.  
  
#### <a name="to-create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>Para criar uma assinatura pull de mesclagem que usa o Resolvedor Interativo  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando **@publication**. Anote o valor de **allow_interactive_resolver** para cada artigo no conjunto de resultados para o qual o Resolvedor Interativo será usado.  
  
    -   Se este valor for **1**, o Resolver Interativo será usado.  
  
    -   Se este valor for **0**, você deverá primeiro habilitar o Resolvedor Interativo de cada artigo. Para tanto, execute o [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **@publication**, **@article**, um valor de **allow_interactive_resolver** para **@property**, e um valor de **true** para **@value**.  
  
2.  No Assinante, no banco de dados de assinatura, execute o [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Para obter mais informações, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  No Publicador do banco de dados de assinatura, execute o [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md), especificando os seguintes parâmetros:  
  
    -   **@publisher**, **@publisher_db** (o banco de dados publicado), e **@publication**.  
  
    -   Um valor de **true** para **@enabled_for_syncmgr**.  
  
    -   Um valor de **true** para **@use_interactive_resolver**.  
  
    -   As informações da conta de segurança requerida pelo Merge Agent. Para obter mais informações, confira [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
4.  No Publicador, no banco de dados da publicação, execute [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md).  
  
#### <a name="to-define-an-article-that-supports-the-interactive-resolver"></a>Para definir um artigo que tem suporte para o Resolvedor Interativo  
  
1.  No Publicador do banco de dados de publicação, execute o [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence, para **@publication**; um nome para o artigo para **@article**, um objeto de banco de dados sendo publicado para **@source_object**, e um valor de **true** para **@allow_interactive_resolver**. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e resolver conflitos de dados em publicações de mesclagem &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
  

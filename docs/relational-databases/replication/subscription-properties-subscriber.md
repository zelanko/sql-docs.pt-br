---
title: "Propriedades da Assinatura - Assinante | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.subproperties.subscriber.f1"
helpviewer_keywords: 
  - "caixa de diálogo Propriedades da Assinatura"
ms.assetid: bef66929-3234-4a45-8ec4-3b271519d07a
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Propriedades da Assinatura - Assinante
  O **Propriedades de assinatura** caixa de diálogo no assinante permite exibir e definir propriedades para assinaturas pull.  
  
 Cada propriedade no **Propriedades de assinatura** caixa de diálogo inclui uma descrição. Clique em uma propriedade para ver sua descrição exibida na parte inferior da caixa de diálogo. Este tópico fornece informações adicionais sobre várias propriedades. As propriedades são agrupadas nas categorias seguintes:  
  
-   Propriedades que se aplicam a todas as assinaturas.  
  
-   Propriedades que se aplicam a assinaturas transacionais.  
  
-   Propriedades que se aplicam a assinaturas de mesclagem.  
  
 Se uma opção for exibida como somente leitura, só poderá ser definida quando a assinatura for criada. Se você quiser definir opções que não estão disponíveis no Assistente para Nova Assinatura, crie a assinatura com procedimentos armazenados. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) e [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
> [!NOTE]  
>  Se um trabalho do Distribution Agent ou Merge Agent ainda não foi criado para a Assinatura, muitas propriedades de assinatura são exibidas agora. Para criar um trabalho do agente para uma assinatura pull, Execute [sp_addpullsubscription_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) (para uma assinatura para uma publicação de instantâneo ou transacional) ou [sp_addmergepullsubscription_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) (para uma assinatura para uma publicação de mesclagem).  
  
## Opções para todas as assinaturas  
 **Inicializar os dados publicados a partir de um instantâneo**  
 Determina se as assinaturas são iniciadas com um instantâneo (o padrão) ou por outro método. Para obter mais informações sobre inicialização de assinaturas, consulte [inicializar uma assinatura](../../relational-databases/replication/initialize-a-subscription.md).  
  
 **Local do Instantâneo**  
 Determina o local do qual são acessados arquivos de instantâneo durante inicialização ou reinicialização. O local pode ser um dos seguintes valores:  
  
-   **Local padrão**: o local padrão, que é definido ao configurar um distribuidor. Para obter mais informações, consulte [especificar o local do instantâneo padrão & #40. SQL Server Management Studio e 41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md).  
  
-   **Pasta alternativa**: um local alternativo, que pode ser especificado no **Propriedades de publicação** caixa de diálogo. Para obter mais informações, consulte [locais de pasta de instantâneo alternativo](../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
-   **Pasta de instantâneo dinâmico**: um local de instantâneo para publicações de mesclagem que usam filtros de linha com parâmetros. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
-   **Pasta FTP**: uma pasta acessível a um servidor de protocolo de transferência de arquivo (FTP). Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
 **Pasta do instantâneo**  
 Se você selecionar qualquer valor diferente de **local padrão** para o **local de instantâneo** opção, você deve especificar um caminho para a pasta de instantâneo.  
  
 **Usar o Gerenciador de Sincronização do Windows**  
 Determina se essa assinatura pode ser sincronizada usando o Gerenciador de Sincronização do Windows da [!INCLUDE[msCoName](../../includes/msconame-md.md)]   
  
 **Segurança**  
 Clique o **conta de processo do agente** linha e, em seguida, clique no botão Propriedades (**...**) para alterar a conta na qual o Distribution Agent ou do Merge Agent é executado no assinante. As opções de segurança relacionadas a conexões dependem do tipo de assinatura:  
  
-   Para assinaturas em uma publicação transacional: para alterar a conta sob a qual o Distribution Agent faz conexões com o distribuidor, clique **conexão do distribuidor**, e, em seguida, clique no botão Propriedades (**...**).  
  
-   Para assinaturas de atualização imediata para uma publicação transacional: além da conexão do distribuidor descrita acima, você pode alterar o método usado para propagar alterações do assinante para o publicador: clique **conexão do publicador**, e, em seguida, clique no botão Propriedades (**...**).  
  
-   Para assinaturas para publicações de mesclagem, clique em **conexão do publicador**, e, em seguida, clique no botão Propriedades (**...**).  
  
 Para obter mais informações sobre as permissões necessárias para cada agente, consulte [modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Opções para assinaturas transacionais  
 **Assinatura atualizável**  
 Determina se as alterações do Assinante serão replicadas de volta no Publicador. As alterações podem ser replicadas usando atualização enfileirada ou imediata. A opção **método de atualização do assinante** determina qual método usar. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## Opções para assinaturas de mesclagem  
 **Definição de partição (HOST_NAME)**  
 Para uma publicação que usa filtros com parâmetros, a replicação de mesclagem avalia uma das duas funções de sistema (ou ambas, se as referências de filtro ambas as funções) durante a sincronização para determinar os dados que um assinante deve receber: **suser_sname ()** ou **HOST_NAME ()**. Por padrão, **HOST_NAME ()** retorna o nome do computador no qual o Merge Agent está em execução, mas você pode substituir esse valor no novo Assistente de assinatura. Para obter mais informações sobre filtros parametrizados e substituindo **HOST_NAME ()**, consulte [filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **Tipo de assinatura** e **prioridade**  
 Exibe se a assinatura é uma assinatura de cliente ou servidor (isso não pode ser alterado depois que a assinatura tiver sido criada). Assinaturas de Servidor podem republicar dados para outros Assinantes e podem ter atribuição de prioridade para resolução de conflito.  
  
 Se você selecionou um tipo de assinatura de servidor no Assistente para Nova Assinatura, o Assinante receberá uma prioridade que será usada durante resolução de conflito  
  
 **Resolver conflitos interativamente**  
 Determina se o Resolver Interativo deve usar a interface do usuário para resolver conflitos durante a sincronização de mesclagem. Isso requer um valor de **Habilitar** para **Gerenciador de sincronização do Windows Use**. Para obter mais informações, confira [Interactive Conflict Resolution](../../relational-databases/replication/merge/interactive-conflict-resolution.md).  
  
 **Sincronização da Web**  
 **Usar sincronização da Web** determina se conectem a um [!INCLUDE[msCoName](../../includes/msconame-md.md)] servidor de serviços de informações da Internet (IIS) para sincronizar a assinatura. Essa opção só estará disponível se a publicação estiver habilitada para sincronização da Web. Para obter mais informações, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Se você selecionar **True** para **usar sincronização da Web**:  
  
-   Digite o endereço completo para o servidor IIS em **endereço de servidor da Web**.  
  
-   Clique a **conexão do servidor Web** linha e, em seguida, clique no botão Propriedades (**...**) para definir ou alterar a conta sob a qual o assinante se conecta ao servidor IIS.  
  
-   Alterar **tempo limite do servidor Web** se necessário. O tempo limite é o período de tempo, em segundos, antes que uma solicitação de sincronização da Web expire.  
  
 Para obter mais informações sobre configuração, consulte [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## Consulte também  
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
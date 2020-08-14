---
title: Caixa de diálogo Propriedades da Assinatura
description: Descreve a caixa de diálogo 'Propriedades da Assinatura' do SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.subproperties.publisher.f1
- sql13.rep.newsubwizard.subproperties.subscriber.f1
ms.assetid: db2be511-c76e-4f21-8be4-6a8c60a50d30
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 7b1338f4e935a2c7e8662a09aacff1cc4b7df9d3
ms.sourcegitcommit: 822d4b3cfa53269535500a3db5877a82b5076728
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87988809"
---
# <a name="sql-server-replication-subscription-properties-dialog-box"></a>Caixa de diálogo Propriedades de Assinatura de Replicação do SQL Server 
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]

### <a name="publisher-properties"></a>Propriedades do publicador
A caixa de diálogo **Propriedades da Assinatura** no Publicador permite exibir e definir propriedades para assinaturas push. Você também pode exibir algumas propriedades de assinaturas pull, mas a caixa de diálogo **Propriedades da Assinatura** no Assinante exibe propriedades adicionais e permite que elas sejam modificadas.  
  
 Cada propriedade na caixa de diálogo **Propriedades da Assinatura** inclui uma descrição. Clique em uma propriedade para ver sua descrição exibida na parte inferior da caixa de diálogo. Esse tópico fornece informações adicionais sobre várias propriedades, muitas das quais são exibidas no Publicador somente para assinaturas push. As propriedades são agrupadas nas categorias seguintes:  
  
-   Propriedades que se aplicam a todas as assinaturas.    
-   Propriedades que se aplicam a assinaturas transacionais.  
-   Propriedades que se aplicam a assinaturas de mesclagem.  
  
 Se uma opção for exibida como somente leitura, só poderá ser definida quando a assinatura for criada. Se você quiser definir opções que não estão disponíveis no Assistente para Nova Assinatura, crie a assinatura com procedimentos armazenados. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) e [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  

### <a name="subscriber-properties"></a>Propriedades do assinante
A caixa de diálogo **Propriedades da Assinatura** no Assinante permite exibir e definir propriedades para assinaturas pull.  
  
 Cada propriedade na caixa de diálogo **Propriedades da Assinatura** inclui uma descrição. Clique em uma propriedade para ver sua descrição exibida na parte inferior da caixa de diálogo. Este tópico fornece informações adicionais sobre várias propriedades. As propriedades são agrupadas nas categorias seguintes:    
-   Propriedades que se aplicam a todas as assinaturas.    
-   Propriedades que se aplicam a assinaturas transacionais.   
-   Propriedades que se aplicam a assinaturas de mesclagem.  
  
 Se uma opção for exibida como somente leitura, só poderá ser definida quando a assinatura for criada. Se você quiser definir opções que não estão disponíveis no Assistente para Nova Assinatura, crie a assinatura com procedimentos armazenados. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) e [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
> [!NOTE]  
>  - Se um trabalho do Distribution Agent ou Merge Agent ainda não foi criado para a Assinatura, muitas propriedades de assinatura são exibidas agora. Para criar um trabalho de agente para uma assinatura pull, execute [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) (para uma assinatura de publicação transacional ou de instantâneo) ou [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) (para uma assinatura de publicação de mesclagem).  
> - Os bancos de dados da Instância Gerenciada de SQL do Azure podem ser um publicador, um distribuidor e um assinante para a replicação transacional e de instantâneo. Os bancos de dados do Banco de Dados SQL do Azure só podem ser assinantes por push para a replicação transacional e de instantâneo. Para obter mais informações, consulte [Replicação transacional com o Banco de Dados SQL do Azure](/azure/sql-database/sql-database-managed-instance-transactional-replication). 
  
## <a name="publisher-options-for-all-subscriptions"></a>Opções do editor para todas as assinaturas  
 **Segurança**  
 Clique na linha **Conta de processo de agente** e, depois, clique no botão de propriedades ( **...** ) para alterar a conta na qual o Distribution Agent ou Merge Agent são executados no Distribuidor. Para alterar a conta na qual o Distribution Agent ou Merge Agent fazem conexões com o Assinante, clique em **Conexão do Assinante**e, depois, clique no botão de propriedades ( **...** ).  
  
 Para obter mais informações sobre as permissões exigidas para cada agente, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="publisher-options-for-transactional-subscriptions"></a>Opções do editor para assinaturas transacionais  
 **Evitar loop de transação**  
 Determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante: Essa opção é usada para replicação transacional bidirecional. Para obter mais informações, consulte [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).  
  
 **Assinatura atualizável**  
 Determina se as alterações do Assinante serão replicadas de volta no Publicador. As alterações podem ser replicadas usando atualização enfileirada ou imediata. A opção **Método de atualização do assinante** determina qual método usar. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## <a name="publisher-options-for-merge-subscriptions"></a>Opções do editor para assinaturas de mesclagem  
 **Definição de partição (HOST_NAME)**  
 Para uma publicação que usa filtros com parâmetros, a replicação de mesclagem avalia uma das duas funções de sistema (ou ambas, se as referências de filtro funcionam) durante a sincronização para determinar a data em que um Assinante deve receber: **SUSER_SNAME()** ou **HOST_NAME()** . Por padrão, **HOST_NAME()** retorna o nome do computador no qual o Merge Agent está sendo executado, mas esse valor pode ser substituído no Assistente para Nova Assinatura. Para obter mais informações sobre filtros com parâmetros e substituição de **HOST_NAME ()** , consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Tipo de assinatura** e **Prioridade**  
 Exibe se a assinatura é uma assinatura de cliente ou servidor (isso não pode ser alterado depois que a assinatura tiver sido criada). Assinaturas de Servidor podem republicar dados para outros Assinantes e podem ter atribuição de prioridade para resolução de conflito.  
  
 Se você selecionou um tipo de assinatura de servidor no Assistente para Nova Assinatura, o Assinante receberá uma prioridade que será usada durante resolução de conflito.  
  
 **Resolver conflitos interativamente**  
 Determina se o Resolver Interativo deve usar a interface do usuário para resolver conflitos durante a sincronização de mesclagem. Isso requer um valor de **Habilitar** para **Usar Gerenciador de Sincronização do Windows**. Para obter mais informações, consulte [Resolução de conflito interativo](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  

  
## <a name="subscriber-options-for-all-subscriptions"></a>Opções do assinante para todas as assinaturas  
 **Inicializar os dados publicados a partir de um instantâneo**  
 Determina se as assinaturas são iniciadas com um instantâneo (o padrão) ou por outro método. Para obter mais informações sobre como inicializar assinaturas, consulte [Inicializar uma assinatura](../../relational-databases/replication/initialize-a-subscription.md).  
  
 **Local do Instantâneo**  
 Determina o local do qual são acessados arquivos de instantâneo durante inicialização ou reinicialização. O local pode ser um dos seguintes valores:  
  
-   **Local padrão**: o local padrão, definido ao configurar um Distribuidor. Para obter mais informações, confira [Especificar opções de instantâneo](../../relational-databases/replication/snapshot-options.md).  
  
-   **Pasta alternativa**: um local alternativo que pode ser especificado na caixa de diálogo **Propriedades de Publicação** . Para obter mais informações, confira [Especificar opções de instantâneo](../../relational-databases/replication/snapshot-options.md).  
  
-   **Pasta de instantâneo dinâmico**: um local de instantâneo para publicações de mesclagem que usam filtros de linha com parâmetros. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
-   **Pasta de FTP**: uma pasta acessível a um servidor FTP (File Transfer Protocol). Para obter mais informações, confira [Entregar instantâneos por FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
 **Pasta do instantâneo**  
 Se você selecionar qualquer valor diferente de **Local padrão** para a opção **Local do instantâneo** , terá de especificar um caminho para a pasta de instantâneo.  
  
 **Usar o Gerenciador de Sincronização do Windows**  
 Determina se essa assinatura pode ser sincronizada usando o Gerenciador de Sincronização do Windows da [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
 **Segurança**  
 Clique na linha **Conta de processo de agente** e, depois, clique no botão de propriedades ( **...** ) para alterar a conta na qual o Agente de Distribuição ou Agente de Mesclagem são executados no Assinante. As opções de segurança relacionadas a conexões dependem do tipo de assinatura:  
  
-   Para assinaturas de uma publicação transacional: para alterar a conta na qual o Distribution Agent faz conexões com o Distribuidor, clique em **Conexão do Distribuidor**e, depois, clique no botão de propriedades ( **...** ).  
  
-   Para assinaturas de atualização imediata de uma publicação transactional, além da conexão do Distribuidor descrita anteriormente, você pode alterar o método usado para propagar alterações do Assinante para o Publicador: clique em **Conexão do Publicador**e, depois, clique no botão de propriedades ( **...** ).  
  
-   Para assinaturas de publicações de mesclagem, clique em **Conexão do Publicador**e, depois, clique no botão de propriedades ( **...** ).  
  
 Para obter mais informações sobre as permissões exigidas para cada agente, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="subscriber-options-for-transactional-subscriptions"></a>Opções do assinante para assinaturas transacionais  
 **Assinatura atualizável**  
 Determina se as alterações do Assinante serão replicadas de volta no Publicador. As alterações podem ser replicadas usando atualização enfileirada ou imediata. A opção **Método de atualização do assinante** determina qual método usar. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## <a name="options-for-merge-subscriptions"></a>Opções para assinaturas de mesclagem  
 **Definição de partição (HOST_NAME)**  
 Para uma publicação que usa filtros com parâmetros, a replicação de mesclagem avalia uma das duas funções de sistema (ou ambas, se as referências de filtro funcionam) durante a sincronização para determinar a data em que um Assinante deve receber: **SUSER_SNAME()** ou **HOST_NAME()** . Por padrão, **HOST_NAME()** retorna o nome do computador no qual o Merge Agent está sendo executado, mas esse valor pode ser substituído no Assistente para Nova Assinatura. Para obter mais informações sobre filtros com parâmetros e substituição de **HOST_NAME ()** , consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Tipo de assinatura** e **Prioridade**  
 Exibe se a assinatura é uma assinatura de cliente ou servidor (isso não pode ser alterado depois que a assinatura tiver sido criada). Assinaturas de Servidor podem republicar dados para outros Assinantes e podem ter atribuição de prioridade para resolução de conflito.  
  
 Se você selecionou um tipo de assinatura de servidor no Assistente para Nova Assinatura, o Assinante receberá uma prioridade que será usada durante resolução de conflito  
  
 **Resolver conflitos interativamente**  
 Determina se o Resolver Interativo deve usar a interface do usuário para resolver conflitos durante a sincronização de mesclagem. Isso requer um valor de **Habilitar** para **Usar Gerenciador de Sincronização do Windows**. Para obter mais informações, consulte [Resolução de conflito interativo](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
 **Sincronização da Web**  
 **Usar Sincronização da Web** determina se deve ser feita a conexão com um IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para sincronizar a assinatura. Essa opção só estará disponível se a publicação estiver habilitada para sincronização da Web. Para obter mais informações, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Se você selecionar **Verdadeiro** para **Usar Sincronização da Web**:  
  
-   Insira o endereço completo do servidor IIS em **Endereço do servidor Web**.    
-   Clique na linha **Conexão do Servidor Web** e, depois, clique no botão de propriedades ( **...** ) para definir ou alterar a conta na qual o Assinante se conecta ao servidor IIS.    
-   Altere o **Tempo limite do servidor Web** se necessário. O tempo limite é o período de tempo, em segundos, antes que uma solicitação de sincronização da Web expire. 

 
Para obter mais informações sobre a configuração, consulte [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md). 
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Exibir e modificar propriedades de assinatura push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)   

  
  

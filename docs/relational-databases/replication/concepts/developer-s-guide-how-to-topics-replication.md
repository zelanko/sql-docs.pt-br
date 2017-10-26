---
title: "Guia do desenvolvedor: tópicos de instruções (replicação) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c6c15ae6-da52-4638-93d3-61c7242e8a0b
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 288ed137e701d6cfb416d12b6ff2176c59ec0278
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="developer39s-guide-how-to-topics-replication"></a>Guia do desenvolvedor: tópicos de instruções (replicação)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este tópico oferece links para informações sobre como executar programaticamente tarefas relacionadas à replicação.  
  
## <a name="securing-a-replication-topology"></a>Protegendo uma topologia de replicação  
  
-   [Exibir e modificar configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
-   [Gerenciar logons na lista de acesso à publicação](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="configuring-modifying-and-disabling-publishing-and-distribution-replication"></a>Configurando, modificando e desabilitando a publicação e a distribuição (replicação)  
  
-   [Configurar a publicação e a distribuição](../../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
-   [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [Desabilitar a publicação e a distribuição](../../../relational-databases/replication/disable-publishing-and-distribution.md)  
  
## <a name="creating-modifying-and-deleting-publications-and-articles"></a>Criando, modificando e excluindo publicações e artigos  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Definir um Artigo](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [Exibir e modificar as propriedades do artigo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [Excluir uma publicação](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [Excluir um artigo](../../../relational-databases/replication/publish/delete-an-article.md)  
  
-   [Criar uma publicação de um Banco de Dados Oracle](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)  
  
-   [Definir o período de validade da assinatura](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)  
  
-   [Especificar opções de esquema](../../../relational-databases/replication/publish/specify-schema-options.md)  
  
-   [Replicar alterações de esquema](../../../relational-databases/replication/publish/replicate-schema-changes.md)  
  
-   [Gerenciar colunas de identidade](../../../relational-databases/replication/publish/manage-identity-columns.md)  
  
-   [Definir o nível de compatibilidade para publicações de mesclagem](../../../relational-databases/replication/publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>Opções de instantâneo  
  
-   [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [Entregar um instantâneo pelo FTP](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)  
  
### <a name="filtering-data"></a>Filtrando dados  
  
-   [Definir e modificar um filtro de colunas](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)  
  
-   [Definir e modificar um filtro de linha estático](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)  
  
-   [Definir e modificar um filtro de linha parametrizado para um artigo de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [Otimizar filtros de linha com parâmetros](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)  
  
-   [Definir e modificar um filtro de junção entre artigos de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>Opções de replicação transacional  
  
-   [Definir o método de propagação de alterações de dados para artigos transacionais](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [Habilitar atualização de assinaturas para publicações transacionais](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>Opções de replicação de mesclagem  
  
-   [Definir uma relação de registro lógico entre artigos da tabela de mesclagem](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [Especificar a ordem de processamento de artigos da tabela de mesclagem &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [Especificar que um artigo da tabela de mesclagem é somente download](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [Especificar que as exclusões não devem ser controladas para artigos de mesclagem &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [Especificar o nível de rastreamento e resolução de conflitos para artigos de mesclagem](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [Especificar um resolvedor de artigo de mesclagem](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
-   [Especificar a resolução de conflitos interativa para artigos de mesclagem](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="creating-modifying-and-deleting-subscriptions"></a>Criando, modificando e excluindo assinaturas  
  
-   [Criar uma assinatura pull](../../../relational-databases/replication/create-a-pull-subscription.md)  
  
-   [Exibir e modificar propriedades de assinatura pull](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
  
-   [Excluir uma assinatura pull](../../../relational-databases/replication/delete-a-pull-subscription.md)  
  
-   [Criar uma assinatura push](../../../relational-databases/replication/create-a-push-subscription.md)  
  
-   [Exibir e modificar propriedades de assinatura push](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)  
  
-   [Excluir uma assinatura push](../../../relational-databases/replication/delete-a-push-subscription.md)  
  
-   [Especificar agendas de sincronização](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
-   [Criar uma assinatura atualizável em uma publicação transacional](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md)
  
-   [Criar uma assinatura para um assinante não SQL Server](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronizing-subscriptions"></a>Sincronizando assinaturas  
  
-   [Criar e aplicar o instantâneo inicial](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Criar um instantâneo para uma publicação de mesclagem com filtros parametrizados](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Inicializar uma assinatura transacional de um backup &#40;Programação de Transact-SQL de Replicação&#41;](../../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [Inicializar uma assinatura manualmente](../../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [Sincronizar uma assinatura pull](../../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [Sincronizar uma assinatura push](../../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [Reinicializar uma assinatura](../../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [Executar scripts durante a sincronização &#40;Programação Transact-SQL de Replicação&#41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [Depurar um manipulador de lógica de negócios &#40;Programação de Replicação&#41;](../../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [Controlar o comportamento de gatilhos e restrições durante a sincronização &#40;Programação de Transact-SQL de Replicação&#41;](../../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administering-a-replication-topology"></a>Administrando uma topologia de replicação  
  
-   [Trabalhar com perfis do Agente de Replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [Validar dados no assinante](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
-   [Gerenciar partições para uma publicação de mesclagem com filtros parametrizados](../../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Carregar dados em massa em tabelas em uma publicação de mesclagem &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/bulk-load-data-into-tables-in-a-merge-publication.md)  
  
-   [Limpar metadados de mesclagem &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/clean-up-merge-metadata-replication-transact-sql-programming.md)  
  
-   [Executar uma atualização fictícia para um artigo de mesclagem &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)  
  
-   [Exibir comandos replicados e outras informações no banco de dados de distribuição &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [Habilitar backups coordenados para a replicação transacional &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)  
  
-   [Administrar uma topologia ponto a ponto &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)  
  
-   [Fechar para novas sessões uma topologia de replicação &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)  
  
-   [Configurar o trabalho do conjunto de transações para um Publicador Oracle &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)  
  
-   [Atualizar scripts de replicação &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitoring-a-replication-topology"></a>Monitorando a topologia de replicação  
  
-   [Permitir que não administradores usem o Replication Monitor](../../../relational-databases/replication/monitor/allow-non-administrators-to-use-replication-monitor.md)  
  
-   [Monitorar programaticamente a replicação](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
-   [Exibir comandos replicados e outras informações no banco de dados de distribuição &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [Exibir informações sobre conflitos para publicações de mesclagem &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
-   [Medir a latência e validar as conexões para a replicação transacional](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  


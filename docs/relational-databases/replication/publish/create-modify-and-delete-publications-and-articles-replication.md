---
title: Criar, modificar e excluir publicações e artigos (Replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], creating
- articles [SQL Server replication], defining
ms.assetid: e66d06ec-a12b-444d-875b-77f958af2f21
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f0827888b23103bb433c1d79d4c62c1d432e0a9c
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37358168"
---
# <a name="create-modify-and-delete-publications-and-articles-replication"></a>Criar, modificar e excluir publicações e artigos (Replicação)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta seção da documentação contém informações de procedimentos sobre tarefas relacionadas para criar publicações e definir artigos.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Defina um Artigo](../../../relational-databases/replication/publish/define-an-article.md)  
  
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
  
## <a name="snapshot-options"></a>Opções de instantâneo  
  
-   [Especificar o formato do instantâneo &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/specify-snapshot-format-sql-server-management-studio.md)  
  
-   [Especificar um local de pasta de instantâneo alternativa &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   [Compactar arquivos de instantâneo &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/compress-snapshot-files-sql-server-management-studio.md)  
  
-   [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [Executar scripts antes e depois de um instantâneo ser aplicado &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [Entregar um instantâneo pelo FTP](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)  
  
## <a name="filtering-data"></a>Filtrando dados  
  
-   [Definir e modificar um filtro de colunas](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)  
  
-   [Definir e modificar um filtro de linha estático](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)  
  
-   [Definir e modificar um filtro de linha parametrizado para um artigo de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [Otimizar filtros de linha com parâmetros](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)  
  
-   [Definir e modificar um filtro de junção entre artigos de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
-   [Gerar automaticamente um conjunto de filtros de junção entre artigos de mesclagem &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/automatically-generate-join-filters-between-merge-articles.md)  
  
## <a name="transactional-replication-options"></a>Opções de replicação transacional  
  
-   [Definir o método de propagação de alterações de dados para artigos transacionais](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [Habilitar atualização de assinaturas para publicações transacionais](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
-   [Definir opções de resolução de conflitos de atualização na fila &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)  
  
-   [Publicar a execução de um procedimento armazenado em uma publicação transacional &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
## <a name="merge-replication-options"></a>Opções de replicação de mesclagem  
  
-   [Definir uma relação de registro lógico entre artigos da tabela de mesclagem](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [Especificar a ordem de processamento de artigos da tabela de mesclagem &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [Especificar que um artigo da tabela de mesclagem é somente download](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [Especificar que as exclusões não devem ser controladas para artigos de mesclagem &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [Especificar o nível de rastreamento e resolução de conflitos para artigos de mesclagem](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [Especificar um resolvedor de artigo de mesclagem](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
-   [Especificar a resolução de conflitos interativa para artigos de mesclagem](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  

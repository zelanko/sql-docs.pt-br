---
title: Snapshot Agent (Assistente para Nova Publicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.configuresnapshotagent.f1
ms.assetid: 0257d4ee-1f7b-49fd-b4ef-65bfc1ef6951
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 102eb733cf0b2ca55f52ec9751e67f51c3cae988
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767630"
---
# <a name="snapshot-agent-new-publication-wizard"></a>Agente de Instantâneo (Assistente para Nova Publicação)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  O Agente de Instantâneo cria arquivos que contêm o esquema de publicação e os dados usados para inicializar novas assinaturas. Por padrão, o Agente de Instantâneo é executado imediatamente depois que a publicação é criada no Assistente para Nova Publicação. Subsequentemente, o agente é executado de acordo com uma agenda especificada. A criação de novos arquivos de instantâneo pelo agente depende do tipo de replicação e das opções escolhidas. Para obter mais informações, consulte [Create and Apply the Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md) (Criar e aplicar o instantâneo).  
  
 Para publicações de mesclagem que usam filtros com parâmetros, você deve criar um instantâneo para cada partição de dados após a conclusão do instantâneo de publicação. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="options"></a>Opções  
 **Criar um instantâneo imediatamente** (publicação de mesclagem) ou **Criar um instantâneo imediatamente e mantê-lo disponível para inicializar assinaturas** (replicação transacional)  
 Marque essa caixa de seleção para criar um instantâneo imediatamente depois que o Assistente para Nova Publicação for concluído. Desmarque essa caixa de seleção se você planejar alterar as propriedades do instantâneo na caixa de diálogo **Propriedades de Publicação** antes de gerar um instantâneo ou se inicializar o Assinante sem um instantâneo. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!NOTE]  
>  O assistente pode solicitar uma conexão com o Distribuidor para iniciar o trabalho apropriado para o Agente de Distribuição ou Agente de Mesclagem.  
  
 **Agendar o Agente de Instantâneo para execução nos seguintes horários**  
 Aceite a agenda padrão para execução do Agente de Instantâneo ou clique em **Alterar** para especificar uma agenda.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  

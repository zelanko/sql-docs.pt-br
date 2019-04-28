---
title: Snapshot Agent (Assistente para Nova Publicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.configuresnapshotagent.f1
ms.assetid: 0257d4ee-1f7b-49fd-b4ef-65bfc1ef6951
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 20e4e015064dcf0e472c2f3c56ecabf4100e6fe7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62676576"
---
# <a name="snapshot-agent-new-publication-wizard"></a>Agente de Instantâneo (Assistente para Nova Publicação)
  O Agente de Instantâneo cria arquivos que contêm o esquema de publicação e os dados usados para inicializar novas assinaturas. Por padrão, o Agente de Instantâneo é executado imediatamente depois que a publicação é criada no Assistente para Nova Publicação. Subsequentemente, o agente é executado de acordo com uma agenda especificada. A criação de novos arquivos de instantâneo pelo agente depende do tipo de replicação e das opções escolhidas. Para obter mais informações, consulte [Create and Apply the Snapshot](create-and-apply-the-snapshot.md) (Criar e aplicar o instantâneo).  
  
 Para publicações de mesclagem que usam filtros com parâmetros, você deve criar um instantâneo para cada partição de dados após a conclusão do instantâneo de publicação. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md).  
  
## <a name="options"></a>Opções  
 **Criar um instantâneo imediatamente** (publicação de mesclagem) ou **Criar um instantâneo imediatamente e mantê-lo disponível para inicializar assinaturas** (replicação transacional)  
 Marque essa caixa de seleção para criar um instantâneo imediatamente depois que o Assistente para Nova Publicação for concluído. Desmarque essa caixa de seleção se você planejar alterar as propriedades do instantâneo na caixa de diálogo **Propriedades de Publicação** antes de gerar um instantâneo ou se inicializar o Assinante sem um instantâneo. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!NOTE]  
>  O assistente pode solicitar uma conexão com o Distribuidor para iniciar o trabalho apropriado para o Agente de Distribuição ou Agente de Mesclagem.  
  
 **Agendar o Agente de Instantâneo para execução nos seguintes horários**  
 Aceite a agenda padrão para execução do Agente de Instantâneo ou clique em **Alterar** para especificar uma agenda.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](publish/create-a-publication.md)   
 [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md)   
 [Exibir e modificar as propriedades da publicação](publish/view-and-modify-publication-properties.md)   
 [Inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md)   
 [Publicar dados e objetos de banco de dados](publish/publish-data-and-database-objects.md)   
 [Visão geral dos agentes de replicação](agents/replication-agents-overview.md)  
  
  

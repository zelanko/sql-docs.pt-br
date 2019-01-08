---
title: Criar e aplicar o instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], applying
- snapshots [SQL Server replication], creating
ms.assetid: 631f48bf-50c9-4015-b9d8-8f1ad92d1ee2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bd78bf7da1a68e7e053af52c4fa8f9cf0cd71094
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52755638"
---
# <a name="create-and-apply-the-snapshot"></a>Criar e aplicar o instantâneo
  Instantâneos são gerados pelo Agente de Instantâneo depois que uma publicação for criada. Eles podem ser gerados:  
  
-   Imediatamente. Por padrão, um instantâneo para uma publicação de mesclagem é gerado imediatamente depois que a publicação seja criada no Assistente para Nova Publicação.  
  
-   Em um momento agendado. Especifique um agendamento na página **Agente de Instantâneo** do Assistente para Nova Publicação ou ao usar procedimentos armazenados no RMO (Replication Management Object).  
  
-   Manualmente Execute o Agente de Instantâneo no prompt de comando ou de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações sobre a execução de agentes, consulte [Conceitos dos executáveis do Replication Agent](concepts/replication-agent-executables-concepts.md) ou [Iniciar e interromper um Agente de Replicação &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
 Para replicação de mesclagem, é gerado um instantâneo toda vez que o Agente de Instantâneo é executado. Para replicação transacional, a geração de instantâneo depende da configuração da propriedade de publicação de **immediate_sync**. Se a propriedade estiver definida como TRUE (padrão ao usar o Assistente para Nova Publicação), um instantâneo é gerado toda vez que o Agente de Instantâneo for executado e pode ser aplicado ao Assinante a qualquer momento. Se a propriedade estiver definida como FALSE (padrão ao usar **sp_addpublication**), o instantâneo só é gerado se uma assinatura nova for adicionada desde a última execução do Agente de Instantâneo; Assinantes devem esperar que o Agente de Instantâneo termine antes de poder sincronizar-se.  
  
 Por padrão, quando são gerados instantâneos, eles são salvados na pasta de instantâneo padrão localizada no Distribuidor. Você também pode salvar os arquivos de instantâneo em mídia removível, como discos removíveis, CD-ROMs ou em locais diferentes da pasta padrão do instantâneo. Adicionalmente, você poderá comprimir os arquivos para que sejam mais fáceis de armazenar e transferir, e executar os scripts antes ou depois de o instantâneo ser aplicado ao Assinante. Para obter mais informações sobre essas opções, consulte [Snapshot Options](snapshot-options.md).  
  
 Se o instantâneo for uma publicação de mesclagem que usa filtros com parâmetros, o instantâneo será criado usando um processo de duas partes. Primeiro é criado um instantâneo do esquema que contém os scripts de replicação e o esquema dos objetos publicados, mas não os dados. Cada assinatura é então inicializada com um instantâneo que inclui os scripts e o esquema copiados do instantâneo do esquema e os dados pertencentes à partição de assinatura. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Se o instantâneo for criado no Publicador e armazenado em um local padrão ou local alternativo de instantâneo, este poderá ser transferido ao Assinante e aplicado. O Agente de Distribuição (para replicação transacional ou de instantâneo) ou Agente de Mesclagem (para replicação de mesclagem) transferem o instantâneo e aplica o esquema e arquivos de dados ao banco de dados da assinatura no Assinante durante a sincronização inicial. Por padrão, a sincronização inicial acontecerá imediatamente depois que uma assinatura seja criada se você usar o Assistente para Nova Assinatura. Este comportamento é controlado pela opção **Inicializar Quando** na página **Inicializar Assinaturas** do assistente. Quando os instantâneos forem criados após a assinatura ser inicializada, eles não serão aplicados ao Assinante, a menos que a assinatura esteja marcada para reinicialização. Para obter mais informações, consulte [Reinicializar as assinaturas](reinitialize-subscriptions.md).  
  
 Após o Agente de Distribuição ou Agente de Mesclagem aplicar o instantâneo inicial, o agente propaga atualizações subsequentes e outras modificações de dados. Quando instantâneos são distribuídos e aplicados a Assinantes, só esses Assinantes que estão à espera de instantâneos iniciais ou novos são afetados. Outros Assinantes daquela publicação (aqueles que já estejam recebendo inserções, atualizações, exclusões ou outras modificações aos dados publicados) não serão afetados.  
  
 Para criar e aplicar o instantâneo inicial, [Create and Apply the Initial Snapshot](create-and-apply-the-initial-snapshot.md).  
  
 Para exibir ou modificar o local padrão de pasta de instantâneo, consulte  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Especifique o local de instantâneo padrão &#40;SQL Server Management Studio&#41;](specify-the-default-snapshot-location-sql-server-management-studio.md)  
  
-   Programação de replicação e programação de RMO: [Configurar a publicação e a distribuição](configure-publishing-and-distribution.md)  
  
## <a name="see-also"></a>Consulte também  
 [Inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md)   
 [Proteger a pasta de instantâneos](security/secure-the-snapshot-folder.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)  
  
  

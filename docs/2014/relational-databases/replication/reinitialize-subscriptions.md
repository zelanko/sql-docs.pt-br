---
title: Reinicializar assinaturas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- initializing subscriptions [SQL Server replication], reinitializing
- subscriptions [SQL Server replication], reinitializing
- reinitializing subscriptions
ms.assetid: fb13712b-e7ad-4f1f-b605-4554bad0cb60
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 189667ecd2756ebf0026a22d981f9bb0ddd347c9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056978"
---
# <a name="reinitialize-subscriptions"></a>Reinicializar as assinaturas
  Reinicializar uma assinatura envolve aplicar um novo instantâneo de um ou mais artigos a um ou mais Assinantes: a replicação transacional e de instantâneo permitem que artigos individuais sejam reinicializados, e a replicação de mesclagem requer que todos os artigos sejam reinicializados. Os nós em uma topologia de replicação transacional ponto a ponto não podem ser reinicializados. Se for necessário assegurar que um nó tenha uma nova cópia dos dados, restaure o backup no nó. A reinicialização ocorre por um ou mais motivos:  
  
-   Marque explicitamente uma assinatura para reinicialização.  
  
-   Execute uma ação, como uma alteração de propriedade, que requeira uma reinicialização. Para obter mais informações sobre as ações que exigem reinicialização, consulte [Alterar as propriedades da publicação e do artigo](publish/change-publication-and-article-properties.md).  
  
 Em ambos os casos, o instantâneo mais recente será aplicado ao Assinante da próxima vez em que o Agente de Distribuição ou o Agente de Mesclagem forem executados. Com relação à replicação de instantâneo e transacional, quando ocorre a reinicialização, todas as alterações feitas no Assinante, mas ainda não sincronizadas com o Publicador, são substituídas pelo aplicativo do novo instantâneo.  
  
 Quanto à replicação de mesclagem, é possível optar por ter todas as alterações de dados carregadas do Assinante antes da aplicação do instantâneo. Todos os esquemas pendentes no Publicador são aplicados ao Assinante e, depois, todas as atualizações feitas no Assinante desde a última sincronização são propagadas para o Publicador, antes da reaplicação do instantâneo. Esse comportamento é controlado pelas propriedades **upload_first** e **automatic_reinitialization_policy** . Para obter mais informações, consulte [Reinitialize a Subscription](reinitialize-a-subscription.md). Ao marcar a assinatura para reinicialização com o SQL Server Management Studio ou com o Replication Monitor, é dada a opção, na caixa de diálogo **Reinicializar Assinaturas** , de carregar primeiramente as alterações.  
  
> [!IMPORTANT]  
>  Se você adicionar, descartar ou alterar um filtro com parâmetros em uma publicação de mesclagem, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
 Se estiver especificado que nenhum instantâneo inicial seria aplicado ao Assinante durante a criação da assinatura e, posteriormente, a assinatura for marcada para reinicialização, não se aplicará um instantâneo. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 **Para reinicializar uma assinatura**  
  
 Para reinicializar todos os artigos de uma assinatura, use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], procedimentos armazenados ou RMO (Replication Management Objects). Para reinicializar artigos individuais em publicações transacionais ou de instantâneo, é preciso usar procedimentos armazenados. Para obter mais informações, consulte [Reinitialize a Subscription](reinitialize-a-subscription.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Inicializar uma assinatura](initialize-a-subscription.md)   
 [Desativação e expiração de assinatura](subscription-expiration-and-deactivation.md)  
  
  

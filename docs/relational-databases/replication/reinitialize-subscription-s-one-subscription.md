---
title: "Reinicializar Assinatura(s) – uma assinatura | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.reinit.single.f1
helpviewer_keywords: Reinitialize Subscription(s) dialog box
ms.assetid: 9b0cf0be-d1f1-4163-a0ca-d6f095aa707e
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 57f205c4f64f1a85312faeded0f47f6489341dee
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="reinitialize-subscriptions---one-subscription"></a>Reiniciar Assinatura(s) - uma assinatura
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A caixa de diálogo **Reinicializar Assinaturas** permite marcar uma assinatura para reinicialização. A reinicialização envolve a aplicação de um instantâneo no Assinante; é executada pelo Distribution Agent para assinaturas em publicações transacionais e pelo Merge Agent para assinaturas em publicações de mesclagem.  
  
## <a name="options"></a>Opções  
 **Usar o instantâneo atual**  
 Selecione para aplicar o instantâneo atual ao Assinante da próxima vez que o Distribution Agent ou Merge Agent forem executados. Se não houver nenhum instantâneo válido disponível, essa opção não poderá ser selecionada.  
  
 **Usar um novo instantâneo**  
 Selecione para reinicializar a assinatura com um novo instantâneo. O instantâneo só poderá ser aplicado ao Assinante depois de ser gerado pelo Snapshot Agent. Se o Snapshot Agent tiver execução agendada, a assinatura não será reiniciada até que a próxima execução agendada do Snapshot Agent ocorra.  
  
 Selecione **Gerar o novo instantâneo agora** para iniciar o Snapshot Agent imediatamente.  
  
 **Carregar alterações não sincronizadas antes da reinicialização**  
 Somente replicação de mesclagem. Selecione para carregar quaisquer alterações pendentes do banco de dados de assinatura antes que os dados no Assinante sejam substituídos com um instantâneo.  
  
 Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
 **Marcar para Reinicialização**  
 Clique para marcar a assinatura para reinicialização. Depois que um instantâneo válido estiver disponível, da próxima vez que o Distribution Agent ou Merge Agent forem executados para a assinatura, o instantâneo será aplicado ao Assinante.  
  
## <a name="see-also"></a>Consulte também  
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)  
  
  

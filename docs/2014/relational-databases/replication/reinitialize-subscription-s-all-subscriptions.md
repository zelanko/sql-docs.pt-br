---
title: Reinicializar Assinatura(s) – todas as assinaturas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.reinit.all.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: e1122018-9f74-43e3-8489-7eae33ff23d9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8bcd42996ee35839162ee4e541f5be44c2d602aa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63131507"
---
# <a name="reinitialize-subscriptions---all-subscriptions"></a>Reiniciar Assinatura(s) - todas as assinaturas
  A caixa de diálogo **Reiniciar Assinatura(s)** permite marcar todas as assinaturas de uma publicação para reinicialização. A reinicialização envolve a aplicação de um instantâneo a cada Assinante; é executada pelo Distribution Agent para assinaturas em publicações transacionais e pelo Merge Agent para assinaturas em publicações de mesclagem.  
  
## <a name="options"></a>Opções  
 **Usar o instantâneo atual**  
 Selecione para aplicar o instantâneo atual a cada Assinante da próxima vez que o Distribution Agent ou Merge Agent forem executados para a assinatura. Se não houver nenhum instantâneo válido disponível, essa opção não poderá ser selecionada.  
  
 **Usar um novo instantâneo**  
 Selecione para reiniciar todas as assinaturas com um instantâneo novo. O instantâneo só pode ser aplicado a cada Assinante depois de ser gerado pelo Snapshot Agent. Se o Snapshot Agent tiver execução agendada, as assinaturas não serão reiniciadas até que a próxima execução agendada do Snapshot Agent ocorra.  
  
 Selecione **Gerar o novo instantâneo agora** para iniciar o Snapshot Agent imediatamente.  
  
 **Carregar alterações não sincronizadas antes da reinicialização**  
 Somente replicação de mesclagem. Selecione para carregar qualquer alteração pendente dos bancos de dados de assinatura antes que os dados nos Assinantes sejam sobrescritos por um instantâneo.  
  
 Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
 **Marcar para Reinicialização**  
 Clique para marcar cada assinatura para reinicialização. Depois que um instantâneo válido estiver disponível, da próxima vez que o Distribution Agent ou Merge Agent forem executados para a assinatura, o instantâneo será aplicado ao Assinante.  
  
## <a name="see-also"></a>Consulte também  
 [Reinicializar as assinaturas](reinitialize-subscriptions.md)  
  
  

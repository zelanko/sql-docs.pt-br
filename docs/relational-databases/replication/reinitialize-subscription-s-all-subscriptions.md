---
title: Reinicializar Assinatura(s) – todas as assinaturas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.reinit.all.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: e1122018-9f74-43e3-8489-7eae33ff23d9
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 809bd25fce24ab0ce859409d38406ea4fa4f2087
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287423"
---
# <a name="reinitialize-subscriptions---all-subscriptions"></a>Reiniciar Assinatura(s) - todas as assinaturas
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>Consulte Também  
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)  
  
  

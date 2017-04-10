---
title: "Reiniciar Assinatura(s) - todas as assinaturas | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.reinit.all.f1"
helpviewer_keywords: 
  - "caixa de diálogo Reiniciar Assinatura(s)"
ms.assetid: e1122018-9f74-43e3-8489-7eae33ff23d9
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# Reiniciar Assinatura(s) - todas as assinaturas
  O **reinicializar assinaturas** caixa de diálogo permite que você marque todas as assinaturas em uma publicação para reinicialização. A reinicialização envolve a aplicação de um instantâneo a cada Assinante; é executada pelo Distribution Agent para assinaturas em publicações transacionais e pelo Merge Agent para assinaturas em publicações de mesclagem.  
  
## Opções  
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
  
## Consulte também  
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)  
  
  
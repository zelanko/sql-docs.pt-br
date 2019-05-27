---
title: A atualização modificará assinaturas de atualização enfileiradas que usam o enfileiramento de mensagens | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication]
- MSMQ [SQL Server replication]
- queues [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
ms.assetid: 97944de3-fbad-4db1-939a-dcd550bf5893
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1c723050f9e860534c5298df9a487337e319ff91
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091407"
---
# <a name="upgrading-will-modify-queued-updating-subscriptions-that-use-message-queuing"></a>A atualização modificará assinaturas de atualização enfileiradas que usam o serviço de enfileiramento de mensagens
  O Supervisor de Atualização detectou que podem haver uma ou mais assinaturas de atualização na fila que usam o serviço de enfileiramento de mensagens da [!INCLUDE[msCoName](../../includes/msconame-md.md)] (também conhecido como MSMQ). A replicação não oferece mais suporte para o serviço de enfileiramento de mensagens. Portanto, as assinaturas serão modificadas para usar uma fila do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Apenas um valor de **sql** é permitido. Publicações existentes que usam o Serviço de Enfileiramento de Mensagens são modificadas durante atualização para usar uma fila [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você tiver aplicativos que dependem de atualização enfileirada usando o enfileiramento de mensagens, esses aplicativos precisarão ser gravados novamente para acomodar uma fila do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre assinaturas de atualização na fila, consulte ‘Assinaturas atualizáveis para replicação transacional’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A atualização irá remover a assinatura do serviço de enfileiramento de mensagens existente se o serviço de enfileiramento de mensagens for executado durante a atualização de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o serviço de enfileiramento de mensagens não estiver em execução, remova as filas manualmente depois da atualização. Para obter mais informações sobre a remoção de filas, consulte a documentação do Windows.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas na atualização da replicação](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  

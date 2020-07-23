---
title: Tipos de replicação | Microsoft Docs
description: Saiba mais sobre os diferentes tipos de replicação que o SQL Server fornece para uso em aplicativos distribuídos.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], types
ms.assetid: c1655e8d-d14c-455a-a7f9-9d2f43e88ab4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 21e1542801112d48b2981cb04d303b61cd7bd21e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86924026"
---
# <a name="types-of-replication"></a>Tipos de replicação
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece os seguintes tipos de replicação para uso em aplicativos distribuídos:  

| **Tipo** | **Descrição** |
|:-------- | :-------------- |
| [Replicação transacional](transactional/transactional-replication.md)| As alterações no Editor são fornecidas ao Assinante conforme ocorrem (quase em tempo real). As alterações nos dados são aplicadas ao Assinante na mesma ordem e dentro dos mesmos limites de transação que ocorreram no editor. | 
| [Replicação de mesclagem](merge/merge-replication.md) | Os dados podem ser alterados no Editor e no Assinante e são acompanhados com gatilhos. O Assinante sincroniza com o Publicador quando está conectado à rede e permuta todas as linhas que foram alteradas entre o Publicador e o Assinante desde a última vez que a sincronização ocorreu. | 
| [Replicação de instantâneo](snapshot-replication.md) | Aplica um instantâneo do Editor ao Assinante, o que distribui os dados exatamente como eles aparecem em um momento específico e não monitora as atualizações feitas aos dados. Quando a sincronização ocorre, todo o instantâneo é gerado e enviado aos Assinantes.| 
| [Ponto a ponto](transactional/peer-to-peer-transactional-replication.md) | Criada na base da replicação transacional, a replicação ponto a ponto se propaga de forma transacional, de acordo com as alterações em tempo real entre várias instâncias do servidor. | 
| [Bidirecional](transactional/bidirectional-transactional-replication.md)| Replicação transacional bidirecional é uma topologia de replicação transacional específica que permite a dois servidores trocarem alterações entre si: cada servidor publica dados e, então, assina uma publicação com os mesmos dados do outro servidor. | 
| [Assinaturas Atualizáveis](transactional/updatable-subscriptions-for-transactional-replication.md) | Criado com base na replicação transacional, quando os dados são atualizados em um Assinante para uma assinatura atualizável, primeiro eles são propagados para o Editor e, em seguida, para outros assinantes. | 
  
 
O tipo de replicação que você escolhe para um aplicativo, depende de muitos fatores, incluindo o ambiente físico da replicação, o tipo e a quantidade de dados a serem replicados e se os dados serão ou não atualizados no Assinante. O ambiente físico inclui o número e local dos computadores envolvidos na replicação e se esses computadores são clientes (estações de trabalho, laptops ou dispositivos portáteis) ou servidores.  
  
Cada tipo de replicação começa normalmente com uma sincronização inicial dos objetos publicados entre o Publicador e os Assinantes. Esta sincronização inicial pode ser executada por replicação com um *instantâneo*, que é uma cópia de todos os objetos e dados especificados por uma publicação. Depois que o instantâneo é criado, ele é distribuído aos Assinantes. Para alguns aplicativos, a replicação de instantâneo é tudo o que é necessário. Para outros tipos de aplicativos, é importante que as alterações de dados subsequentes fluam para o Assinante de forma incremental com o passar do tempo. Alguns aplicativos também exigem que as alterações fluam do Assinante de volta para o Publicador. A replicação transacional e a replicação de mesclagem fornecem opções para estes tipos de aplicativos.  
  
 
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)
  
  

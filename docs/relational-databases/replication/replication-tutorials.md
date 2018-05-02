---
title: Tutoriais de replicação | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- walkthroughs [SQL Server replication]
- replication [SQL Server], tutorials
ms.assetid: 19fbd10e-5b59-4cd0-a988-52d5d9206242
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3900aae4e96b5490b0b65cbbee004fc66337ff63
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="replication-tutorials"></a>Tutoriais de Replicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
A replicação é uma solução avançada para movimentação de dados, ou de subconjuntos de dados, entre servidores. Replique dados entre servidores totalmente conectados usando a Replicação Transacional. Replique também dados entre servidores e clientes conectados de maneira intermitente usando a Replicação de Mesclagem. Abaixo, você encontrará tutoriais que ajudam a preparar o servidor para replicação e, em seguida, ensinam a configurar a replicação Transacional e de Mesclagem. 
  
Nos Tutoriais sobre Replicação, "Publicador" refere-se ao servidor que contém os dados de origem sendo replicados e "Assinante" refere-se ao servidor de destino. O Publicador e o Assinante podem compartilhar a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas isso não é um requisito. Para obter mais informações, consulte [Visão geral do modelo de publicação do Replication](../../relational-databases/replication/publish/replication-publishing-model-overview.md).  

Esses tutoriais usam NODE1\SQL2016 como o Publicador e Distribuidor e NODE2\SQL2016 como o Assinante. 
  
> [!NOTE]  
> A maioria das tarefas mostradas nos tutoriais podem ser executadas de forma programática. Para obter mais informações, consulte [Documentação do desenvolvedor do Replication](../../relational-databases/replication/concepts/replication-developer-documentation.md).  
  
## <a name="replication-tutorials"></a>Tutoriais de Replicação  
[Tutorial: Preparar o SQL Server para replicação – Publicador, Distribuidor, Assinante](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md) 
 
Aprenda a preparar servidores de forma que a replicação possa ser executada com menos privilégios. É preciso completar este tutorial antes dos outros tutoriais de replicação.  
  
[Tutorial: Configurar a replicação entre dois servidores totalmente conectados (Transacional)](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)

Saiba como configurar a Replicação Transacional para replicar dados entre servidores totalmente conectados. Este tutorial também inclui uma metodologia de solução básica de erros. 

  
[Tutorial: Configurar a replicação entre um servidor e clientes móveis (Mesclagem)](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md)

Saiba como configurar a Replicação de Mesclagem para trocar dados entre um servidor e um ou mais clientes conectados apenas ocasionalmente.  
  
## <a name="see-also"></a>Consulte Também  
[Segurança e proteção da replicação](../../relational-databases/replication/security/security-and-protection-replication.md) 

[Visão geral da replicação transacional](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-replication) 

[Visão geral da replicação de mesclagem](https://docs.microsoft.com/en-us/sql/relational-databases/replication/merge/merge-replication)

  
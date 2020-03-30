---
title: Tutoriais de replicação | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- tutorials [SQL Server replication]
- walkthroughs [SQL Server replication]
- replication [SQL Server], tutorials
ms.assetid: 19fbd10e-5b59-4cd0-a988-52d5d9206242
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 3df80893c54978060387c7ff96cb975b34740534
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287330"
---
# <a name="replication-tutorials"></a>Tutoriais de replicação
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
A replicação é uma solução avançada para movimentação de dados, ou de subconjuntos de dados, entre servidores. É possível replicar dados entre servidores totalmente conectados usando a replicação transacional. Também é possível replicar dados entre servidores e clientes conectados intermitentemente usando a replicação de mesclagem. Neste artigo, você encontrará tutoriais que ajudam a preparar o servidor para replicação e, em seguida, ensinam a configurar a replicação transacional e de mesclagem. 
  
Nos tutoriais de replicação, "editor" refere-se ao servidor que contém os dados de origem que estão sendo replicados. "Assinante" refere-se ao servidor de destino. O editor e o assinante podem compartilhar a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas isso não é um requisito. Para obter mais informações, consulte a [visão geral do modelo de publicação de replicação](../../relational-databases/replication/publish/replication-publishing-model-overview.md).  

Esses tutoriais usam NODE1\SQL2016 como o editor e o distribuidor. Eles usam NODE2\SQL2016 como o assinante. 
  
> [!NOTE]  
> A maioria das tarefas mostradas nos tutoriais podem ser executadas de forma programática. Para obter mais informações, consulte a [documentação do desenvolvedor de replicação](../../relational-databases/replication/concepts/replication-developer-documentation.md).  
  
## <a name="replication-tutorials"></a>Tutoriais de replicação  
[Tutorial: Preparar o SQL Server para replicação (editor, distribuidor, assinante)](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md) 
 
Aprenda a preparar servidores de forma que a replicação possa ser executada com menos privilégios. É preciso completar este tutorial antes dos outros tutoriais de replicação.  
  
[Tutorial: Configurar a replicação entre dois servidores totalmente conectados (Transacional)](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)

Saiba como configurar a replicação transacional para replicar dados entre servidores totalmente conectados. Este tutorial também inclui uma metodologia de solução básica de erros. 

  
[Tutorial: Configurar a replicação entre um servidor e clientes móveis (mesclagem)](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md)

Saiba como configurar a replicação de mesclagem para trocar dados entre um servidor e um ou mais clientes conectados apenas ocasionalmente.  
  
## <a name="see-also"></a>Confira também  
[Exibir e modificar configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md) 

[Visão geral da replicação transacional](https://docs.microsoft.com/sql/relational-databases/replication/transactional/transactional-replication) 

[Visão geral da replicação de mesclagem](https://docs.microsoft.com/sql/relational-databases/replication/merge/merge-replication)

  

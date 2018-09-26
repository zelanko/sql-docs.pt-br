---
title: Replicação do SQL Server no Linux | Microsoft Docs
description: Este artigo descreve a replicação do SQL Server no Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.workload: On Demand
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2f9cd86f3d061265a1ecca018ee64159b6f10d04
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46714844"
---
# <a name="sql-server-replication-on-linux"></a>Replicação do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] apresenta a replicação do SQL Server para instâncias do SQL Server no Linux.

Configurar a replicação no Linux com o SQL Server Management Studio (SSMS) [procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

Uma instância do SQL Server pode participar de qualquer função de replicação:

* Publicador
* Distribuidor
* Assinante

Um esquema de replicação pode misturar e combinar plataformas de sistema operacional. Por exemplo, um esquema de replicação pode usar instâncias do SQL Server no Linux para o publicador e distribuidor e assinantes podem incluir instâncias do SQL Server no Windows.

Instâncias do SQL Server no Linux podem participar de qualquer tipo de replicação.

* Transacional.
* Mesclagem
* Instantâneo

Para obter informações detalhadas sobre a replicação, consulte [documentação do SQL Server replication](../relational-databases/replication/sql-server-replication.md).

## <a name="supported-features"></a>Recursos com suporte

Para [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] os recursos de replicação a seguir têm suporte:

* Replicação de instantâneo
* Replicação transacional
* Replicação de mesclagem
* Replicação ponto a ponto
* Replicação com portas não padrão <!--Add link to explanation-->
* Replicação com a autenticação do AD
* Configurações de replicação entre o Windows e Linux
* Atualizações imediatas para replicação transacional

## <a name="limitations"></a>Limitações

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] não suporta os seguintes recursos:

* Assinantes de atualização imediata

## <a name="next-steps"></a>Próximas etapas

[Configurar a replicação do SQL Server no Linux](sql-server-linux-replication-tutorial-tsql.md)

[Exemplo: Configurar a replicação do SQL Server no Linux](sql-server-linux-replication-configure.md)
---
title: Replicação do SQL Server em Linux
description: Este artigo descreve a Replicação do SQL Server em Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/17/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b049866d9752485cb1b9eb609404a3bd86f28a41
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68065189"
---
# <a name="sql-server-replication-on-linux"></a>Replicação do SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

O [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] apresenta a Replicação do SQL Server para instâncias do SQL Server em Linux.

Configure a replicação no Linux com os [procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md) do SSMS (SQL Server Management Studio).

Uma instância do SQL Server pode participar de qualquer função de replicação:

* Publicador
* Distribuidor
* Assinante

Um esquema de replicação pode combinar várias plataformas de sistema operacional. Por exemplo, um esquema de replicação pode incluir uma instância do SQL Server em Linux para o publicador e o distribuidor e os assinantes incluem instâncias do SQL Server em Windows, bem como em Linux.

Instâncias do SQL Server no Linux podem participar de qualquer tipo de replicação.

* Transacional.
* Mesclagem
* Instantâneo

Para obter informações detalhadas sobre a replicação, confira [Documentação da Replicação do SQL Server](../relational-databases/replication/sql-server-replication.md).

## <a name="supported-features"></a>Recursos compatíveis

Os recursos de replicação a seguir são compatíveis com o [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]:

* Replicação de instantâneo
* Replicação transacional
* Replicação de mesclagem
* Replicação ponto a ponto
* Replicação com portas não padrão <!--Add link to explanation-->
* Replicação com autenticação do AD
* Configurações de replicação no Windows e no Linux
* Atualizações imediatas para replicação transacional

## <a name="limitations"></a>Limitações

O [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] não dá suporte aos seguintes recursos:

* Assinantes de atualização imediata
* publicação Oracle

## <a name="next-steps"></a>Próximas etapas

[Configurar a Replicação do SQL Server em Linux](sql-server-linux-replication-tutorial-tsql.md)

[Exemplo: Configurar a Replicação do SQL Server em Linux](sql-server-linux-replication-configure.md)

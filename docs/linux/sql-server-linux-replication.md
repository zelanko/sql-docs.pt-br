---
title: Replicação do SQL Server em Linux
description: Este artigo descreve a Replicação do SQL Server em Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/09/2019
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: f0e1acd5af76f5b0b075879fc1c5122713caed55
ms.sourcegitcommit: 56fb0b7750ad5967f5d8e43d87922dfa67b2deac
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2019
ms.locfileid: "75001984"
---
# <a name="sql-server-replication-on-linux"></a>Replicação do SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2017](../includes/sssqlv14-md.md)] ([CU18](https://support.microsoft.com/help/4527377)) e posteriores são compatíveis com a Replicação do SQL Server para instâncias do SQL Server em Linux.

Configure a replicação no Linux com os [procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md) do SSMS (SQL Server Management Studio).

Uma instância do SQL Server pode participar de qualquer função de replicação:

* Publicador
* Distribuidor
* Subscriber

Um esquema de replicação pode combinar várias plataformas de sistema operacional. Por exemplo, um esquema de replicação pode incluir uma instância do SQL Server em Linux para o publicador e o distribuidor e os assinantes incluem instâncias do SQL Server em Windows, bem como em Linux.

Instâncias do SQL Server no Linux podem participar de qualquer tipo de replicação.

* Transacional
* Instantâneo

Para obter informações detalhadas sobre a replicação, confira [Documentação da Replicação do SQL Server](../relational-databases/replication/sql-server-replication.md).

## <a name="supported-features"></a>Recursos compatíveis

Há suporte para os seguintes recursos de replicação:

* Replicação de instantâneo
* Replicação transacional
* Replicação com portas não padrão <!--Add link to explanation-->
* Replicação com autenticação do AD
* Configurações de replicação no Windows e no Linux
* Atualizações imediatas para replicação transacional

## <a name="limitations"></a>Limitações

Não há suporte para os seguintes recursos:

* Replicação de mesclagem
* Replicação ponto a ponto
* publicação Oracle

## <a name="next-steps"></a>Próximas etapas

[Configurar a Replicação do SQL Server em Linux](sql-server-linux-replication-tutorial-tsql.md)

[Exemplo: Configurar a Replicação do SQL Server em Linux](sql-server-linux-replication-configure.md)

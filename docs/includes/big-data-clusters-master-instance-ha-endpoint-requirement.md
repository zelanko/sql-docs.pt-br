---
ms.openlocfilehash: 497a564a10a3d35b33f47222fce8f89fe36bd15e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73530940"
---
Determinadas operações, incluindo a definir configurações de servidor (nível de instância) ou adicionar manualmente um banco de dados a um grupo de disponibilidade, exigem uma conexão com a Instância do SQL Server. Operações como `sp_configure`, `RESTORE DATABASE` ou qualquer comando DDL em um banco de dados que pertence a um grupo de disponibilidade exigem uma conexão com a instância do SQL Server. Por padrão, um cluster Big Data não inclui um ponto de extremidade que habilita uma conexão com a instância. Você deve expor esse ponto de extremidade manualmente.

Para instruções, confira [Conectar-se a bancos de dados na réplica primária](../big-data-cluster/deployment-high-availability.md#instance-connect).
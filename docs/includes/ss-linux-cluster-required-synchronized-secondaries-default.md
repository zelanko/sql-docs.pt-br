---
ms.openlocfilehash: 2dc81d434714e0a13912fa6f14e1194df5e5afe3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68215602"
---
> [!NOTE]
> Ao criar o recurso e, depois, periodicamente, o agente de recurso do Pacemaker define automaticamente o valor do `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` com base na configuração do grupo de disponibilidade. Por exemplo, se o grupo de disponibilidade tem três réplicas síncronas, o agente definirá `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` como `1`. Para obter detalhes e mais opções de configuração, consulte [Alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](../linux/sql-server-linux-availability-group-ha.md). 
---
title: Comutador de recurso (Analytics Platform System)
description: Exibe informações sobre as opções de dois recursos que foram introduzidos no Analytics Platform System AU7.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: d9657b1433b0647d7165cb427da6333c0a325583
ms.sourcegitcommit: 0cda14b1151d9bce1253d96dea038c038484f07a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39400919"
---
#<a name="appliance-feature-switch"></a>Comutador de recurso de dispositivo
O **comutador de recurso** página exibe informações sobre as opções de dois recursos que foram introduzidos no Analytics Platform System 2016-AU7. Use esta página para atualizar ou ativar/desativar configurações no Analytics Platform System e os recursos. Alterando os valores de comutador de recurso exige uma reinicialização do serviço.

![Comutador de recurso de dispositivo DWConig](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig comutador de recurso de dispositivo") 

##<a name="autostatsenabled-switch"></a>Comutador AutoStatsEnabled
Controla o recurso de estatísticas automático. Essa opção é definida como true por padrão após a atualização para AU7. Qualquer banco de dados criado após a atualização herdará a criação automática e assíncrona de atualização de estatísticas. Para bancos de dados existentes, os administradores de banco de dados podem habilitar estatísticas automaticamente com [ALTER DATABASE (Parallel Data Warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw). Para obter mais informações sobre estatísticas, consulte [estatísticas](../relational-databases/statistics/statistics.md).

##<a name="dmsprocessstopmessagetimeoutinseconds-switch"></a>Comutador DmsProcessStopMessageTimeoutInSeconds
Controla o tempo de espera do serviço de movimentação de dados (DMS) para sincronizar em um sistema ocupado quando uma consulta que envolvem a movimentação de dados é cancelada. Atualizando para AU7 define esse valor como 900 segundos (15 minutos) por padrão. O intervalo válido é 0 – 3600 segundos.

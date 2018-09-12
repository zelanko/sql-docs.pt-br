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
ms.openlocfilehash: 70eed88b1224a712dcb8d1c76085fffc839155a5
ms.sourcegitcommit: 8008ea52e25e65baae236631b48ddfc33014a5e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44311636"
---
#<a name="appliance-feature-switches"></a>Opções de recursos do dispositivo
O **comutador de recurso** página exibe informações sobre as opções de recursos que estão sendo introduzidas no Analytics Platform System AU7 e versões posteriores. Use esta página de configuração para atualizar ou ativar/desativar configurações no Analytics Platform System e os recursos. Alterações em valores de switch de recursos exigem uma reinicialização do serviço.

![Comutador de recurso de dispositivo DWConig](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig comutador de recurso de dispositivo") 

##<a name="autostatsenabled"></a>AutoStatsEnabled
Controla o recurso de estatísticas automático. Essa opção é definida como true por padrão após a atualização para AU7. Qualquer banco de dados criado após a atualização herdará a criação automática e assíncrona de atualização de estatísticas. Para bancos de dados existentes, os administradores de banco de dados podem habilitar estatísticas automaticamente com [ALTER DATABASE (Parallel Data Warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw). Para obter mais informações sobre estatísticas, consulte [estatísticas](../relational-databases/statistics/statistics.md).

##<a name="usecatalogqueries"></a>UseCatalogQueries
Usando objetos de catálogo para algumas chamadas de metadados em vez de usar o SMO mostrou a melhoria de desempenho. Definido como true por padrão no CU7.1, essa opção controla esse comportamento. 

##<a name="dmsprocessstopmessagetimeoutinseconds"></a>DmsProcessStopMessageTimeoutInSeconds
Controla o tempo de espera do serviço de movimentação de dados (DMS) para sincronizar em um sistema ocupado quando uma consulta que envolvem a movimentação de dados é cancelada. Atualizando para AU7 define esse valor como 900 segundos (15 minutos) por padrão. O intervalo válido é 0 – 3600 segundos.

---
title: Opção de recurso (Analytics Platform System)
description: Exibe informações sobre as opções de dois recursos que foram introduzidos no AU7 de sistema de plataforma de análise.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e384a252584fed0e7543a7a4000fc9a70f6533e7
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34550887"
---
#<a name="appliance-feature-switch"></a>Opção de recurso do dispositivo
O **opção** página exibe informações sobre as opções de dois recursos que foram introduzidos no AU7 de sistema de plataforma de análise. Use esta página para atualizar ou habilitar/desabilitar recursos e configurações no sistema de plataforma de análise. Alterando os valores de chave de recurso requer uma reinicialização do serviço.

![Comutador de recurso do dispositivo DWConig](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig Switch de recurso de dispositivo") 

##<a name="autostatsenabled-switch"></a>Opção AutoStatsEnabled
Controla o recurso de estatísticas automática. Essa opção é definida como true por padrão após a atualização para AU7. Qualquer banco de dados criado após a atualização herdará a criação automática e a atualização assíncrona de estatísticas. Para bancos de dados existentes, os administradores de banco de dados podem habilitar estatísticas automaticamente com [alterar banco de dados] (/ sql/t-sql/statements/alter-database-parallel-data-warehouse). Para obter mais informações sobre estatísticas, consulte [estatísticas](../relational-databases/statistics/statistics.md).

##<a name="dmsprocessstopmessagetimeoutinseconds-switch"></a>Opção DmsProcessStopMessageTimeoutInSeconds
Controla o tempo de espera de serviço de movimentação de dados (DMS) para sincronizar em um sistema ocupado quando uma consulta que envolve a movimentação de dados foi cancelada. Atualizando para AU7 define esse valor como 900 segundos (15 minutos) por padrão. O intervalo válido é 0 a 3600 segundos.

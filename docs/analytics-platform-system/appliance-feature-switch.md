---
title: Opção de recurso
description: Exibe informações sobre as duas opções de recurso que são introduzidas no Analytics Platform System AU7.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 8642f27a329da8819acf0ab99a648c4979ed40d0
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401449"
---
# <a name="appliance-feature-switches"></a>Opções de recurso do dispositivo

A página **switch de recurso** exibe informações sobre as opções de recurso que estão sendo introduzidas no Analytics Platform System AU7 e posterior. Use esta página de configuração para atualizar ou habilitar/desabilitar recursos e configurações no Analytics Platform System.

> [!NOTE]
> As alterações nos valores de switch de recursos exigem uma reinicialização do serviço.

![Opção de recurso do dispositivo DWConfig](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "Opção de recurso do dispositivo DWConfig")

## <a name="autostatsenabled"></a>AutoStatsEnabled

Controla o recurso de estatísticas automáticas. Essa opção de recurso é definida como true por padrão após a atualização para AU7. Qualquer banco de dados criado após a atualização herdará a criação automática e a atualização assíncrona de estatísticas. Para bancos de dados existentes, os administradores de banco de dados podem habilitar estatísticas automáticas com [ALTER DATABASE (Parallel Data warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw). Para obter mais informações sobre estatísticas, consulte [estatísticas](../relational-databases/statistics/statistics.md).

## <a name="maxdopforinsertqueries"></a>MaxDOPForInsertQueries

Permite que você escolha as configurações de MAXDOP maiores que 1 para operações de inserção/seleção. As opções para essa configuração são 0, 1, 2 e 4, sendo que o padrão é 1.

## <a name="optimizecommonsubexpressions"></a>OptimizeCommonSubExpressions

Melhora o desempenho da consulta eliminando a movimentação de dados para subexpressão comum no otimizador de consulta do SQL. A explicação detalhada desse recurso pode ser encontrada [aqui](common-sub-expression-elimination.md).

## <a name="usecatalogqueries"></a>UseCatalogQueries

O uso de objetos de catálogo para algumas chamadas de metadados em vez de usar o SMO mostrou a melhoria do desempenho. Definido como true por padrão em CU 7.1, essa opção controla esse comportamento.

## <a name="dmsprocessstopmessagetimeoutinseconds"></a>DmsProcessStopMessageTimeoutInSeconds

Controla o serviço de movimentação de dados de tempo (DMS) aguarda a sincronização em um sistema ocupado quando uma consulta que envolve a movimentação de dados é cancelada. A atualização para AU7 define esse valor como 900 segundos (15 minutos) por padrão. O intervalo válido é de 0-3600 segundos.

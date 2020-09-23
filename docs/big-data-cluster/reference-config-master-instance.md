---
title: Propriedades de configuração de instância mestra do SQL Server
titleSuffix: SQL Server big data clusters
description: Artigo de referência para propriedades de configuração da instância mestra do SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 60888246623796d9b4d17c498da47ab4b6557cf2
ms.sourcegitcommit: 6ab28d954f3a63168463321a8bc6ecced099b247
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87790404"
---
# <a name="sql-server-master-instance-configuration-properties"></a>Propriedades de configuração da instância mestra do SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

## <a name="properties"></a>Propriedades

No momento da implantação, é possível configurar as opções a seguir do SQL Server para a instância mestra.

|Propriedade|Opções|
| --- | --- |
|`[sqlagent]`|`enabled = { true | false }` |
|`[telemetry]`|`customerfeedback = { true | false }` |
|`[telemetry]`|`userRequestedLocalAuditDirectory = </path/file>`|
|`[licensing]`| `pid = { Enterprise | Developer }`|
|`[traceflag]`|` traceflag<#> = <####>`|

### <a name="examples"></a>Exemplos

O seguinte exemplo habilita o SQL Agent, a telemetria, define um PID para a Edição Enterprise e habilita o sinalizador de rastreamento 1204:

```
[sqlagent]
enabled=true

[telemetry]
customerfeedback=true
userRequestedLocalAuditDirectory = /tmp/audit

[licensing]
pid = Enterprise

[traceflag]
traceflag0 = 1204
```

Confira as instruções em [Configurar a instância mestra do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](configure-sql-server-master-instance.md).

## <a name="next-steps"></a>Próximas etapas

[Configurar a instância mestra do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](configure-sql-server-master-instance.md)

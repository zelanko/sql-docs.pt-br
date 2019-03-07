---
title: referência de cluster mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Artigo de referência para os comandos de cluster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 130d3019d49deb7851696f6a1db2f77040734b31
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527209"
---
# <a name="mssqlctl-cluster"></a>cluster mssqlctl

O artigo a seguir fornece referência para o **cluster** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [create](#create) | Crie o cluster. |
| [delete](#delete) | Exclua o cluster. |
| [config](reference-mssqlctl-cluster-config.md) | Comandos de configuração do cluster. |
| [debug](reference-mssqlctl-cluster-debug.md) | Comandos de depuração. |

## <a id="create"></a> Criar cluster mssqlctl

Crie o cluster.

```
mssqlctl cluster create
   --name
   --accept-eula
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--name -n** | Nome do cluster, usado para o namespace de kubernetes. |
| **--accept-eula -e** | Você aceita os termos de licença? \[Sim/não\].  Valores permitidos: não, Sim. Obrigatórios. |

## <a id="delete"></a> exclusão de cluster mssqlctl

Exclua o cluster.

```
mssqlctl cluster delete
   --name
   [--force]
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--name -n** | Nome do cluster, usado para o namespace de kubernetes. Obrigatórios. |
| **--force -f** | Cluster de exclusão de força. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md). Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).
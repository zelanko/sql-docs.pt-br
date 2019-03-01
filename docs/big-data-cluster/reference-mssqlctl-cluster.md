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
ms.openlocfilehash: 088168e3400feea78fb9b92fa120f1140714ab34
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018422"
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
   [--accept-eula]
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
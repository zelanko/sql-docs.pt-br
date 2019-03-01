---
title: referência de configuração de cluster mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Artigo de referência para os comandos de cluster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 26e93151a1150bbbbd1798b38486ca5b01aaab1d
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018432"
---
# <a name="mssqlctl-cluster-config"></a>configuração de cluster mssqlctl

O artigo a seguir fornece referência para o **configuração do cluster** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [get](#get) | Obtenha o cluster. |

## <a id="get"></a> mssqlctl cluster config get

Obtenha o cluster.

```
mssqlctl cluster config get
   --name
   --output-file
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--name -n** | Nome do cluster, usado para o namespace de kubernetes. Obrigatórios. |
| **--output-file -f** | Arquivo de saída para armazenar o resultado no. Obrigatórios. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md). Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).
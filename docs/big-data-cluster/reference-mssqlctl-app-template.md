---
title: referência de modelo de aplicativo mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Artigo de referência para comandos de modelo de aplicativo mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 16583ba970bfc13312864ea2e9d2571b04c20fcb
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527219"
---
# <a name="mssqlctl-app-template"></a>modelo de aplicativo mssqlctl

O artigo a seguir fornece referência para o **modelo de aplicativo** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [list](#list) | Modelos de Fetch com suporte. |
| [pull](#pull) | Baixe os modelos com suporte. |

## <a id="list"></a> lista de modelos de aplicativo mssqlctl

Modelos de Fetch com suporte.

```
mssqlctl app template list
   --url
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--url -u** | Especifique um local de repositório de modelo diferente. Padrão: https://github.com/Microsoft/sql-server-samples.git. |

### <a name="examples"></a>Exemplos

Busca todos os modelos em um local de repositório do modelo padrão.

```
mssqlctl app template list
```

Busca todos os modelos em um local de repositório diferente.

```
mssqlctl app template list --url https://github.com/diffrent/templates.git
```

## <a id="pull"></a> mssqlctl pull de modelo de aplicativo

Baixe os modelos com suporte.

```
mssqlctl app template pull
   --destination
   --name
   --url
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--destination -d** | Onde colocar o modelo de aplicativo de esqueleto.  Padrão:. / modelos. |
| **--name -n** | Nome do modelo. Para obter uma lista completa desativar nomes de modelo com suporte, execute `mssqlctl app template list`. |
| **--url -u** | Especifique um local de repositório de modelo diferente. Padrão:
https://github.com/Microsoft/sql-server-samples.git. |

### <a name="examples"></a>Exemplos

Baixe todos os modelos em um local de repositório do modelo padrão.

```
mssqlctl app template pull
```

Baixe todos os modelos em um local de repositório diferente.

```
mssqlctl app template list --url https://github.com/diffrent/templates.git
```

Baixe o modelo individual por nome.

```
mssqlctl app template pull --name ssis
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md). Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).
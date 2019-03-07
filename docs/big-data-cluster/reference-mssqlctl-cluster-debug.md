---
title: referência de depuração de cluster mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Artigo de referência para os comandos de cluster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9312e972dfcb439f4ef19a4e72d8d66454622096
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527229"
---
# <a name="mssqlctl-cluster-debug"></a>depuração de cluster mssqlctl

O artigo a seguir fornece referência para o **depuração de cluster** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [copy-logs](#copy-logs) | Copie os logs. |
| [dump](#dump) | Despejo de registro em log do gatilho. |

## <a id="copy-logs"></a> logs de cópia de depuração de cluster

Copie os logs.

```
mssqlctl cluster debug copy-logs
   --namespace
   [--container]
   [--pod]
   [--target-folder]
   [--timeout]
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--namespace -n** | Nome do cluster, usado para o namespace de kubernetes. Obrigatórios. |
| **--container -c** | Copiar os logs para os contêineres com nome semelhante, opcional, por padrão copia logs para todos os contêineres. Não pode ser especificado várias vezes. Se especificado várias vezes, pela última vez um será usado. |
| **– pod -p** | Copie os logs para os pods com nome semelhante. Opcional, por padrão, copia os logs para todos os pods. Não pode ser especificado várias vezes. Se especificado várias vezes, pela última vez um será usado. |
| **– pasta de destino - d** | Caminho da pasta para copiar logs de destino. Opcional, por padrão cria o resultado na pasta local.  Não pode ser especificado várias vezes. Se especificado várias vezes, pela última vez um será usado. |
| **-- timeout -t** | O número de segundos de espera para o comando ser concluído. O valor padrão é 0, que é ilimitado. |

## <a id="dump"></a> despejo de depuração de cluster

Despejo de registro em log do gatilho.

```
mssqlctl cluster debug dump
   [--container]
   [--namespace]
   --target-folder
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--container -c** | Copiar os logs para os contêineres com nome semelhante, opcional, por padrão copia logs para todos os contêineres. Não pode ser especificado várias vezes. Se especificado várias vezes, pela última vez um será usado.  Valores permitidos: mssql-controller. |
| **--namespace -n** | Nome do cluster, usado para o namespace de kubernetes. Obrigatórios. |
| **– pasta de destino - d** | Caminho da pasta para copiar logs de destino. Opcional, por padrão cria o resultado na pasta local.  Não pode ser especificado várias vezes. Se especificado várias vezes, pela última vez um será usado.  Padrão: `./output/dump`. Obrigatórios. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md). Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).
---
title: referência de montagem do armazenamento mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Artigo de referência para comandos de armazenamento mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8580c3c52cda484581f1c88ccfc039d8bd0bf78
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018452"
---
# <a name="mssqlctl-storage-mount"></a>montagem do armazenamento mssqlctl

O artigo a seguir fornece referência para o **montagem do armazenamento** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [create](#create) | Crie repositórios remotos de montagens no HDFS. |
| [delete](#delete) | Exclua montagens de repositórios remotos em HDFS. |
| [status](#status) | Status do mount(s). |

## <a id="create"></a> montagem do armazenamento mssqlctl criar

Crie repositórios remotos de montagens no HDFS.

```
mssqlctl storage mount create
   --mount-path
   --remote-uri
   [--credential-file]
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--mount-path** | Caminho do HDFS em que a montagem deve ser criar (destino de montagem). Obrigatórios. |
| **--remote-uri** | URI do repositório remoto que deve ser montado (fonte de montagem). Obrigatórios. |
| **--credential-file** | Arquivo que contém as credenciais para acessar o armazenamento remoto. As credenciais devem ser especificados como chave = pares de valor com uma chave = valor por linha. Qualquer é igual a chaves ou valores precisa de escape. Por padrão, é necessária nenhuma credencial. As chaves necessárias dependem do tipo de armazenamento remoto que está sendo montado e o tipo de autorização usado. |

### <a name="examples"></a>Exemplos

Para montar "dados" do contêiner na conta do ADLS Gen 2 "adlsv2example" no caminho do HDFS `/mounts/adlsv2/data` usando a chave compartilhada:

```
mssqlctl storage mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/ --mount-path /mounts/adlsv2/data --credentials credential_file
```

Para montar um cluster remoto do HDFS (`hdfs://namenode1:8080/`) no caminho do HDFS local `/mounts/hdfs/`:

```
mssqlctl storage mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```

## <a id="delete"></a> exclusão de montagem do armazenamento mssqlctl

Exclua montagens de repositórios remotos em HDFS.

```
mssqlctl storage mount delete
   --mount-path
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--mount-path** | O caminho do HDFS correspondente para a montagem que deve ser excluídos. Obrigatórios. |

### <a name="examples"></a>Exemplos

Exclua a montagem criada no /mounts/adlsv2/data para uma conta de armazenamento do ADLS Gen 2.

```
mssqlctl storage mount delete --mount-path /mounts/adlsv2/data
```

## <a id="status"></a> status de montagem do armazenamento mssqlctl

Status do mount(s).

```
mssqlctl storage mount status
   --mount-path
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--mount-path** | Caminho de montagem. Obrigatórios. |

### <a name="examples"></a>Exemplos

Obter o status de montagem pelo caminho

```
mssqlctl storage mount status --mount-path /mounts/hdfs
```

Obter status de todas as montagens.

```
mssqlctl storage mount status
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md). Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).
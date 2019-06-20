---
title: referência de montagem de pool de armazenamento de cluster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de montagem de pool de armazenamento de cluster mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: eb527779cd844064bcabccc91f5356676e06f004
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66779307"
---
# <a name="mssqlctl-cluster-storage-pool-mount"></a>Montagem do pool de armazenamento de cluster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **montagem do pool de armazenamento do cluster** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[Criar mssqlctl montagem do pool de armazenamento do cluster](#mssqlctl-cluster-storage-pool-mount-create) | Crie repositórios remotos de montagens no HDFS.
[exclusão de montagem de pool de armazenamento de cluster mssqlctl](#mssqlctl-cluster-storage-pool-mount-delete) | Exclua montagens de repositórios remotos em HDFS.
[status de montagem do pool de armazenamento de cluster mssqlctl](#mssqlctl-cluster-storage-pool-mount-status) | Status do mount(s).
## <a name="mssqlctl-cluster-storage-pool-mount-create"></a>Criar mssqlctl montagem do pool de armazenamento do cluster
Crie repositórios remotos de montagens no HDFS.
```bash
mssqlctl cluster storage-pool mount create --remote-uri 
                                           --mount-path  
                                           [--credential-file]
```
### <a name="examples"></a>Exemplos
Montar o contêiner "dados" na conta do ADLS Gen 2 "adlsv2example" em /mounts/adlsv2/data de caminho do HDFS usando a chave compartilhada
```bash
mssqlctl cluster storage-pool mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data --credentials credential_file
```
Para montar um cluster remoto do HDFS (hdfs://namenode1:8080 /) no local HDFS caminho /mounts/hdfs /
```bash
mssqlctl cluster storage-pool mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--remote-uri`
URI do repositório remoto que deve ser montado (fonte de montagem).
#### `--mount-path`
Caminho do HDFS onde montagem deve ser criado (destino de montagem).
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--credential-file`
Arquivo que contém as credenciais para acessar o armazenamento remoto. As credenciais devem ser especificados como chave = pares de valor com uma chave = valor por linha. Qualquer é igual a chaves ou valores precisa de escape. Por padrão, é necessária nenhuma credencial. As chaves necessárias dependem do tipo de armazenamento remoto que está sendo montado e o tipo de autorização usado.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-cluster-storage-pool-mount-delete"></a>exclusão de montagem de pool de armazenamento de cluster mssqlctl
Exclua montagens de repositórios remotos em HDFS.
```bash
mssqlctl cluster storage-pool mount delete --mount-path 
                                           
```
### <a name="examples"></a>Exemplos
Exclua a montagem criada no /mounts/adlsv2/data para uma conta de armazenamento do ADLS Gen 2.
```bash
mssqlctl cluster storage-pool mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--mount-path`
O caminho do HDFS correspondente para a montagem que deve ser excluídos.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-cluster-storage-pool-mount-status"></a>status de montagem do pool de armazenamento de cluster mssqlctl
Status do mount(s).
```bash
mssqlctl cluster storage-pool mount status [--mount-path] 
                                           
```
### <a name="examples"></a>Exemplos
Obter o status de montagem pelo caminho
```bash
mssqlctl cluster storage-pool mount status --mount-path /mounts/hdfs
```
Obter status de todas as montagens.
```bash
mssqlctl cluster storage-pool mount status
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--mount-path`
Caminho de montagem.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md). Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).
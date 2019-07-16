---
title: referência de montagem de pool de armazenamento mssqlctl bdc
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de montagem de pool de armazenamento mssqlctl bdc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b6a412c6d7cab9fb869a9aa8ee1b62ae0ed3f717
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958009"
---
# <a name="mssqlctl-bdc-storage-pool-mount"></a>montagem de pool de armazenamento do bdc mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **montagem de pool de armazenamento do bdc** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[montagem de pool de armazenamento do bdc mssqlctl criar](#mssqlctl-bdc-storage-pool-mount-create) | Crie repositórios remotos de montagens no HDFS.
[exclusão de montagem de pool de armazenamento mssqlctl bdc](#mssqlctl-bdc-storage-pool-mount-delete) | Exclua montagens de repositórios remotos em HDFS.
[status da montagem mssqlctl bdc pool de armazenamento](#mssqlctl-bdc-storage-pool-mount-status) | Status do mount(s).
## <a name="mssqlctl-bdc-storage-pool-mount-create"></a>montagem de pool de armazenamento do bdc mssqlctl criar
Crie repositórios remotos de montagens no HDFS. As credenciais para acessar o repositório remoto, se houver, devem ser especificadas usando a variável de ambiente MOUNT_CREDENTIALS como uma lista separada por vírgulas de chave = pares de valor. Qualquer vírgulas em chaves ou valores devem ser escapadas.
```bash
mssqlctl bdc storage-pool mount create --remote-uri 
                                       --mount-path
```
### <a name="examples"></a>Exemplos
Montar o contêiner "dados" na conta do ADLS Gen 2 "adlsv2example" em /mounts/adlsv2/data de caminho do HDFS usando a chave compartilhada
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
mssqlctl bdc storage-pool mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
Para montar um BDC HDFS remoto (hdfs://namenode1:8080 /) no local HDFS caminho /mounts/hdfs /
```bash
mssqlctl bdc storage-pool mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--remote-uri`
URI do repositório remoto que deve ser montado (fonte de montagem).
#### `--mount-path`
Caminho do HDFS onde montagem deve ser criado (destino de montagem).
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
## <a name="mssqlctl-bdc-storage-pool-mount-delete"></a>exclusão de montagem de pool de armazenamento mssqlctl bdc
Exclua montagens de repositórios remotos em HDFS.
```bash
mssqlctl bdc storage-pool mount delete --mount-path 
                                       
```
### <a name="examples"></a>Exemplos
Exclua a montagem criada no /mounts/adlsv2/data para uma conta de armazenamento do ADLS Gen 2.
```bash
mssqlctl bdc storage-pool mount delete --mount-path /mounts/adlsv2/data
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
## <a name="mssqlctl-bdc-storage-pool-mount-status"></a>status da montagem mssqlctl bdc pool de armazenamento
Status do mount(s).
```bash
mssqlctl bdc storage-pool mount status [--mount-path] 
                                       
```
### <a name="examples"></a>Exemplos
Obter o status de montagem pelo caminho
```bash
mssqlctl bdc storage-pool mount status --mount-path /mounts/hdfs
```
Obter status de todas as montagens.
```bash
mssqlctl bdc storage-pool mount status
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
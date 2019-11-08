---
title: azdata bdc hdfs mount reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc hdfs mount de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 43796ca3dc02804472298b17f8ddaeed946df5bb
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531843"
---
# <a name="azdata-bdc-hdfs-mount"></a>azdata bdc hdfs mount

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[azdata bdc hdfs mount create](#azdata-bdc-hdfs-mount-create) | Criar montagens de repositórios remotos no HDFS.
[azdata bdc hdfs mount delete](#azdata-bdc-hdfs-mount-delete) | Excluir montagens de repositórios remotos no HDFS.
[azdata bdc hdfs mount status](#azdata-bdc-hdfs-mount-status) | Status das montagens.
[azdata bdc hdfs mount refresh](#azdata-bdc-hdfs-mount-refresh) | Atualizar o conteúdo de uma montagem no HDFS.
## <a name="azdata-bdc-hdfs-mount-create"></a>azdata bdc hdfs mount create
Criar montagens de repositórios remotos no HDFS. As credenciais para acessar o armazenamento remoto, se houver, devem ser especificadas usando a variável de ambiente MOUNT_CREDENTIALS como uma lista separada por vírgula de pares chave = valor. Qualquer vírgula nas chaves ou valores deve ter escape.
```bash
azdata bdc hdfs mount create --remote-uri -r 
                             --mount-path -m
```
### <a name="examples"></a>Exemplos
Para montar "dados" do contêiner na conta do ADLS Gen 2 "adlsv2example" no caminho do HDFS/mounts/adlsv2/data usando a chave compartilhada
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
azdata bdc hdfs mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
Para montar um BDC HDFS remoto (hdfs://namenode1:8080/) no caminho do HDFS local /mounts/hdfs/
```bash
azdata bdc hdfs mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--remote-uri -r`
URI do repositório remoto que deve ser montado (fonte da montagem).
#### `--mount-path -m`
Caminho do HDFS em que a montagem deve ser criada (destino de montagem).
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-mount-delete"></a>azdata bdc hdfs mount delete
Excluir montagens de repositórios remotos no HDFS.
```bash
azdata bdc hdfs mount delete --mount-path -m 
           ```
### Examples
Delete mount created at /mounts/adlsv2/data for a ADLS Gen 2 storage account.
```bash
azdata bdc hdfs mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--mount-path -m`
O caminho do HDFS correspondente à montagem que deve ser excluída.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-mount-status"></a>azdata bdc hdfs mount status
Status das montagens.
```bash
azdata bdc hdfs mount status [--mount-path -m] 
           ```
### Examples
Get mount status by path
```bash
azdata bdc hdfs mount status --mount-path /mounts/hdfs
```
Obter o status de todas as montagens.
```bash
azdata bdc hdfs mount status
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--mount-path -m`
Caminho de montagem.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-mount-refresh"></a>azdata bdc hdfs mount refresh
Atualizar o conteúdo de uma montagem no HDFS.
```bash
azdata bdc hdfs mount refresh --mount-path -m 
            ```
### Examples
Refresh mount created at /mounts/adlsv2/data.
```bash
azdata bdc hdfs mount refresh --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--mount-path -m`
Caminho do HDFS correspondente à montagem que deve ser atualizada.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).

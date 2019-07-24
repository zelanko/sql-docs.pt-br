---
title: referência de montagem do azdata BDC HDFS
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de montagem do azdata BDC HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f0b259a3ac4ac0850fa05de3867e928b035307b
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426266"
---
# <a name="azdata-bdc-hdfs-mount"></a>montagem do HDFS do BDC azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos de **montagem de HDFS do BDC** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[criação de montagem do azdata BDC HDFS](#azdata-bdc-hdfs-mount-create) | Criar montagens de repositórios remotos no HDFS.
[exclusão de montagem do azdata BDC HDFS](#azdata-bdc-hdfs-mount-delete) | Exclua as montagens de repositórios remotos no HDFS.
[status de montagem do azdata BDC HDFS](#azdata-bdc-hdfs-mount-status) | Status de montagem (ões).
[atualização de montagem do azdata BDC HDFS](#azdata-bdc-hdfs-mount-refresh) | Atualize o conteúdo de uma montagem no HDFS.
## <a name="azdata-bdc-hdfs-mount-create"></a>criação de montagem do azdata BDC HDFS
Criar montagens de repositórios remotos no HDFS. As credenciais para acessar o armazenamento remoto, se houver, devem ser especificadas usando a variável de ambiente MOUNT_CREDENTIALS como uma lista separada por vírgulas de pares chave = valor. Qualquer vírgula nas chaves ou valores deve ter escape.
```bash
azdata bdc hdfs mount create --remote-uri -r 
                             --mount-path -m
```
### <a name="examples"></a>Exemplos
Para montar o contêiner "dados" na conta do ADLS Gen 2 "adlsv2example" no caminho do HDFS/mounts/adlsv2/data usando a chave compartilhada
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
azdata bdc hdfs mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
Para montar um BDC HDFS remoto (hdfs://namenode1:8080/) no caminho do HDFS local/mounts/HDFS/
```bash
azdata bdc hdfs mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--remote-uri -r`
URI do repositório remoto que deve ser montado (fonte de montagem).
#### `--mount-path -m`
Caminho do HDFS em que a montagem deve ser criada (destino de montagem).
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-mount-delete"></a>exclusão de montagem do azdata BDC HDFS
Exclua as montagens de repositórios remotos no HDFS.
```bash
azdata bdc hdfs mount delete --mount-path -m 
                             
```
### <a name="examples"></a>Exemplos
Exclua a montagem criada em/mounts/adlsv2/data para uma conta de armazenamento ADLS Gen 2.
```bash
azdata bdc hdfs mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--mount-path -m`
o caminho do HDFS correspondente à montagem que deve ser excluída.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-mount-status"></a>status de montagem do azdata BDC HDFS
Status de montagem (ões).
```bash
azdata bdc hdfs mount status [--mount-path -m] 
                             
```
### <a name="examples"></a>Exemplos
Obter status de montagem por caminho
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
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-mount-refresh"></a>atualização de montagem do azdata BDC HDFS
Atualize o conteúdo de uma montagem no HDFS.
```bash
azdata bdc hdfs mount refresh --mount-path -m 
                              
```
### <a name="examples"></a>Exemplos
Atualizar montagem criada em/mounts/adlsv2/Data.
```bash
azdata bdc hdfs mount refresh --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--mount-path -m`
Caminho do HDFS correspondente à montagem que deve ser atualizada.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para gerenciar SQL Server 2019 Big data clusters](deploy-install-azdata.md).

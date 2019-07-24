---
title: referência de depuração do BDC azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de depuração do BDC azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 38c327287273ae6596326d88d9e0d67c8e014d47
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426226"
---
# <a name="azdata-bdc-debug"></a>depuração do BDC azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos de **depuração do BDC** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[cópia de depuração do BDC do azdata-logs](#azdata-bdc-debug-copy-logs) | Copiar logs.
[despejo de depuração do BDC azdata](#azdata-bdc-debug-dump) | Despejo de log de gatilho.
## <a name="azdata-bdc-debug-copy-logs"></a>cópia de depuração do BDC do azdata-logs
Copie os logs de depuração do cluster de Big data – a configuração Kube é necessária no seu sistema.
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           [--target-folder -d]  
                           [--pod -p]  
                           [--timeout -t]
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--namespace -n`
Nome do cluster de Big data, usado para o namespace kubernetes.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--container -c`
Copie os logs para os contêineres com nome semelhante, opcional, por padrão copia logs para todos os contêineres. Não pode ser especificado várias vezes. Se especificado várias vezes, a última será usada
#### `--target-folder -d`
Caminho da pasta de destino para a qual copiar os logs. Opcional, por padrão, o cria o resultado na pasta local.  Não pode ser especificado várias vezes. Se especificado várias vezes, a última será usada
#### `--pod -p`
Copie os logs para o pods com um nome semelhante. Opcional, por padrão, o copia os logs para todos os pods. Não pode ser especificado várias vezes. Se especificado várias vezes, a última será usada
#### `--timeout -t`
O número de segundos a aguardar até que o comando seja concluído. O valor padrão é 0, o que é ilimitado
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
## <a name="azdata-bdc-debug-dump"></a>despejo de depuração do BDC azdata
Disparar o despejo de log e copiá-lo do contêiner-a configuração Kube é necessária no seu sistema.
```bash
azdata bdc debug dump --namespace -n 
                      --container -c  
                      [--target-folder -d]
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--namespace -n`
Nome do cluster de Big data, usado para o namespace kubernetes.
#### `--container -c`
Copie os logs para os contêineres com nome semelhante, opcional, por padrão copia logs para todos os contêineres. Não pode ser especificado várias vezes. Se especificado várias vezes, a última será usada
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--target-folder -d`
Caminho da pasta de destino para a qual copiar os logs. Opcional, por padrão, o cria o resultado na pasta local.  Não pode ser especificado várias vezes. Se especificado várias vezes, a última será usada`./output/dump`
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

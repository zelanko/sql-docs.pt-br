---
title: azdata bdc debug reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc debug de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d2cdb04cfc0bf98e2143b8e7b5ae67a7b0db9069
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653362"
---
# <a name="azdata-bdc-debug"></a>azdata bdc debug

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos **bdc debug** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc debug copy-logs](#azdata-bdc-debug-copy-logs) | Copiar logs.
[azdata bdc debug dump](#azdata-bdc-debug-dump) | Gatilho de despejo de log.
## <a name="azdata-bdc-debug-copy-logs"></a>azdata bdc debug copy-logs
Copiar os logs de depuração do cluster de Big Data – a configuração de kube é necessária em seu sistema.
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           [--target-folder -d]  
                           [--pod -p]  
                           [--timeout -t]
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--namespace -n`
Nome do cluster de Big Data, usado para namespaces de Kubernetes.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--container -c`
Copiar os logs para os contêineres com nome semelhante, opcional. Por padrão, copia logs para todos os contêineres. Não pode ser especificado várias vezes. Se especificado várias vezes, o último será usado
#### `--target-folder -d`
Caminho da pasta de destino para a qual copiar os logs. Opcional; por padrão, cria o resultado na pasta local.  Não pode ser especificado várias vezes. Se especificado várias vezes, o último será usado
#### `--pod -p`
Copiar os logs para o pods com nome semelhante. Opcional; por padrão, copia os logs para todos os pods. Não pode ser especificado várias vezes. Se especificado várias vezes, o último será usado
#### `--timeout -t`
O número de segundos a esperar para que o comando seja concluído. O valor padrão é 0, que é ilimitado
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-debug-dump"></a>azdata bdc debug dump
Disparar o despejo de log e copiá-lo do contêiner – a configuração de kube é necessária no seu sistema.
```bash
azdata bdc debug dump --namespace -n 
                      --container -c  
                      [--target-folder -d]
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--namespace -n`
Nome do cluster de Big Data, usado para namespaces de Kubernetes.
#### `--container -c`
Copiar os logs para os contêineres com nome semelhante, opcional. Por padrão, copia logs para todos os contêineres. Não pode ser especificado várias vezes. Se especificado várias vezes, o último será usado
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--target-folder -d`
Caminho da pasta de destino para a qual copiar os logs. Opcional; por padrão, cria o resultado na pasta local.  Não pode ser especificado várias vezes. Se especificado várias vezes, o último será usado `./output/dump`
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]gerenciar ](deploy-install-azdata.md).

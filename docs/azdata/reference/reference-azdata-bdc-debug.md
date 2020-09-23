---
title: azdata bdc debug reference
titleSuffix: SQL Server big data clusters
description: Use este artigo de referência para entender os comandos SQL na ferramenta azdata, especificamente os comandos bdc debug.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e9d1f561666bf6aefdef6abf4b1daf568a5a89d8
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733467"
---
# <a name="azdata-bdc-debug"></a>azdata bdc debug

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
| Comando | Descrição |
| --- | --- |
[azdata bdc debug copy-logs](#azdata-bdc-debug-copy-logs) | Copiar logs.
[azdata bdc debug dump](#azdata-bdc-debug-dump) | Dispara o despejo de memória.
## <a name="azdata-bdc-debug-copy-logs"></a>azdata bdc debug copy-logs
Copiar os logs de depuração do cluster de Big Data – a configuração do Kubernetes é necessária em seu sistema.
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           
[--target-folder -d]  
                           
[--pod -p]  
                           
[--timeout -t]  
                           
[--skip-compress -sc]  
                           
[--exclude-dumps -ed]
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
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
#### `--skip-compress -sc`
Se a compactação da pasta de resultados deve ser ignorada ou não. O valor padrão é False, que compacta a pasta de resultados.
#### `--exclude-dumps -ed`
Se você deseja ou não excluir os despejos da pasta de resultados. O valor padrão é False, que inclui despejos.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-debug-dump"></a>azdata bdc debug dump
Dispara o despejo de memória e copia-o do contêiner; é necessário realizar a configuração do Kubernetes no sistema.
```bash
azdata bdc debug dump --namespace -n 
                      [--container -c]  
                      
[--target-folder -d]
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--namespace -n`
Nome do cluster de Big Data, usado para namespaces de Kubernetes.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--container -c`
O contêiner de destino a ser disparado para despejar os processos `controller` em execução
#### `--target-folder -d`
Pasta de destino de cópia do despejo. `./output/dump`
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](../install/deploy-install-azdata.md).

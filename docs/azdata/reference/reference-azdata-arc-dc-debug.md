---
title: Referência do azdata arc dc debug
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata arc dc debug.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8020bebddbf8ae1f28f3513f08239daac47cbe42
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942268"
---
# <a name="azdata-arc-dc-debug"></a>azdata arc dc debug

Aplica-se ao `azdata`

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata arc dc debug copy-logs](#azdata-arc-dc-debug-copy-logs) | Copiar logs.
[azdata arc dc debug dump](#azdata-arc-dc-debug-dump) | Dispara o despejo de memória.
## <a name="azdata-arc-dc-debug-copy-logs"></a>azdata arc dc debug copy-logs
Copiar os logs de depuração do controlador de dados – a configuração do Kubernetes é necessária em seu sistema.
```bash
azdata arc dc debug copy-logs --namespace -ns 
                              [--container -c]  
                              
[--target-folder -d]  
                              
[--pod]  
                              
[--resource-kind -rk]  
                              
[--resource-name -rn]  
                              
[--timeout -t]  
                              
[--skip-compress -sc]  
                              
[--exclude-dumps -ed]
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--namespace -ns`
Namespace do Kubernetes do controlador de dados.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--container -c`
Copiar os logs para os contêineres com nome semelhante, opcional. Por padrão, copia logs para todos os contêineres. Não pode ser especificado várias vezes. Se especificado várias vezes, o último será usado
#### `--target-folder -d`
Caminho da pasta de destino para a qual copiar os logs. Opcional; por padrão, cria o resultado na pasta local.  Não pode ser especificado várias vezes. Se especificado várias vezes, o último será usado
#### `--pod`
Copiar os logs para o pods com nome semelhante. Opcional; por padrão, copia os logs para todos os pods. Não pode ser especificado várias vezes. Se especificado várias vezes, o último será usado
#### `--resource-kind -rk`
Copiar os logs para o recurso de um tipo específico. Não pode ser especificado várias vezes. Se especificado várias vezes, o último será usado. Se especificado, --resource-name também deverá ser especificado para identificar o recurso.
#### `--resource-name -rn`
Copiar os logs para o recurso do nome especificado. Não pode ser especificado várias vezes. Se especificado várias vezes, o último será usado. Se especificado, --resource-kind também deverá ser especificado para identificar o recurso.
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
## <a name="azdata-arc-dc-debug-dump"></a>azdata arc dc debug dump
Dispara o despejo de memória e copia-o do contêiner; é necessário realizar a configuração do Kubernetes no sistema.
```bash
azdata arc dc debug dump --namespace -ns 
                         [--container -c]  
                         
[--target-folder -d]
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--namespace -ns`
Namespace do Kubernetes do controlador de dados.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--container -c`
O contêiner de destino a ser disparado para despejar os processos em execução.
`controller`
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

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata](..\install\deploy-install-azdata.md).


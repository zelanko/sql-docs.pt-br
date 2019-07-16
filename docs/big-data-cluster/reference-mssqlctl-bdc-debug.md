---
title: referência de depuração do bdc mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de depuração mssqlctl bdc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9e7fc8e54a1473803dbeacb9c671b060b8ff8b07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958100"
---
# <a name="mssqlctl-bdc-debug"></a>depuração de bdc mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **depuração bdc** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[logs de cópia de depuração de bdc de mssqlctl](#mssqlctl-bdc-debug-copy-logs) | Copie os logs.
[despejo de depuração do bdc mssqlctl](#mssqlctl-bdc-debug-dump) | Despejo de registro em log do gatilho.
## <a name="mssqlctl-bdc-debug-copy-logs"></a>logs de cópia de depuração de bdc de mssqlctl
Copiar os logs de depuração do Cluster dados Big - config kube é necessária no seu sistema.
```bash
mssqlctl bdc debug copy-logs --namespace -n 
                             [--container -c]  
                             [--target-folder -d]  
                             [--pod -p]  
                             [--timeout -t]
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--namespace -n`
Nome do BDC, usado para o namespace de kubernetes.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--container -c`
Copiar os logs para os contêineres com nome semelhante, opcional, por padrão copia logs para todos os contêineres. Não pode ser especificado várias vezes. Se especificado várias vezes, pela última vez um será usado
#### `--target-folder -d`
Caminho da pasta para copiar logs de destino. Opcional, por padrão cria o resultado na pasta local.  Não pode ser especificado várias vezes. Se especificado várias vezes, pela última vez um será usado
#### `--pod -p`
Copie os logs para os pods com nome semelhante. Opcional, por padrão, copia os logs para todos os pods. Não pode ser especificado várias vezes. Se especificado várias vezes, pela última vez um será usado
#### `--timeout -t`
O número de segundos de espera para o comando ser concluído. O valor padrão é 0, que é ilimitado
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
## <a name="mssqlctl-bdc-debug-dump"></a>despejo de depuração do bdc mssqlctl
Disparar um despejo de registro em log e copiá-lo do contêiner - config kube é necessária no seu sistema.
```bash
mssqlctl bdc debug dump --namespace -n 
                        --container -c  
                        [--target-folder -d]
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--namespace -n`
Nome do BDC, usado para o namespace de kubernetes.
#### `--container -c`
Copiar os logs para os contêineres com nome semelhante, opcional, por padrão copia logs para todos os contêineres. Não pode ser especificado várias vezes. Se especificado várias vezes, pela última vez um será usado
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--target-folder -d`
Caminho da pasta para copiar logs de destino. Opcional, por padrão cria o resultado na pasta local.  Não pode ser especificado várias vezes. Se especificado várias vezes, pela última vez um será usado `./output/dump`
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
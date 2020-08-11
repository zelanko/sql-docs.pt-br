---
title: Referência de azdata extension
titleSuffix: SQL Server big data clusters
description: Artigo de referência dos comandos azdata extension.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9e2585a77c3117df8514622728d0f09df93d7bc2
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242985"
---
# <a name="azdata-extension"></a>azdata extension

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
| Comando | Descrição |
| --- | --- |
[azdata extension add](#azdata-extension-add) | Adiciona uma extensão.
[azdata extension remove](#azdata-extension-remove) | Remove uma extensão.
[azdata extension list](#azdata-extension-list) | Lista todas as extensões instaladas.
## <a name="azdata-extension-add"></a>azdata extension add
Adiciona uma extensão.
```bash
azdata extension add --source -s 
                     [--index]  
                     
[--pip-proxy]  
                     
[--pip-extra-index-urls]  
                     
[--yes -y]
```
### <a name="examples"></a>Exemplos
Adicionar a extensão por meio da URL.
```bash
azdata extension add --source https://contoso.com/some_ext-0.0.1-py2.py3-none-any.whl
```
Adicionar a extensão por meio do disco local.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl
```
Adicionar a extensão por meio do disco local e usar o proxy do Pip para dependências.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl --pip-proxy https://user:pass@proxy.server:8080
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--source -s`
Caminho para uma roda de extensão em disco ou URL para uma extensão
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--index`
URL base do Índice de Pacotes do Python (padrão: https://pypi.org/simple). Isso precisará apontar para um repositório que esteja em conformidade com o PEP 503 (a API de repositório simples) ou com um diretório local disposto no mesmo formato.
#### `--pip-proxy`
Proxy do Pip a ser usado para dependências de extensão no formato [usuário:senha@]proxy.servidor:porta
#### `--pip-extra-index-urls`
Lista separada por espaço de URLs extras dos índices de pacotes a serem usados. Isso precisará apontar para um repositório que esteja em conformidade com o PEP 503 (a API de repositório simples) ou com um diretório local disposto no mesmo formato.
#### `--yes -y`
Não solicite confirmação.
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
## <a name="azdata-extension-remove"></a>azdata extension remove
Remove uma extensão.
```bash
azdata extension remove --name -n 
                        [--yes -y]
```
### <a name="examples"></a>Exemplos
Remove uma extensão.
```bash
azdata extension remove --name some-ext
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--name -n`
Nome da extensão
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--yes -y`
Não solicite confirmação.
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
## <a name="azdata-extension-list"></a>azdata extension list
Lista todas as extensões instaladas.
```bash
azdata extension list 
```
### <a name="examples"></a>Exemplos
Listar extensões.
```bash
azdata extension list
```
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

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).

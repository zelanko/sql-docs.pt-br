---
title: Referência de azdata extension
titleSuffix: SQL Server big data clusters
description: Artigo de referência dos comandos azdata extension.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 07862632feeb4fc33f82597cf7d2b1319f320776
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358136"
---
# <a name="azdata-extension"></a>azdata extension

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
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
azdata extension add --source https://contoso.com/some_ext-0.0.1-py2.py3-none-any.whl```
Add extension from local disk.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl```
Add extension from local disk and use pip proxy for dependencies.
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

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata](..\install\deploy-install-azdata.md).


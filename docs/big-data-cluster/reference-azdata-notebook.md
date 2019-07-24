---
title: referência do azdata Notebook
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos do azdata notebook.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b96c5e06ec51f53964a28cac86f385d6b42c1dc4
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426006"
---
# <a name="azdata-notebook"></a>azdata Notebook

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos de **bloco de anotações** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md)

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[exibição do bloco de anotações azdata](#azdata-notebook-view) | Exibir um bloco de anotações.  Opção para parar no primeiro erro de execução de célula.
[execução do bloco de anotações azdata](#azdata-notebook-run) | Executar um bloco de anotações.  A execução é interrompida no primeiro erro.
## <a name="azdata-notebook-view"></a>exibição do bloco de anotações azdata
Esse comando pode pegar um arquivo de bloco de notas e converter o formato de terminal de redução, código e saída em cores.
```bash
azdata notebook view --path -p 
                     [--continue-on-error -c]
```
### <a name="examples"></a>Exemplos
Exibir bloco de anotações.  Isso mostra todas as células.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb'
```
Exibir bloco de anotações.  Isso mostrará todas as células, a menos que uma célula com erro na saída seja encontrada.  Nesse caso, a saída para.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb' --stop-on-error
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
O caminho para o bloco de anotações a ser exibido.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--continue-on-error -c`
Continue exibindo células adicionais ignorando os erros de célula encontrados na saída do bloco de anotações.  O comportamento padrão é parar em caso de erro.  Parando, fica mais fácil ver a primeira célula que encontrou um erro.
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
## <a name="azdata-notebook-run"></a>execução do bloco de anotações azdata
Esse comando cria um diretório temporário e executa o bloco de anotações fornecido nele como o diretório de trabalho.
```bash
azdata notebook run --path -p 
                    [--output-path]  
                    [--output-html]
```
### <a name="examples"></a>Exemplos
Execute o bloco de anotações.
```bash
azdata notebook run --path '/home/me/notebooks/demo_notebook.ipynb'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
O caminho do arquivo para o bloco de anotações a ser executado.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--output-path`
Caminho do diretório a ser usado para a saída do bloco de anotações.  O bloco de anotações com dados de saída e todos os arquivos gerados pelo notebook são gerados em relação a esse diretório.
#### `--output-html`
Sinalizador opcional indicatingg se o bloco de anotações de saída deve ser convertido adicionalmente no formato HTML.  Cria um segundo arquivo de saída.
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

Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para gerenciar SQL Server 2019 Big data clusters](deploy-install-azdata.md).

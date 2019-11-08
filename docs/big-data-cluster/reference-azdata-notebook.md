---
title: referência de notebook de azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos notebook de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3d9b5538170e57b09a1cf8bc4360a68187595ac2
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531669"
---
# <a name="azdata-notebook"></a>azdata notebook

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[azdata notebook view](#azdata-notebook-view) | Exibir um notebook.  Opção para parar no primeiro erro de execução de célula.
[azdata notebook run](#azdata-notebook-run) | Executar um notebook.  A execução é interrompida no primeiro erro.
## <a name="azdata-notebook-view"></a>azdata notebook view
Esse comando pode usar um arquivo de notebook e converter o markdown, o código e a saída no formato de terminal de cores.
```bash
azdata notebook view --path -p 
                     [--continue-on-error -c]
```
### <a name="examples"></a>Exemplos
Exibir notebook.  Isso mostra todas as células.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb'
```
Exibir notebook.  Isso mostra todas as células, a menos que uma célula com erro na saída seja encontrada.  Nesse caso, a saída para.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb' --stop-on-error
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
O caminho para o notebook a ser exibido.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--continue-on-error -c`
Continuar exibindo células adicionais ignorando os erros de célula encontrados na saída do notebook.  O comportamento padrão é parar mediante um erro.  Parar torna mais fácil ver a primeira célula que encontrou um erro.
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
## <a name="azdata-notebook-run"></a>azdata notebook run
Esse comando cria um diretório temporário e executa o notebook fornecido nele como o diretório de trabalho.
```bash
azdata notebook run --path -p 
                    [--output-path]  
                    [--output-html]  
                    [--arguments -a]  
                    [--interactive -i]  
                    [--clear -c]  
                    [--timeout -t]
```
### <a name="examples"></a>Exemplos
Executar notebook.
```bash
azdata notebook run --path '/home/me/notebooks/demo_notebook.ipynb'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
O caminho de arquivo para o notebook a ser executado.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--output-path`
Caminho do diretório a ser usado para a saída do notebook.  O notebook com os dados de saída e todos os arquivos gerados pelo notebook são gerados em relação a esse diretório.
#### `--output-html`
Sinalizador opcional indicando se o notebook de saída deve ser convertido adicionalmente no formato HTML.  Cria um segundo arquivo de saída.
#### `--arguments -a`
Lista opcional de argumentos do notebook para injetar na execução do notebook.  Codificado como um dicionário JSON.  Exemplo: '{"name":"value", "name2":"value2"}'
#### `--interactive -i`
Execute um notebook em um modo interativo.
#### `--clear -c`
No modo interativo, limpe o console antes de renderizar uma célula.
#### `--timeout -t`
Segundos a aguardar a conclusão da execução. O valor -1 indica espera para sempre.
`600`
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

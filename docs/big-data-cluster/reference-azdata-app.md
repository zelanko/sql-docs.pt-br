---
title: azdata app reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos app de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 793edde26ebebf9e55c5751adbedf662142280de
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426276"
---
# <a name="azdata-app"></a>azdata app

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos **app** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md).

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[azdata app template](reference-azdata-app-template.md) | Modelos.
[azdata app init](#azdata-app-init) | Iniciar rapidamente um novo esqueleto de aplicativo.
[azdata app create](#azdata-app-create) | Criar aplicativo.
[azdata app update](#azdata-app-update) | Atualizar o aplicativo.
[azdata app list](#azdata-app-list) | Listar os aplicativos.
[azdata app delete](#azdata-app-delete) | Excluir o aplicativo.
[azdata app run](#azdata-app-run) | Executar o aplicativo.
[azdata app describe](#azdata-app-describe) | Descrever o aplicativo.
## <a name="azdata-app-init"></a>azdata app init
Ajuda você a iniciar o esqueleto do novo aplicativo e/ou arquivos de especificação com base em ambientes de tempo de execução.
```bash
azdata app init [--spec -s] 
                [--name -n]  
                [--version -v]  
                [--template -t]  
                [--destination -d]  
                [--url -u]
```
### <a name="examples"></a>Exemplos
Efetuar scaffold apenas do `spec.yaml` de um novo aplicativo.
```bash
azdata app init --spec
```
Efetuar scaffold do esqueleto de um novo aplicativo R baseado no modelo `r`.
```bash
azdata app init --name reduce --template r
```
Efetuar scaffold do esqueleto de um novo aplicativo Python baseado no modelo `python`.
```bash
azdata app init --name reduce --template python
```
Efetuar scaffold do esqueleto de um novo aplicativo SSIS baseado no modelo `ssis`.
```bash
azdata app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--spec -s`
Gerar apenas o spec.yaml de um aplicativo.
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do Aplicativo.
#### `--template -t`
Nome do modelo. Para obter uma lista completa de nomes de modelos com suporte, execute `azdata app template list`
#### `--destination -d`
Onde posicionar o esqueleto do aplicativo. Padrão: o diretório de trabalho atual.
#### `--url -u`
Especificar uma localização de repositório de modelos diferente. Padrão: https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="azdata-app-create"></a>azdata app create
Criar um aplicativo.
```bash
azdata app create --spec -s 
                  
```
### <a name="examples"></a>Exemplos
Criar um novo aplicativo usando um diretório contendo uma especificação de implantação spec.yaml válida.
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--spec -s`
Caminho para um diretório com um arquivo de especificação YAML que descreve o aplicativo.
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
## <a name="azdata-app-update"></a>azdata app update
Atualizar um aplicativo.
```bash
azdata app update [--spec -s] 
                  [--yes -y]
```
### <a name="examples"></a>Exemplos
Atualizar um aplicativo existente usando um diretório contendo uma especificação de implantação spec.yaml válida.
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--spec -s`
Caminho para um diretório com um arquivo de especificação YAML que descreve o aplicativo.
#### `--yes -y`
Não solicite confirmação ao atualizar um aplicativo usando um arquivo spec.yaml do CWD.
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
## <a name="azdata-app-list"></a>azdata app list
Listar um aplicativo.
```bash
azdata app list [--name -n] 
                [--version -v]
```
### <a name="examples"></a>Exemplos
Listar o aplicativo por nome e versão.
```bash
azdata app list --name reduce  --version v1
```
Listar todas as versões do aplicativo por nome.
```bash
azdata app list --name reduce
```
Listar todas as versões do aplicativo por nome.
```bash
azdata app list
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do Aplicativo.
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
## <a name="azdata-app-delete"></a>azdata app delete
Excluir um aplicativo.
```bash
azdata app delete --name -n 
                  --version -v
```
### <a name="examples"></a>Exemplos
Excluir o aplicativo por nome e versão.
```bash
azdata app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do Aplicativo.
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
## <a name="azdata-app-run"></a>azdata app run
Executar um aplicativo.
```bash
azdata app run --name -n 
               --version -v  
               [--inputs]
```
### <a name="examples"></a>Exemplos
Executar um aplicativo sem parâmetros de entrada.
```bash
azdata app run --name reduce --version v1
```
Executar um aplicativo com um parâmetro de entrada.
```bash
azdata app run --name reduce --version v1 --inputs x=10
```
Executar um aplicativo com vários parâmetros de entrada.
```bash
azdata app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do Aplicativo.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--inputs`
Parâmetros de entrada do aplicativo em um formato CSV `name=value`.
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
## <a name="azdata-app-describe"></a>azdata app describe
Descrever um aplicativo.
```bash
azdata app describe [--spec -s] 
                    [--name -n]  
                    [--version -v]
```
### <a name="examples"></a>Exemplos
Descrever o aplicativo.
```bash
azdata app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--spec -s`
Caminho para um diretório com um arquivo de especificação YAML que descreve o aplicativo.
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do Aplicativo.
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

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).

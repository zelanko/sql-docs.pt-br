---
title: referência de aplicativo azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos do aplicativo azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 793edde26ebebf9e55c5751adbedf662142280de
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426276"
---
# <a name="azdata-app"></a>aplicativo azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos do **aplicativo** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[modelo de aplicativo azdata](reference-azdata-app-template.md) | Modelo.
[inicialização do aplicativo azdata](#azdata-app-init) | Início rápido novo esqueleto do aplicativo.
[criação de aplicativo azdata](#azdata-app-create) | Criar aplicativo.
[atualização do aplicativo azdata](#azdata-app-update) | Atualizar aplicativo.
[lista de aplicativos azdata](#azdata-app-list) | Listar aplicativo (s).
[exclusão do aplicativo azdata](#azdata-app-delete) | Excluir aplicativo.
[execução do aplicativo azdata](#azdata-app-run) | Execute o aplicativo.
[Descrição do aplicativo azdata](#azdata-app-describe) | Descreva o aplicativo.
## <a name="azdata-app-init"></a>inicialização do aplicativo azdata
Ajuda você a início rápido o novo esqueleto de aplicativo e/ou arquivos de especificação com base em ambientes de tempo de execução.
```bash
azdata app init [--spec -s] 
                [--name -n]  
                [--version -v]  
                [--template -t]  
                [--destination -d]  
                [--url -u]
```
### <a name="examples"></a>Exemplos
Scaffold apenas um novo `spec.yaml` aplicativo.
```bash
azdata app init --spec
```
Scaffold um novo esqueleto de aplicativo R baseado no `r` modelo.
```bash
azdata app init --name reduce --template r
```
Scaffold um novo esqueleto de aplicativo Python com base `python` no modelo.
```bash
azdata app init --name reduce --template python
```
Scaffold um novo esqueleto de aplicativo do SSIS com `ssis` base no modelo.
```bash
azdata app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--spec -s`
Gere apenas um aplicativo spec. YAML.
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do aplicativo.
#### `--template -t`
Nome do modelo. Para obter uma lista completa de nomes de modelos com suporte, execute`azdata app template list`
#### `--destination -d`
Onde posicionar o esqueleto do aplicativo. Padrão: diretório de trabalho atual.
#### `--url -u`
Especifique um local de repositório de modelos diferente. Os https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="azdata-app-create"></a>criação de aplicativo azdata
Crie um aplicativo.
```bash
azdata app create --spec -s 
                  
```
### <a name="examples"></a>Exemplos
Crie um novo aplicativo a partir de um diretório que contenha uma especificação de implantação spec. YAML válida.
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--spec -s`
Caminho para um diretório com um arquivo de especificação de YAML que descreve o aplicativo.
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
## <a name="azdata-app-update"></a>atualização do aplicativo azdata
Atualizar um aplicativo.
```bash
azdata app update [--spec -s] 
                  [--yes -y]
```
### <a name="examples"></a>Exemplos
Atualize um aplicativo existente de um diretório que contém uma especificação de implantação spec. YAML válida.
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--spec -s`
Caminho para um diretório com um arquivo de especificação de YAML que descreve o aplicativo.
#### `--yes -y`
Não solicite confirmação ao atualizar um aplicativo do arquivo spec. YAML do CWD.
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
## <a name="azdata-app-list"></a>lista de aplicativos azdata
Listar um ou mais aplicativos.
```bash
azdata app list [--name -n] 
                [--version -v]
```
### <a name="examples"></a>Exemplos
Listar aplicativo por nome e versão.
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
Versão do aplicativo.
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
## <a name="azdata-app-delete"></a>exclusão do aplicativo azdata
Excluir um aplicativo.
```bash
azdata app delete --name -n 
                  --version -v
```
### <a name="examples"></a>Exemplos
Excluir aplicativo por nome e versão.
```bash
azdata app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do aplicativo.
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
## <a name="azdata-app-run"></a>execução do aplicativo azdata
Executar um aplicativo.
```bash
azdata app run --name -n 
               --version -v  
               [--inputs]
```
### <a name="examples"></a>Exemplos
Execute o aplicativo sem parâmetros de entrada.
```bash
azdata app run --name reduce --version v1
```
Execute o aplicativo com um parâmetro de entrada.
```bash
azdata app run --name reduce --version v1 --inputs x=10
```
Execute o aplicativo com vários parâmetros de entrada.
```bash
azdata app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do aplicativo.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--inputs`
Parâmetros de entrada do aplicativo em `name=value` um formato CSV.
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
## <a name="azdata-app-describe"></a>Descrição do aplicativo azdata
Descreva um aplicativo.
```bash
azdata app describe [--spec -s] 
                    [--name -n]  
                    [--version -v]
```
### <a name="examples"></a>Exemplos
Descreva o aplicativo.
```bash
azdata app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--spec -s`
Caminho para um diretório com um arquivo de especificação de YAML que descreve o aplicativo.
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do aplicativo.
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

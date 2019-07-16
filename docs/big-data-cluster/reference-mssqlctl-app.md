---
title: referência de aplicativo mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência de comandos do aplicativo mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a14b548ed8c16776b4883e54f3ca47588dbb3e6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958201"
---
# <a name="mssqlctl-app"></a>Aplicativo do mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **app** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[modelo de aplicativo mssqlctl](reference-mssqlctl-app-template.md) | modelos.
[inicialização de aplicativo mssqlctl](#mssqlctl-app-init) | Início rápido novo esqueleto do aplicativo.
[Criar aplicativo mssqlctl](#mssqlctl-app-create) | Crie aplicativo.
[atualização do aplicativo mssqlctl](#mssqlctl-app-update) | Atualize o aplicativo.
[lista de aplicativos mssqlctl](#mssqlctl-app-list) | Lista de aplicativos.
[exclusão de aplicativo mssqlctl](#mssqlctl-app-delete) | Exclua o aplicativo.
[execução do aplicativo mssqlctl](#mssqlctl-app-run) | Execute o aplicativo.
[aplicativo mssqlctl descrevem](#mssqlctl-app-describe) | Descreva o aplicativo.
## <a name="mssqlctl-app-init"></a>inicialização de aplicativo mssqlctl
Ajuda você a kickstart esqueleto de aplicativo nova e/ou arquivos de especificações, com base em ambientes de tempo de execução.
```bash
mssqlctl app init [--spec -s] 
                  [--name -n]  
                  [--version -v]  
                  [--template -t]  
                  [--destination -d]  
                  [--url -u]
```
### <a name="examples"></a>Exemplos
Criar o scaffolding de um novo aplicativo `spec.yaml` apenas.
```bash
mssqlctl app init --spec
```
Gerar automaticamente um esqueleto de aplicativo de aplicativo R novo com base no `r` modelo.
```bash
mssqlctl app init --name reduce --template r
```
Gerar automaticamente um esqueleto de aplicativo de aplicativo Python novo com base no `python` modelo.
```bash
mssqlctl app init --name reduce --template python
```
Gerar automaticamente um esqueleto de aplicativo de aplicativo SSIS novo com base no `ssis` modelo.
```bash
mssqlctl app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--spec -s`
Gere apenas um spec.yaml do aplicativo.
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do aplicativo.
#### `--template -t`
Nome do modelo. Para obter uma lista completa desativar nomes de modelo com suporte de execução `mssqlctl app template list`
#### `--destination -d`
Onde colocar o esqueleto do aplicativo. Padrão: diretório de trabalho atual.
#### `--url -u`
Especifique um local de repositório de modelo diferente. Padrão: https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="mssqlctl-app-create"></a>Criar aplicativo mssqlctl
Crie um aplicativo.
```bash
mssqlctl app create --spec -s 
                    
```
### <a name="examples"></a>Exemplos
Crie um novo aplicativo de um diretório que contém uma especificação de implantação spec.yaml válido.
```bash
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--spec -s`
Caminho para um diretório com um arquivo de especificações YAML descrevendo o aplicativo.
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
## <a name="mssqlctl-app-update"></a>atualização do aplicativo mssqlctl
Atualize um aplicativo.
```bash
mssqlctl app update [--spec -s] 
                    [--yes -y]
```
### <a name="examples"></a>Exemplos
Atualize um aplicativo existente de um diretório que contém uma especificação de implantação spec.yaml válido.
```bash
mssqlctl app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--spec -s`
Caminho para um diretório com um arquivo de especificações YAML descrevendo o aplicativo.
#### `--yes -y`
Não solicite confirmação ao atualizar um aplicativo do arquivo de spec.yaml do CWD.
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
## <a name="mssqlctl-app-list"></a>lista de aplicativos mssqlctl
Listar um aplicativo (s).,
```bash
mssqlctl app list [--name -n] 
                  [--version -v]
```
### <a name="examples"></a>Exemplos
Aplicativo de lista por nome e versão.
```bash
mssqlctl app list --name reduce  --version v1
```
Liste todas as versões de aplicativo por nome.
```bash
mssqlctl app list --name reduce
```
Liste todas as versões de aplicativo por nome.
```bash
mssqlctl app list
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do aplicativo.
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
## <a name="mssqlctl-app-delete"></a>exclusão de aplicativo mssqlctl
Exclua um aplicativo.
```bash
mssqlctl app delete --name -n 
                    --version -v
```
### <a name="examples"></a>Exemplos
Exclua aplicativo por nome e versão.
```bash
mssqlctl app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do aplicativo.
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
## <a name="mssqlctl-app-run"></a>execução do aplicativo mssqlctl
Execute um aplicativo.
```bash
mssqlctl app run --name -n 
                 --version -v  
                 [--inputs]
```
### <a name="examples"></a>Exemplos
Execute o aplicativo sem parâmetros de entrada.
```bash
mssqlctl app run --name reduce --version v1
```
Execute o aplicativo com o parâmetro de entrada 1.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10
```
Execute o aplicativo com vários parâmetros de entrada.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do aplicativo.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--inputs`
Aplicativo de parâmetros de entrada em um CSV `name=value` formato.
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
## <a name="mssqlctl-app-describe"></a>aplicativo mssqlctl descrevem
Descreva um aplicativo.
```bash
mssqlctl app describe [--spec -s] 
                      [--name -n]  
                      [--version -v]
```
### <a name="examples"></a>Exemplos
Descreva o aplicativo.
```bash
mssqlctl app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--spec -s`
Caminho para um diretório com um arquivo de especificações YAML descrevendo o aplicativo.
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do aplicativo.
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
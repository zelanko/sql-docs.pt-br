---
title: referência de aplicativo mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos do aplicativo mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d0df3e9ca007fb6546310236f4c23d1775687cc5
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388392"
---
# <a name="mssqlctl-app"></a>Aplicativo do mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos do **aplicativo** na ferramenta **mssqlctl** . Para obter mais informações sobre outros comandos do **mssqlctl** , consulte [referência do mssqlctl](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[modelo de aplicativo mssqlctl](reference-mssqlctl-app-template.md) | Modelo.
[inicialização do aplicativo mssqlctl](#mssqlctl-app-init) | Início rápido novo esqueleto do aplicativo.
[criação de aplicativo mssqlctl](#mssqlctl-app-create) | Criar aplicativo.
[atualização do aplicativo mssqlctl](#mssqlctl-app-update) | Atualizar aplicativo.
[lista de aplicativos mssqlctl](#mssqlctl-app-list) | Listar aplicativo (s).
[exclusão do aplicativo mssqlctl](#mssqlctl-app-delete) | Excluir aplicativo.
[execução do aplicativo mssqlctl](#mssqlctl-app-run) | Execute o aplicativo.
[Descrição do aplicativo mssqlctl](#mssqlctl-app-describe) | Descreva o aplicativo.
## <a name="mssqlctl-app-init"></a>inicialização do aplicativo mssqlctl
Ajuda você a início rápido o novo esqueleto de aplicativo e/ou arquivos de especificação com base em ambientes de tempo de execução.
```bash
mssqlctl app init [--spec -s] 
                  [--name -n]  
                  [--version -v]  
                  [--template -t]  
                  [--destination -d]  
                  [--url -u]
```
### <a name="examples"></a>Exemplos
Scaffold apenas um novo `spec.yaml` aplicativo.
```bash
mssqlctl app init --spec
```
Scaffold um novo esqueleto de aplicativo R baseado no `r` modelo.
```bash
mssqlctl app init --name reduce --template r
```
Scaffold um novo esqueleto de aplicativo Python com base `python` no modelo.
```bash
mssqlctl app init --name reduce --template python
```
Scaffold um novo esqueleto de aplicativo do SSIS com `ssis` base no modelo.
```bash
mssqlctl app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--spec -s`
Gere apenas um aplicativo spec. YAML.
#### `--name -n`
Nome do aplicativo.
#### `--version -v`
Versão do aplicativo.
#### `--template -t`
Nome do modelo. Para obter uma lista completa de nomes de modelos com suporte, execute`mssqlctl app template list`
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
## <a name="mssqlctl-app-create"></a>criação de aplicativo mssqlctl
Crie um aplicativo.
```bash
mssqlctl app create --spec -s 
                    
```
### <a name="examples"></a>Exemplos
Crie um novo aplicativo a partir de um diretório que contenha uma especificação de implantação spec. YAML válida.
```bash
mssqlctl app create --spec /path/to/dir/with/spec/yaml
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
## <a name="mssqlctl-app-update"></a>atualização do aplicativo mssqlctl
Atualizar um aplicativo.
```bash
mssqlctl app update [--spec -s] 
                    [--yes -y]
```
### <a name="examples"></a>Exemplos
Atualize um aplicativo existente de um diretório que contém uma especificação de implantação spec. YAML válida.
```bash
mssqlctl app update --spec /path/to/dir/with/spec/yaml    
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
## <a name="mssqlctl-app-list"></a>lista de aplicativos mssqlctl
Listar um ou mais aplicativos.
```bash
mssqlctl app list [--name -n] 
                  [--version -v]
```
### <a name="examples"></a>Exemplos
Listar aplicativo por nome e versão.
```bash
mssqlctl app list --name reduce  --version v1
```
Listar todas as versões do aplicativo por nome.
```bash
mssqlctl app list --name reduce
```
Listar todas as versões do aplicativo por nome.
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
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-app-delete"></a>exclusão do aplicativo mssqlctl
Excluir um aplicativo.
```bash
mssqlctl app delete --name -n 
                    --version -v
```
### <a name="examples"></a>Exemplos
Excluir aplicativo por nome e versão.
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
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-app-run"></a>execução do aplicativo mssqlctl
Executar um aplicativo.
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
Execute o aplicativo com um parâmetro de entrada.
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
## <a name="mssqlctl-app-describe"></a>Descrição do aplicativo mssqlctl
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

Para obter mais informações sobre outros comandos do **mssqlctl** , consulte [referência do mssqlctl](reference-mssqlctl.md). Para obter mais informações sobre como instalar a ferramenta **mssqlctl** , consulte [instalar o mssqlctl para gerenciar SQL Server 2019 Big data clusters](deploy-install-mssqlctl.md).
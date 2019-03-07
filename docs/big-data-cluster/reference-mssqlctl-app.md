---
title: referência de aplicativo mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Artigo de referência de comandos do aplicativo mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fa2b43c352fbab39cd00112b9646a87a2b752f5b
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527249"
---
# <a name="mssqlctl-app"></a>aplicativo mssqlctl

O artigo a seguir fornece referência para o **app** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [create](#create) | Crie aplicativo. |
| [delete](#delete) | Exclua o aplicativo. |
| [describe](#describe) | Descreva o aplicativo. |
| [init](#init) | Início rápido novo esqueleto do aplicativo. |
| [list](#list) | Lista de aplicativos. |
| [run](#run) | Execute o aplicativo. |
| [update](#update) | Atualize o aplicativo. |
| [template](reference-mssqlctl-app-template.md) | Comandos de modelo. |

## <a id="create"></a> Criar aplicativo mssqlctl

Crie aplicativo.

```
mssqlctl app create
   --assets
   --code
   --description
   --entrypoint
   --inputs
   --name
   --outputs
   --runtime
   --spec
   --version
   --yes
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--assets -a** | Lista de ativos de arquivos de aplicativo adicionais a serem incluídos. |
| **--code -c** | Caminho do arquivo de código R ou Python. |
| **– Descrição -d** | Descrição do aplicativo. |
| **--entrypoint** |  |
| **– entradas** | Esquema de parâmetro de entrada. |
| **--name -n** | Nome do aplicativo. |
| **--outputs** | Esquema de parâmetros de saída. |
| **– o tempo de execução - r** | Tempo de execução do aplicativo.  Valores permitidos: Mleap, Python, R, SSIS. |
| **--spec -s** | Caminho para um diretório com um arquivo de especificações YAML descrevendo o aplicativo. |
| **– versão - v** | Versão do aplicativo. |
| **– Sim -y** | Não solicite confirmação ao criar um aplicativo do arquivo de spec.yaml do CWD. |

### <a name="examples"></a>Exemplos

Crie um novo aplicativo por meio de spec.yaml (recomendado).

```
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```

Crie um novo embutida de aplicativo do Python usando argumentos.

```
mssqlctl app create --name add --version v1 --inputs x=float, y=float --outputs result=float --runtime Python --code add.py  --init init.py
```

Crie um novo embutida de aplicativo do R usando os argumentos.

```
mssqlctl app create --name add --version v1 --inputs x=numeric, y=numeric --outputs result=numeric --runtime R --code add.R  --init init.R
```

Crie uma novo aplicativo de R em linha com ativos de arquivos adicionais a serem incluídos.

```
mssqlctl app create --name add --version v1 --runtime R --code  add.R --assets file.RData,/path/to/more/files
```

## <a id="delete"></a> exclusão de aplicativo mssqlctl

Exclua o aplicativo.

```
mssqlctl app delete
   --name
   --version
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--name -n** | Nome do aplicativo. |
| **– versão - v** | Versão do aplicativo. |

### <a name="examples"></a>Exemplos

Exclua aplicativo por nome e versão.

```
mssqlctl app delete --name reduce --version v1
```

## <a id="describe"></a> mssqlctl app describe

Descreva o aplicativo.

```
mssqlctl app describe
   --name
   --spec
   --version
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--name -n** | Nome do aplicativo. |
| **--spec -s** | Caminho para um diretório com um arquivo de especificações YAML descrevendo o aplicativo. |
| **– versão - v** | Versão do aplicativo. |

### <a name="examples"></a>Exemplos

Descreva o aplicativo.

```
mssqlctl app describe --name reduce --version v1
```

## <a id="init"></a> inicialização de aplicativo mssqlctl

Início rápido novo esqueleto do aplicativo.

```
mssqlctl app init
   --destination
   --name
   --spec
   --template
   --url
   --version
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--destination -d** | Onde colocar o esqueleto do aplicativo. Padrão: diretório de trabalho atual. |
| **--name -n** | Nome do aplicativo. |
| **--spec -s** | Gere apenas um spec.yaml do aplicativo. |
| **-modelo -t** | Nome do modelo. Para obter uma lista completa desativar nomes de modelo com suporte, execute `mssqlctl app template list`. |
| **--url -u** | Especifique um local de repositório de modelo diferente. Padrão: https://github.com/Microsoft/sql-server-samples.git. |
| **– versão - v** | Versão do aplicativo. |

### <a name="examples"></a>Exemplos

Criar o scaffolding de um novo aplicativo `spec.yaml` apenas.

```
mssqlctl app init --spec
```

Gerar automaticamente um esqueleto de aplicativo de aplicativo R novo com base no `r` modelo.

```
mssqlctl app init --name reduce --template r
```

Gerar automaticamente um esqueleto de aplicativo de aplicativo Python novo com base no `python` modelo.

```
mssqlctl app init --name reduce --template python
```

Gerar automaticamente um esqueleto de aplicativo de aplicativo SSIS novo com base no `ssis` modelo.

```
mssqlctl app init --name reduce --template ssis
```

## <a id="list"></a> lista de aplicativos mssqlctl

Lista de aplicativos.

```
mssqlctl app list
   --name
   --version
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--name -n** | Nome do aplicativo. |
| **– versão - v** | Versão do aplicativo. |

### <a name="examples"></a>Exemplos

Aplicativo de lista por nome e versão.

```
mssqlctl app list --name reduce  --version v1
```

Liste todas as versões de aplicativo por nome.

```
mssqlctl app list --name reduce
```

Liste todos os aplicativos.

```
mssqlctl app list
```

## <a id="run"></a> execução do aplicativo mssqlctl

Execute o aplicativo.

```
mssqlctl app run
   --name
   --version
   --inputs
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--name -n** | Nome do aplicativo. |
| **– versão - v** | Versão do aplicativo. |
| **– entradas** | Aplicativo de parâmetros de entrada em um CSV `name=value` formato. |

### <a name="examples"></a>Exemplos

Execute o aplicativo sem parâmetros de entrada.

```
mssqlctl app run --name reduce --version v1
```

Execute o aplicativo com o parâmetro de entrada 1.

```
mssqlctl app run --name reduce --version v1 --inputs x=10
```

Execute o aplicativo com vários parâmetros de entrada.

```
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6
```

## <a id="update"></a> atualização do aplicativo mssqlctl

Atualize o aplicativo.

```
mssqlctl app update
   --spec
   --yes
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--spec -s** | Caminho para um diretório com um arquivo de especificações YAML descrevendo o aplicativo. |
| **– Sim -y** | Não solicite confirmação ao atualizar um aplicativo do arquivo de spec.yaml do CWD. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md). Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).
---
title: referência de sql mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de sql mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 536d4712a6ccb288ca60c038a37e99c2be8a5eba
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394198"
---
# <a name="mssqlctl-sql"></a>mssqlctl sql

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **sql** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[mssqlctl sql shell](#mssqlctl-sql-shell) | A CLI do banco de dados SQL permite que o usuário interaja com o SQL Server por meio do T-SQL.
[mssqlctl sql query](#mssqlctl-sql-query) | O comando de consulta permite a execução de uma consulta T-SQL.
## <a name="mssqlctl-sql-shell"></a>mssqlctl sql shell
A CLI do banco de dados SQL permite que o usuário interaja com o SQL Server por meio do T-SQL.
```bash
mssqlctl sql shell 
```
### <a name="examples"></a>Exemplos
Linha de comando de exemplo para iniciar a experiência interativa.
```bash
mssqlctl sql shell
```
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
## <a name="mssqlctl-sql-query"></a>consulta de sql mssqlctl
O comando de consulta permite a execução de uma consulta T-SQL.
```bash
mssqlctl sql query --database -d 
                   -q
```
### <a name="examples"></a>Exemplos
Selecione a lista de nomes de tabelas.  Padrões de banco de dados mestre.
```bash
mssqlctl sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--database -d`
Banco de dados para executar a consulta.  O padrão é mestre.
#### `-q`
Consulta de T-SQL para executar.
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

Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).
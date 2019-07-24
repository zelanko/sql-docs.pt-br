---
title: referência SQL do azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata SQL.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 90512592901fcf83e4697b5eefc80a6df7aeb032
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426016"
---
# <a name="azdata-sql"></a>azdata SQL

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos **SQL** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[Shell do SQL do azdata](#azdata-sql-shell) | A CLI do banco de BD SQL permite que o usuário interaja com SQL Server por meio de T-SQL.
[consulta SQL azdata](#azdata-sql-query) | O comando de consulta permite a execução de uma consulta T-SQL.
## <a name="azdata-sql-shell"></a>Shell do SQL do azdata
A CLI do banco de BD SQL permite que o usuário interaja com SQL Server por meio de T-SQL.
```bash
azdata sql shell 
```
### <a name="examples"></a>Exemplos
Exemplo de linha de comando para iniciar a experiência interativa.
```bash
azdata sql shell
```
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
## <a name="azdata-sql-query"></a>consulta SQL azdata
O comando de consulta permite a execução de uma consulta T-SQL.
```bash
azdata sql query --database -d 
                 -q
```
### <a name="examples"></a>Exemplos
Selecione a lista de nomes de tabelas.  O banco de dados usa como padrão o mestre.
```bash
azdata sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--database -d`
Banco de dados no qual executar a consulta.  O padrão é mestre.
#### `-q`
Consulta T-SQL a ser executada.
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

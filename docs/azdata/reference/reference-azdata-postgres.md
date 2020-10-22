---
title: Referência do azdata postgres
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata postgres.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ab6518677ffdbba92ec51da9f3c0fb7dbb0af0d7
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358125"
---
# <a name="azdata-postgres"></a>azdata postgres

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata postgres shell](#azdata-postgres-shell) | Uma interface de shell de linha de comando para Postgres. Veja https://www.pgcli.com/
[azdata postgres query](#azdata-postgres-query) | O comando de consulta permite a execução de comandos do PostgreSQL em uma sessão de banco de dados.
## <a name="azdata-postgres-shell"></a>azdata postgres shell
Uma interface de shell de linha de comando para Postgres. Veja https://www.pgcli.com/
```bash
azdata postgres shell [--dbname -d] 
                      [--host]  
                      
[--port -p]  
                      
[--password -w]  
                      
[--no-password]  
                      
[--single-connection]  
                      
[--username -u]  
                      
[--pgclirc]  
                      
[--dsn]  
                      
[--list-dsn]  
                      
[--row-limit]  
                      
[--less-chatty]  
                      
[--prompt]  
                      
[--prompt-dsn]  
                      
[--list -l]  
                      
[--auto-vertical-output]  
                      
[--warn]  
                      
[--no-warn]
```
### <a name="examples"></a>Exemplos
Exemplo de linha de comando para iniciar a experiência interativa.
```bash
azdata postgres shell
```
Exemplo de linha de comando usando um banco de dados e um usuário fornecidos
```bash
azdata postgres shell --dbname <database> --username <username> --host <host>
```
Exemplo de linha de comando para começar a usar uma cadeia de conexão completa.
```bash
azdata postgres shell --dbname postgres://user:passw0rd@example.com:5432/master 
```
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--dbname -d`
Nome do banco de dados ao qual se conectar.
#### `--host`
Endereço de host do banco de dados Postgres.
#### `--port -p`
Número da porta na qual a instância do Postgres está escutando.
#### `--password -w`
Forçar a solicitação de senha.
#### `--no-password`
Nunca solicitar uma senha.
#### `--single-connection`
Não usar uma conexão separada para as conclusões.
#### `--username -u`
Nome de usuário para se conectar ao banco de dados Postgres.
#### `--pgclirc`
Local do arquivo pgclirc.
#### `--dsn`
Usar o DSN configurado na seção [alias_dsn] do arquivo pgclirc.
#### `--list-dsn`
Lista de DSNs configurados na seção [alias_dsn] do arquivo pgclirc.
#### `--row-limit`
Definir o limite para o prompt do limite de linha. Usar 0 para desabilitar o prompt.
#### `--less-chatty`
Ignorar a introdução na inicialização e o adeus ao sair.
#### `--prompt`
Formato de prompt (Padrão: "\u@\h:\d> ").
#### `--prompt-dsn`
Formato de prompt para conexões usando aliases DSN (Padrão: "\u@\h:\d> ").
#### `--list -l`
Listar os bancos de dados disponíveis, depois sair.
#### `--auto-vertical-output`
Alternar automaticamente para o modo de saída vertical se o resultado for mais largo do que a largura do terminal.
#### `--warn`
Avisar antes de executar uma consulta destrutiva.
#### `--no-warn`
Avisar antes de executar uma consulta destrutiva.
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
## <a name="azdata-postgres-query"></a>azdata postgres query
O comando de consulta permite a execução de comandos do PostgreSQL em uma sessão de banco de dados.
```bash
azdata postgres query --q -q 
                      [--host]  
                      
[--dbname -d]  
                      
[--port -p]  
                      
[--username -u]
```
### <a name="examples"></a>Exemplos
Listar todas as tabelas em information_schema.
```bash
azdata postgres query --host <host> --username <username> -q "SELECT * FROM information_schema.tables"
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--q -q`
A consulta PostgreSQL a ser executada.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--host`
Endereço de host do banco de dados Postgres.
`localhost`
#### `--dbname -d`
Banco de dados nos quais executar a consulta.
#### `--port -p`
Número da porta na qual a instância do Postgres está escutando.
`5432`
#### `--username -u`
Nome de usuário para se conectar ao banco de dados Postgres.
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


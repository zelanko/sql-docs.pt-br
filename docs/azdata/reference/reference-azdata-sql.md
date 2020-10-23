---
title: azdata sql reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos sql de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 794c7be56eaa0591d120b4fea40a725fdeecaac1
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358104"
---
# <a name="azdata-sql"></a>azdata sql

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | A CLI do SQL permite que o usuário interaja com o SQL Server e com o SQL do Azure por meio de T-SQL.
[azdata sql query](#azdata-sql-query) | A CLI do SQL permite que o usuário interaja com o SQL Server e com o SQL do Azure por meio de T-SQL.
## <a name="azdata-sql-shell"></a>azdata sql shell
A CLI do SQL permite que o usuário interaja com o SQL Server e com o SQL do Azure por meio de T-SQL.
```bash
azdata sql shell [--username -u] 
                 [--database -d]  
                 
[--server -s]  
                 
[--integrated -e]  
                 
[--mssqlclirc]  
                 
[--row-limit]  
                 
[--less-chatty]  
                 
[--auto-vertical-output]  
                 
[--encrypt -n]  
                 
[--trust-server-certificate -c]  
                 
[--connect-timeout -l]  
                 
[--application-intent -k]  
                 
[--multi-subnet-failover -m]  
                 
[--packet-size]  
                 
[--dac-connection -a]  
                 
[--input-file -i]  
                 
[--output-file]  
                 
[--enable-sqltoolsservice-logging]  
                 
[--prompt]
```
### <a name="examples"></a>Exemplos
Exemplo de linha de comando para iniciar a experiência interativa.
```bash
azdata sql shell
```
Exemplo de linha de comando usando um servidor, usuário e banco de dados fornecidos
```bash
azdata sql shell --server localhost --username sa --database master         
```
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--username -u`
Nome de usuário para se conectar ao banco de dados.
#### `--database -d`
Nome do banco de dados ao qual se conectar.
#### `--server -s`
Nome ou endereço da instância do SQL Server.
#### `--integrated -e`
Usar a autenticação integrada no Windows.
#### `--mssqlclirc`
Local do arquivo de configuração mssqlclirc.
#### `--row-limit`
Definir o limite para o prompt do limite de linha. Usar 0 para desabilitar o prompt.
#### `--less-chatty`
Ignorar a introdução na inicialização e o adeus ao sair.
#### `--auto-vertical-output`
Alternar automaticamente para o modo de saída vertical se o resultado for mais largo do que a largura do terminal.
#### `--encrypt -n`
O SQL Server usará a criptografia SSL para todos os dados se o servidor tiver um certificado instalado.
#### `--trust-server-certificate -c`
O canal será criptografado enquanto ignora a passagem pela cadeia de certificados para validar a confiança.
#### `--connect-timeout -l`
Tempo em segundos para aguardar por uma conexão com o servidor antes de encerrar a solicitação.
#### `--application-intent -k`
Declara o tipo de carga de trabalho de aplicativo ao se conectar a um banco de dados em um Grupo de Disponibilidade do SQL Server.
#### `--multi-subnet-failover -m`
Se o aplicativo estiver se conectando aos AG (grupos de disponibilidade) AlwaysOn em sub-redes diferentes, essa configuração fornecerá detecção e conexão mais rápidas ao servidor ativo no momento.
#### `--packet-size`
O tamanho em bytes dos pacotes de rede usados para se comunicar com o SQL Server.
#### `--dac-connection -a`
Conecta-se ao SQL Server com uma conexão de administrador dedicada.
#### `--input-file -i`
Identifica o arquivo que contém um lote de instruções SQL ou procedimentos armazenados.
#### `--output-file`
Especifica o arquivo que recebe a saída de uma consulta.
#### `--enable-sqltoolsservice-logging`
Habilita o log de diagnóstico para o SqlToolsService.
#### `--prompt`
Formato do prompt (padrão: \d>
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
## <a name="azdata-sql-query"></a>azdata sql query
A CLI do SQL permite que o usuário interaja com o SQL Server e com o SQL do Azure por meio de T-SQL.
```bash
azdata sql query -q 
                 [--database -d]  
                 
[--username -u]  
                 
[--server -s]  
                 
[--integrated -e]
```
### <a name="examples"></a>Exemplos
Exemplo de linha de comando para selecionar a lista de nomes de tabelas.
```bash
azdata sql query --server localhost --username sa --database master -q "SELECT name FROM SYS.TABLES"
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `-q`
A consulta de T-SQL a ser executada.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--database -d`
Nome do banco de dados ao qual se conectar.
`master`
#### `--username -u`
Nome de usuário para se conectar ao banco de dados.
#### `--server -s`
Nome ou endereço da instância do SQL Server.
#### `--integrated -e`
Usar a autenticação integrada no Windows.
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

Para saber mais sobre como instalar a ferramenta **azdata**, confira [Instalar azdata](..\install\deploy-install-azdata.md).


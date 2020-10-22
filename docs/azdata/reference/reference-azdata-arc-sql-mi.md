---
title: Referência do azdata arc sql mi
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata arc sql mi.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 234a990cde52a6fd051410d30000413b9acfa3a0
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358674"
---
# <a name="azdata-arc-sql-mi"></a>azdata arc sql mi

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata arc sql mi create](#azdata-arc-sql-mi-create) | Criar uma Instância Gerenciada de SQL.
[azdata arc sql mi edit](#azdata-arc-sql-mi-edit) | Editar a configuração de uma Instância Gerenciada de SQL.
[azdata arc sql mi delete](#azdata-arc-sql-mi-delete) | Excluir uma instância gerenciada de SQL.
[azdata arc sql mi show](#azdata-arc-sql-mi-show) | Mostrar os detalhes de uma Instância Gerenciada de SQL.
[azdata arc sql mi list](#azdata-arc-sql-mi-list) | Listar Instâncias Gerenciadas de SQL.
[azdata arc sql mi config](reference-azdata-arc-sql-mi-config.md) | Comandos de configuração.
## <a name="azdata-arc-sql-mi-create"></a>azdata arc sql mi create
Para definir a senha da Instância Gerenciada de SQL, defina a variável de ambiente AZDATA_PASSWORD
```bash
azdata arc sql mi create --name -n 
                         [--path]  
                         
[--cores-limit -cl]  
                         
[--cores-request -cr]  
                         
[--memory-limit -ml]  
                         
[--memory-request -mr]  
                         
[--storage-class-data -scd]  
                         
[--storage-class-logs -scl]  
                         
[--storage-class-data-logs -scdl]  
                         
[--storage-class-backups -scb]  
                         
[--volume-size-data -vsd]  
                         
[--volume-size-logs -vsl]  
                         
[--volume-size-data-logs -vsdl]  
                         
[--volume-size-backups -vsb]  
                         
[--no-external-endpoint]  
                         
[--dev]  
                         
[--no-wait]
```
### <a name="examples"></a>Exemplos
Criar uma Instância Gerenciada de SQL.
```bash
azdata arc sql mi create -n sqlmi1
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--name -n`
O nome da Instância Gerenciada de SQL.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--path`
O caminho para o arquivo src para o arquivo json da Instância Gerenciada de SQL.
#### `--cores-limit -cl`
O limite de núcleos da instância gerenciada como um inteiro.
#### `--cores-request -cr`
A solicitação de núcleos da instância gerenciada como um inteiro.
#### `--memory-limit -ml`
O limite da capacidade da instância gerenciada como um inteiro.
#### `--memory-request -mr`
A solicitação para a capacidade da instância gerenciada como uma quantidade de memória em GBs representada por um inteiro.
#### `--storage-class-data -scd`
A classe de armazenamento a ser usada para dados (.mdf). Se nenhum valor for especificado, nenhuma classe de armazenamento será especificada, o que resultará no uso da classe de armazenamento padrão pelo Kubernetes.
#### `--storage-class-logs -scl`
A classe de armazenamento a ser usada para logs (/var/log). Se nenhum valor for especificado, nenhuma classe de armazenamento será especificada, o que resultará no uso da classe de armazenamento padrão pelo Kubernetes.
#### `--storage-class-data-logs -scdl`
A classe de armazenamento a ser usada para logs de banco de dados (.ldf). Se nenhum valor for especificado, nenhuma classe de armazenamento será especificada, o que resultará no uso da classe de armazenamento padrão pelo Kubernetes.
#### `--storage-class-backups -scb`
A classe de armazenamento a ser usada para backups (/var/opt/mssql/backups). Se nenhum valor for especificado, nenhuma classe de armazenamento será especificada, o que resultará no uso da classe de armazenamento padrão pelo Kubernetes.
#### `--volume-size-data -vsd`
O tamanho do volume de armazenamento a ser usado para os dados como um número positivo seguido por Ki (quilobytes), Mi (megabytes) ou Gi (gigabytes).
#### `--volume-size-logs -vsl`
O tamanho do volume de armazenamento a ser usado para os logs como um número positivo seguido por Ki (quilobytes), Mi (megabytes) ou Gi (gigabytes).
#### `--volume-size-data-logs -vsdl`
O tamanho do volume de armazenamento a ser usado para os logs de dados como um número positivo seguido por Ki (quilobytes), Mi (megabytes) ou Gi (gigabytes).
#### `--volume-size-backups -vsb`
O tamanho do volume de armazenamento a ser usado para backups como um número positivo seguido por Ki (quilobytes), Mi (megabytes) ou Gi (gigabytes).
#### `--no-external-endpoint`
Se especificado, nenhum serviço externo será criado. Caso contrário, um serviço externo será criado usando o mesmo tipo de serviço que o controlador de dados.
#### `--dev`
Se isso for especificado, será considerado uma instância de desenvolvimento e não será cobrado.
#### `--no-wait`
Se for fornecido, o comando não aguardará que a instância esteja em um estado pronto antes de retornar.
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
## <a name="azdata-arc-sql-mi-edit"></a>azdata arc sql mi edit
Editar a configuração de uma Instância Gerenciada de SQL.
```bash
azdata arc sql mi edit --name -n 
                       [--path]  
                       
[--cores-limit -cl]  
                       
[--cores-request -cr]  
                       
[--memory-limit -ml]  
                       
[--memory-request -mr]  
                       
[--dev]  
                       
[--no-wait]
```
### <a name="examples"></a>Exemplos
Editar a configuração de uma Instância Gerenciada de SQL.
```bash
azdata arc sql mi edit --path ./spec.json -n sqlmi1
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--name -n`
O nome da Instância Gerenciada de SQL sendo editada. O nome sob o qual sua instância está implantada não pode ser alterado.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--path`
O caminho para o arquivo src para o arquivo json da Instância Gerenciada de SQL.
#### `--cores-limit -cl`
O limite de núcleos da instância gerenciada como um inteiro.
#### `--cores-request -cr`
A solicitação de núcleos da instância gerenciada como um inteiro.
#### `--memory-limit -ml`
O limite da capacidade da instância gerenciada como um inteiro.
#### `--memory-request -mr`
A solicitação para a capacidade da instância gerenciada como uma quantidade de memória em GBs representada por um inteiro.
#### `--dev`
Se isso for especificado, será considerado uma instância de desenvolvimento e não será cobrado.
#### `--no-wait`
Se for fornecido, o comando não aguardará que a instância esteja em um estado pronto antes de retornar.
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
## <a name="azdata-arc-sql-mi-delete"></a>azdata arc sql mi delete
Excluir uma instância gerenciada de SQL.
```bash
azdata arc sql mi delete --name -n 
                         
```
### <a name="examples"></a>Exemplos
Excluir uma instância gerenciada de SQL.
```bash
azdata arc sql mi delete -n sqlmi1
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--name -n`
O nome da Instância Gerenciada de SQL a ser excluída.
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
## <a name="azdata-arc-sql-mi-show"></a>azdata arc sql mi show
Mostrar os detalhes de uma Instância Gerenciada de SQL.
```bash
azdata arc sql mi show --name -n 
                       [--path -p]
```
### <a name="examples"></a>Exemplos
Mostrar os detalhes de uma Instância Gerenciada de SQL.
```bash
azdata arc sql mi show -n sqlmi1
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--name -n`
O nome da Instância Gerenciada de SQL a ser mostrada.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--path -p`
Um caminho em que a especificação completa da Instância Gerenciada de SQL deve ser gravada. Se omitida, a especificação será gravada na saída padrão.
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
## <a name="azdata-arc-sql-mi-list"></a>azdata arc sql mi list
Listar Instâncias Gerenciadas de SQL.
```bash
azdata arc sql mi list 
```
### <a name="examples"></a>Exemplos
Listar Instâncias Gerenciadas de SQL.
```bash
azdata arc sql mi list
```
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


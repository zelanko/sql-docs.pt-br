---
title: Referência do azdata arc postgres server
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata arc postgres server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3f34baeca8914adfcceda30766d46da50aa13517
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942257"
---
# <a name="azdata-arc-postgres-server"></a>azdata arc postgres server

Aplica-se ao `azdata`

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata arc postgres server create](#azdata-arc-postgres-server-create) | Criar um grupo de servidores PostgreSQL.
[azdata arc postgres server edit](#azdata-arc-postgres-server-edit) | Editar a configuração de um grupo de servidores PostgreSQL.
[azdata arc postgres server delete](#azdata-arc-postgres-server-delete) | Excluir um grupo de servidores PostgreSQL.
[azdata arc postgres server show](#azdata-arc-postgres-server-show) | Mostrar os detalhes de um grupo de servidores PostgreSQL.
[azdata arc postgres server list](#azdata-arc-postgres-server-list) | Listar grupos de servidores PostgreSQL.
[azdata arc postgres server config](reference-azdata-arc-postgres-server-config.md) | Comandos de configuração.
[azdata arc postgres server backup](reference-azdata-arc-postgres-server-backup.md) | Gerenciar backups do grupo de servidores PostgreSQL.
## <a name="azdata-arc-postgres-server-create"></a>azdata arc postgres server create
Para definir a senha do grupo de servidores, defina a variável de ambiente AZDATA_PASSWORD
```bash
azdata arc postgres server create --name -n 
                                  [--path]  
                                  
[--cores-limit -cl]  
                                  
[--cores-request -cr]  
                                  
[--memory-limit -ml]  
                                  
[--memory-request -mr]  
                                  
[--storage-class-data -scd]  
                                  
[--storage-class-logs -scl]  
                                  
[--storage-class-backups -scb]  
                                  
[--extensions]  
                                  
[--volume-size-data -vsd]  
                                  
[--volume-size-logs -vsl]  
                                  
[--volume-size-backups -vsb]  
                                  
[--workers -w]  
                                  
[--engine-version -ev]  
                                  
[--no-external-endpoint]  
                                  
[--dev]  
                                  
[--port]  
                                  
[--no-wait]  
                                  
[--engine-settings -e]
```
### <a name="examples"></a>Exemplos
Criar um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server create -n pg1
```
Crie um grupo de servidores PostgreSQL com as configurações do mecanismo. Ambos os exemplos abaixo são válidos.
```bash
azdata arc postgres server create -n pg1 --engine-settings "key1=val1"
azdata arc postgres server create -n pg1 --engine-settings "key2=val2"
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--name -n`
Nome da instância.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--path`
O caminho para o arquivo JSON de origem para o grupo de servidores PostgreSQL. Isso é opcional.
#### `--cores-limit -cl`
O número máximo de núcleos de CPU para a instância de postgres que pode ser usada por nó. O uso de núcleos fracionários é compatível.
#### `--cores-request -cr`
O número mínimo de núcleos de CPU que precisam estar disponíveis por nó para agendar o serviço. O uso de núcleos fracionários é compatível.
#### `--memory-limit -ml`
O limite de memória da instância do postgres como um número seguido por Ki (quilobytes), Mi (megabytes) ou Gi (gigabytes).
#### `--memory-request -mr`
A solicitação de memória da instância do postgres como um número seguido por Ki (quilobytes), Mi (megabytes) ou Gi (gigabytes).
#### `--storage-class-data -scd`
A classe de armazenamento a ser usada para volumes de dados persistentes.
#### `--storage-class-logs -scl`
A classe de armazenamento a ser usada para volumes de logs persistentes.
#### `--storage-class-backups -scb`
A classe de armazenamento a ser usada para volumes de backup persistentes.
#### `--extensions`
Uma lista separada por vírgulas das extensões Postgres que devem ser carregadas na inicialização. Confira a documentação do Postgres para obter a lista de valores compatíveis.
#### `--volume-size-data -vsd`
O tamanho do volume de armazenamento a ser usado para os dados como um número positivo seguido por Ki (quilobytes), Mi (megabytes) ou Gi (gigabytes).
#### `--volume-size-logs -vsl`
O tamanho do volume de armazenamento a ser usado para os logs como um número positivo seguido por Ki (quilobytes), Mi (megabytes) ou Gi (gigabytes).
#### `--volume-size-backups -vsb`
O tamanho do volume de armazenamento a ser usado para backups como um número positivo seguido por Ki (quilobytes), Mi (megabytes) ou Gi (gigabytes).
#### `--workers -w`
O número de nós de trabalho a serem provisionados em um cluster fragmentado ou então zero (o padrão) para um Postgres de nó único.
#### `--engine-version -ev`
Precisa ser 11 ou 12. O valor padrão é 12.
#### `--no-external-endpoint`
Se especificado, nenhum serviço externo será criado. Caso contrário, um serviço externo será criado usando o mesmo tipo de serviço que o controlador de dados.
#### `--dev`
Se isso for especificado, será considerado uma instância de desenvolvimento e não será cobrado.
#### `--port`
Opcional.
#### `--no-wait`
Se for fornecido, o comando não aguardará que a instância esteja em um estado pronto antes de retornar.
#### `--engine-settings -e`
Uma lista separada por vírgulas das configurações do mecanismo Postgres no formato 'key1=val1, key2=val2'.
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
## <a name="azdata-arc-postgres-server-edit"></a>azdata arc postgres server edit
Editar a configuração de um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server edit --name -n 
                                [--path]  
                                
[--workers -w]  
                                
[--engine-version -ev]  
                                
[--cores-limit -cl]  
                                
[--cores-request -cr]  
                                
[--memory-limit -ml]  
                                
[--memory-request -mr]  
                                
[--extensions]  
                                
[--dev]  
                                
[--port]  
                                
[--no-wait]  
                                
[--engine-settings -e]  
                                
[--replace-engine-settings -re]  
                                
[--admin-password]
```
### <a name="examples"></a>Exemplos
Editar a configuração de um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server edit --src ./spec.json -n pg1
```
Edite um grupo de servidores PostgreSQL com as configurações do mecanismo.
```bash
azdata arc postgres server edit -n pg1 --engine-settings "key2=val2"
```
Edita um grupo de servidores PostgreSQL e substitui as configurações de mecanismo existentes por uma nova configuração key1 = val1.
```bash
azdata arc postgres server edit -n pg1 --engine-settings "key1=val1" --replace-engine-settings
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--name -n`
Nome do grupo de servidores PostgreSQL que está sendo editado. O nome sob o qual sua instância está implantada não pode ser alterado.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--path`
O caminho para o arquivo JSON de origem para o grupo de servidores PostgreSQL. Isso é opcional.
#### `--workers -w`
O número de nós de trabalho a serem provisionados em um cluster fragmentado ou então zero (o padrão) para um Postgres de nó único.
#### `--engine-version -ev`
A versão do mecanismo não pode ser alterada. --engine-version pode ser usado em conjunto com --name para identificar um grupo de servidores de hiperescala do PostgreSQL quando dois grupos de servidores com versões de mecanismo diferentes têm o mesmo nome. --engine-version é opcional e, quando usado para identificar um grupo de servidores, deve ser igual a 11 ou 12.
#### `--cores-limit -cl`
O número máximo de núcleos de CPU para a instância de postgres que pode ser usada por nó. O uso de núcleos fracionários é compatível. Para remover cores_limit, especifique o valor dele como uma cadeia de caracteres vazia.
#### `--cores-request -cr`
O número mínimo de núcleos de CPU que precisam estar disponíveis por nó para agendar o serviço. O uso de núcleos fracionários é compatível. Para remover cores_request, especifique o valor dele como uma cadeia de caracteres vazia.
#### `--memory-limit -ml`
O limite de memória da instância do postgres como um número seguido por Ki (quilobytes), Mi (megabytes) ou Gi (gigabytes). Para remover memory_limit, especifique o valor dele como uma cadeia de caracteres vazia.
#### `--memory-request -mr`
A solicitação de memória da instância do postgres como um número seguido por Ki (quilobytes), Mi (megabytes) ou Gi (gigabytes). Para remover memory_request, especifique o valor dele como uma cadeia de caracteres vazia.
#### `--extensions`
Uma lista separada por vírgulas das extensões Postgres que devem ser carregadas na inicialização. Confira a documentação do Postgres para obter a lista de valores compatíveis.
#### `--dev`
Se isso for especificado, será considerado uma instância de desenvolvimento e não será cobrado.
#### `--port`
Opcional.
#### `--no-wait`
Se for fornecido, o comando não aguardará que a instância esteja em um estado pronto antes de retornar.
#### `--engine-settings -e`
Uma lista separada por vírgulas das configurações do mecanismo Postgres no formato 'key1=val1, key2=val2'. As configurações fornecidas serão mescladas com as configurações existentes. Para remover uma configuração, forneça um valor vazio, como 'removedKey='. Se você alterar uma configuração de mecanismo que exija uma reinicialização, o serviço será reiniciado para aplicar as configurações imediatamente.
#### `--replace-engine-settings -re`
Quando especificado com --engine-settings, ele substituirá todas as configurações de mecanismo personalizadas existentes pelo novo conjunto de configurações e valores.
#### `--admin-password`
Se especificado, a senha de administrador do servidor Postgres será definida como o valor da variável de ambiente AZDATA_PASSWORD se ela estiver presente. Caso contrário, será um valor solicitado.
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
## <a name="azdata-arc-postgres-server-delete"></a>azdata arc postgres server delete
Excluir um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server delete --name -n 
                                  [--engine-version -ev]
```
### <a name="examples"></a>Exemplos
Excluir um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server delete -n pg1
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--name -n`
Nome do grupo de servidores PostgreSQL.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--engine-version -ev`
--engine-version pode ser usado em conjunto com --name para identificar um grupo de servidores de hiperescala do PostgreSQL quando dois grupos de servidores com versões de mecanismo diferentes têm o mesmo nome. --engine-version é opcional e, quando usado para identificar um grupo de servidores, deve ser igual a 11 ou 12.
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
## <a name="azdata-arc-postgres-server-show"></a>azdata arc postgres server show
Mostrar os detalhes de um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server show --name -n 
                                [--engine-version -ev]  
                                
[--path -p]
```
### <a name="examples"></a>Exemplos
Mostrar os detalhes de um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server show -n pg1
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--name -n`
Nome do grupo de servidores PostgreSQL.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--engine-version -ev`
--engine-version pode ser usado em conjunto com --name para identificar um grupo de servidores de hiperescala do PostgreSQL quando dois grupos de servidores com versões de mecanismo diferentes têm o mesmo nome. --engine-version é opcional e, quando usado para identificar um grupo de servidores, deve ser igual a 11 ou 12.
#### `--path -p`
Um caminho em que a especificação completa do grupo de servidores PostgreSQL devem ser gravados. Se omitida, a especificação será gravada na saída padrão.
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
## <a name="azdata-arc-postgres-server-list"></a>azdata arc postgres server list
Listar grupos de servidores PostgreSQL.
```bash
azdata arc postgres server list 
```
### <a name="examples"></a>Exemplos
Listar grupos de servidores PostgreSQL.
```bash
azdata arc postgres server list
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


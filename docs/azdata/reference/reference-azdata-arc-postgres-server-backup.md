---
title: Referência do azdata arc postgres server backup
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata arc postgres server backup.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 44a3811ab3412a7631a0a0bf95aecc85150206b0
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358744"
---
# <a name="azdata-arc-postgres-server-backup"></a>azdata arc postgres server backup

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata arc postgres server backup create](#azdata-arc-postgres-server-backup-create) | Criar um backup de um grupo de servidores PostgreSQL.
[azdata arc postgres server backup delete](#azdata-arc-postgres-server-backup-delete) | Excluir um backup de um grupo de servidores PostgreSQL.
[azdata arc postgres server backup restore](#azdata-arc-postgres-server-backup-restore) | Restaurar um backup de um grupo de servidores PostgreSQL.
[azdata arc postgres server backup restorestatus](#azdata-arc-postgres-server-backup-restorestatus) | Obter o status da operação de restauração mais recente do sistema, se houver.
[azdata arc postgres server backup show](#azdata-arc-postgres-server-backup-show) | Mostrar os detalhes sobre um backup de um grupo de servidores PostgreSQL.
## <a name="azdata-arc-postgres-server-backup-create"></a>azdata arc postgres server backup create
Criar um backup de um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server backup create 
```
### <a name="examples"></a>Exemplos
Cria um backup para o serviço 'pg'.
```bash
azdata arc postgres server backup create -sn pg
```
Cria um backup nomeado para o serviço 'pg'.
```bash
azdata arc postgres server backup create -sn pg -n backup1
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
## <a name="azdata-arc-postgres-server-backup-delete"></a>azdata arc postgres server backup delete
Excluir um backup de um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server backup delete 
```
### <a name="examples"></a>Exemplos
Excluir um backup de um grupo de servidores PostgreSQL.
```bash
azdata arc postgres backup delete -sn pg -id e07dd3940e374bd9acbc86869cbc123d
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
## <a name="azdata-arc-postgres-server-backup-restore"></a>azdata arc postgres server backup restore
Restaurar um backup de um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server backup restore 
```
### <a name="examples"></a>Exemplos
Restaurar o backup mais recente.
```bash
azdata arc postgres server restore -sn pg```
Restore a backup by ID
```bash
azdata arc postgres server restore -sn pg -id 123e4567e89b12d3a456426655440000
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
## <a name="azdata-arc-postgres-server-backup-restorestatus"></a>azdata arc postgres server backup restorestatus
Obter o status da operação de restauração mais recente do sistema, se houver.
```bash
azdata arc postgres server backup restorestatus 
```
### <a name="examples"></a>Exemplos
Obtenha o status de restauração recente para o serviço 'pg' por ID.
```bash
azdata arc postgres server backup restorestatus -sn pg -id 123e4567e89b12d3a456426655440000
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
## <a name="azdata-arc-postgres-server-backup-show"></a>azdata arc postgres server backup show
Mostrar os detalhes sobre um backup de um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server backup show 
```
### <a name="examples"></a>Exemplos
Obtém um backup para o serviço 'pg' por ID
```bash
azdata arc postgres server backup show -sn pg -id 123e4567e89b12d3a456426655440000
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


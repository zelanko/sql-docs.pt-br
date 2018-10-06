---
title: Restaurar um banco de dados no cluster de big data do SQL Server | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 04514fb0184fa28e0ba959f3dd33cb2e1ec945cb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795800"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>Restaurar um banco de dados para a instância de mestre de cluster de big data do SQL Server

Para transferir um banco de dados existente do SQL Server para a instância mestre, recomendamos usar um backup, cópia e restauração abordagem.  Neste exemplo, mostraremos como restaurar o banco de dados AdventureWorks, mas você pode usar qualquer backup de banco de dados que você tem.  Você pode baixar o backup do AdventureWorks [aqui](https://www.microsoft.com/en-us/download/details.aspx?id=49502).

Primeiro, fazer backup de seu banco de dados existente do SQL Server no SQL Server no Windows ou Linux usando qualquer um dos métodos comuns de criação de um backup de banco de dados.

Copie o arquivo de backup para o contêiner do SQL Server no pod instância mestre do cluster Kubernetes.

```bash
kubectl cp <path to .bak file> mssql-data-pool-master-0:/tmp/ -c mssql-data-pool-data -n <name of your cluster>
```

Exemplo:

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-data-pool-master-0:/tmp/ -c mssql-data-pool-data -n clustertest
```

Em seguida, verifique se o arquivo de backup foram copiado para o contêiner de pod.

```bash
kubectl exec -it mssql-data-pool-master-0 -n <name of your cluster> -c mssql-data-pool-data -- bin/bash
root@mssql-data-pool-master-0:/# ls /tmp
root@mssql-data-pool-master-0:/# exit
```

Exemplo:

```bash
kubectl exec -it mssql-data-pool-master-0 -n clustertest -c mssql-data-pool-data -- bin/bash
root@mssql-data-pool-master-0:/# ls /tmp
```

Em seguida, restaure o backup de banco de dados para a instância mestre do SQL Server.  Se você estiver restaurando um backup de banco de dados que foi criado no Windows, você precisará obter os nomes dos arquivos.  No Studio de Ops conectado à instância do mestre, execute este script SQL:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

Exemplo:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![Lista de arquivos de backup](media/restore-database/database-restore-file-list.png)

Agora, restaure o banco de dados com um script como este, substituindo os nomes ou caminhos, conforme necessário, dependendo de seu backup de banco de dados.

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

Agora, se você quiser ter seu banco de dados de alto valor ser capaz de acessar os pools de dados, que você precisará configurar procedimentos armazenados do pool de dados abrindo e executar esses scripts do repositório do GitHub.

Execute o **alto valor-db configuration\data_pool_ddl_install. SQL** script.

- Procedimentos armazenado de capacidade de suporte de configuração

Execute o **alto valor-db configuration\supportability. SQL** script.

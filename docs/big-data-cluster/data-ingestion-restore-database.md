---
title: Restaurar um banco de dados
titleSuffix: SQL Server big data clusters
description: Este artigo mostra como restaurar um banco de dados na instância mestre de um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bad1a62752dd75e181d30c28485e1c9b707aa888
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69652232"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>Restaurar um banco de dados na instância mestre de cluster de Big Data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como restaurar um banco de dados existente na instância mestre de um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. O método recomendado é usar uma abordagem de backup, cópia e restauração.

## <a name="backup-your-existing-database"></a>Backup do banco de dados existente

Primeiro, faça backup do banco de dados do SQL Server existente do SQL Server no Windows ou no Linux. Use técnicas de backup padrão com o Transact-SQL ou com uma ferramenta como o SSMS (SQL Server Management Studio).

Este artigo mostra como restaurar o banco de dados AdventureWorks, mas você pode usar qualquer backup de banco de dados. 

> [!TIP]
> Você pode baixar o backup do AdventureWorks [aqui](https://www.microsoft.com/download/details.aspx?id=49502).

## <a name="copy-the-backup-file"></a>Copiar o arquivo de backup

Copie o arquivo de backup para o contêiner do SQL Server no pod da instância mestre do cluster do Kubernetes.

```bash
kubectl cp <path to .bak file> master-0:/tmp -c mssql-server -n <name of your big data cluster>
```

Exemplo:

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n clustertest
```

Em seguida, verifique se o arquivo de backup foi copiado para o contêiner de pod.

```bash
kubectl exec -it master-0 -n <name of your big data cluster> -c mssql-server -- bin/bash
cd /var/
ls /tmp
exit
```

Exemplo:

```bash
kubectl exec -it master-0 -n clustertest -c mssql-server -- bin/bash
ls /tmp
exit
```

## <a name="restore-the-backup-file"></a>Restaurar o arquivo de backup

Em seguida, restaure o backup do banco de dados para o SQL Server da instância mestre.  Se você estiver restaurando um backup de banco de dados criado no Windows, será necessário obter os nomes dos arquivos.  No Azure Data Studio, conecte-se à instância mestre e execute este script SQL:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

Exemplo:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![Lista de arquivos de backup](media/restore-database/database-restore-file-list.png)

Agora, restaure o banco de dados. O seguinte script é um exemplo. Substitua os nomes/caminhos conforme necessário, dependendo do backup do banco de dados.

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

## <a name="configure-data-pool-and-hdfs-access"></a>Configurar o pool de dados e o acesso ao HDFS

Agora, para que a instância mestre do SQL Server acesse pools de dados e o HDFS, execute o pool de dados e os procedimentos armazenados do pool de armazenamento. Execute os seguintes scripts Transact-SQL em seu banco de dados restaurado recentemente:

```sql
USE AdventureWorks2016CTP3
GO
-- Create the SqlDataPool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
  CREATE EXTERNAL DATA SOURCE SqlDataPool
  WITH (LOCATION = 'sqldatapool://controller-svc/default');

-- Create the SqlStoragePool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   CREATE EXTERNAL DATA SOURCE SqlStoragePool
   WITH (LOCATION = 'sqlhdfs://controller-svc/default');
GO
```

> [!NOTE]
> Você precisará executar esses scripts de instalação somente para bancos de dados restaurados de versões mais antigas do SQL Server. Se você criar um novo banco de dados na instância mestre do SQL Server, os procedimentos de pool de dados e pool de armazenamento já estarão configurados para você.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira a visão geral a seguir:

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)

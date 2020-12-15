---
title: Instalar PolyBase em Linux
titlesuffix: SQL Server
description: Saiba como instalar o PolyBase do SQL Server no Linux. O PolyBase permite que você execute consultas externas com relação a fontes de dados remotas.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: dakryze
ms.date: 8/18/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15'
ms.openlocfilehash: 2c93d219860f2bbbdf11050966955a63d44387e4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97416379"
---
# <a name="install-polybase-on-linux"></a>Instalar PolyBase em Linux

[!INCLUDE [sqlserver2019-linux](../../includes/applies-to-version/sqlserver2019-linux.md)]

As etapas a seguir instalam o [PolyBase](../../relational-databases/polybase/polybase-guide.md) (`mssql-server-polybase` e `mssql-server-polybase-hadoop`) no Linux. O PolyBase permite que você execute consultas externas com relação a fontes de dados remotas.

>[!NOTE]
> Antes de instalar o PolyBase, [instale o SQL Server 2019](../../linux/sql-server-linux-setup.md#platforms). Isso configura as chaves e os repositórios que você usa ao instar os pacotes `mssql-server-polybase` e `mssql-server-polybase-hadoop`.

>[!NOTE]
>
> - Não há suporte para o PolyBase no SQL Server 2017 para Linux.
> - Expansão para PolyBase no Linux não está disponível no momento.

Instalar PolyBase para seu sistema operacional:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="install-on-rhel"></a><a name="RHEL"></a>Instalar no RHEL

Use o seguinte comando para instalar o `mssql-server-polybase` no Red Hat Enterprise Linux. 

```bash
sudo yum install -y mssql-server-polybase
```

Você será solicitado a reiniciar a instância do SQL Server. Use o seguinte comando para fazer isso.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>Após a instalação, é necessário [habilitar o recurso do PolyBase](#enable).

Use o comando a seguir para instalar o `mssql-server-polybase-hadoop`. 

```bash
sudo yum install -y mssql-server-polybase-hadoop
```

O pacote Hadoop do PolyBase tem dependências nos seguintes pacotes:
- `mssql-server`
- `mssql-server-polybase`
- `mssql-server-extensibility`
- `mssql-zulu-jre-11`. 

Prompts de instalação para reiniciar `launchpadd`. Use o seguinte comando para fazer isso.

```bash
sudo systemctl restart mssql-launchpadd
```

>[!NOTE]
>Após a instalação, você deverá [definir o nível de conectividade do Hadoop](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md#c-set-hadoop-connectivity).

Se você precisar de uma instalação offline, localize o download do pacote do PolyBase nas [Notas sobre a versão](../../linux/sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [Instalar o SQL Server](../../linux/sql-server-linux-setup.md#offline).

## <a name="install-on-ubuntu"></a><a name="ubuntu"></a>Instalação no Ubuntu

Use o seguinte comando para instalar o `mssql-server-polybase` no Ubuntu. 

```bash
sudo apt-get install mssql-server-polybase
```

Você será solicitado a reiniciar a instância do SQL Server. Use o seguinte comando para fazer isso.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>Após a instalação, é necessário [habilitar o recurso do PolyBase](#enable).

Se você precisar de uma instalação offline, localize o download do pacote do PolyBase nas [Notas sobre a versão](../../linux/sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [Instalar o SQL Server](../../linux/sql-server-linux-setup.md#offline).

Use o comando a seguir para instalar o `mssql-server-polybase-hadoop`. 

```bash
sudo apt-get install mssql-server-polybase-hadoop
```

O pacote Hadoop do PolyBase tem dependências nos seguintes pacotes:
- `mssql-server`
- `mssql-server-polybase`
- `mssql-server-extensibility`
- `mssql-zulu-jre-11`. 

Prompts de instalação para reiniciar `launchpadd`. Use o seguinte comando para fazer isso.

```bash
sudo systemctl restart mssql-launchpadd
```

>[!NOTE]
>Após a instalação, você deverá [definir o nível de conectividade do Hadoop](../../relational-databases/polybase/polybase-configure-hadoop.md#configure-hadoop-connectivity).

## <a name="install-on-sles"></a><a name="SLES"></a>Instalar no SLES

Use o seguinte comando para instalar o `mssql-server-polybase` no SUSE Linux Enterprise Server. 

```bash
sudo zypper install mssql-server-polybase
```

Você será solicitado a reiniciar a instância do SQL Server. Use o seguinte comando para fazer isso.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>Após a instalação, é necessário [habilitar o recurso do PolyBase](#enable).

Se você precisar de uma instalação offline, localize o download do pacote do PolyBase nas [Notas sobre a versão](../../linux/sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [Instalar o SQL Server](../../linux/sql-server-linux-setup.md#offline).


## <a name="enable-polybase"></a><a name="enable"></a> Habilitar o PolyBase

Após a instalação, o PolyBase deverá ser habilitado para acessar seus recursos. Conectar-se à instância do SQL Server instalada e use o seguinte comando Transact-SQL para habilitar.

```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE WITH OVERRIDE;
```

## <a name="update-polybase"></a>Atualizar o PolyBase

Se você já tiver `mssql-server-polybase` instalado, poderá atualizar para a versão mais recente com os seguintes comandos:

### <a name="rhel"></a>RHEL

```bash
sudo yum remove -y mssql-server-polybase-hadoop
sudo yum remove -y mssql-server-polybase
sudo yum check-update
sudo yum install -y mssql-server-polybase
sudo yum install -y mssql-server-polybase-hadoop
```

Você será solicitado a reiniciar a instância do SQL Server. Use o seguinte comando para fazer isso.

```
sudo systemctl restart mssql-server
```

### <a name="ubuntu"></a>Ubuntu

```bash
sudo apt-get remove mssql-server-polybase-hadoop
sudo apt-get remove mssql-server-polybase
sudo apt-get update 
sudo apt-get install mssql-server-polybase
sudo apt-get remove mssql-server-polybase-hadoop
```

Você será solicitado a reiniciar a instância do SQL Server. Use o seguinte comando para fazer isso.

```
sudo systemctl restart mssql-server
```

### <a name="sles"></a>SLES

```bash
sudo zypper remove mssql-server-polybase
sudo zypper refresh
sudo zypper install mssql-server-polybase
```

Você será solicitado a reiniciar a instância do SQL Server. Use o seguinte comando para fazer isso.

```
sudo systemctl restart mssql-server
```

>[!NOTE]
>Após a instalação, é necessário [habilitar o recurso do PolyBase](#enable).

## <a name="next-steps"></a>Próximas etapas

O PolyBase no Linux pode acessar as fontes de dados a seguir. Siga os links fornecidos para obter mais informações sobre como a opção de criar uma tabela externa dessas fontes no PolyBase é habilitada. 

- [SQL Server, Banco de Dados SQL, Azure Synapse Analytics)](../../relational-databases/polybase/polybase-configure-sql-server.md)
- [Hadoop](../../relational-databases/polybase/polybase-configure-hadoop.md)
- [Armazenamento de Blobs do Azure](../../relational-databases/polybase/polybase-configure-azure-blob-storage.md)
- [Oracle](../../relational-databases/polybase/polybase-configure-oracle.md)
- [Teradata](../../relational-databases/polybase/polybase-configure-teradata.md)
- [MongoDB (e Cosmos DB)](../../relational-databases/polybase/polybase-configure-mongodb.md)

Para obter mais informações sobre como isso é usado, consulte o artigo de referência do Transact-SQL sobre [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).

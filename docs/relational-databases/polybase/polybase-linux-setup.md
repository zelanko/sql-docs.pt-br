---
title: Instalar PolyBase em Linux
titlesuffix: SQL Server
description: Saiba como instalar o PolyBase do SQL Server no Linux. O PolyBase permite que você execute consultas externas com relação a fontes de dados remotas.
author: MikeRayMSFT
ms.author: mikeray
ms.date: 7/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: f886c1d1ae3b5054c6ca0f0159ca8202054ec375
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88087334"
---
# <a name="install-polybase-on-linux"></a>Instalar PolyBase em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

As etapas a seguir instalam o [PolyBase](../../relational-databases/search/full-text-search.md) (**mssql-server-polybase**) no Linux. O PolyBase permite que você execute consultas externas com relação a fontes de dados remotas. 

>[!NOTE]
> Antes de instalar o PolyBase, primeiro [instale a versão prévia do SQL Server 2019](../../linux/sql-server-linux-setup.md#platforms). Isso configura as chaves e os repositórios que você usa ao instar o pacote **mssql-server-polybase**.
>
> Não há suporte para o PolyBase no SQL Server 2017 para Linux.
> Expansão para PolyBase no Linux não está disponível no momento.

Instalar PolyBase para seu sistema operacional:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)



## <a name=""></a><a name="RHEL">Instalar no RHEL</a>

Use o seguinte comando para instalar o **mssql-server-polybase** no Red Hat Enterprise Linux. 

```bash
sudo yum install -y mssql-server-polybase
```

Você será solicitado a reiniciar a instância do SQL Server. Use o seguinte comando para fazer isso.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>Após a instalação, é necessário [habilitar o recurso do PolyBase](#enable).

Se você precisar de uma instalação offline, localize o download do pacote do PolyBase nas [Notas sobre a versão](../../linux/sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [Instalar o SQL Server](../../linux/sql-server-linux-setup.md#offline).

## <a name=""></a><a name="ubuntu">Instalar no Ubuntu</a>

Use o seguinte comando para instalar o **mssql-server-polybase** no Ubuntu. 

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

## <a name=""></a><a name="SLES">Instalar no SLES</a>

Use o seguinte comando para instalar o **mssql-server-polybase** no SUSE Linux Enterprise Server. 

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


## <a name=""></a><a name="enable">Habilitar o PolyBase</a> 

Após a instalação, o PolyBase deverá ser habilitado para acessar seus recursos. Conectar-se à instância do SQL Server instalada e use o seguinte comando Transact-SQL para habilitar.

```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE WITH OVERRIDE;
```

## <a name="update-polybase"></a>Atualizar o PolyBase

Se você já tiver **mssql-server-polybase** instalado, poderá atualizar para a versão mais recente com os seguintes comandos:

### <a name="rhel"></a>RHEL

```bash
sudo yum remove -y mssql-server-polybase
sudo yum check-update
sudo yum install -y mssql-server-polybase
```

Você será solicitado a reiniciar a instância do SQL Server. Use o seguinte comando para fazer isso.

```
sudo systemctl restart mssql-server
```

### <a name="ubuntu"></a>Ubuntu

```bash
sudo apt-get remove mssql-server-polybase
sudo apt-get update 
sudo apt-get install mssql-server-polybase
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

- [SQL Server (e Banco de Dados SQL, SQL Data Warehouse do Azure)](../../relational-databases/polybase/polybase-configure-sql-server.md)
- [Oracle](../../relational-databases/polybase/polybase-configure-oracle.md)
- [Teradata](../../relational-databases/polybase/polybase-configure-teradata.md)
- [MongoDB (e Cosmos DB)](../../relational-databases/polybase/polybase-configure-mongodb.md)

Para obter mais informações sobre como isso é usado, consulte o artigo de referência do Transact-SQL sobre [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).

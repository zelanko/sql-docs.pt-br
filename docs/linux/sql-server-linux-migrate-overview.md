---
title: Migrar bancos de dados para o SQL Server em Linux
description: Este artigo descreve as diferentes opções para a migração de dados e bancos de dados para o SQL Server em Linux.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.openlocfilehash: e7affa88f1856571d0b2142f7dcfdf762ed79197
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68129348"
---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>Migrar bancos de dados e dados estruturados para o SQL Server em Linux 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Você pode migrar seus dados e bancos de dados para o SQL Server em execução no Linux. O método que você escolherá usar depende dos dados de origem e de seu cenário específico. As seções a seguir fornecem as melhores práticas para vários cenários de migração.

## <a name="migrate-from-sql-server-on-windows"></a>Migrar do SQL Server no Windows
Se você quiser migrar bancos de dados do SQL Server no Windows para o SQL Server em Linux, a técnica recomendada será usar o backup e restauração do SQL Server.

1. Crie um backup do banco de dados no computador com Windows.
2. Transfira o arquivo de backup para o computador de destino com SQL Server em Linux.
3. Restaure o backup no computador com Linux. 

Para obter um tutorial sobre como migrar um banco de dados com backup e restauração, confira o seguinte tópico:

- [Restaurar um banco de dados do SQL Server do Windows para o Linux](sql-server-linux-migrate-restore-database.md).

Também é possível exportar seu banco de dados para um arquivo BACPAC (um arquivo compactado que contém o esquema e os dados de seu banco de dados). Se tiver um arquivo BACPAC, você poderá transferir esse arquivo para o computador Linux e, em seguida, importá-lo para o SQL Server. Para obter mais informações, consulte os tópicos a seguir:

- [Exportar e importar um banco de dados com SSMS ou SqlPackage.exe](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>Migrar de outros servidores de banco de dados
Você pode migrar bancos de dados em outros sistemas de banco de dados para o SQL Server em Linux. Isso inclui bancos de dados do Microsoft Access, DB2, MySQL, Oracle e Sybase. Nesse cenário, use o SSMA (Assistente de Migração do Microsoft SQL Server) para automatizar a migração para o SQL Server em Linux. Para obter mais informações, confira [Usar o SSMA para migrar bancos de dados para o SQL Server em Linux](sql-server-linux-migrate-ssma.md).  

## <a name="migrate-structured-data"></a>Migrar dados estruturados
Também há técnicas para importar dados brutos. Você pode ter arquivos de dados estruturados que foram exportados de outros bancos de dados ou fontes de dados. Nesse caso, você pode usar a ferramenta bcp para inserir os dados em massa. Ou pode executar o SQL Server Integration Services no Windows para importar os dados para um banco de dados do SQL Server em Linux. O SQL Server Integration Services permite que você execute transformações mais complexas nos dados durante a importação. 

Para saber mais sobre essas técnicas, confira os seguintes tópicos:

- [Cópia em massa de dados com bcp](sql-server-linux-migrate-bcp.md)
- [Extrair, transformar e carregar dados no SQL Server em Linux com o SSIS](sql-server-linux-migrate-ssis.md) 

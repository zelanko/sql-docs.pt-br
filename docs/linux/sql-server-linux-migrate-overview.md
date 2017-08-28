---
title: Migrar bancos de dados para o SQL Server no Linux | Microsoft Docs
description: "Este tópico descreve as diferentes opções para migrar bancos de dados e os dados para o SQL Server no Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 61b4ba948df071768380d4a6f2b4ddc4421692d8
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>Migrar bancos de dados e os dados estruturados para o SQL Server no Linux 

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Você pode migrar seus bancos de dados e os dados para o SQL Server de 2017 RC2 em execução no Linux. O método que você optar por usar depende dos dados de origem e o seu cenário específico. As seções a seguir fornecem práticas recomendadas para vários cenários de migração.

## <a name="migrate-from-sql-server-on-windows"></a>Migrar do SQL Server no Windows
Se você quiser migrar bancos de dados do SQL Server no Windows para o SQL Server 2017 no Linux, a técnica recomendada é usar o SQL Server backup e restauração.

1. Crie um backup do banco de dados no computador Windows.
2. Transferir o arquivo de backup para a máquina do SQL Server Linux de destino.
3. Restaure o backup no computador Linux. 

Para obter um tutorial sobre como migrar um banco de dados com backup e restauração, consulte o tópico a seguir:

- [Restaurar um banco de dados do SQL Server do Windows para Linux](sql-server-linux-migrate-restore-database.md).

Também é possível exportar seu banco de dados para um arquivo BACPAC (um arquivo compactado que contém o esquema de banco de dados e os dados). Se você tiver um arquivo BACPAC, você pode transferir esse arquivo para o computador Linux e, em seguida, importá-lo para o SQL Server. Para obter mais informações, consulte os tópicos a seguir:

- [Exportar e importar um banco de dados com o SSMS ou SqlPackage.exe](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>Migrar de outros servidores de banco de dados
Você pode migrar bancos de dados em outros sistemas de banco de dados para SQL Server 2017 no Linux. Isso inclui bancos de dados do Microsoft Access, DB2, MySQL, Oracle e Sybase. Neste cenário, use o gerenciamento de assistente SSMA (SQL Server) para automatizar a migração para o SQL Server no Linux. Para obter mais informações, consulte [Use SSMA para migrar bancos de dados para o SQL Server no Linux](sql-server-linux-migrate-ssma.md).  

## <a name="migrate-structured-data"></a>Migrar dados estruturados
Também há técnicas para importar dados brutos. Você pode ter estruturado arquivos de dados que foram exportados de outros bancos de dados ou fontes de dados. Nesse caso, você pode usar a ferramenta bcp para inserção em massa os dados. Ou você pode executar o SQL Server Integration Services no Windows para importar os dados para um banco de dados do SQL Server no Linux. SQL Server Integration Services permite que você execute transformações mais complexas sobre os dados durante a importação. 

Para obter mais informações sobre essas técnicas, consulte os tópicos a seguir:

- [Dados de cópia em massa com bcp](sql-server-linux-migrate-bcp.md)
- [Extrair, transformar e carregar dados para o SQL Server no Linux com o SSIS](sql-server-linux-migrate-ssis.md) 


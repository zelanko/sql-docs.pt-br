---
title: Migrar bancos de dados do SQL Server no Linux | Microsoft Docs
description: Este artigo descreve as diferentes opções para migrar bancos de dados e os dados para o SQL Server no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.openlocfilehash: 2443611a63bee3f62ae8225384d79d34dfcb18e0
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705299"
---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>Migrar bancos de dados e dados estruturados para o SQL Server no Linux 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Você pode migrar seus bancos de dados e os dados para o SQL Server em execução no Linux. O método que você optar por usar depende da fonte de dados e seu cenário específico. As seções a seguir fornecem práticas recomendadas para vários cenários de migração.

## <a name="migrate-from-sql-server-on-windows"></a>Migrar do SQL Server no Windows
Se você quiser migrar bancos de dados do SQL Server no Windows para o SQL Server no Linux, a técnica recomendada é usar o SQL Server backup e restauração.

1. Crie um backup do banco de dados no computador do Windows.
2. Transferir o arquivo de backup para a máquina do SQL Server Linux de destino.
3. Restaure o backup na máquina Linux. 

Para obter um tutorial sobre como migrar um banco de dados com backup e restauração, consulte o tópico a seguir:

- [Restaurar um banco de dados do SQL Server do Windows para Linux](sql-server-linux-migrate-restore-database.md).

Também é possível exportar seu banco de dados para um arquivo BACPAC (um arquivo compactado que contém o esquema de banco de dados e dados). Se você tiver um arquivo BACPAC, você pode transferir este arquivo em seu computador Linux e, em seguida, importá-lo para o SQL Server. Para mais informações, consulte os seguintes tópicos:

- [Exportar e importar um banco de dados com o SSMS ou SqlPackage.exe](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>Migrar de outros servidores de banco de dados
Você pode migrar bancos de dados em outros sistemas de banco de dados do SQL Server no Linux. Isso inclui bancos de dados Microsoft Access, DB2, MySQL, Oracle e Sybase. Nesse cenário, use o gerenciamento de Assistente do SSMA (SQL Server) para automatizar a migração para o SQL Server no Linux. Para obter mais informações, consulte [Use o SSMA para migrar bancos de dados do SQL Server no Linux](sql-server-linux-migrate-ssma.md).  

## <a name="migrate-structured-data"></a>Migrar dados estruturados
Também existem técnicas de importação de dados brutos. Você pode estruturar os arquivos de dados que foram exportados de outros bancos de dados ou fontes de dados. Nesse caso, você pode usar a ferramenta bcp para inserção em massa os dados. Ou você pode executar o SQL Server Integration Services no Windows para importar os dados para um banco de dados do SQL Server no Linux. SQL Server Integration Services permite que você execute transformações mais complexas sobre os dados durante a importação. 

Para obter mais informações sobre essas técnicas, consulte os tópicos a seguir:

- [Dados de cópia em massa com bcp](sql-server-linux-migrate-bcp.md)
- [Extrair, transformar e carregar dados do SQL Server no Linux com o SSIS](sql-server-linux-migrate-ssis.md) 

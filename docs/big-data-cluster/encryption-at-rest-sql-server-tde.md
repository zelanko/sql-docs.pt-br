---
title: Guia de uso da TDE (Transparent Data Encryption) em repouso dos Clusters de Big Data do SQL Server
titleSuffix: SQL Server Big Data Clusters
description: Este artigo mostra como usar o recurso de criptografia TDE em repouso do SQL Server do BDC
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mihaelab
ms.date: 10/19/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 55456185a6503ee11465a1e65cb9cd91de3ba6e2
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92199552"
---
# <a name="sql-server-big-data-clusters-transparent-data-encryption-tde-at-rest-usage-guide"></a>Guia de uso da TDE (Transparent Data Encryption) em repouso dos Clusters de Big Data do SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este guia demonstra como usar os recursos de criptografia em repouso dos Clusters de Big Data do SQL Server para criptografar bancos de dados.

Em linhas gerais, a experiência é igual à do SQL Server em Linux e a [documentação padrão do TDE](../relational-databases/security/encryption/transparent-data-encryption.md) se aplica, exceto quando indicado. Para monitorar o status de criptografia no mestre, siga os padrões de consulta DMV padrão na parte superior de [`sys.dm_database_encryption_keys`](../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) e [`sys.certificates`](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md).

__Recursos não compatíveis:__
* Criptografia do pool de dados
* Rotação de chaves de criptografia para bancos de dados em um grupo de disponibilidade contido em uma [implantação de HA](deployment-high-availability.md).


## <a name="prerequisites"></a><a id="prereqs"></a> Pré-requisitos

- [Cluster de Big Data do SQL Server CU8+](release-notes-big-data-cluster.md)
- [Ferramentas de Big Data](deploy-big-data-tools.md)
   - **Azure Data Studio**
- Usuário com privilégios de administrador do SQL Server.

## <a name="query-the-installed-certificates"></a>Consultar os certificados instalados

1. No Azure Data Studio, conecte-se à instância mestre do SQL Server do cluster de Big Data. Para obter mais informações, confira [Conectar-se à instância mestre do SQL Server](connect-to-big-data-cluster.md#master).

1. Clique duas vezes na conexão na janela **Servidores** para mostrar o painel do servidor da instância mestre do SQL Server. Selecione **Nova Consulta** .

   ![Consulta da instância mestre do SQL Server](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. Execute o comando Transact-SQL a seguir para alterar o contexto para o banco de dados **mestre** na instância mestra.

   ```sql
   USE master
   GO
   ```

1. Consulte os certificados gerenciados pelo sistema instalados. 

   ```sql
    SELECT TOP 1 name FROM sys.certificates WHERE name LIKE 'TDECertificate%' ORDER BY name DESC
   ```

    Use critérios de consulta diferentes, conforme necessário.

    O nome do certificado será listado como “TDECertificate{carimbo de data/hora}”. Quando você vir um prefixo de TDECertificate seguido pelo carimbo de data/hora, esse será o certificado fornecido pelo recurso gerenciado pelo sistema.

## <a name="encrypt-a-database-using-the-system-provided-certificate"></a>Criptografar um banco de dados usando o certificado fornecido pelo sistema

Nos exemplos a seguir, considere um banco de dados chamado __userdb__ como o destino para criptografia e um certificado fornecido pelo sistema chamado __TDECertificate2020_09_15_22_46_27__ por saída da seção anterior.

1. Use o padrão a seguir para gerar uma chave de criptografia de banco de dados usando o certificado de sistema fornecido.

   ```sql
    USE userdb; 
    GO
    CREATE DATABASE ENCRYPTION KEY WITH ALGORITHM = AES_256 ENCRYPTION BY SERVER CERTIFICATE TDECertificate2020_09_15_22_46_27;
    GO
   ```

1. Criptografe o banco de dados __userdb__ com o comando a seguir.

   ```sql
    ALTER DATABASE userdb SET ENCRYPTION ON;
    GO
   ```

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre a criptografia em repouso para o HDFS:
> [!div class="nextstepaction"]
> [Zonas de criptografia de HDFS](encryption-at-rest-hdfs-encryption-zones.md)

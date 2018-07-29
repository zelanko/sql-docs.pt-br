---
title: Replicação com Instância Gerenciada do Banco de Dados SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Database replication
- replication, SQL Database
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8dd8931bcc3fdaaa489d0a190c5ce1f6210e5f64
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088642"
---
# <a name="replication-with-sql-database-managed-instance"></a>Replicação com Instância Gerenciada do Banco de Dados SQL

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

A Instância Gerenciada do Banco de Dados SQL do Azure (versão prévia) dá suporte à replicação transacional. A Instância Gerenciada pode hospedar bancos de dados de publicador, distribuidor e assinante.

## <a name="common-configurations"></a>Configurações comuns

Em geral, o publicador e o distribuidor devem estar na nuvem ou no local. Há suporte para as configurações a seguir:

- **Publicador com distribuidor local na instância gerenciada**

   ![Replication-with-azure-sql-db-single-managed-instance-publisher-distributor](./media/replication-with-sql-database-managed-instance/01-single-instance-asdbmi-pubdist.png)

   Os bancos de dados de publicador e distribuidor são configurados em uma única instância gerenciada.

- **Publicador com distribuidor remoto na instância gerenciada**

   ![Replication-with-azure-sql-db-separate-managed-instances-publisher-distributor](./media/replication-with-sql-database-managed-instance/02-separate-instances-asdbmi-pubdist.png)

   O publicador e o distribuidor são configurados em duas instâncias gerenciadas. Nesta configuração:

  - As duas instâncias gerenciadas estão na mesma rede virtual.

  - As duas instâncias gerenciadas estão no mesmo local.

- **Publicador e distribuidor locais com o assinante na instância gerenciada**

   ![Replication-from-on-premises-to-azure-sql-db-subscriber](./media/replication-with-sql-database-managed-instance/03-azure-sql-db-subscriber.png)

   Nessa configuração, o Banco de Dados SQL é um assinante. Essa configuração dá suporte à migração do local para o Azure. Na função de assinante, o banco de dados SQL não precisa da instância gerenciada, porém você pode usar uma Instância Gerenciada do Banco de Dados SQL como uma etapa da migração do local para o Azure. Para saber mais sobre os assinantes do Banco de Dados SQL do Azure, confira [Replicação no Banco de Dados SQL](replication-to-sql-database.md).

## <a name="requirements"></a>Requisitos

O publicador e o distribuidor no Banco de Dados SQL do Azure exigem:

- Instância Gerenciada do Banco de Dados SQL do Azure.

   >[!NOTE]
   >Bancos de Dados SQL do Azure que não sejam configurados com a Instância Gerenciada só podem ser assinantes.

- Todas as instâncias do SQL Server precisam estar na mesma rede virtual.

- A conectividade usa a Autenticação do SQL entre os participantes da replicação.

- Um compartilhamento de Conta de Armazenamento do Azure para o diretório de trabalho de replicação.

## <a name="features"></a>Recursos

Oferece suporte a:

- Combinação de replicação transacional e de instantâneo de instâncias locais e Instâncias Gerenciadas do Banco de Dados SQL do Azure.

- Os assinantes podem ser locais, no Banco de Dados SQL ou pools elásticos.

- Replicação unidirecional ou bidirecional

## <a name="configure-publishing-and-distribution-example"></a>Exemplo de configuração de publicação e distribuição

1. [Crie uma Instância Gerenciada do Banco de Dados SQL do Azure](http://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal) no portal.

1. [Crie uma Conta de Armazenamento do Azure](http://docs.microsoft.com/azure/storage/common/storage-create-storage-account#create-a-storage-account) para o diretório de trabalho. Copie as chaves de armazenamento. Confira [Exibir e copiar chaves de acesso de armazenamento](http://docs.microsoft.com/azure/storage/common/storage-create-storage-account#manage-your-storage-access-keys).

1. Crie um banco de dados para o publicador.

   Nos exemplos de script abaixo, substitua `<Publishing_DB>` pelo nome desse banco de dados.

1. Crie um usuário de banco de dados com a Autenticação SQL para o distribuidor. Confira [Criar usuários de banco de dados](http://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial#creating-database-users). Use uma senha segura.

   Nos exemplos de script abaixo, use `<SQL_USER>` e `<PASSWORD>` para usuário e senha do banco de dados da Conta do SQL Server.

1. [Conecte-se à Instância Gerenciada do Banco de Dados SQL](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ssms).

1. Execute a consulta a seguir para adicionar o distribuidor e o banco de dados de distribuição.

   ```sql
   USE [master]
   GO
   EXEC sp_adddistributor @distributor = @@ServerName;
   EXEC sp_adddistributiondb @database = N'distribution';
   ```

1. Para configurar um publicador para usar um banco de dados de distribuição especificado, atualize e execute a consulta a seguir.

   Substitua `<SQL_USER>` e `<PASSWORD>` pela conta e senha do SQL Server.

   Substitua `\\<STORAGE_ACCOUNT>.file.core.windows.net\<SHARE>` pelo valor da sua conta de armazenamento. 

   Substitua `<STORAGE_CONNECTION_STRING>` pelo valor das suas chaves de acesso.

   Depois de atualizar a consulta a seguir, execute-a. 

   ```sql
   USE [master]
   EXEC sp_adddistpublisher @publisher = @@ServerName,
                @distribution_db = N'distribution',
                @security_mode = 0,
                @login = N'<SQL_USER>',
                @password = N'<PASSWORD>',
                @working_directory = N'\\<STORAGE_ACCOUNT>.file.core.windows.net\<SHARE>',
                @storage_connection_string = N'<STORAGE_CONNECTION_STRING>';
   GO
   ```

1. Configure o publicador para a replicação. 

    Na consulta a seguir, substitua `<Publishing_DB>` pelo nome do banco de dados do publicador.

    Substitua `<Publication_Name>` pelo nome da sua publicação.

    Substitua `<SQL_USER>` e `<PASSWORD>` pela conta e senha do SQL Server.

    Depois de atualizar a consulta, execute-a para criar a publicação.

   ```sql
   USE [<Publishing_DB>]
   EXEC sp_replicationdboption @dbname = N'<Publishing_DB>',
                @optname = N'publish',
                @value = N'true';

   EXEC sp_addpublication @publication = N'<Publication_Name>',
                @status = N'active';

   EXEC sp_changelogreader_agent @publisher_security_mode = 0,
                @publisher_login = N'<SQL_USER>',
                @publisher_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>',
                @job_password = N'<PASSWORD>';

   EXEC sp_addpublication_snapshot @publication = N'<Publication_Name>',
                @frequency_type = 1,
                @publisher_security_mode = 0,
                @publisher_login = N'<SQL_USER>',
                @publisher_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>',
                @job_password = N'<PASSWORD>'
   ```

1. Adicione o artigo, a assinatura e o agente de assinatura push. 

   Para adicionar esses objetos, atualize o script a seguir.

   Substitua `<Object_Name>` pelo nome do objeto de publicação.

   Substitua `<Object_Schema>` pelo nome do esquema de origem. 

   Substitua os outros parâmetros entre colchetes angulares `<>` para corresponder aos valores nos scripts anteriores. 

   ```sql
   EXEC sp_addarticle @publication = N'<Publication_Name>',
                @type = N'logbased',
                @article = N'<Object_Name>',
                @source_object = N'<Object_Name>',
                @source_owner = N'<Object_Schema>'

   EXEC sp_addsubscription @publication = N'<Publication_Name>',
                @subscriber = @@ServerName,
                @destination_db = N'<Subscribing_DB>',
                @subscription_type = N'Push'

   EXEC sp_addpushsubscription_agent @publication = N'<Publication_Name>',
                @subscriber = @@ServerName,
                @subscriber_db = N'<Subscribing_DB>',
                @subscriber_security_mode = 0,
                @subscriber_login = N'<SQL_USER>',
                @subscriber_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>', 
                @job_password = N'<PASSWORD>'
   GO
   ```

## <a name="limitations"></a>Limitações

Os recursos a seguir não têm suporte:

- Assinaturas atualizáveis

- Replicação geográfica ativa

## <a name="see-also"></a>Consulte Também

- [O que é uma Instância Gerenciada (versão prévia)?](http://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)
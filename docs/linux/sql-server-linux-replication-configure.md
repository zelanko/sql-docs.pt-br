---
title: Configurar replicação (SSMS)
description: Este artigo descreve como configurar a Replicação do SQL Server em Linux.
ms.custom: seo-dt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
titleSuffix: SQL Server on Linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0979f05808c59336dec7a6e4a664b2e970029dd6
ms.sourcegitcommit: 0a9058c7da0da9587089a37debcec4fbd5e2e53a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75952495"
---
# <a name="configure-sql-server-replication-on-linux"></a>Configurar a Replicação do SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

O [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] apresenta a Replicação do SQL Server para instâncias do SQL Server em Linux.

Para obter informações detalhadas sobre a replicação, confira [Documentação da Replicação do SQL Server](../relational-databases/replication/sql-server-replication.md).

Configure a replicação no Linux com os procedimentos armazenados do SSMS (SQL Server Management Studio) ou do Transact-SQL.

* Para usar o SSMS, siga as instruções neste artigo.

  Use o SSMS em um sistema operacional Windows para se conectar a instâncias do SQL Server. Para tela de fundo e instruções, confira [Usar o SSMS para gerenciar o SQL Server em Linux](./sql-server-linux-manage-ssms.md).
  
* Para obter um exemplo com procedimentos armazenados, siga o tutorial [Configurar a Replicação do SQL Server em Linux](sql-server-linux-replication-tutorial-tsql.md).

## <a name="prerequisites"></a>Prerequisites

Antes de configurar publicadores, distribuidores e assinantes, é necessário concluir algumas etapas de configuração para a instância do SQL Server.

1. Habilite o SQL Server Agent para usar agentes de replicação. Em todos os servidores Linux, execute os seguintes comandos no terminal.

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
  ```

1. Configure a instância do SQL Server para replicação. Para configurar a instância do SQL Server para replicação, execute `sys.sp_MSrepl_createdatatypemappings` em todas as instâncias que participam da replicação.

  ```sql
  USE msdb
  GO
  exec sys.sp_MSrepl_createdatatypemappings;
  GO
  ```

1. Crie uma pasta de instantâneo. Os agentes do SQL Server exigem uma pasta de instantâneo para ler/na qual gravar. Crie a pasta de instantâneo no distribuidor.

  Para criar a pasta de instantâneo e permitir acesso ao usuário `mssql`, execute o seguinte comando:

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

## <a name="configure-and-monitor-replication-with-sql-server-management-studio-ssms"></a>Configurar e monitorar a replicação com o SSMS (SQL Server Management Studio)

### <a name="configure-the-distributor"></a>Configurar o distribuidor
  
Para configurar o distribuidor: 

1. No SSMS, conecte-se à sua instância do SQL Server no Pesquisador de Objetos.

1. Clique com o botão direito do mouse em **Replicação** e em **Configurar Distribuição...** .

1. Siga as instruções no **Assistente para Configurar Distribuição**.

### <a name="create-publication-and-articles"></a>Criar publicação e artigos

Para criar uma publicação e artigos:

1. No Pesquisador de Objetos, clique em **Replicação** > **Publicações Locais**> **Nova Publicação...** .

1. Siga a instrução no **Assistente de Nova Publicação** para configurar o tipo de replicação e os artigos que pertencem à publicação.

### <a name="configure-the-subscription"></a>Configurar a assinatura

Para configurar a assinatura no Pesquisador de Objetos, clique em **Replicação** > **Assinaturas Locais**> **Novas Assinaturas...** .

### <a name="monitor-replication-jobs"></a>Monitorar trabalhos de replicação

Use o Monitor de Replicação para monitorar trabalhos de replicação.

No Pesquisador de Objetos, clique com o botão direito do mouse em **Replicação** e clique em **Iniciar o Monitor de Replicação**.

## <a name="next-steps"></a>Próximas etapas

[Conceitos: Replicação do SQL Server em Linux](sql-server-linux-replication.md)

[Procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

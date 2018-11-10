---
title: Configurar a replicação do SQL Server no Linux | Microsoft Docs
description: Este artigo descreve como configurar a replicação do SQL Server no Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.workload: On Demand
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 71ad9b87f701a1f1de4f13a7788bba13543056e8
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030013"
---
# <a name="configure-sql-server-replication-on-linux"></a>Configurar a replicação do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] apresenta a replicação do SQL Server para instâncias do SQL Server no Linux.

Para obter informações detalhadas sobre a replicação, consulte [documentação do SQL Server replication](../relational-databases/replication/sql-server-replication.md).

Configure a replicação no Linux com o SQL Server Management Studio (SSMS) ou procedimentos armazenados do Transact-SQL.

* Para usar o SSMS, siga as instruções neste artigo.

  Use o SSMS em um sistema de operacional do Windows para se conectar a instâncias do SQL Server. Para informações detalhadas e instruções, consulte [usar o SSMS para gerenciar o SQL Server no Linux](./sql-server-linux-manage-ssms.md).
  
* Para obter um exemplo com procedimentos armazenados, execute as [replicação de configurar o SQL Server no Linux](sql-server-linux-replication-tutorial-tsql.md) tutorial.

## <a name="prerequisites"></a>Prerequisites

Antes de configurar os publicadores, distribuidores e assinantes, você precisará concluir algumas etapas de configuração para a instância do SQL Server.

1. Habilite o SQL Server Agent para usar agentes de replicação. Em todos os servidores do Linux, execute os seguintes comandos no terminal.

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

1. Crie uma pasta de instantâneo. Os agentes do SQL Server exigem uma pasta de instantâneo, leitura/gravação. Crie a pasta de instantâneo no distribuidor.

  Para criar a pasta de instantâneo e conceder acesso a `mssql` usuário, execute o seguinte comando:

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

## <a name="configure-and-monitor-replication-with-sql-server-management-studio-ssms"></a>Configurar e monitorar a replicação com o SQL Server Management Studio (SSMS)

### <a name="configure-the-distributor"></a>Configurar o distribuidor
  
Para configurar o distribuidor: 

1. No SSMS se conectar à sua instância do SQL Server no Pesquisador de objetos.

1. Clique com botão direito **replicação**e clique em **Configurar distribuição...** .

1. Siga as instruções sobre o **Assistente para configurar distribuição**.

### <a name="create-publication-and-articles"></a>Criar a publicação e os artigos

Para criar uma publicação e os artigos:

1. No Pesquisador de objetos, clique em **replicação** > **publicações locais**> **nova publicação...** .

1. Siga as instruções o **Assistente para nova publicação** para configurar o tipo de replicação e os artigos que pertencem à publicação.

### <a name="configure-the-subscription"></a>Configurar a assinatura

Para configurar a assinatura no Pesquisador de objetos, clique em **replicação** > **assinaturas locais**> **novas assinaturas...** .

### <a name="monitor-replication-jobs"></a>Monitorar trabalhos de replicação

Use o Replication Monitor para monitorar trabalhos de replicação.

No Pesquisador de objetos, clique com botão direito **replicação**e clique em **iniciar o Replication Monitor**.

## <a name="next-steps"></a>Próximas etapas

[Conceitos: Replicação do SQL Server no Linux](sql-server-linux-replication.md)

[Procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

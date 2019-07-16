---
title: Conectar-se ao mestre e HDFS
titleSuffix: SQL Server big data clusters
description: Saiba como se conectar a instância mestre do SQL Server e o gateway HDFS/Spark para um cluster de big data do SQL Server 2019 (visualização).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1f09763b210427c84efe75d693fee302d7048db7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958641"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conectar a um cluster de big data do SQL Server com o Studio de dados do Azure

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como se conectar a um cluster de big data de 2019 do SQL Server (versão prévia) no Studio de dados do Azure.

## <a name="prerequisites"></a>Pré-requisitos

- Implantado [cluster de big data do SQL Server 2019](deployment-guidance.md).
- [Ferramentas de big data do SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensão do SQL Server de 2019**
   - **kubectl**

## <a id="master"></a> Conectar-se ao cluster

Para se conectar a um cluster de big data com o Azure Data Studio, faça uma nova conexão para a instância mestre do SQL Server no cluster. As etapas a seguir descrevem como conectar-se à instância mestre usando o Studio de dados do Azure.

1. Na linha de comando, localize o IP da sua instância mestre com o seguinte comando:

   ```
   kubectl get svc master-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > O big data padrão é nome do cluster **mssql-cluster** , a menos que você personalizou o nome em um arquivo de configuração de implantação. Para obter mais informações, consulte [definir as configurações de implantação para clusters de big data](deployment-custom-configuration.md#clustername).

1. No Azure Data Studio, pressione **F1** > **nova Conexão**.

1. Na **tipo de Conexão**, selecione **Microsoft SQL Server**.

1. Digite o endereço IP da instância mestre do SQL Server no **nome do servidor** (por exemplo: **\<Endereço IP\>, 31433**).

1. Insira um logon do SQL **nome de usuário** e **senha**.

   > [!TIP]
   > Por padrão, é o nome de usuário **SA** e, a menos que alteradas, a senha corresponde à **MSSQL_SA_PASSWORD** variável de ambiente usada durante a implantação.

1. Alterar o destino **nome do banco de dados** para um dos seus bancos de dados relacionais.

   ![Conectar-se à instância do mestre](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. Pressione **Connect**e o **painel Server** deve aparecer.

Com a versão de fevereiro de 2019 do estúdio de dados do Azure, conectar-se a instância mestre do SQL Server também permite que você interaja com o gateway HDFS/Spark. Isso significa que você não precisará usar uma conexão separada para HDFS e o Spark que descreve a próxima seção.

- O Pesquisador de objetos agora contém uma nova **serviços de dados** nó com o botão direito do mouse suporte para tarefas de cluster de big data, como criar novos notebooks ou envio de trabalhos do spark. 
- O **serviços de dados** nó também contém uma **HDFS** pasta para executar as ações, como Create External Table ou analisar no bloco de anotações e exploração de HDFS.
- O **painel do servidor** para a conexão também contém guias para **cluster de big data do SQL Server** e **2019 do SQL Server (versão prévia)** quando a extensão está instalada.

   ![Nó de serviços de dados do Azure Data Studio](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data de 2019 do SQL Server, consulte [quais são os clusters do SQL Server 2019 grandes dados](big-data-cluster-overview.md).
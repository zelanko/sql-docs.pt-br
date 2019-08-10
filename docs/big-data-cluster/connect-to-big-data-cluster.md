---
title: Conectar-se ao mestre e ao HDFS
titleSuffix: SQL Server big data clusters
description: Saiba como se conectar à instância mestre do SQL Server e ao gateway HDFS/Spark para um cluster de Big Data do SQL Server 2019 (versão prévia).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1f09763b210427c84efe75d693fee302d7048db7
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958641"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como se conectar a um cluster de Big Data do SQL Server 2019 (versão prévia) do Azure Data Studio.

## <a name="prerequisites"></a>Prerequisites

- Um [cluster de Big Data do SQL Server 2019](deployment-guidance.md) implantado.
- [Ferramentas de Big Data do SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensão do SQL Server 2019**
   - **kubectl**

## <a id="master"></a> Conectar-se ao cluster

Para se conectar a um cluster de Big Data com o Azure Data Studio, faça uma nova conexão com a instância mestre do SQL Server no cluster. As etapas a seguir descrevem como se conectar à instância mestre usando o Azure Data Studio.

1. Na linha de comando, localize o IP da sua instância mestre com o seguinte comando:

   ```
   kubectl get svc master-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > O nome do cluster de Big Data usa **mssql-cluster** como padrão, a menos que você tenha personalizado o nome em um arquivo de configuração de implantação. Para obter mais informações, confira [Definir configurações de implantação para clusters de Big Data](deployment-custom-configuration.md#clustername).

1. No Azure Data Studio, pressione **F1** > **Nova Conexão**.

1. Em **Tipo de conexão**, selecione **Microsoft SQL Server**.

1. Digite o endereço IP da instância mestre do SQL Server no **Nome do servidor** (por exemplo: **\<Endereço IP\>,31433**).

1. Insira um **Nome de usuário** e uma **Senha** de logon do SQL.

   > [!TIP]
   > Por padrão, o nome de usuário é **SA** e, a menos que alterada, a senha corresponde à variável de ambiente **MSSQL_SA_PASSWORD** usada durante a implantação.

1. Altere o **Nome do banco de dados** de destino para um de seus bancos de dados relacionais.

   ![Conectar-se à instância mestre](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. Pressione **Conectar**, e o **Painel do Servidor** deverá aparecer.

Com a versão de fevereiro de 2019 do Azure Data Studio, a conexão com a instância mestre do SQL Server também permite que você interaja com o gateway HDFS/Spark. Isso significa que você não precisa usar uma conexão separada para o HDFS e Spark que a próxima seção descreve.

- Agora, o Pesquisador de Objetos contém um novo nó de **Serviços de Dados** com suporte do botão direito do mouse para tarefas de cluster de Big Data, como criar novos notebooks ou enviar trabalhos do Spark. 
- O nó de **Serviços de Dados** também contém uma pasta **HDFS** para exploração do HDFS e execução de ações como criar tabela externa ou analisar no notebook.
- O **Painel do Servidor** para a conexão também contém guias para **cluster de Big Data do SQL Server** e **SQL Server 2019 (versão prévia)** quando a extensão é instalada.

   ![Nó de Serviços de Dados do Azure Data Studio](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os clusters de Big Data do SQL Server 2019, confira [O que são clusters de Big Data do SQL Server 2019?](big-data-cluster-overview.md).
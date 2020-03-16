---
title: Conectar-se a clusters de Big Data mestre e do HDFS
description: Saiba como se conectar à instância mestre do SQL Server e ao gateway HDFS/Spark para um Cluster de Big Data do SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0c5ba08a492be621e4b1f8871bdfcb49983af26d
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79285980"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como se conectar a um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] do Azure Data Studio.

## <a name="prerequisites"></a>Pré-requisitos

- Um [cluster de Big Data do SQL Server 2019](deployment-guidance.md) implantado.
- [Ferramentas de Big Data do SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensão do SQL Server 2019**
   - **kubectl**
   - **azdata**

## <a id="master"></a> Conectar-se ao cluster

Para se conectar a um cluster de Big Data com o Azure Data Studio, faça uma nova conexão com a instância mestre do SQL Server no cluster. Veja como.

1. Localize o ponto de extremidade da instância mestre do SQL Server:

   ```
   azdata bdc endpoint list -e sql-server-master
   ```

   > [!TIP]
   > Para obter mais informações sobre como recuperar pontos de extremidade, confira [Recuperar pontos de extremidade](deployment-guidance.md#endpoints).

1. No Azure Data Studio, pressione **F1** > **Nova Conexão**.

1. Em **Tipo de conexão**, selecione **Microsoft SQL Server**.

1. Digite o nome do ponto de extremidade que você encontrou para a instância mestre do SQL Server na caixa de texto **Nome do servidor** (por exemplo: **\<IP_Address\>,31433**). 

1. Escolha seu tipo de autenticação. Para a instância mestre do SQL Server em execução em um cluster de Big Data, somente a **Autenticação do Windows** e o **logon do SQL** têm suporte. 

1. Se estiver usando o logon do SQL, insira seu **nome de usuário** e **senha** de logon do SQL.

   > [!TIP]
   > Por padrão, o nome de usuário **SA** é desabilitado durante a implantação do cluster de Big Data. Um novo usuário sysadmin é provisionado durante a implantação, com o nome e a senha correspondentes às variáveis de ambiente **AZDATA_USERNAME** e **AZDATA_PASSWORD**, que foram definidas durante a implantação ou antes dela.

1. Altere o **Nome do banco de dados** de destino para um de seus bancos de dados relacionais.

   ![Conectar-se à instância mestre](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. Pressione **Conectar**, e o **Painel do Servidor** deverá aparecer.

Com a versão de fevereiro de 2019 do Azure Data Studio, a conexão com a instância mestre do SQL Server também permite que você interaja com o gateway HDFS/Spark. Isso significa que você não precisa usar uma conexão separada para o HDFS e Spark que a próxima seção descreve.

- Agora, o Pesquisador de Objetos contém um novo nó de **Serviços de Dados** com suporte do botão direito do mouse para tarefas de cluster de Big Data, como criar novos notebooks ou enviar trabalhos do Spark. 
- O nó **Serviços de Dados** também contém uma pasta **HDFS** para permitir que você explore o conteúdo do HDFS e execute tarefas comuns envolvendo o HDFS (por exemplo, criar uma tabela externa ou abrir um notebook para analisar o conteúdo do HDFS).
- O **Painel do Servidor** para a conexão também contém guias para o **cluster de Big Data do SQL Server** e o **SQL Server 2019** quando a extensão é instalada.

   ![Nó de Serviços de Dados do Azure Data Studio](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md).

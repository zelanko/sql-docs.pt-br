---
title: Conectar-se ao mestre e HDFS
titleSuffix: SQL Server 2019 big data clusters
description: Saiba como se conectar a instância mestre do SQL Server e o gateway HDFS/Spark para um cluster de big data do SQL Server 2019 (visualização).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/10/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 8bccadd8fbce9fe2a8cc6f16db75dbd09f3d1ed0
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53264358"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conectar a um cluster de big data do SQL Server com o Studio de dados do Azure

Este artigo descreve como se conectar a um cluster de big data de 2019 do SQL Server (versão prévia) no Studio de dados do Azure.

## <a name="prerequisites"></a>Prerequisites

- Implantado [cluster de big data do SQL Server 2019](deployment-guidance.md).
- [Ferramentas de big data do SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensão do SQL Server de 2019**
   - **Kubectl**

## <a name="connect-to-the-cluster"></a>Conectar-se ao cluster

Quando você se conectar a um cluster de big data, você tem a opção para se conectar ao SQL Server [instância mestre](concept-master-instance.md) ou para o gateway HDFS/Spark. As seções a seguir mostram como se conectar a cada um.

## <a id="master"></a> Instância principal

A instância mestre do SQL Server é uma instância do SQL Server tradicional que contém os bancos de dados relacionais do SQL Server. As etapas a seguir descrevem como conectar-se à instância mestre usando o Studio de dados do Azure.

1. Na linha de comando, localize o IP da sua instância mestre com o seguinte comando:

   ```
   kubectl get svc endpoint-master-pool -n <your-cluster-name>
   ```

1. No Azure Data Studio, pressione **F1** > **nova Conexão**.

1. Na **tipo de Conexão**, selecione **Microsoft SQL Server**.

1. Digite o endereço IP da instância mestre do SQL Server no **nome do servidor** (por exemplo: **\<Endereço IP\>, 31433**).

1. Insira um logon do SQL **nome de usuário** e **senha**.

   > [!TIP]
   > Por padrão, é o nome de usuário **SA** e, a menos que alteradas, a senha corresponde à **MSSQL_SA_PASSWORD** variável de ambiente usada durante a implantação.

1. Alterar o destino **nome do banco de dados** para um dos seus bancos de dados relacionais.

   ![Conectar-se à instância do mestre](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. Pressione **Connect**e o **painel Server** deve aparecer.

## <a id="hdfs"></a> Gateway HDFS/Spark

O **gateway HDFS/Spark** permite que você conecte para trabalhar com o pool de armazenamento do HDFS e executar trabalhos do Spark. As etapas a seguir descrevem como conectar-se com o Studio de dados do Azure.

1. Na linha de comando, localize o endereço IP do seu gateway HDFS/Spark com um dos comandos a seguir.
   
   **Implantações de AKS:**

   ```
   kubectl get svc service-security-lb -n <your-cluster-name>
   ```

   **Implantações de AKS não**:

   ```
   kubectl get svc service-security-nodeport -n <your-cluster-name>
   ```
 
1. No Azure Data Studio, pressione **F1** > **nova Conexão**.

1. Na **tipo de Conexão**, selecione **cluster de big data do SQL Server**.

1. Digite o endereço IP do cluster de big data no **nome do servidor** (não especificar uma porta).

1. Insira `root` para o **usuário** e especifique o **senha** para seu cluster de big data.

   ![Conectar-se ao gateway HDFS/Spark](./media/connect-to-big-data-cluster/connect-to-cluster-hdfs-spark.png)

   > [!TIP]
   > Por padrão, é o nome de usuário **raiz** e a senha corresponde à **KNOX_PASSWORD** variável de ambiente usada durante a implantação.

1. Pressione **Connect**e o **painel Server** deve aparecer.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data de 2019 do SQL Server, consulte [quais são os clusters do SQL Server 2019 grandes dados](big-data-cluster-overview.md).
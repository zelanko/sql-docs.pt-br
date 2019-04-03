---
title: Conectar-se ao mestre e HDFS
titleSuffix: SQL Server big data clusters
description: Saiba como se conectar a instância mestre do SQL Server e o gateway HDFS/Spark para um cluster de big data do SQL Server 2019 (visualização).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed563fe6d0bfd69ce5dfb7484d4213bc9a47dd54
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860167"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conectar a um cluster de big data do SQL Server com o Studio de dados do Azure

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como se conectar a um cluster de big data de 2019 do SQL Server (versão prévia) no Studio de dados do Azure. Há dois pontos de extremidade principais são usados para interagir com um cluster de big data:

| Ponto de extremidade | Descrição |
|---|---|
| Instância mestre do SQL Server | A instância mestre do SQL Server no cluster que contém os bancos de dados relacionais do SQL Server. |
| Gateway HDFS/Spark | Acesso ao armazenamento do HDFS no cluster e a capacidade de executar trabalhos do Spark. |

> [!TIP]
> Com a versão de fevereiro de 2019 do estúdio de dados do Azure, conectar-se automaticamente a instância mestre do SQL Server fornece acesso de interface do usuário para o gateway HDFS/Spark.

## <a name="prerequisites"></a>Prerequisites

- Implantado [cluster de big data do SQL Server 2019](deployment-guidance.md).
- [Ferramentas de big data do SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensão do SQL Server de 2019**
   - **Kubectl**

## <a id="master"></a> Conectar-se ao cluster

Para se conectar a um cluster de big data com o Azure Data Studio, faça uma nova conexão para a instância mestre do SQL Server no cluster. As etapas a seguir descrevem como conectar-se à instância mestre usando o Studio de dados do Azure.

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

Com a versão de fevereiro de 2019 do estúdio de dados do Azure, conectar-se a instância mestre do SQL Server também permite que você interaja com o gateway HDFS/Spark. Isso significa que você não precisará usar uma conexão separada para HDFS e o Spark que descreve a próxima seção.

- O Pesquisador de objetos agora contém uma nova **serviços de dados** nó com o botão direito do mouse suporte para tarefas de cluster de big data, como criar novos notebooks ou envio de trabalhos do spark. 
- O **serviços de dados** nó também contém uma **HDFS** pasta para executar as ações, como Create External Table ou analisar no bloco de anotações e exploração de HDFS.
- O **painel do servidor** para a conexão também contém guias para **cluster de big data do SQL Server** e **2019 do SQL Server (versão prévia)** quando a extensão está instalada.

   ![Nó de serviços de dados do Azure Data Studio](./media/connect-to-big-data-cluster/connect-data-services-node.png)

> [!IMPORTANT]
> Se você vir **erro desconhecido** na interface do usuário, talvez você precise [conectar-se diretamente ao gateway de HDFS/Spark](#hdfs). Uma causa desse erro são senhas diferentes para a instância mestre do SQL Server e o gateway HDFS/Spark. O estúdio de dados do Azure pressupõe que a mesma senha é usada para ambos.
  
## <a id="hdfs"></a> Conectar ao gateway de HDFS/Spark

Na maioria dos casos, conectando-se a instância mestre do SQL Server fornece acesso para o HDFS e o Spark também por meio de **serviços de dados** nó. No entanto, você ainda pode criar uma conexão dedicada para o **gateway HDFS/Spark** se necessário. As etapas a seguir descrevem como conectar-se com o Studio de dados do Azure.

1. Na linha de comando, localize o endereço IP do seu gateway HDFS/Spark com um dos comandos a seguir.

   ```
   kubectl get svc endpoint-security -n <your-cluster-name>
   ```
 
1. No Azure Data Studio, pressione **F1** > **nova Conexão**.

1. Na **tipo de Conexão**, selecione **cluster de big data do SQL Server**.

   > [!TIP]
   > Se você não vir as **cluster de big data do SQL Server** conexão de tipo, certifique-se de ter instalado o [extensão do SQL Server 2019](../azure-data-studio/sql-server-2019-extension.md) e que você reiniciou o estúdio de dados do Azure após a conclusão de extensão instalando.

1. Digite o endereço IP do cluster de big data no **nome do servidor** (não especificar uma porta).

1. Insira `root` para o **usuário** e especifique o **senha** para seu cluster de big data.

   ![Conectar-se ao gateway HDFS/Spark](./media/connect-to-big-data-cluster/connect-to-cluster-hdfs-spark.png)

   > [!TIP]
   > Por padrão, é o nome de usuário **raiz** e a senha corresponde à **KNOX_PASSWORD** variável de ambiente usada durante a implantação.

1. Pressione **Connect**e o **painel Server** deve aparecer.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data de 2019 do SQL Server, consulte [quais são os clusters do SQL Server 2019 grandes dados](big-data-cluster-overview.md).
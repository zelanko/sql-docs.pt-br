---
title: Conectar a um servidor SQL grandes dados de cluster com o Studio de dados do Azure | Microsoft Docs
description: Saiba como se conectar a um cluster de big data 2019 do SQL Server com o Studio de dados do Azure.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 18df937cfed15d7302a58267eb392a1933d73052
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49643784"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conectar a um cluster de big data do SQL Server com o Studio de dados do Azure

Este artigo descreve como instalar o estúdio de dados do Azure, a extensão do SQL Server 2019 (visualização) e, em seguida, conecte-se a um cluster de big data. A nova extensão do SQL Server 2019 inclui suporte para visualização [clusters do SQL Server 2019 big data](big-data-cluster-overview.md), um integrada [experiência de notebook](notebooks-guidance.md)e um PolyBase [assistente Create External Table](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-azure-data-studio"></a>Instalar o Studio de dados do Azure

Para instalar o Azure Data Studio, consulte [Baixe e instale a versão mais recente do Azure Data Studio](../azure-data-studio/download.md).

## <a name="install-the-sql-server-2019-extension-preview"></a>Instalar a extensão do SQL Server 2019 (visualização)

Para instalar a extensão, consulte [instalar a extensão de 2019 do SQL Server (versão prévia)](../azure-data-studio/sql-server-2019-extension.md).

## <a name="connect-to-the-cluster"></a>Conectar-se ao cluster

Quando você se conectar a um cluster de big data, você tem a opção para se conectar ao SQL Server [instância mestre](concept-master-instance.md) ou para o gateway HDFS/Spark. As seções a seguir mostram como se conectar a cada um.

## <a id="master"></a> Instância principal

1. No Azure Data Studio, pressione **F1** > **nova Conexão**.

1. Na **tipo de Conexão**, selecione **Microsoft SQL Server**.

1. Digite o endereço IP da instância mestre do SQL Server no **nome do servidor** (por exemplo:  **\<endereço IP\>, 31433**).

1. Insira um logon do SQL **nome de usuário** e **senha**.

1. Alterar o **nome do banco de dados** para o **high_value_data** banco de dados.

   ![Conectar-se à instância do mestre](./media/deploy-big-data-tools/connect-to-cluster.png)

1. Pressione **Connect**e o **painel Server** deve aparecer.

## <a id="hdfs"></a> Gateway HDFS/Spark

1. No Azure Data Studio, pressione **F1** > **nova Conexão**.

1. Na **tipo de Conexão**, selecione **cluster de big data do SQL Server**.

1. Digite o endereço IP do cluster de big data no **nome do servidor**.

1. Insira `root` para o **usuário** e especifique o **senha** para seu cluster de big data.

   ![Conectar-se ao gateway HDFS/Spark](./media/deploy-big-data-tools/connect-to-cluster-hdfs-spark.png)

1. Pressione **Connect**e o **painel Server** deve aparecer.

## <a name="next-steps"></a>Próximas etapas

Para executar os notebooks no estúdio de dados do Azure, consulte [como usar blocos de anotações na visualização do SQL Server 2019](notebooks-guidance.md).

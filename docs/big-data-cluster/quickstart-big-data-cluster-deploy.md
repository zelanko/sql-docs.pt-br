---
title: Implantar com um script Python
titleSuffix: SQL Server Big Data Clusters
description: Saiba como usar um script de implantação para implantar Clusters de Big Data do SQL Server no AKS (Serviço Kubernetes do Azure).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: eea087ed3a4859e179f7bb0d1e77140bb8229a17
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77608387"
---
# <a name="use-a-python-script-to-deploy-a-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Usar um script Python para implantar um cluster de Big Data do SQL Server no AKS (Serviço de Kubernetes do Azure)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Neste tutorial, use um script de implantação Python de exemplo para implantar um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] no AKS (Serviço Kubernetes do Azure).

> [!TIP]
> O AKS é apenas uma opção para hospedar o Kubernetes para seu cluster de Big Data. Para saber mais sobre outras opções de implantação, bem como personalizar opções de implantação, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md).

A implantação padrão de cluster de Big Data usada aqui consiste em uma instância do SQL mestre, uma instância do pool de computação, duas instâncias do pool de dados e duas instâncias do pool de armazenamento. Os dados são persistidos usando volumes persistentes do Kubernetes que usam as classes de armazenamento padrão do AKS. A configuração padrão usada neste tutorial é adequada para ambientes de desenvolvimento/teste.

## <a name="prerequisites"></a>Pré-requisitos

- Uma assinatura do Azure.
- [Ferramentas de Big Data](deploy-big-data-tools.md):
   - **azdata**
   - **kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server 2019**
   - **CLI do Azure**

## <a name="log-in-to-your-azure-account"></a>Faça logon na sua conta do Azure

O script usa a CLI do Azure para automatizar a criação de um cluster do AKS. Antes de executar o script, você deve fazer logon em sua conta do Azure com a CLI do Azure pelo menos uma vez. Execute o seguinte comando de um prompt de comando.

```
az login
```

## <a name="download-the-deployment-script"></a>Baixar o script de implantação

Este tutorial automatiza a criação do cluster de Big Data no AKS usando um script Python **deploy-sql-big-data-aks.py**. Se você já tiver instalado o Python para **azdata**, poderá executar o script com êxito neste tutorial. 

Em um prompt de Bash do Windows PowerShell ou Linux, execute o seguinte comando para baixar o script de implantação do GitHub.

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>Executar o script de implantação

Use as etapas a seguir para executar o script de implantação em um prompt do Bash do Linux ou Windows PowerShell. Esse script criará um serviço AKS no Azure e, em seguida, implantará um cluster de Big Data do SQL Server 2019 no AKS. Você também pode modificar o script com outras [variáveis de ambiente](deployment-guidance.md#configfile) para criar uma implantação personalizada.

1. Execute o script com o seguinte comando:

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > Se você tiver python3 e python2 no computador cliente e no caminho, será necessário executar o comando usando python3: `python3 deploy-sql-big-data-aks.py`.

1. Quando solicitadas, insira as seguintes informações:

   | Valor | Descrição |
   |---|---|
   | **ID da assinatura do Azure** | A ID da assinatura do Azure a ser usada no AKS. Você pode listar todas as suas assinaturas e suas IDs executando `az account list` de outra linha de comando. |
   | **Grupo de recursos do Azure** | O nome do grupo de recursos do Azure a ser criado para o cluster do AKS. |
   | **Região do Azure** | A região do Azure para o novo cluster do AKS (**westus** padrão). |
   | **Tamanho do computador** | O [tamanho do computador](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) a ser usado para os nós no cluster do AKS (**Standard_L8s** padrão). |
   | **Nó de trabalho** | O número de nós de trabalho no cluster do AKS (**1** padrão). |
   | **Nome do cluster** | O nome do cluster do AKS e do cluster de Big Data. O nome do cluster de Big Data deve ter apenas caracteres alfanuméricos minúsculos e nenhum espaço. (**sqlbigdata** padrão). |
   | **Senha** | Senha para o controlador, o gateway HDFS/Spark e a instância mestre (**MySQLBigData2019** padrão). |
   | **Nome de usuário** | Nome de usuário do controlador (padrão: **admin**). |

   > [!IMPORTANT]
   > O tamanho padrão do computador **Standard_L8s** pode não estar disponível em todas as regiões do Azure. Se você selecionar um tamanho de computador diferente, verifique se o número total de discos que podem ser anexados entre os nós no cluster é maior ou igual a 24. Cada declaração de volume persistente no cluster requer um disco anexado. Atualmente, o cluster de Big Data requer 24 declarações de volume persistente. Por exemplo, o tamanho do computador [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/lsv2-series) dá suporte a 32 discos anexados, portanto, você pode avaliar clusters de Big Data com um único nó desse tamanho de computador.

   > [!NOTE]
   > A conta `sa` do SQL Server é desabilitada durante a implantação do cluster de Big Data. Um novo logon sysadmin é provisionado na instância mestra do SQL Server com o mesmo nome especificado para a entrada de **Nome de usuário** e a senha correspondente à entrada **Senha**. Os mesmos valores de **Nome de usuário** e **Senha** são usados para provisionar um usuário administrador do controlador. O único usuário com suporte para o gateway (Knox) é **raiz** e a senha é a mesma que a apresentada acima.

1. O script será iniciado criando um cluster do AKS usando os parâmetros especificados. Esta etapa demora vários minutos.

## <a name="monitor-the-status"></a>Monitorar o status

Depois que o script cria o cluster do AKS, ele continua a definir as variáveis de ambiente necessárias com as configurações especificadas anteriormente. Em seguida, ele chama **azdata** para implantar o cluster de Big Data no AKS.

A janela Comando do cliente produzirá o status da implantação. Durante o processo de implantação, você deverá ver uma série de mensagens em que ele está aguardando o pod do controlador:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

Após 10 a 20 minutos, você deve ser notificado de que o pod do controlador está em execução:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> A implantação inteira pode ser muito demorada devido ao tempo necessário para baixar as imagens de contêiner para os componentes do cluster de Big Data. No entanto, não deve demorar várias horas. Se estiver encontrando problemas em sua implantação, confira [Monitoramento e solução de problemas de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](cluster-troubleshooting-commands.md).

## <a name="inspect-the-cluster"></a>Inspecionar o cluster

A qualquer momento durante a implantação, você pode usar **kubectl** ou **azdata** para inspecionar o status e os detalhes sobre o cluster de Big Data em execução.

### <a name="use-kubectl"></a>Usar kubectl

Abra uma nova janela Comando para usar **kubectl** durante o processo de implantação.

1. Execute o seguinte comando para obter um resumo do status do cluster inteiro:

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se você não alterou o nome do cluster de Big Data, o script usa **sqlbigdata** como padrão.

1. Inspecione os serviços do Kubernetes e seus pontos de extremidade internos e externos com o seguinte comando **kubectl**:

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. Você também pode inspecionar o status dos pods do Kubernetes com o seguinte comando:

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. Saiba mais sobre um pod específico com o seguinte comando:

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> Para obter mais detalhes sobre como monitorar e solucionar problemas de implantação, confira [Monitoramento e solução de problemas de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](cluster-troubleshooting-commands.md).

## <a name="connect-to-the-cluster"></a>Conectar-se ao cluster

Quando o script de implantação for concluído, a saída notificará você sobre o sucesso:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

O cluster de Big Data do SQL Server já está implantado no AKS. Agora você pode usar Azure Data Studio para se conectar ao cluster. Para obter mais informações, confira [Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="clean-up"></a>Limpar

Se você estiver testando [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Azure, deverá excluir o cluster do AKS quando terminar para evitar encargos inesperados. Não remova o cluster se pretender continuar a usá-lo.

> [!WARNING]
> As etapas a seguir desmontam o cluster do AKS, que remove o cluster de Big Data do SQL Server também. Se você tiver bancos de dados ou dados do HDFS que deseja manter, faça backup desses dados antes de excluir o cluster.

Execute o seguinte comando da CLI do Azure para remover o cluster de Big Data e o serviço do AKS no Azure (substitua `<resource group name>` pelo **grupo de recursos do Azure** especificado no script de implantação):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>Próximas etapas

O script de implantação configurou o Serviço de Kubernetes do Azure e também implantou um cluster de Big Data do SQL Server 2019. Você também pode optar por personalizar implantações futuras por meio de instalações manuais. Para saber mais sobre como os clusters de Big Data são implantados e como personalizar implantações, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md).

Agora que o cluster de Big Data do SQL Server está implantado, você pode carregar dados de exemplo e explorar os tutoriais:

> [!div class="nextstepaction"]
> [Tutorial: Carregar dados de exemplo em um cluster de Big Data do SQL Server 2019](tutorial-load-sample-data.md)

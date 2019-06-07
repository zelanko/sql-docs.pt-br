---
title: Início rápido da implantação
titleSuffix: SQL Server big data clusters
description: Passo a passo uma implantação de clusters de big data 2019 do SQL Server (versão prévia) no serviço de Kubernetes do Azure (AKS).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: quickstart
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a385a2691d37bf31186a3530e91bdf937ac4dc05
ms.sourcegitcommit: 32dce314bb66c03043a93ccf6e972af455349377
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66744207"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Início Rápido: Implantar um cluster de big data do SQL Server no serviço de Kubernetes do Azure (AKS)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Neste início rápido, você pode usar um exemplo de script de implantação para implantar o cluster de big data de 2019 do SQL Server (versão prévia) para o serviço de Kubernetes do Azure (AKS). 

> [!TIP]
> O AKS é apenas uma opção para hospedagem de Kubernetes para seu cluster de big data. Para saber mais sobre outras opções de implantação, como personalizar a implantação de opções, consulte [clusters de como implantar grandes de dados do SQL Server em Kubernetes](deployment-guidance.md).

A implantação de cluster de big data padrão usada aqui consiste em duas instâncias de pool de armazenamento, computação de uma instância de pool, duas instâncias de pool de dados e uma instância do SQL Master. Os dados persistem usando volumes persistentes Kubernetes que usam as classes de armazenamento de padrão do AKS. A configuração padrão usada neste início rápido é adequada para ambientes de desenvolvimento/teste.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>Prerequisites

- Uma assinatura do Azure.
- [Ferramentas de big data](deploy-big-data-tools.md):
   - **mssqlctl**
   - **kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server de 2019**
   - **CLI do Azure**

## <a name="log-in-to-your-azure-account"></a>Faça logon sua conta do Azure

O script usa a CLI do Azure para automatizar a criação de um cluster do AKS. Antes de executar o script, você deve fazer logon sua conta do Azure com CLI do Azure pelo menos uma vez. Execute o seguinte comando em um prompt de comando.

```
az login
```

## <a name="download-the-deployment-script"></a>Baixe o script de implantação

Neste início rápido automatiza a criação do cluster de big data no AKS usando um script python **implantar-sql-big-data-aks.py**. Se você tiver instalado o python para o **mssqlctl**, você deve ser capaz de executar o script com êxito neste início rápido. 

Em um prompt de bash do Windows PowerShell ou do Linux, execute o seguinte comando para baixar o script de implantação do GitHub.

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>Execute o script de implantação

Use as etapas a seguir para executar o script de implantação. Esse script criará um serviço AKS no Azure e, em seguida, implantar um cluster de big data 2019 do SQL Server no AKS. Você também pode modificar o script com os outros [variáveis de ambiente](deployment-guidance.md#configfile) para criar uma implantação personalizada.

1. Execute o script com o seguinte comando:

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > Se você tiver o python3 e python2 no computador cliente e no caminho, você precisa executar o comando usando python3: `python3 deploy-sql-big-data-aks.py`.

1. Quando solicitado, insira as seguintes informações:

   | Valor | Descrição |
   |---|---|
   | **ID da assinatura do Azure** | A ID de assinatura do Azure a ser usado para o AKS. Você pode listar todas as suas assinaturas e suas IDs executando `az account list` de outra linha de comando. |
   | **Grupo de recursos do Azure** | O nome do grupo de recursos do Azure para criar para o cluster do AKS. |
   | **Nome de usuário do docker** | O nome de usuário de Docker fornecido como parte da visualização pública limitada. |
   | **Senha do docker** | A senha de Docker fornecida como parte da visualização pública limitada. |
   | **Região do Azure** | A região do Azure para o novo cluster do AKS (padrão **westus**). |
   | **Tamanho da máquina** | O [tamanho de máquina](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) a ser usado para nós no cluster do AKS (padrão **Standard_L8s**). |
   | **Nós de trabalho** | O número de nós de trabalho no cluster do AKS (padrão **1**). |
   | **Nome do cluster** | O nome do cluster do AKS e o cluster de big data. O nome do seu cluster de big data deve ser apenas caracteres alfanuméricos em letras minúsculas e sem espaços. (padrão **sqlbigdata**). |
   | **Senha** | Senha para o controlador, o gateway HDFS/Spark e a instância mestre (padrão **MySQLBigData2019**). |
   | **Usuário do controlador** | Nome de usuário para o usuário controlador (padrão: **admin**). |

   > [!IMPORTANT]
   > O padrão **Standard_L8s** tamanho da máquina pode não estar disponível em todas as regiões do Azure. Se você selecionar um tamanho de máquina diferente, certifique-se de que o número total de discos que podem ser anexados em todos os nós do cluster é maior que ou igual a 24. Cada declaração de volume persistente no cluster exige um disco anexado. Atualmente, o cluster de big data requer declarações de volume persistente 24. Por exemplo, o [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series) tamanho da máquina dá suporte a 32 discos anexados, portanto, é possível avaliar a clusters de big data com um único nó desse tamanho de máquina.

   > [!NOTE]
   > O `sa` conta é um administrador do sistema na instância mestre do SQL Server que é criada durante a instalação. Depois de criar a implantação, o `MSSQL_SA_PASSWORD` variável de ambiente é detectável executando `echo $MSSQL_SA_PASSWORD` no contêiner de instância principal. Para fins de segurança, altere sua `sa` senha na instância mestre após a implantação. Para obter mais informações, consulte [alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

1. O script começar criando um cluster AKS usando os parâmetros especificados. Esta etapa leva vários minutos.

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>Monitorar o status

Depois que o script cria o cluster do AKS, ele prossegue para definir variáveis de ambiente necessárias com as configurações que você especificou anteriormente. Em seguida, ele chama **mssqlctl** para implantar o cluster de big data no AKS.

A janela de comando do cliente produzirá o status da implantação. Durante o processo de implantação, você deverá ver uma série de mensagens em que ele está aguardando o pod do controlador:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

Depois de 10 a 20 minutos, você deve ser notificado se o pod de controlador está em execução:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> Toda a implantação pode levar muito tempo devido ao tempo necessário para baixar as imagens de contêiner para os componentes do cluster de big data. No entanto, ele não deve levar várias horas. Se você estiver tendo problemas com sua implantação, consulte [monitoramento e solução de problemas de clusters de grandes dados do SQL Server](cluster-troubleshooting-commands.md).

## <a name="inspect-the-cluster"></a>Inspecione o cluster

A qualquer momento durante a implantação, você pode usar **kubectl** ou **mssqlctl** para inspecionar o status e detalhes sobre o cluster de execução big data.

### <a name="use-kubectl"></a>Usar o kubectl

Abra uma nova janela de comando para usar **kubectl** durante o processo de implantação.

1. Execute o seguinte comando para obter um resumo do status de todo o cluster:

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se você não alterou o nome do cluster de big data, o script assume como padrão **sqlbigdata**.

1. Inspecione os serviços do kubernetes e seus pontos de extremidade internos e externos com os seguintes **kubectl** comando:

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. Você também pode inspecionar o status dos pods kubernetes com o seguinte comando:

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. Encontre mais informações sobre um pod específico com o seguinte comando:

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> Para obter mais detalhes sobre como monitorar e solucionar problemas de uma implantação, consulte [monitoramento e solução de problemas de clusters de grandes dados do SQL Server](cluster-troubleshooting-commands.md).

## <a name="connect-to-the-cluster"></a>Conectar-se ao cluster

Quando o script de implantação for concluída, a saída notifica você de sucesso:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

Agora, o cluster de big data do SQL Server é implantado no AKS. Agora você pode usar o Studio de dados do Azure para se conectar ao cluster. Para obter mais informações, consulte [conectar-se a um SQL Server cluster de big data com o Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="clean-up"></a>Limpar

Se você estiver testando a clusters de grandes dados do SQL Server no Azure, você deve excluir o cluster do AKS quando tiver terminado de evitar cobranças inesperadas. Não remova o cluster se você pretende continuar a usá-lo.

> [!WARNING]
> As etapas a seguir destrói o cluster do AKS que remove o cluster de big data do SQL Server. Se você tiver bancos de dados ou dados do HDFS que você deseja manter, fazer esses backup dos dados antes de excluir o cluster.

Execute o seguinte comando da CLI do Azure para remover o cluster de big data e o serviço AKS no Azure (substitua `<resource group name>` com o **grupo de recursos do Azure** especificado no script de implantação):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>Próximas etapas

O script de implantação configurado o serviço Kubernetes do Azure e também implantado um cluster de big data do SQL Server de 2019. Você também pode optar por personalizar as futuras implantações por meio de instalações manuais. Para saber mais sobre como grandes dados clusters são implantados, bem como como personalizar as implantações, consulte [clusters de como implantar grandes de dados do SQL Server em Kubernetes](deployment-guidance.md).

Agora que o cluster de big data do SQL Server é implantado, você pode carregar dados de exemplo e explore os tutoriais:

> [!div class="nextstepaction"]
> [Tutorial: Carregar dados de exemplo em um cluster de big data do SQL Server de 2019](tutorial-load-sample-data.md)
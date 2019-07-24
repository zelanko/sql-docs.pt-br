---
title: Script de implantação
titleSuffix: SQL Server big data clusters
description: Walkthrough uma implantação de SQL Server 2019 Big Data clusters (versão prévia) no serviço kubernetes do Azure (AKS).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7ff1ec3672fbcf101d98ad30913742186dea574d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419395"
---
# <a name="deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Implantar SQL Server Cluster de Big Data no serviço de kubernetes do Azure (AKS)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Neste tutorial, você usa um exemplo de script de implantação para implantar SQL Server 2019 Big Data cluster (versão prévia) no serviço kubernetes do Azure (AKS). 

> [!TIP]
> AKS é apenas uma opção para hospedar o kubernetes para o cluster Big Data. Para saber mais sobre outras opções de implantação, bem como personalizar opções de implantação, consulte [como implantar SQL Server clusters de Big data no kubernetes](deployment-guidance.md).

A implantação de cluster padrão Big Data usada aqui consiste em uma instância do SQL mestre, uma instância do pool de computação, duas instâncias do pool de dados e duas instâncias do pool de armazenamento. Os dados são persistidos usando volumes persistentes kubernetes que usam as classes de armazenamento padrão AKS. A configuração padrão usada neste tutorial é adequada para ambientes de desenvolvimento/teste.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>Pré-requisitos

- Uma assinatura do Azure.
- [Ferramentas de Big data](deploy-big-data-tools.md):
   - **azdata**
   - **kubectl**
   - **Azure Data Studio**
   - **Extensão SQL Server 2019**
   - **CLI do Azure**

## <a name="log-in-to-your-azure-account"></a>Faça logon em sua conta do Azure

O script usa CLI do Azure para automatizar a criação de um cluster AKS. Antes de executar o script, você deve fazer logon em sua conta do Azure com CLI do Azure pelo menos uma vez. Execute o comando a seguir em um prompt de comando.

```
az login
```

## <a name="download-the-deployment-script"></a>Baixar o script de implantação

Este tutorial automatiza a criação do cluster Big Data no AKS usando um script Python **Deploy-SQL-Big-data-AKs.py**. Se você já tiver instalado o Python para **azdata**, você poderá executar o script com êxito neste tutorial. 

Em um prompt de bash do Windows PowerShell ou Linux, execute o seguinte comando para baixar o script de implantação do GitHub.

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>Executar o script de implantação

Use as etapas a seguir para executar o script de implantação. Esse script criará um serviço AKS no Azure e, em seguida, implantará um cluster SQL Server 2019 Big Data no AKS. Você também pode modificar o script com outras [variáveis de ambiente](deployment-guidance.md#configfile) para criar uma implantação personalizada.

1. Execute o script com o seguinte comando:

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > Se você tiver python3 e python2 no computador cliente e no caminho, será necessário executar o comando usando python3: `python3 deploy-sql-big-data-aks.py`.

1. Quando solicitado, insira as seguintes informações:

   | Valor | Descrição |
   |---|---|
   | **ID da assinatura do Azure** | A ID de assinatura do Azure a ser usada para AKS. Você pode listar todas as suas assinaturas e suas IDs executando `az account list` a partir de outra linha de comando. |
   | **Grupo de recursos do Azure** | O nome do grupo de recursos do Azure a ser criado para o cluster AKS. |
   | **Região do Azure** | A região do Azure para o novo cluster AKS ( **westus**padrão). |
   | **Tamanho da máquina** | O [tamanho da máquina](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) a ser usado para os nós no cluster AKs (padrão **Standard_L8s**). |
   | **Nós de trabalho** | O número de nós de trabalho no cluster AKS (padrão **1**). |
   | **Nome do cluster** | O nome do cluster AKS e do cluster Big Data. O nome do cluster de Big Data deve ter apenas caracteres alfanuméricos minúsculos e nenhum espaço. (padrão **sqlbigdata**). |
   | **Senha** | Senha para o controlador, o gateway HDFS/Spark e a instância mestra ( **MySQLBigData2019**padrão). |
   | **Usuário do controlador** | Nome de usuário do controlador (padrão: **admin**). |

Os seguintes parâmetros foram necessários para os participantes no programa de pioneiros do cluster SQL Server 2019 Big Data: **Nome de usuário**e **senha**do Docker. A partir do CTP 3,2, eles não são mais necessários.

   > [!IMPORTANT]
   > O tamanho padrão do computador **Standard_L8s** pode não estar disponível em todas as regiões do Azure. Se você selecionar um tamanho de máquina diferente, certifique-se de que o número total de discos que podem ser anexados entre os nós no cluster seja maior ou igual a 24. Cada declaração de volume persistente no cluster requer um disco anexado. Atualmente, Big Data cluster requer 24 declarações de volume persistentes. Por exemplo, o tamanho do computador [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series) dá suporte a 32 discos anexados, portanto, você pode avaliar Big data clusters com um único nó desse tamanho de máquina.

   > [!NOTE]
   > A `sa` conta é um administrador do sistema na instância mestra do SQL Server que é criada durante a instalação. Depois de criar a implantação `MSSQL_SA_PASSWORD` , a variável de ambiente é detectável por `echo $MSSQL_SA_PASSWORD` meio da execução no contêiner da instância mestra. Para fins de segurança, altere `sa` sua senha na instância mestra após a implantação. Para obter mais informações, consulte [alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

1. O script será iniciado criando um cluster AKS usando os parâmetros especificados. Esta etapa leva vários minutos.

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>Monitorar o status

Depois que o script cria o cluster AKS, ele continua a definir as variáveis de ambiente necessárias com as configurações especificadas anteriormente. Em seguida, ele chama **azdata** para implantar o cluster de Big data no AKs.

A janela comando do cliente produzirá o status da implantação. Durante o processo de implantação, você deverá ver uma série de mensagens em que ela está aguardando o Pod do controlador:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

Após 10 a 20 minutos, você deve ser notificado de que o Pod do controlador está em execução:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> A implantação inteira pode levar muito tempo devido ao tempo necessário para baixar as imagens de contêiner para os componentes do cluster de Big Data. No entanto, não deve levar várias horas. Se você estiver tendo problemas com sua implantação, consulte [monitoramento e solução de problemas SQL Server clusters de Big data](cluster-troubleshooting-commands.md).

## <a name="inspect-the-cluster"></a>Inspecionar o cluster

A qualquer momento durante a implantação, você pode usar **kubectl** ou **azdata** para inspecionar o status e os detalhes sobre o cluster de Big data em execução.

### <a name="use-kubectl"></a>Usar kubectl

Abra uma nova janela de comando para usar o **kubectl** durante o processo de implantação.

1. Execute o seguinte comando para obter um resumo do status do cluster inteiro:

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se você não alterou o nome do cluster Big Data, o script usa como padrão **sqlbigdata**.

1. Inspecione os serviços kubernetes e seus pontos de extremidade internos e externos com o seguinte comando **kubectl** :

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. Você também pode inspecionar o status do pods kubernetes com o seguinte comando:

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. Saiba mais sobre um pod específico com o seguinte comando:

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> Para obter mais detalhes sobre como monitorar e solucionar problemas de implantação, consulte [monitoramento e solução de problemas SQL Server clusters de Big data](cluster-troubleshooting-commands.md).

## <a name="connect-to-the-cluster"></a>Conectar-se ao cluster

Quando o script de implantação for concluído, a saída notifica você sobre o sucesso:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

O cluster de Big Data de SQL Server agora está implantado em AKS. Agora você pode usar Azure Data Studio para se conectar ao cluster. Para obter mais informações, consulte [conectar-se a um cluster SQL Server Big data com o Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="clean-up"></a>Limpar

Se você estiver testando SQL Server Big Data clusters no Azure, deverá excluir o cluster AKS quando terminar para evitar encargos inesperados. Não remova o cluster se você pretende continuar a usá-lo.

> [!WARNING]
> As etapas a seguir desdividirão o cluster AKS, que remove o cluster SQL Server Big Data também. Se você tiver bancos de dados ou de HDFS que deseja manter, faça backup desses dados antes de excluir o cluster.

Execute o seguinte comando CLI do Azure para remover o cluster Big data e o serviço AKs no Azure (substitua `<resource group name>` pelo **grupo de recursos do Azure** especificado no script de implantação):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>Próximas etapas

O script de implantação configurou o serviço kubernetes do Azure e também implantou um cluster SQL Server 2019 Big Data. Você também pode optar por personalizar implantações futuras por meio de instalações manuais. Para saber mais sobre como Big Data clusters são implantados e como personalizar implantações, consulte [como implantar SQL Server Big data clusters no kubernetes](deployment-guidance.md).

Agora que o cluster de Big Data SQL Server está implantado, você pode carregar dados de exemplo e explorar os tutoriais:

> [!div class="nextstepaction"]
> [Tutorial: Carregar dados de exemplo em um cluster SQL Server Big Data 2019](tutorial-load-sample-data.md)
---
title: Implantar um contêiner do SQL Server com o AKS (Serviço de Kubernetes do Azure)
description: Este tutorial mostra como implantar uma solução de alta disponibilidade do SQL Server com o Kubernetes no Serviço de Kubernetes do Azure.
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 09/01/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: c8563738c8d1465c6573ca2a92f0839f54c8e29c
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155105"
---
# <a name="deploy-a-sql-server-container-in-kubernetes-with-azure-kubernetes-services-aks"></a>Implantar um contêiner do SQL Server no Kubernetes com o AKS (Serviços de Kubernetes do Azure)

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Saiba como configurar uma instância do SQL Server no Kubernetes no AKS (Serviço de Kubernetes do Azure), com armazenamento persistente para HA (alta disponibilidade). A solução oferece resiliência. Se a instância do SQL Server falhar, o Kubernetes a recriará automaticamente em um novo pod. O Kubernetes também oferece resiliência com relação a uma falha de nó.

Este tutorial demonstra como configurar uma instância do SQL Server altamente disponível em um contêiner no AKS.

> [!div class="checklist"]
> * Criar uma senha SA
> * Criar armazenamento
> * Criar a implantação
> * Conectar-se com o SSMS (SQL Server Management Studio)
> * Verificar falha e recuperação

## <a name="ha-solution-on-kubernetes-running-in-azure-kubernetes-service"></a>Solução de HA no Kubernetes sendo executada no Serviço de Kubernetes do Azure

O Kubernetes 1.6 e posterior tem suporte para [classes de armazenamento](https://kubernetes.io/docs/concepts/storage/storage-classes/), [declarações de volume persistentes](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims) e o [tipo de volume de disco do Azure](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). Você pode criar e gerenciar suas instâncias do SQL Server nativamente no Kubernetes. O exemplo neste artigo mostra como criar uma [implantação](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) para obter uma configuração de alta disponibilidade semelhante a uma instância de cluster de failover de disco compartilhado. Nessa configuração, o Kubernetes desempenha a função do orquestrador de cluster. Quando uma instância do SQL Server em um contêiner falha, o orquestrador inicializa outra instância do contêiner que é anexada ao mesmo armazenamento persistente.

![Contêiner do SQL Server no cluster do Kubernetes](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

No diagrama anterior, `mssql-server` é um contêiner em um [Pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/). O Kubernetes orquestra os recursos no cluster. Um [conjunto de réplicas](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) verifica se o pod está recuperado automaticamente após uma falha de nó. Os aplicativos conectam-se ao serviço. Nesse caso, o serviço representa um balanceador de carga que hospeda um endereço IP que permanece o mesmo após a falha do `mssql-server`.

No diagrama a seguir, o contêiner `mssql-server` falhou. Como o orquestrador, o Kubernetes garante que a contagem correta de instâncias íntegras no conjunto de réplicas e inicia um novo contêiner de acordo com a configuração. O orquestrador inicia um novo pod no mesmo nó e `mssql-server` se reconecta ao mesmo armazenamento persistente. O serviço conecta-se ao `mssql-server` recriado.

![Falha no pod do SQL Server no cluster do Kubernetes](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

No diagrama a seguir, o nó que hospeda o contêiner `mssql-server` falhou. O orquestrador inicia o novo pod em um nó diferente e `mssql-server` reconecta-se ao mesmo armazenamento persistente. O serviço conecta-se ao `mssql-server` recriado.

![Recuperação do pod do SQL Server no cluster do Kubernetes](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>Pré-requisitos

* **Cluster do Kubernetes**
   - O tutorial requer um cluster do Kubernetes. As etapas usam [kubectl](https://kubernetes.io/docs/user-guide/kubectl/) para gerenciar o cluster. 

   - Confira [Implantar um cluster do AKS (Serviço de Kubernetes do Azure)](/azure/aks/tutorial-kubernetes-deploy-cluster) para criar e conectar-se a um cluster Kubernetes de nó único no AKS com `kubectl`. 

   >[!NOTE]
   >Para proteger contra falhas de nó, um cluster Kubernetes requer mais de um nó.

* **CLI do Azure 2.0.23**
   - As instruções neste tutorial foram validadas com relação à CLI do Azure 2.0.23.

## <a name="create-an-sa-password"></a>Criar uma senha SA

Crie a senha SA no cluster Kubernetes. O Kubernetes pode gerenciar informações de configuração confidenciais, por exemplo, senhas como [segredos](https://kubernetes.io/docs/concepts/configuration/secret/).

O comando a seguir cria uma senha para a conta SA:

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   Substitua `MyC0m9l&xP@ssw0rd` por uma senha complexa.

   Para criar um segredo no Kubernetes chamado `mssql` que contém o valor `MyC0m9l&xP@ssw0rd` para `SA_PASSWORD`, execute o comando.


## <a name="create-storage"></a>Criar armazenamento

Configure um [volume persistente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) e uma [declaração de volume persistente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection) no cluster Kubernetes. Conclua as seguintes etapas: 

1. Crie um manifesto para definir a classe de armazenamento e a declaração de volume persistente.  O manifesto especifica o provisionador de armazenamento, os parâmetros e a [política de recuperação](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming). O cluster Kubernetes usa esse manifesto para criar o armazenamento persistente. 

   O exemplo de yaml a seguir define uma classe de armazenamento e uma declaração de volume persistente. O provisionador de classe de armazenamento é `azure-disk`, porque esse cluster Kubernetes está no Azure. O tipo de conta de armazenamento é `Standard_LRS`. A declaração de volume persistente é denominada `mssql-data`. Os metadados da declaração de volume persistente incluem uma anotação que os conecta de volta à classe de armazenamento. 

   ```yaml
   kind: StorageClass
   apiVersion: storage.k8s.io/v1
   metadata:
        name: azure-disk
   provisioner: kubernetes.io/azure-disk
   parameters:
     storageaccounttype: Standard_LRS
     kind: Managed
   ---
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: mssql-data
     annotations:
       volume.beta.kubernetes.io/storage-class: azure-disk
   spec:
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi
   ```

   Salve o arquivo (por exemplo, **pvc.yaml**).

1. Crie a declaração de volume persistente no Kubernetes.

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>` é a localização em que você salvou o arquivo.

   O volume persistente é criado automaticamente como uma conta de armazenamento do Azure e associado à declaração de volume persistente. 

    ![Captura de tela do comando da declaração de volume persistente](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. Verifique a declaração de volume persistente.

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>` é o nome da declaração de volume persistente.

   Na etapa anterior, a declaração de volume persistente é denominada `mssql-data`. Para ver os metadados sobre a declaração de volume persistente, execute o seguinte comando:

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   Os metadados retornados incluem um valor chamado `Volume`. Esse valor é mapeado para o nome do blob.

   ![Captura de tela dos metadados retornados, incluindo Volume](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   O valor do volume corresponde a parte do nome do blob na seguinte imagem do portal do Azure: 

   ![Captura de tela do nome do blob do portal do Azure](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. Verifique o volume persistente.

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` retorna metadados sobre o volume persistente que foi criado automaticamente e associado à declaração de volume persistente. 

## <a name="create-the-deployment"></a>Criar a implantação

Neste exemplo, o contêiner que hospeda a instância do SQL Server é descrito como um objeto de implantação Kubernetes. A implantação cria um conjunto de réplicas. O conjunto de réplicas cria o pod. 

Nesta etapa, crie um manifesto para descrever o contêiner com base na imagem do Docker [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) do SQL Server. O manifesto referencia a declaração de volume persistente do `mssql-server` e o segredo `mssql` que você já aplicou ao cluster Kubernetes. O manifesto também descreve um [serviço](https://kubernetes.io/docs/concepts/services-networking/service/). Esse serviço é um balanceador de carga. O balanceador de carga garante que o endereço IP persiste após a recuperação da instância do SQL Server. 

1. Crie um manifesto (um arquivo YAML) para descrever a implantação. O exemplo a seguir descreve uma implantação, incluindo um contêiner baseado na imagem de contêiner do SQL Server.

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: mssql-deployment
   spec:
     replicas: 1
     selector:
        matchLabels:
          app: mssql
     template:
       metadata:
         labels:
           app: mssql
       spec:
         terminationGracePeriodSeconds: 30
         hostname: mssqlinst
         securityContext:
           fsGroup: 10001
         containers:
         - name: mssql
           image: mcr.microsoft.com/mssql/server:2019-latest
           ports:
           - containerPort: 1433
           env:
           - name: MSSQL_PID
             value: "Developer"
           - name: ACCEPT_EULA
             value: "Y"
           - name: SA_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: mssql
                 key: SA_PASSWORD 
           volumeMounts:
           - name: mssqldb
             mountPath: /var/opt/mssql
         volumes:
         - name: mssqldb
           persistentVolumeClaim:
             claimName: mssql-data
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: mssql-deployment
   spec:
     selector:
       app: mssql
     ports:
       - protocol: TCP
         port: 1433
         targetPort: 1433
     type: LoadBalancer
   ```

   Copie o código anterior para um novo arquivo, denominado `sqldeployment.yaml`. Atualize os seguintes valores: 

   * MSSQL_PID `value: "Developer"`: define o contêiner para executar o SQL Server Developer Edition. O Developer Edition não é licenciado para dados de produção. Se a implantação for para uso em produção, defina a edição apropriada (`Enterprise`, `Standard` ou `Express`). 

      >[!NOTE]
      >Para saber mais, confira [Como licenciar o SQL Server](https://www.microsoft.com/sql-server/sql-server-2017-pricing).

   * `persistentVolumeClaim`: esse valor requer uma entrada para `claimName:` mapeada para o nome usado para a declaração de volume persistente. Este tutorial usa `mssql-data`. 

   * `name: SA_PASSWORD`: configura a imagem de contêiner para definir a senha SA, conforme definido nesta seção.

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD
     ```

    Quando o Kubernetes implanta o contêiner, ele refere-se ao segredo chamado `mssql` para obter o valor da senha.

   * `securityContext`: um securityContext define as configurações de privilégio e controle de acesso para um pod ou um contêiner, nesse caso, ele é especificado no nível do pod, de modo que todos os contêineres (nesse caso, apenas um) respeitam esse contexto de segurança. No contexto de segurança, definimos o fsGroup com o valor 10001 (que é o GID do grupo mssql), o que significa que todos os processos do contêiner também fazem parte da ID de grupo suplementar 10001 (mssql). O proprietário do volume /var/opt/mssql e de todos os arquivos criados nesse volume será a ID do grupo 10001 (grupo mssql).

   >[!NOTE]
   >Usando o tipo de serviço `LoadBalancer`, a instância do SQL Server pode ser acessada remotamente (pela Internet) na porta 1433.

   Salve o arquivo (por exemplo, **sqldeployment.yaml**).

1. Crie a implantação.

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>` é a localização em que você salvou o arquivo.

   ![Captura de tela do comando de implantação](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   A implantação e o serviço são criados. A instância do SQL Server está em um contêiner, conectada ao armazenamento persistente.

   Para exibir o status do pod, digite `kubectl get pod`.

   ![Captura de tela do comando get pod](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   Na imagem anterior, o pod tem um status de `Running`. Esse status indica que o contêiner está pronto. Isso pode levar alguns minutos.

   >[!NOTE]
   >Após a criação da implantação, pode levar alguns minutos antes que o pod fique visível. O atraso ocorre porque o cluster efetua pull da imagem [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) do Docker Hub. Depois o pull da imagem for efetuado pela primeira vez, implantações subsequentes poderão ser mais rápidas se a implantação for para um nó que já tem a imagem armazenada em cache. 

1. Verifique se os serviços estão em execução. Execute o comando a seguir:

   ```azurecli
   kubectl get services 
   ```

   Esse comando retorna serviços em execução, assim como endereços IP internos e externos para os serviços. Observe o endereço IP externo do serviço `mssql-deployment`. Use o endereço IP para conectar-se ao SQL Server. 

   ![Captura de tela do comando get service](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Para saber mais sobre o status dos objetos no cluster Kubernetes, execute:

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```

1. Confirme também se o contêiner está sendo executado como não raiz executando o seguinte comando:

    ```azurecli
    kubectl.exe exec <name of SQL POD> -it -- /bin/bash 
    ```

    em seguida, execute 'whoami' para ver o nome de usuário como mssql. Que é um usuário não raiz.

    ```azurecli
    whoami
    ```

## <a name="connect-to-the-sql-server-instance"></a>Conectar-se à instância do SQL Server

Se você tiver configurado o contêiner, conforme descrito, poderá conectar-se com um aplicativo de fora da rede virtual do Azure. Use a conta `sa` e o endereço IP externo para o serviço. Use a senha que você configurou como o segredo Kubernetes. 

É possível usar os seguintes aplicativos para se conectar à instância do SQL Server. 

* [SSMS](./sql-server-linux-manage-ssms.md)

* [SSDT](./sql-server-linux-develop-use-ssdt.md)

* sqlcmd

   Para se conectar com `sqlcmd`, execute o seguinte comando:

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   Substitua os seguintes valores:

  * `<External IP Address>` pelo endereço IP do serviço `mssql-deployment` 
  * `MyC0m9l&xP@ssw0rd` por sua senha

## <a name="verify-failure-and-recovery"></a>Verificar falha e recuperação

Para verificar a falha e a recuperação, exclua o pod. Execute as seguintes etapas:

1. Listar o pod que está executando o SQL Server.

   ```azurecli
   kubectl get pods
   ```

   Anotar o nome do pod que está executando o SQL Server.

1. Excluir o pod.

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```

   `mssql-deployment-0` é o valor retornado da etapa anterior para o nome do pod. 

O Kubernetes recria automaticamente o pod para recuperar uma instância do SQL Server e conectar-se ao armazenamento persistente. Use `kubectl get pods` para verificar se um novo pod foi implantado. Use `kubectl get services` para verificar se o endereço IP do novo contêiner é o mesmo. 

## <a name="summary"></a>Resumo

Neste tutorial, você aprendeu a implantar contêineres do SQL Server em um cluster Kubernetes para alta disponibilidade. 

> [!div class="checklist"]
> * Criar uma senha SA
> * Criar armazenamento
> * Criar a implantação
> * Conectar-se com o SSMS (SQL Server Management Studio)
> * Verificar falha e recuperação

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
>[Introdução ao Kubernetes](/azure/aks/intro-kubernetes)

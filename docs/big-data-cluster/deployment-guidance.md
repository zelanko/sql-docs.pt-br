---
title: Diretrizes de implantação
titleSuffix: SQL Server big data clusters
description: Saiba como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (visualização) em kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1655525fd9ec8acba80637a86936484859f85df2
ms.sourcegitcommit: dacf6c57f6a2e3cf2005f3268116f3c609639905
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70878721"
---
# <a name="how-to-deploy-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-kubernetes"></a>Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] o no kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O cluster de Big Data do SQL Server é implantado como contêineres do Docker em um cluster do Kubernetes. Esta é uma visão geral das etapas de instalação e configuração:

- Configure um cluster do Kubernetes em uma única VM, no cluster de VMs ou no AKS (Serviço de Kubernetes do Azure).
- Instale a ferramenta de configuração de cluster **azdata** no computador cliente.
- Implante um cluster de Big Data do SQL Server em um cluster do Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>Instalar as ferramentas de Big Data do SQL Server 2019

Antes de implantar um cluster de Big Data do SQL Server 2019, primeiro [instale as ferramentas de Big Data](deploy-big-data-tools.md):

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **Extensão do SQL Server 2019**

## <a id="prereqs"></a> Pré-requisitos do Kubernetes

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]exigir uma versão mínima do kubernetes de pelo menos v 1.13 para servidor e cliente (kubectl).

> [!NOTE]
> Observe que as versões do Kubernetes do cliente e do servidor devem estar dentro da versão secundária +1 ou -1. Para obter mais informações, confira [Notas sobre a versão do Kubernetes e política de SKU de distorção de versão)](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

### <a id="kubernetes"></a> Configuração do cluster do Kubernetes

Se você já tiver um cluster do Kubernetes que atenda aos pré-requisitos acima, poderá pular diretamente para a [etapa de implantação](#deploy). Esta seção pressupõe uma compreensão básica dos conceitos do Kubernetes.  Para obter informações detalhadas sobre o Kubernetes, confira a [documentação do Kubernetes](https://kubernetes.io/docs/home).

Você pode optar por implantar o Kubernetes de uma das três maneiras:

| Implantar o Kubernetes em: | Descrição | Link |
|---|---|---|
| **AKS (Serviço de Kubernetes do Azure)** | Um serviço de contêiner do Kubernetes gerenciado no Azure. | [Instruções](deploy-on-aks.md) |
| **Vários computadores (kubeadm)** | Um cluster do Kubernetes implantado em máquinas virtuais ou físicas usando **kubeadm** | [Instruções](deploy-with-kubeadm.md) |
| **Minikube** | Um cluster do Kubernetes de nó único em uma VM. | [Instruções](deploy-on-minikube.md) |

> [!TIP]
> Você também pode criar o script da implantação do AKS e de um cluster de Big Data em uma única etapa. Para obter mais informações, confira como fazer isso em um [script Python](quickstart-big-data-cluster-deploy.md) ou em um [notebook](deploy-notebooks.md) do Azure Data Studio.

### <a name="verify-kubernetes-configuration"></a>Verificar configuração do Kubernetes

Execute o comando **kubectl** para exibir a configuração do cluster. Verifique se kubectl está apontado para o contexto de cluster correto.

```bash
kubectl config view
```

Depois de configurar o cluster do Kubernetes, você pode prosseguir com a implantação de um novo cluster de Big Data do SQL Server. Se você estiver atualizando de uma versão anterior, consulte [como atualizar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](deployment-upgrade.md).

## <a id="deploy"></a> Visão geral da implantação

A maioria das configurações de cluster de Big Data é definida em um arquivo de configuração de implantação JSON. Você pode usar um perfil de implantação padrão para o AKS, `kubeadm`, ou `minikube` ou pode personalizar seu próprio arquivo de configuração de implantação a ser usado durante a instalação. Por motivos de segurança, as configurações de autenticação são passadas por meio de variáveis de ambiente.

As seções a seguir fornecem mais detalhes sobre como configurar suas implantações de cluster de Big Data, bem como exemplos de personalizações comuns. Além disso, você pode sempre editar o arquivo de configuração de implantação personalizada usando um editor como o VS Code, por exemplo.

## <a id="configfile"></a> Configurações padrão

As opções de implantação de cluster de Big Data são definidas em arquivos de configuração JSON. Você pode iniciar a personalização da implantação de cluster a partir dos perfis de implantação internos com configurações padrão para ambientes de desenvolvimento/teste:

| Perfil de implantação | Ambiente do Kubernetes |
|---|---|
| **aks-dev-test** | AKS (Serviço de Kubernetes do Azure) |
| **kubeadm-dev-test** | Vários computadores (kubeadm) |
| **minikube-dev-test** | minikube |

Você pode implantar um cluster de Big Data executando **azdata bdc create**. Isso solicitará que você escolha uma das configurações padrão e, em seguida, o guiará pela implantação.

Na primeira vez que executar `azdata`, você deverá incluir `--accept-eula=yes` para aceitar o EULA (contrato de licença de usuário final).

```bash
azdata bdc create --accept-eula=yes
```

Nesse cenário, são solicitadas as configurações que não fazem parte da configuração padrão, como senhas. 

> [!IMPORTANT]
> O nome padrão do cluster de Big Data é **mssql-cluster**. É importante saber isso para executar qualquer um dos comandos **kubectl** que especificam o namespace do Kubernetes com o parâmetro `-n`.

## <a id="customconfig"></a> Configurações personalizadas

Também é possível personalizar seu próprio perfil de configuração de implantação. Você pode fazer isso executando as etapas a seguir:

1. Comece com um dos perfis de implantação padrão que correspondem ao seu ambiente do Kubernetes. Use o comando **azdata bdc config list** para listá-los:

   ```bash
   azdata bdc config list
   ```

1. Para personalizar sua implantação, crie uma cópia do perfil de implantação com o comando **azdata bdc config init**. Por exemplo, o comando a seguir cria uma cópia dos arquivos de configuração de implantação **aks-dev-test** em um diretório de destino chamado `custom`:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   azdata
   > O `--target` especifica um diretório que contém os arquivos de configuração, **BDC. JSON** e `--source` **Control. JSON**, com base no parâmetro.

1. Para personalizar as configurações em seu perfil de configuração de implantação, você pode editar o arquivo de configuração de implantação em uma ferramenta que é boa para editar arquivos JSON, como o VS Code. Para automação com script, você também pode editar o perfil de implantação personalizado usando o comando **azdata bdc config**. Por exemplo, o comando a seguir altera um perfil de implantação personalizado para alterar o nome do cluster implantado do padrão (**mssql-cluster**) para **test-cluster**:  

   ```bash
   azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
   ```
   
   > [!TIP]
   > Você também pode passar o nome do cluster no momento da implantação usando o parâmetro *--name* para o comando *azdata create bdc*. Os parâmetros no comando têm precedência sobre os valores nos arquivos de configuração.

   > Uma ferramenta útil para localizar caminhos JSON é o [JSONPath Online Evaluator](https://jsonpath.com/).

   Além de passar os pares chave-valor, você também pode fornecer valores JSON embutidos ou passar arquivos de patch JSON. Para obter mais informações, confira [Definir configurações de implantação para clusters de Big Data](deployment-custom-configuration.md).

1. Em seguida, passe o arquivo de configuração personalizada para **azdata bdc create**. Observe que você deve definir as [variáveis de ambiente](#env) necessárias, caso contrário, os valores serão solicitados:

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> Para obter mais informações sobre a estrutura de um arquivo de configuração de implantação, confira a [Referência do arquivo de configuração de implantação](reference-deployment-config.md). Para obter mais exemplos de configuração, confira [Definir configurações de implantação para clusters de Big Data](deployment-custom-configuration.md).

## <a id="env"></a> Variáveis de ambiente

As variáveis de ambiente a seguir são usadas para configurações de segurança que não são armazenadas em um arquivo de configuração de implantação. Observe que as configurações do Docker, exceto as credenciais, podem ser definidas no arquivo de configuração.

| Variável de ambiente | Requisito |Descrição |
|---|---|---|
| **CONTROLLER_USERNAME** | Obrigatório |O nome de usuário do administrador do cluster. |
| **CONTROLLER_PASSWORD** | Obrigatório |A senha do administrador do cluster. |
| **MSSQL_SA_PASSWORD** | Obrigatório |A senha do usuário SA para a instância mestre do SQL. |
| **KNOX_PASSWORD** | Obrigatório |A senha para o usuário **raiz** do Knox. Observação do que em uma configuração de autenticação básica, somente o usuário com suporte para o Knox é a **raiz**.|
| **ACCEPT_EULA**| Necessário para o primeiro uso de `azdata`| Não requer valor. Quando definido como uma variável de ambiente, ele aplica o EULA ao SQL Server e ao `azdata`. Se não estiver definido como variável de ambiente, você poderá incluir `--accept-eula` no primeiro uso do comando `azdata`.|
| **DOCKER_USERNAME** | Opcional | O nome de usuário para acessar as imagens de contêiner caso elas sejam armazenadas em um repositório privado. Confira o tópico [Implantações offline](deploy-offline.md) para obter mais detalhes sobre como usar um repositório privado do Docker para implantação de cluster de Big Data.|
| **DOCKER_PASSWORD** | Opcional |A senha para acessar o repositório privado acima. |

Essas variáveis de ambiente devem ser definidas antes de chamar **azdata bdc create**. Se alguma variável não for definida, você deverá fazê-lo.

O exemplo a seguir mostra como definir as variáveis de ambiente para Linux (Bash) e Windows (PowerShell):

```bash
export CONTROLLER_USERNAME=admin
export CONTROLLER_PASSWORD=<password>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
```

> [!NOTE]
> Você deve usar o usuário **raiz** para o gateway do Knox com a senha acima. **root** é o único usuário com suporte para essa configuração básica de autenticação (nome de usuário/senha). Para SQL Server mestre, o nome de usuário provisionado para ser usado com a senha acima é **SA**.


Depois de definir as variáveis de ambiente, você deve executar `azdata bdc create` para disparar a implantação. Este exemplo usa o perfil de configuração de cluster criado acima:

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

Observe as seguintes diretrizes:

- Encapsule a senha entre aspas duplas se ela contiver caracteres especiais. Você pode definir **MSSQL_SA_PASSWORD** como o que desejar, mas garanta que a senha seja suficientemente complexa e não use os caracteres `!`, `&` ou `'`. Observe que os delimitadores de aspas duplas funcionam apenas em comandos de Bash.
- O logon **SA** é um administrador do sistema na instância mestre do SQL Server que é criada durante a instalação. Depois de criar o contêiner do SQL Server, a variável de ambiente **MSSQL_SA_PASSWORD** especificada é detectável executando `echo $MSSQL_SA_PASSWORD` no contêiner. Para fins de segurança, altere sua senha SA de acordo com as práticas recomendadas documentadas [aqui](../linux/quickstart-install-connect-docker.md#sapassword).

## <a id="unattended"></a> Instalação autônoma

Para uma implantação autônoma, você precisa definir todas as variáveis de ambiente necessárias, usar um arquivo de configuração e chamar o comando `azdata bdc create` com o parâmetro `--accept-eula yes`. Os exemplos na seção anterior demonstram a sintaxe de uma instalação autônoma.

## <a id="monitor"></a> Monitorar a implantação

Durante a inicialização do cluster, a janela Comando do cliente produzirá o status da implantação. Durante o processo de implantação, você deverá ver uma série de mensagens em que ele está aguardando o pod do controlador:

```output
Waiting for cluster controller to start.
```

Em 15 a 30 minutos, você deve ser notificado de que o pod do controlador está em execução:

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> A implantação inteira pode ser muito demorada devido ao tempo necessário para baixar as imagens de contêiner para os componentes do cluster de Big Data. No entanto, não deve demorar várias horas. Se você estiver tendo problemas com sua implantação, consulte [monitoramento e solução [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]de problemas ](cluster-troubleshooting-commands.md).

Quando a implantação for concluída, a saída notificará você sobre o sucesso:

```output
Cluster deployed successfully.
```

> [!TIP]
> O nome padrão para o cluster de Big Data implantado é `mssql-cluster`, a menos que seja modificado por uma configuração personalizada.

## <a id="endpoints"></a> Recuperar pontos de extremidade

Depois que o script de implantação foi concluído com êxito, você pode obter os endereços IP dos pontos de extremidade externos do cluster de Big Data usando as etapas a seguir.

1. Após a implantação, localize o endereço IP do ponto de extremidade do controlador da saída padrão de implantação ou examinando a saída EXTERNAL-IP do seguinte comando **kubectl**:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se não tiver alterado o nome padrão durante a implantação, use `-n mssql-cluster` no comando anterior. **mssql-cluster** é o nome padrão do cluster de Big Data.

1. Faça logon no cluster de Big Data usando [azdata login](reference-azdata.md). Defina o parâmetro **--controller-endpoint** como o endereço IP externo do ponto de extremidade do controlador.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique o nome de usuário e a senha que você configurou para o controlador (CONTROLLER_USERNAME e CONTROLLER_PASSWORD) durante a implantação.

1. Execute [azdata bdc endpoint list](reference-azdata-bdc-endpoint.md) para obter uma lista com uma descrição de cada ponto de extremidade e seus valores de porta e endereço IP correspondentes. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   A lista a seguir mostra a saída de exemplo deste comando:

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

Você também pode obter todos os pontos de extremidade de serviço implantados para o cluster executando o seguinte comando **kubectl**:

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

### <a name="minikube"></a>Minikube

Se você estiver usando o minikube, será necessário executar o comando a seguir para obter o endereço IP ao qual você precisa se conectar. Além do IP, especifique a porta para o ponto de extremidade ao qual você precisa se conectar.

```bash
minikube ip
```

## <a id="status"></a> Verificar o status do cluster

Após a implantação, você pode verificar o status do cluster usando o comando [azdata bdc status show](reference-azdata-bdc-status.md).

```bash
azdata bdc status show
```

> [!TIP]
> Para executar os comandos de status, primeiro você precisa fazer logon usando o comando **azdata login**, que foi mostrado na seção anterior sobre pontos de extremidade.

Veja a seguir a saída de exemplo deste comando:

```output
Bdc: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Services: ready                                                                                                                                                                                                     Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Servicename    State    Healthstatus    Details

 sql            ready    healthy         -
 hdfs           ready    healthy         -
 spark          ready    healthy         -
 control        ready    healthy         -
 gateway        ready    healthy         -
 app            ready    healthy         -


 Sql Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Hdfs Services: ready                                                                                                                                                                                                Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 nmnode-0        ready    healthy         StatefulSet nmnode-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
 sparkhead       ready    healthy         StatefulSet sparkhead is healthy


 Spark Services: ready                                                                                                                                                                                               Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Control Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         -
 control         ready    healthy         -
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy


 Gateway Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 gateway         ready    healthy         StatefulSet gateway is healthy


 App Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 appproxy        ready    healthy         ReplicaSet appproxy is healthy
```

Você também pode obter o status mais detalhado com os seguintes comandos:

- o [status show do controle BDC azdata](reference-azdata-bdc-control-status.md) retornará o status de integridade de todos os componentes associados ao serviço de gerenciamento de controle
```
azdata bdc control status show
```
Saída de exemplo:
```output
Control: ready                                                                                                                                                                                                      Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         -
 control         ready    healthy         -
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy
```

- o **status SQL do BDC azdata** retornará o status de integridade de todos os recursos que têm um serviço SQL Server
```
azdata bdc sql status show
```
Saída de exemplo:
```output
Sql: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
```

> [!IMPORTANT]
> Ao usar **--todos** os parâmetros a saída desses comandos contém URLs para os painéis Kibana e Grafana para uma análise mais detalhada.

Além de usar **azdata**, você também pode usar o Azure Data Studio para localizar os pontos de extremidade e as informações de status. Para obter mais informações sobre como exibir o status do cluster com **azdata** e o Azure Data Studio, confira [Como exibir o status de um cluster de Big Data](view-cluster-status.md).

## <a id="connect"></a> Conectar-se ao cluster

Para obter mais informações sobre como conectar-se ao cluster de Big Data, confira [Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a implantação do cluster de Big Data, confira os seguintes recursos:

- [Definir configurações de implantação para clusters de Big Data](deployment-custom-configuration.md)
- [Executar uma implantação offline de um cluster de Big Data do SQL Server](deploy-offline.md)
- [Workshop: Arquitetura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)

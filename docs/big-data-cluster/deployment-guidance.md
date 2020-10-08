---
title: Diretrizes de implantação
titleSuffix: SQL Server Big Data Clusters
description: Saiba como implantar clusters de Big Data do SQL Server no Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0564d83508dafa650735981537599c7b0068da67
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725862"
---
# <a name="how-to-deploy-big-data-clusters-2019-on-kubernetes"></a>Como implantar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

O cluster de Big Data do SQL Server é implantado como contêineres do Docker em um cluster do Kubernetes. Esta é uma visão geral das etapas de instalação e configuração:

- Configure um cluster do Kubernetes em uma só VM, em um cluster de VMs, no AKS (Serviço de Kubernetes do Azure), no Red Hat OpenShift ou no ARO (Red Hat OpenShift no Azure).
- Instale a ferramenta de configuração de cluster `azdata` no computador cliente.
- Implante um cluster de Big Data do SQL Server em um cluster do Kubernetes.

## <a name="supported-platforms"></a>Plataformas compatíveis

Confira [Plataformas com suporte](release-notes-big-data-cluster.md#supported-platforms) para ver uma lista completa das várias plataformas do Kubernetes validadas para implantação de Clusters de Big Data do SQL Server.

### <a name="sql-server-editions"></a>Edições do SQL Server

|Edition|Observações|
|---------|---------|
|Enterprise<br/>Standard<br/>Desenvolvedor| A edição de cluster de Big Data é determinada pela edição da instância mestra do SQL Server. No momento da implantação, a Developer Edition é implantada por padrão. Você pode alterar a edição após a implantação. Confira [Configurar a instância mestra do SQL Server](./configure-sql-server-master-instance.md). |

## <a name="kubernetes"></a><a id="prereqs"></a> Kubernetes

### <a name="kubernetes-cluster-setup"></a><a id="kubernetes"></a> Configuração do cluster do Kubernetes

Se você já tiver um cluster do Kubernetes que atenda aos pré-requisitos acima, poderá pular diretamente para a [etapa de implantação](#deploy). Esta seção pressupõe uma compreensão básica dos conceitos do Kubernetes.  Para obter informações detalhadas sobre o Kubernetes, confira a [documentação do Kubernetes](https://kubernetes.io/docs/home).

Você pode optar por implantar o Kubernetes das seguintes maneiras:

| Implantar o Kubernetes em: | Descrição | Link |
|---|---|---|
| **AKS (Serviço de Kubernetes do Azure)** | Um serviço de contêiner do Kubernetes gerenciado no Azure. | [Instruções](deploy-on-aks.md) |
| **Uma ou várias máquinas (`kubeadm`)** | Um cluster do Kubernetes implantado em máquinas virtuais ou físicas usando `kubeadm` | [Instruções](deploy-with-kubeadm.md) |
|**Red Hat OpenShift no Azure** | Uma oferta totalmente gerenciada do OpenShift em execução no Azure. | [Instruções](deploy-openshift.md)|
|**Red Hat OpenShift**|Uma plataforma de aplicativos Kubernetes empresariais na nuvem híbrida.| [Instruções](deploy-openshift.md)|

> [!TIP]
> Você também pode criar o script da implantação do AKS e de um cluster de Big Data em uma única etapa. Para obter mais informações, confira como fazer isso em um [script Python](quickstart-big-data-cluster-deploy.md) ou em um [notebook](notebooks-deploy.md) do Azure Data Studio.

### <a name="verify-kubernetes-configuration"></a>Verificar configuração do Kubernetes

Execute o comando `kubectl` para exibir a configuração do cluster. Verifique se kubectl está apontado para o contexto de cluster correto.

```bash
kubectl config view
```

> [!Important] 
> Se estiver implantando em um cluster do Kuberntes com vários nós que você inicializou usando `kubeadm`, antes de iniciar a implantação do cluster de Big Data, verifique se os relógios estão sincronizados em todos os nós do Kubernetes que serão destinos da implantação. Como o cluster de Big Data tem propriedades de integridade internas para vários serviços que são sensíveis ao tempo, distorções de relógio podem causar status incorretos.

Depois de configurar o cluster do Kubernetes, você pode prosseguir com a implantação de um novo cluster de Big Data do SQL Server. Se você estiver atualizando de uma versão anterior, confira [Como atualizar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-upgrade.md).

## <a name="ensure-you-have-storage-configured"></a>Verifique se você tem o armazenamento configurado

A maioria das implantações do cluster de Big Data deve ter armazenamento persistente. Neste momento, você precisa verificar se tem um plano de como fornecerá o armazenamento persistente no cluster do Kubernetes antes de implantar o BDC.

Se você fizer a implantação no AKS, nenhuma configuração de armazenamento será necessária. O AKS fornece classes de armazenamento internas com provisionamento dinâmico. Personalize a classe de armazenamento (`default` ou `managed-premium`) no arquivo de configuração de implantação. Os perfis internos usam uma classe de armazenamento `default`. Se você estiver fazendo a implantação em um cluster do Kubernetes implantado com `kubeadm`, precisará garantir que tem armazenamento suficiente para um cluster da escala desejada disponível e configurado para uso. Caso deseje personalizar como o armazenamento é usado, faça isto antes de continuar. Confira [Persistência de dados com o cluster de Big Data do SQL Server no Kubernetes](concept-data-persistence.md).

## <a name="install-sql-server-2019-big-data-tools"></a>Instalar as ferramentas de Big Data do SQL Server 2019

Antes de implantar um cluster de Big Data do SQL Server 2019, primeiro [instale as ferramentas de Big Data](deploy-big-data-tools.md):

- `azdata`
- `kubectl`
- Azure Data Studio
- [Extensão Virtualização de Dados](../azure-data-studio/extensions/data-virtualization-extension.md) para o Azure Data Studio


## <a name="deployment-overview"></a><a id="deploy"></a> Visão geral da implantação

A maioria das configurações de cluster de Big Data é definida em um arquivo de configuração de implantação JSON. Você pode usar um perfil de implantação padrão para o AKS e para clusters do Kubernetes criados com `kubeadm` ou pode personalizar seu próprio arquivo de configuração de implantação a ser usado durante a instalação. Por motivos de segurança, as configurações de autenticação são passadas por meio de variáveis de ambiente.

As seções a seguir fornecem mais detalhes sobre como configurar suas implantações de cluster de Big Data, bem como exemplos de personalizações comuns. Além disso, você pode sempre editar o arquivo de configuração de implantação personalizada usando um editor como o VS Code, por exemplo.

## <a name="default-configurations"></a><a id="configfile"></a> Configurações padrão

As opções de implantação de cluster de Big Data são definidas em arquivos de configuração JSON. Você pode iniciar a personalização da implantação do cluster nos perfis de implantação internos disponíveis no `azdata`. 

> [!NOTE]
> As imagens de contêiner necessárias para a implantação de cluster de Big Data estão hospedadas no Registro de Contêiner da Microsoft (`mcr.microsoft.com`), no repositório `mssql/bdc`. Por padrão, essas configurações já estão incluídas no arquivo de configuração `control.json` em cada um dos perfis de implantação incluídos no `azdata`. Além disso, a tag de imagem de contêiner para cada versão também é preenchida previamente no mesmo arquivo de configuração. Se você precisar efetuar pull das imagens de contêiner para seu próprio registro de contêiner privado e/ou modificar as configurações do repositório/registro de contêiner, siga as instruções no artigo [Instalação offline](deploy-offline.md)

Execute este comando para localizar os modelos disponíveis:

```
azdata bdc config list -o table 
```

Os seguintes modelos estão disponíveis começando no SQL Server 2019 CU5: 

| Perfil de implantação | Ambiente do Kubernetes |
|---|---|
| `aks-dev-test` | Implantar um cluster de Big Data do SQL Server no AKS (Serviço de Kubernetes do Azure)|
| `aks-dev-test-ha` | Implantar um cluster de Big Data do SQL Server no AKS (Serviço de Kubernetes do Azure). Serviços críticos, como o mestre do SQL Server e o nó de nome do HDFS, são configurados para alta disponibilidade.|
| `aro-dev-test`|Implantar um cluster de Big Data do SQL Server no Red Hat OpenShift no Azure para desenvolvimento e teste. <br/><br/>Introduzido no SQL Server 2019 CU 5.|
| `aro-dev-test-ha`|Implante o cluster de Big Data do SQL Server com alta disponibilidade em um cluster do Red Hat OpenShift para desenvolvimento e teste. <br/><br/>Introduzido no SQL Server 2019 CU 5.|
| `kubeadm-dev-test` | Implante o cluster de Big Data do SQL Server em um cluster do Kubernetes criado com kubeadm usando uma ou várias máquinas virtuais ou computadores físicos.|
| `kubeadm-prod`| Implante o cluster de Big Data do SQL Server em um cluster do Kubernetes criado com kubeadm usando uma ou várias máquinas virtuais ou computadores físicos. Use este modelo para habilitar a integração dos serviços de cluster de Big Data com o Active Directory. Serviços críticos, como a instância mestre do SQL Server e o nó de nome do HDFS, são implantados com uma configuração altamente disponível.  |
| `openshift-dev-test`|Implante um cluster de Big Data do SQL Server em um cluster do Red Hat OpenShift para desenvolvimento e teste. <br/><br/>Introduzido no SQL Server 2019 CU 5.|
| `openshift-prod`|Implante um cluster de Big Data do SQL Server com alta disponibilidade em um cluster do Red Hat OpenShift. <br/><br/>Introduzido no SQL Server 2019 CU 5.|

Você pode implantar um cluster de Big Data executando `azdata bdc create`. Isso solicitará que você escolha uma das configurações padrão e, em seguida, o guiará pela implantação.

Na primeira vez que executar `azdata`, você deverá incluir `--accept-eula=yes` para aceitar o EULA (contrato de licença de usuário final).

```bash
azdata bdc create --accept-eula=yes
```

Nesse cenário, são solicitadas as configurações que não fazem parte da configuração padrão, como senhas. 

> [!IMPORTANT]
> O nome padrão do cluster de Big Data é `mssql-cluster`. É importante saber isso para executar qualquer um dos comandos `kubectl` que especificam o namespace do Kubernetes com o parâmetro `-n`.

## <a name="custom-configurations"></a><a id="customconfig"></a> Configurações personalizadas

Também é possível personalizar sua implantação para acomodar as cargas de trabalho que você planeja executar. Você não pode alterar as configurações de escala (número de réplicas) ou armazenamento dos serviços do cluster de Big Data após as implantações, portanto, planeje sua configuração de implantação com cuidado para evitar problemas de capacidade. Para personalizar sua implantação, siga estas etapas:

1. Comece com um dos perfis de implantação padrão que correspondem ao seu ambiente do Kubernetes. Você pode usar o comando `azdata bdc config list` para listá-los:

   ```bash
   azdata bdc config list
   ```

1. Para personalizar sua implantação, crie uma cópia do perfil de implantação com o comando `azdata bdc config init`. Por exemplo, o comando a seguir cria uma cópia dos arquivos de configuração de implantação `aks-dev-test` em um diretório de destino chamado `custom`:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   >[!TIP]
   >`--target` especifica um diretório que contém os arquivos de configuração, `bdc.json` e `control.json`, com base no parâmetro `--source`.

1. Para personalizar as configurações em seu perfil de configuração de implantação, você pode editar o arquivo de configuração de implantação em uma ferramenta que é boa para editar arquivos JSON, como o VS Code. Para automação com script, você também pode editar o perfil de implantação personalizado usando o comando `azdata bdc config`. Por exemplo, o comando a seguir altera um perfil de implantação personalizado para alterar o nome do cluster implantado do padrão (`mssql-cluster`) para `test-cluster`:  

   ```bash
   azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
   ```

   > [!TIP]
   > Você também pode passar o nome do cluster no momento da implantação usando o parâmetro *--name* para o comando *azdata create bdc*. Os parâmetros no comando têm precedência sobre os valores nos arquivos de configuração.
   >
   > Uma ferramenta útil para localizar caminhos JSON é o [JSONPath Online Evaluator](https://jsonpath.com/).
   >
   Além de passar os pares chave-valor, você também pode fornecer valores JSON embutidos ou passar arquivos de patch JSON. Para obter mais informações, confira [Definir configurações de implantação para clusters de Big Data](deployment-custom-configuration.md).

1. Passe o arquivo de configuração personalizado para `azdata bdc create`. Observe que você deve definir as [variáveis de ambiente](#env) necessárias, caso contrário, o terminal solicitará os valores:

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> Para obter mais informações sobre a estrutura de um arquivo de configuração de implantação, confira a [Referência do arquivo de configuração de implantação](reference-deployment-config.md). Para obter mais exemplos de configuração, confira [Definir configurações de implantação para clusters de Big Data](deployment-custom-configuration.md).

## <a name="environment-variables"></a><a id="env"></a> Variáveis de ambiente

As variáveis de ambiente a seguir são usadas para configurações de segurança que não são armazenadas em um arquivo de configuração de implantação. Observe que as configurações do Docker, exceto as credenciais, podem ser definidas no arquivo de configuração.

| Variável de ambiente | Requisito |Descrição |
|---|---|---|
| `AZDATA_USERNAME` | Obrigatório |O nome de usuário do administrador do cluster de Big Data do SQL Server. Um logon sysadmin com o mesmo nome é criado na instância mestre do SQL Server. Como melhor prática de segurança, a conta `sa` está desabilitada. <br/><br/>[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]|
| `AZDATA_PASSWORD` | Obrigatório |A senha das contas de usuário criadas acima. Em clusters implantados antes do SQL Server 2019 CU5, a mesma senha é usada para o usuário `root`, a fim de proteger o gateway do Knox e o HDFS. |
| `ACCEPT_EULA`| Necessário para o primeiro uso de `azdata`| Defina como "sim". Quando definido como uma variável de ambiente, ele aplica o EULA ao SQL Server e ao `azdata`. Se não estiver definido como variável de ambiente, você poderá incluir `--accept-eula=yes` no primeiro uso do comando `azdata`.|
| `DOCKER_USERNAME` | Opcional | O nome de usuário para acessar as imagens de contêiner caso elas sejam armazenadas em um repositório privado. Confira o tópico [Implantações offline](deploy-offline.md) para obter mais detalhes sobre como usar um repositório privado do Docker para implantação de cluster de Big Data.|
| `DOCKER_PASSWORD` | Opcional |A senha para acessar o repositório privado acima. |

Essas variáveis de ambiente devem ser definidas antes de chamar `azdata bdc create`. Se alguma variável não for definida, você deverá fazê-lo.

O exemplo a seguir mostra como definir as variáveis de ambiente para Linux (Bash) e Windows (PowerShell):

```bash
export AZDATA_USERNAME=admin
export AZDATA_PASSWORD=<password>
export ACCEPT_EULA=yes
```

```PowerShell
SET AZDATA_USERNAME=admin
SET AZDATA_PASSWORD=<password>
```

> [!NOTE]
> Em clusters implantados antes do SQL Server 2019 CU 5, use o usuário `root` para o gateway do Knox com a senha acima. `root` é o único usuário compatível com essa autenticação Básica (nome de usuário/senha).
> [!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]
> Para se conectar ao SQL Server com a autenticação Básica, use os mesmos valores que as [variáveis de ambiente](#env) AZDATA_USERNAME e AZDATA_PASSWORD. 

Depois de definir as variáveis de ambiente, você deve executar `azdata bdc create` para disparar a implantação. Este exemplo usa o perfil de configuração de cluster criado acima:

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

Observe as seguintes diretrizes:

- Encapsule a senha entre aspas duplas se ela contiver caracteres especiais. Você pode definir `AZDATA_PASSWORD` como desejar, mas a senha deve ser suficientemente complexa e não pode conter os caracteres `!`, `&` ou `'`. Observe que os delimitadores de aspas duplas funcionam apenas em comandos de Bash.
- O logon `AZDATA_USERNAME` é um administrador do sistema na instância mestre do SQL Server que é criada durante a instalação. Depois de criar o contêiner do SQL Server, a variável de ambiente `AZDATA_PASSWORD` especificada é detectável executando `echo $AZDATA_PASSWORD` no contêiner. Para fins de segurança, adote a melhor prática de alterar a senha.

## <a name="unattended-install"></a><a id="unattended"></a> Instalação autônoma

Para uma implantação autônoma, você precisa definir todas as variáveis de ambiente necessárias, usar um arquivo de configuração e chamar o comando `azdata bdc create` com o parâmetro `--accept-eula yes`. Os exemplos na seção anterior demonstram a sintaxe de uma instalação autônoma.

## <a name="monitor-the-deployment"></a><a id="monitor"></a> Monitorar a implantação

Durante a inicialização do cluster, a janela Comando do cliente retorna o status da implantação. Durante o processo de implantação, você deverá ver uma série de mensagens em que ele está aguardando o pod do controlador:

```output
Waiting for cluster controller to start.
```

Em 15 a 30 minutos, você deve ser notificado de que o pod do controlador está em execução:

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> A implantação inteira pode ser muito demorada devido ao tempo necessário para baixar as imagens de contêiner para os componentes do cluster de Big Data. No entanto, não deve demorar várias horas. Se estiver encontrando problemas em sua implantação, confira [Monitoramento e solução de problemas de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](cluster-troubleshooting-commands.md).

Quando a implantação for concluída, a saída notificará você sobre o sucesso:

```output
Cluster deployed successfully.
```

> [!TIP]
> O nome padrão para o cluster de Big Data implantado é `mssql-cluster`, a menos que seja modificado por uma configuração personalizada.

## <a name="retrieve-endpoints"></a><a id="endpoints"></a> Recuperar pontos de extremidade

Depois que o script de implantação for concluído com êxito, você poderá obter os endereços dos pontos de extremidade externos do cluster de Big Data usando as etapas a seguir.

1. Após a implantação, localize o endereço IP do ponto de extremidade do controlador da saída padrão da implantação ou examinando a saída EXTERNAL-IP do seguinte comando `kubectl`:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se não tiver alterado o nome padrão durante a implantação, use `-n mssql-cluster` no comando anterior. `mssql-cluster` é o nome padrão do cluster de Big Data.

1. Faça logon no cluster de Big Data usando [azdata login](../azdata/reference/reference-azdata.md). Defina o parâmetro `--endpoint` como o endereço IP externo do ponto de extremidade do controlador.

   ```bash
   azdata login --endpoint https://<ip-address-of-controller-svc-external>:30080 --username <user-name>
   ```

   Especifique o nome de usuário e a senha que você configurou para o administrador do cluster de Big Data (AZDATA_USERNAME e AZDATA_PASSWORD) durante a implantação.

   > [!TIP]
   > Se for o administrador do cluster do Kubernetes e tiver acesso ao arquivo de configuração do cluster (arquivo de configuração de kube), você poderá configurar o contexto atual para apontar para o cluster do Kubernetes de destino. Nesse caso, você pode fazer logon com `azdata login -n <namespaceName>`, em que `namespace` é o nome do cluster de Big Data. As credenciais serão solicitadas se não forem especificadas no comando de logon.
   
1. Execute [azdata bdc endpoint list](../azdata/reference/reference-azdata-bdc-endpoint.md) para obter uma lista com uma descrição de cada ponto de extremidade e seus valores de porta e endereço IP correspondentes. 

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

Você também pode obter todos os pontos de extremidade de serviço implantados para o cluster executando o seguinte comando `kubectl`:

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

## <a name="verify-the-cluster-status"></a><a id="status"></a> Verificar o status do cluster

Após a implantação, você pode verificar o status do cluster usando o comando [azdata bdc status show](../azdata/reference/reference-azdata-bdc-status.md).

```bash
azdata bdc status show
```

> [!TIP]
> Para executar os comandos de status, primeiro você precisa fazer logon usando o comando `azdata login`, que foi mostrado na seção anterior sobre pontos de extremidade.

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

- [azdata bdc control status show](../azdata/reference/reference-azdata-bdc-control-status.md) retorna o status de integridade de todos os componentes associados ao serviço de gerenciamento de controle
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

- `azdata bdc sql status show` retorna o status de integridade de todos os recursos que têm um serviço do SQL Server
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
> Ao usar o parâmetro `--all`, a saída desses comandos contém URLs para os painéis Kibana e Grafana para uma análise mais detalhada.

Além de usar `azdata`, você também pode usar o Azure Data Studio para localizar os pontos de extremidade e as informações de status. Para obter mais informações sobre como exibir o status do cluster com `azdata` e o Azure Data Studio, confira [Como exibir o status de um cluster de Big Data](view-cluster-status.md).

## <a name="connect-to-the-cluster"></a><a id="connect"></a> Conectar-se ao cluster

Para obter mais informações sobre como conectar-se ao cluster de Big Data, confira [Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a implantação do cluster de Big Data, confira os seguintes recursos:

- [Definir configurações de implantação para clusters de Big Data](deployment-custom-configuration.md)
- [Executar uma implantação offline de um cluster de Big Data do SQL Server](deploy-offline.md)
- [Workshop: Arquitetura dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
---
title: Diretrizes de implantação
titleSuffix: SQL Server big data clusters
description: Saiba como implantar SQL Server clusters de Big Data 2019 (versão prévia) em kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e6f2eefd37c45753e3051722448b80d88712df26
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419423"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Como implantar SQL Server clusters de Big Data no kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server Cluster de Big Data é implantado como contêineres do Docker em um cluster kubernetes. Esta é uma visão geral das etapas de instalação e configuração:

- Configure um cluster kubernetes em uma única VM, cluster de VMs ou no AKS (serviço kubernetes do Azure).
- Instale a ferramenta de configuração de cluster **azdata** no computador cliente.
- Implante um cluster SQL Server Big Data em um cluster kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>Instalar as ferramentas do SQL Server 2019 Big Data

Antes de implantar um cluster SQL Server 2019 Big Data, primeiro [Instale as ferramentas de Big data](deploy-big-data-tools.md):

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **Extensão SQL Server 2019**

## <a id="prereqs"></a>Pré-requisitos do kubernetes

SQL Server clusters Big Data exigem uma versão mínima do kubernetes de pelo menos v 1,10 tanto para o servidor quanto para o cliente (kubectl).

> [!NOTE]
> Observe que as versões de kubernetes do cliente e do servidor devem estar dentro de + 1 ou-1 versão secundária. Para obter mais informações, consulte [notas de versão do kubernetes e política de SKU de distorção de versão)](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

### <a id="kubernetes"></a>Configuração do cluster kubernetes

Se você já tiver um cluster kubernetes que atenda aos pré-requisitos acima, poderá pular diretamente para a [etapa de implantação](#deploy). Esta seção pressupõe uma compreensão básica dos conceitos de kubernetes.  Para obter informações detalhadas sobre o kubernetes, consulte a [documentação do kubernetes](https://kubernetes.io/docs/home).

Você pode optar por implantar o kubernetes de uma das três maneiras:

| Implantar kubernetes em: | Descrição | Link |
|---|---|---|
| **AKS (serviços Kubernetess do Azure)** | Um serviço de contêiner kubernetes gerenciado no Azure. | [Sobre](deploy-on-aks.md) |
| **Vários computadores (kubeadm)** | Um cluster kubernetes implantado em máquinas físicas ou virtuais usando o **kubeadm** | [Sobre](deploy-with-kubeadm.md) |
| **Minikube** | Um cluster kubernetes de nó único em uma VM. | [Sobre](deploy-on-minikube.md) |

> [!TIP]
> Para obter um exemplo de script Python que implanta AKs e um SQL Server Big data cluster em uma única etapa, [consulte início rápido: Implante SQL Server Cluster de Big Data no serviço de kubernetes do Azure](quickstart-big-data-cluster-deploy.md)(AKs).

### <a name="verify-kubernetes-configuration"></a>Verificar configuração do kubernetes

Execute o comando **kubectl** para exibir a configuração do cluster. Verifique se kubectl está apontado para o contexto de cluster correto.

```bash
kubectl config view
```

Depois de configurar o cluster kubernetes, você pode prosseguir com a implantação de um novo cluster SQL Server Big Data. Se você estiver atualizando de uma versão anterior, consulte [como atualizar SQL Server clusters de Big data](deployment-upgrade.md).

## <a id="deploy"></a>Visão geral da implantação

A maioria Big Data configurações de cluster são definidas em um arquivo de configuração de implantação JSON. Você pode usar um perfil de implantação padrão para AKs `kubeadm`, ou `minikube` ou pode personalizar seu próprio arquivo de configuração de implantação a ser usado durante a instalação. Por motivos de segurança, as configurações de autenticação são passadas por meio de variáveis de ambiente.

As seções a seguir fornecem mais detalhes sobre como configurar suas implantações de cluster Big Data, bem como exemplos de personalizações comuns. Além disso, você sempre pode editar o arquivo de configuração de implantação personalizada usando um editor como VS Code por exemplo.

## <a id="configfile"></a>Configurações padrão

As opções de implantação de cluster de Big data são definidas em arquivos de configuração JSON. Há três perfis de implantação padrão com configurações padrão para ambientes de desenvolvimento/teste:

| Perfil de implantação | Ambiente kubernetes |
|---|---|
| **aks-dev-test** | AKS (serviço kubernetes do Azure) |
| **kubeadm-dev-test** | Vários computadores (kubeadm) |
| **minikube-dev-test** | minikube |

Você pode implantar um cluster Big Data executando a **criação do BDC azdata**. Isso solicitará que você escolha uma das configurações padrão e, em seguida, o guiará pela implantação.

Na primeira vez que você `azdata` executar o, `--accept-eula` deverá incluir para aceitar o EULA (contrato de licença de usuário final).

```bash
azdata bdc create --accept-eula
```

Nesse cenário, são solicitadas as configurações que não fazem parte da configuração padrão, como senhas. 

> [!NOTE]
> A partir do SQL Server 2019 CTP 3,2, você não é mais membro do que o SQL Server 2019 [programa de adoção antecipada](https://aka.ms/eapsignup) para experimentar as versões de visualização do cluster Big Data.

> [!IMPORTANT]
> O nome padrão do cluster de Big Data é **MSSQL-cluster**. Isso é importante saber para executar qualquer um dos comandos **kubectl** que especificam o namespace kubernetes com o `-n` parâmetro.

## <a id="customconfig"></a>Configurações personalizadas

Também é possível personalizar seu próprio perfil de configuração de implantação. Você pode fazer isso com as seguintes etapas:

1. Comece com um dos perfis de implantação padrão que correspondem ao seu ambiente kubernetes. Você pode usar o comando **azdata BDC config List** para listá-los:

   ```bash
   azdata bdc config list
   ```

1. Para personalizar sua implantação, crie uma cópia do perfil de implantação com o comando **azdata BDC config init** . Por exemplo, o comando a seguir cria uma cópia dos arquivos de configuração de implantação **AKs-dev-Test** em um diretório `custom`de destino chamado:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   azdata
   > O `--target` especifica um diretório que contém os arquivos de configuração, **cluster. JSON** e `--source` **Control. JSON**, com base no parâmetro.

1. Para personalizar as configurações em seu perfil de configuração de implantação, você pode editar o arquivo de configuração de implantação em uma ferramenta que é boa para editar arquivos JSON, como VS Code. Para automação com script, você também pode editar o perfil de implantação personalizado usando o comando **azdata BDC config** . Por exemplo, o comando a seguir altera um perfil de implantação personalizado para alterar o nome do cluster implantado do padrão (**MSSQL-cluster**) para **Test-cluster**:  

   ```bash
   azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
   ```

   > Uma ferramenta útil para localizar caminhos JSON é o [avaliador do JSONPath online](https://jsonpath.com/).

   Além de passar os pares de chave-valor, você também pode fornecer valores JSON embutidos ou passar arquivos de patch JSON. Para obter mais informações, consulte [definir configurações de implantação para clusters de Big data](deployment-custom-configuration.md).

1. Em seguida, passe o arquivo de configuração personalizada para o **azdata BDC Create**. Observe que você deve definir as [variáveis de ambiente](#env)necessárias, caso contrário, os valores serão solicitados:

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> Para obter mais informações sobre a estrutura de um arquivo de configuração de implantação, consulte a [referência do arquivo de configuração de implantação](reference-deployment-config.md). Para obter mais exemplos de configuração, consulte [definir configurações de implantação para clusters de Big data](deployment-custom-configuration.md).

## <a id="env"></a>Variáveis de ambiente

As variáveis de ambiente a seguir são usadas para configurações de segurança que não são armazenadas em um arquivo de configuração de implantação. Observe que as configurações do Docker, exceto as credenciais, podem ser definidas no arquivo de configuração.

| Variável de ambiente | Requisito |Descrição |
|---|---|---|
| **CONTROLLER_USERNAME** | Obrigatório |O nome de usuário para o administrador de cluster. |
| **CONTROLLER_PASSWORD** | Obrigatório |A senha para o administrador do cluster. |
| **MSSQL_SA_PASSWORD** | Obrigatório |A senha do usuário SA para a instância mestra do SQL. |
| **KNOX_PASSWORD** | Obrigatório |A senha do usuário do Knox. |
| **ACCEPT_EULA**| Necessário para o primeiro uso de`azdata`| Não requer valor. Quando definido como uma variável de ambiente, ele aplica o EULA ao SQL Server `azdata`e ao. Se não estiver definido como variável de ambiente, você `--accept-eula` poderá incluir no primeiro uso `azdata` do comando.|
| **DOCKER_USERNAME** | Opcional | O nome de usuário para acessar as imagens de contêiner, caso elas sejam armazenadas em um repositório privado. Consulte o tópico [offline](deploy-offline.md) Implantations para obter mais detalhes sobre como usar um repositório privado do Docker para Big data implantação de cluster.|
| **DOCKER_PASSWORD** | Opcional |A senha para acessar o repositório privado acima. |

Essas variáveis de ambiente devem ser definidas antes de chamar **azdata BDC Create**. Se qualquer variável não for definida, você será solicitado a fazê-lo.

O exemplo a seguir mostra como definir as variáveis de ambiente para Linux (bash) e Windows (PowerShell):

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

Depois de definir as variáveis de ambiente, você `azdata bdc create` deve executar o para disparar a implantação. Este exemplo usa o perfil de configuração de cluster criado acima:

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

Observe as seguintes diretrizes:

- Certifique-se de encapsular a senha entre aspas duplas se ela contiver caracteres especiais. Você pode definir o **MSSQL_SA_PASSWORD** como o que desejar, mas certifique-se de que a senha seja suficientemente complexa e `!`não `&` use `'` os caracteres ou. Observe que os delimitadores de aspas duplas funcionam apenas em comandos bash.
- O logon **SA** é um administrador do sistema na instância mestra do SQL Server que é criada durante a instalação. Depois de criar seu contêiner de SQL Server, a variável de ambiente **MSSQL_SA_PASSWORD** especificada é detectável por meio `echo $MSSQL_SA_PASSWORD` da execução no contêiner. Para fins de segurança, altere sua senha SA de acordo com as práticas recomendadas documentadas [aqui](../linux/quickstart-install-connect-docker.md#sapassword).

## <a id="unattended"></a>Instalação autônoma

Para uma implantação autônoma, você deve definir todas as variáveis de ambiente necessárias, usar um arquivo de configuração e chamar `azdata bdc create` o comando com `--accept-eula yes` o parâmetro. Os exemplos na seção anterior demonstram a sintaxe de uma instalação autônoma.

## <a id="monitor"></a>Monitorar a implantação

Durante a inicialização do cluster, a janela de comando do cliente produzirá o status da implantação. Durante o processo de implantação, você deverá ver uma série de mensagens em que ela está aguardando o Pod do controlador:

```output
Waiting for cluster controller to start.
```

Em 15 a 30 minutos, você deve ser notificado de que o Pod do controlador está em execução:

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> A implantação inteira pode levar muito tempo devido ao tempo necessário para baixar as imagens de contêiner para os componentes do cluster de Big Data. No entanto, não deve levar várias horas. Se você estiver tendo problemas com sua implantação, consulte [monitoramento e solução de problemas SQL Server clusters de Big data](cluster-troubleshooting-commands.md).

Quando a implantação for concluída, a saída notifica você sobre o sucesso:

```output
Cluster deployed successfully.
```

> [!TIP]
> O nome padrão para o cluster Big data implantado é a menos que seja `mssql-cluster` modificado por uma configuração personalizada.

## <a id="endpoints"></a>Recuperar pontos de extremidade

Depois que o script de implantação for concluído com êxito, você poderá obter os endereços IP dos pontos de extremidade externos para o cluster Big Data usando as etapas a seguir.

1. Após a implantação, localize o endereço IP do ponto de extremidade do controlador da saída padrão de implantação ou examinando a saída de IP externo do seguinte comando **kubectl** :

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se você não alterou o nome padrão durante a implantação, `-n mssql-cluster` use no comando anterior. **MSSQL-cluster** é o nome padrão para o cluster de Big Data.

1. Faça logon no cluster Big Data com [logon azdata](reference-azdata.md). Defina o parâmetro **--Controller-Endpoint** como o endereço IP externo do ponto de extremidade do controlador.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique o nome de usuário e a senha que você configurou para o controlador (CONTROLLER_USERNAME e CONTROLLER_PASSWORD) durante a implantação.

1. Execute a [lista de pontos de extremidade do BDC do azdata](reference-azdata-bdc-endpoint.md) para obter uma lista com uma descrição de cada ponto de extremidade e seus valores de porta e endereço IP correspondentes. 

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

Você também pode obter todos os pontos de extremidade de serviço implantados para o cluster executando o seguinte comando **kubectl** :

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

### <a name="minikube"></a>Minikube

Se você estiver usando o minikube, será necessário executar o comando a seguir para obter o endereço IP ao qual você precisa se conectar. Além do IP, especifique a porta para o ponto de extremidade ao qual você precisa se conectar.

```bash
minikube ip
```

## <a id="status"></a>Verificar o status do cluster

Após a implantação, você pode verificar o status do cluster com o comando [azdata BDC status show](reference-azdata-bdc-status.md) .

```bash
azdata bdc status show -o table
```

> [!TIP]
> Para executar os comandos de status, primeiro você deve fazer logon com o comando de **logon azdata** , que foi mostrado na seção pontos de extremidade anteriores.

Veja a seguir uma saída de exemplo deste comando:

```output
Kind     Name           State
-------  -------------  -------
BDC      mssql-cluster  Ready
Control  default        Ready
Master   default        Ready
Compute  default        Ready
Data     default        Ready
Storage  default        Ready
```

No status do resumo, você também pode obter o status mais detalhado com os seguintes comandos:

- [status do controle do BDC azdata](reference-azdata-bdc-control-status.md)
- [status do pool BDC azdata](reference-azdata-bdc-pool-status.md)

A saída desses comandos contém URLs para os painéis Kibana e Grafana para uma análise mais detalhada.

Além de usar o **azdata**, você também pode usar Azure Data Studio para localizar os pontos de extremidade e as informações de status. Para obter mais informações sobre como exibir o status do cluster com **azdata** e Azure Data Studio, consulte [como exibir o status de um cluster de Big data](view-cluster-status.md).

## <a id="connect"></a>Conectar-se ao cluster

Para obter mais informações sobre como se conectar ao cluster de Big Data, consulte [conectar-se a um SQL Server Big data cluster com Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a implantação de cluster Big Data, consulte os seguintes recursos:

- [Definir configurações de implantação para clusters de Big Data](deployment-custom-configuration.md)
- [Executar uma implantação offline de um cluster SQL Server Big Data](deploy-offline.md)
- [Oficina Arquitetura de clusters de Big Data Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)

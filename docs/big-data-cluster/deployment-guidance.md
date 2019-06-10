---
title: Diretrizes de implantação
titleSuffix: SQL Server big data clusters
description: Aprenda a implantar clusters de big data de 2019 do SQL Server (versão prévia) no Kubernetes.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 15cd412de1dda9d1245859c27d35a7c7f9f52710
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782244"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Como implantar clusters de grandes dados do SQL Server no Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Cluster de big data do SQL Server é implantado como contêineres do docker em um cluster Kubernetes. Isso é uma visão geral das etapas de instalação e configuração:

- Configure um cluster Kubernetes em uma única VM, o cluster de VMs ou no serviço de Kubernetes do Azure (AKS).
- Instalar a ferramenta de configuração de cluster **mssqlctl** no computador cliente.
- Implante um cluster de big data do SQL Server em um cluster Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>Instalar ferramentas do SQL Server 2019 big data

Antes de implantar um cluster de big data de 2019 do SQL Server, primeiro [instalar as ferramentas de big data](deploy-big-data-tools.md):

- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **Extensão do SQL Server de 2019**

## <a id="prereqs"></a> Pré-requisitos do Kubernetes

Clusters de grandes dados do SQL Server requerem uma versão mínima do Kubernetes de pelo menos v 1.10 para servidor e cliente (kubectl).

> [!NOTE]
> Observe que as versões de servidor e cliente Kubernetes devem estar dentro de + 1 ou -1, versão secundária. Para obter mais informações, consulte [Kubernetes suporte para versões e componente distorção](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

### <a id="kubernetes"></a> Instalação de cluster do Kubernetes

Se você já tiver um cluster do Kubernetes que atende aos pré-requisitos acima e, em seguida, você poderá pular diretamente para o [etapa de implantação](#deploy). Esta seção pressupõe uma compreensão básica dos conceitos de Kubernetes.  Para obter informações detalhadas sobre Kubernetes, consulte o [documentação do Kubernetes](https://kubernetes.io/docs/home).

Você pode optar por implantar Kubernetes em qualquer uma das três maneiras:

| Implante Kubernetes em: | Descrição | Link |
|---|---|---|
| **Serviços de Kubernetes do Azure (AKS)** | Um serviço gerenciado de contêiner do Kubernetes no Azure. | [Instruções](deploy-on-aks.md) |
| **Várias máquinas (kubeadm)** | Um cluster Kubernetes implantado em máquinas físicas ou virtuais usando **kubeadm** | [Instruções](deploy-with-kubeadm.md) |
| **Minikube** | Um cluster do Kubernetes de nó único em uma VM. | [Instruções](deploy-on-minikube.md) |

> [!TIP]
> Para um script de python de exemplo que implanta o AKS e um cluster de big data em uma etapa do SQL Server, consulte [guia de início rápido: Implantar o SQL Server no serviço de Kubernetes do Azure (AKS) de cluster de big data](quickstart-big-data-cluster-deploy.md).

### <a name="verify-kubernetes-configuration"></a>Verifique se a configuração do Kubernetes

Execute o **kubectl** comando para exibir a configuração do cluster. Certifique-se de que kubectl está apontada para o contexto do cluster correto.

```bash
kubectl config view
```

Depois de configurar o cluster Kubernetes, você pode continuar com a implantação de um novo cluster de big data do SQL Server. Se você estiver atualizando de uma versão anterior, consulte [como atualizar clusters de grandes dados do SQL Server](deployment-upgrade.md).

## <a id="deploy"></a> Visão geral da implantação

A partir do CTP 2.5, a maioria das configurações de cluster de big data são definidos em um arquivo de configuração de implantação de JSON. Você pode usar um perfil de implantação padrão para o AKS, kubeadm, ou minikube ou você pode personalizar o seu próprio arquivo de configuração de implantação para usar durante a instalação. Por motivos de segurança, as configurações de autenticação são passadas por meio de variáveis de ambiente.

As seções a seguir fornecem mais detalhes sobre como configurar seu big data implantações, bem como exemplos de personalização comuns do cluster. Além disso, você sempre pode editar o arquivo de configuração de implantação personalizada usando um editor como o VSCode por exemplo.

## <a id="configfile"></a> Configurações padrão

As opções são definidas nos arquivos de configuração do JSON de implantação de cluster de big data. Há três perfis de implantação padrão com configurações padrão para ambientes de desenvolvimento/teste:

| Perfil de implantação | Ambiente do Kubernetes |
|---|---|
| **aks-dev-test.json** | Serviço de Kubernetes do Azure (AKS) |
| **kubeadm-dev-test.json** | Várias máquinas (kubeadm) |
| **minikube-dev-test.json** | minikube |

Você pode implantar um cluster de big data, executando **criar cluster mssqlctl**. Isso solicitará que você escolha uma das configurações padrão e orientará você durante a implantação.

```bash
mssqlctl cluster create
```

Nesse cenário, você será solicitado para todas as configurações que não fazem parte da configuração padrão, como senhas. Observe que as informações do Docker são fornecidas a você pela Microsoft como parte do SQL Server 2019 [programa de adoção antecipada](https://aka.ms/eapsignup).

> [!IMPORTANT]
> É o nome padrão do cluster de big data **mssql-cluster**. Isso é importante saber para executar qualquer um dos **kubectl** comandos que especifica o namespace do Kubernetes com o `-n` parâmetro.

## <a id="customconfig"></a> Configurações personalizadas

Também é possível personalizar seu próprio arquivo de configuração de implantação. Você pode fazer isso com as seguintes etapas:

1. Comece com um dos perfis de implantação padrão que correspondem ao seu ambiente de Kubernetes. Você pode usar o **lista de configuração de cluster mssqlctl** comando para listá-los:

   ```bash
   mssqlctl cluster config list
   ```

1. Para personalizar sua implantação, crie uma cópia do perfil de implantação com o **mssqlctl cluster config init** comando. Por exemplo, o comando a seguir cria uma cópia do **aks-dev-test.json** arquivo de configuração de implantação no diretório atual:

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
   ```

1. Para personalizar configurações no arquivo de configuração de implantação, você pode editá-lo em uma ferramenta que é bom para edição de documentos json como o VS Code. Para a automação com scripts, você pode editar o arquivo de configuração personalizada usando **conjunto de seção de configuração de cluster mssqlctl** comando. Por exemplo, o comando a seguir altera um arquivo de configuração personalizada para alterar o nome do cluster implantado do padrão (**mssql-cluster**) para **test-cluster**:  

   ```bash
   mssqlctl cluster config section set --config-file custom.json --json-values "metadata.name=test-cluster"
   ```

   > [!TIP]
   > Uma ferramenta útil para encontrar caminhos JSON é o [avaliador on-line de JSONPath](https://jsonpath.com/).

   Além de passar pares chave-valor, você pode também fornecer embutido valores JSON ou transmitir arquivos de patch JSON. Para obter mais informações, consulte [definir as configurações de implantação para clusters de big data](deployment-custom-configuration.md).

1. Em seguida, passar o arquivo de configuração personalizada para **criar cluster mssqlctl**. Observe que você deve definir exigida [variáveis de ambiente](#env), caso contrário, você será solicitado para os valores:

   ```bash
   mssqlctl cluster create --config-file custom.json --accept-eula yes
   ```

> [!TIP]
> Para obter mais informações sobre a estrutura de um arquivo de configuração de implantação, consulte o [referência de arquivo de configuração de implantação](reference-deployment-config.md). Para obter mais exemplos de configuração, consulte [definir as configurações de implantação para clusters de big data](deployment-custom-configuration.md).

## <a id="env"></a> Variáveis de ambiente

As seguintes variáveis de ambiente são usadas para configurações de segurança que não são armazenadas em um arquivo de configuração de implantação. Observe que o Docker, exceto as credenciais podem ser definidas no arquivo de configuração.

| Variável de ambiente | Descrição |
|---|---|---|---|
| **DOCKER_USERNAME** | O nome de usuário para acessar as imagens de contêiner, caso eles são armazenados em um repositório privado. |
| **DOCKER_PASSWORD** | A senha para acessar o repositório privado acima. |
| **CONTROLLER_USERNAME** | O nome de usuário para o administrador de cluster. |
| **CONTROLLER_PASSWORD** | A senha para o administrador de cluster. |
| **KNOX_PASSWORD** | A senha do usuário do Knox. |
| **MSSQL_SA_PASSWORD** | A senha do usuário de SA para a instância mestre do SQL. |

Essas variáveis de ambiente devem ser definidas antes de chamar **criar cluster mssqlctl**. Se qualquer variável não for definido, você será solicitado para ele.

O exemplo a seguir mostra como definir as variáveis de ambiente para Linux (bash) e Windows (PowerShell):

```bash
export CONTROLLER_USERNAME=admin
export CONTROLLER_PASSWORD=<password>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
export DOCKER_USERNAME=<docker-username>
export DOCKER_PASSWORD=<docker-password>
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
SET DOCKER_USERNAME=<docker-username>
SET DOCKER_PASSWORD=<docker-password>
```

Após definir as variáveis de ambiente, você deve executar `mssqlctl cluster create` para disparar a implantação. Este exemplo usa o arquivo de configuração de cluster criado acima:

```
mssqlctl cluster create --config-file custom.json --accept-eula yes
```

Observe as seguintes diretrizes:

- Neste momento, as credenciais para o registro privado do Docker serão fornecidas para você após a separação sua [registro do programa de adoção antecipada](https://aka.ms/eapsignup). Registro do programa de adoção antecipado é necessária para testar a clusters de grandes dados do SQL Server.
- Certifique-se de que encapsular as senhas entre aspas duplas se ele contiver caracteres especiais. Você pode definir as **MSSQL_SA_PASSWORD** para tudo o que você gosta, mas certifique-se a senha é suficientemente complexa e não usar o `!`, `&` ou `'` caracteres. Observe que os delimitadores de aspas duplas funcionam somente em comandos de bash.
- O **SA** logon é um administrador do sistema na instância mestre do SQL Server que é criada durante a instalação. Depois de criar o contêiner do SQL Server, o **MSSQL_SA_PASSWORD** variável de ambiente especificada é detectável executando echo MSSQL_SA_PASSWORD $ no contêiner. Para fins de segurança, altere sua senha de SA, de acordo com práticas recomendadas documentadas [aqui](../linux/quickstart-install-connect-docker.md#sapassword).

## <a id="unattended"></a> Instalação autônoma

Para uma implantação autônoma, você deve definir todas as variáveis de ambiente necessárias, use um arquivo de configuração e chamada `mssqlctl cluster create` com o `--accept-eula yes` parâmetro. Os exemplos na seção anterior demonstram a sintaxe para uma instalação autônoma.

## <a id="monitor"></a> Monitore a implantação

Durante a inicialização do cluster, a janela de comando do cliente produzirá o status da implantação. Durante o processo de implantação, você deverá ver uma série de mensagens em que ele está aguardando o pod do controlador:

```output
2019-04-12 14:40:10.0129 UTC | INFO | Waiting for controller pod to be up...
```

Em menos de 15 a 30 minutos, você deve ser notificado se o pod de controlador está em execução:

```output
2019-04-12 15:01:10.0809 UTC | INFO | Waiting for controller pod to be up. Checkthe mssqlctl.log file for more details.
2019-04-12 15:01:40.0861 UTC | INFO | Controller pod is running.
2019-04-12 15:01:40.0884 UTC | INFO | Controller Endpoint: https://<ip-address>:30080
```

> [!IMPORTANT]
> Toda a implantação pode levar muito tempo devido ao tempo necessário para baixar as imagens de contêiner para os componentes do cluster de big data. No entanto, ele não deve levar várias horas. Se você estiver tendo problemas com sua implantação, consulte [monitoramento e solução de problemas de clusters de grandes dados do SQL Server](cluster-troubleshooting-commands.md).

Quando a implantação for concluída, a saída notifica você de sucesso:

```output
2019-04-12 15:37:18.0271 UTC | INFO | Monitor and track your cluster at the Portal Endpoint: https://<ip-address>:30777/portal/
2019-04-12 15:37:18.0271 UTC | INFO | Cluster deployed successfully.
```

Anote a URL da **ponto de extremidade do Portal** na saída anterior para uso na próxima seção.

> [!TIP]
> É o nome padrão para o cluster de big data implantados `mssql-cluster` , a menos que modificado por uma configuração personalizada.

## <a id="endpoints"></a> Recuperar pontos de extremidade

Depois que o script de implantação foi concluída com êxito, você pode obter os endereços IP dos pontos de extremidade externos para o cluster de big data usando as etapas a seguir.

1. Após a implantação, localize o endereço IP do ponto de extremidade controlador examinando a saída EXTERNAL-IP das seguintes **kubectl** comando:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se você não alterou o nome padrão durante a implantação, use `-n mssql-cluster` no comando anterior. **MSSQL-cluster** é o nome padrão para o cluster de big data.

1. Faça logon no cluster de big data com **mssqlctl logon**. Defina a **– controlador de ponto de extremidade** parâmetro para o endereço IP externo do ponto de extremidade de controlador.

   ```bash
   mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique o nome de usuário e a senha que você configurou para o controlador (CONTROLLER_USERNAME e CONTROLLER_PASSWORD) durante a implantação.

1. Execute **lista de ponto de extremidade do cluster mssqlctl** para obter uma lista com uma descrição de cada ponto de extremidade e seus valores correspondentes de porta e endereço IP. 

   ```bash
   mssqlctl cluster endpoint list
   ```

   A lista a seguir mostra um exemplo de saída deste comando:

   ```output
   Name               Description                                             Endpoint                                                   Ip              Port    Protocol
   -----------------  ------------------------------------------------------  ---------------------------------------------------------  --------------  ------  ----------
   gateway            Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  30443   https
   spark-history      Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  30443   https
   yarn-ui            Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  30443   https
   app-proxy          Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  30778   https
   management-proxy   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  30777   https
   portal             Management Portal                                       https://11.111.111.111:30777/portal                        11.111.111.111  30777   https
   log-search-ui      Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  30777   https
   metrics-ui         Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  30777   https
   controller         Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  30080   https
   sql-server-master  SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  31433   tcp
   webhdfs            HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  30443   https
   livy               Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  30443   https
   ```

### <a name="minikube"></a>Minikube

Se você estiver usando o minikube, você precisa executar o seguinte comando para obter o endereço IP que você precisa para se conectar ao. Além de IP, especifique a porta para o ponto de extremidade que você precisa para se conectar ao.

```bash
minikube ip
```

Independentemente da plataforma você está executando o cluster Kubernetes, para obter todos os pontos de serviço implantados para o cluster, execute o comando a seguir:

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

## <a id="connect"></a> Conectar-se ao cluster

Para obter mais informações sobre como se conectar ao cluster de big data, consulte [conectar-se a um SQL Server cluster de big data com o Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a implantação de cluster de big data, consulte os seguintes recursos:

- [Definir as configurações de implantação para clusters de big data](deployment-custom-configuration.md)
- [Executar uma implantação offline de um cluster de big data do SQL Server](deploy-offline.md)
- [Workshop: Arquitetura de clusters de grandes dados do Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)

---
title: Notas sobre a versão de Clusters de Big Data do SQL Server
titleSuffix: SQL Server big data clusters
description: Este artigo descreve as atualizações mais recentes e problemas conhecidos dos Clusters de Big Data do SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4217e2be765e29fe58ff423be8632f7e18e1b2eb
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834511"
---
# <a name="sql-server-2019-big-data-clusters-release-notes"></a>Notas sobre a versão de Clusters de Big Data do SQL Server 2019

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

As notas sobre a versão a seguir se aplicam a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Este artigo está dividido em seções para cada versão. Cada versão tem um link para um artigo de suporte que descreve as alterações da CU, bem como links para os downloads dos pacotes do Linux. O artigo também lista [problemas conhecidos](#known-issues) para as versões mais recentes do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC).

## <a name="supported-platforms"></a>Plataformas compatíveis

Nesta seção, há uma explicação sobre as plataformas compatíveis com o BDC.

### <a name="kubernetes-platforms"></a>Plataformas do Kubernetes

|Plataforma|Versões com suporte|
|---------|---------|
|Kubernetes Vanilla (upstream)|Implante o BDC localmente usando uma versão de cluster do Kubernetes igual ou superior à 1.13. Confira [Política de suporte à distorção de versão e à versão do Kubernetes](https://kubernetes.io/docs/setup/release/version-skew-policy/).|
|Red Hat OpenShift|Implante o BDC localmente usando uma versão de cluster do OpenShift igual ou superior à 4.3. Confira [Política de ciclo de vida de Red Hat OpenShift Container Platform](https://access.redhat.com/support/policy/updates/openshift).<br><br> Suporte introduzido no SQL Server 2019 CU5.|
|AKS (Serviço de Kubernetes do Azure)|Implante o BDC em um cluster do AKS com versão igual ou superior à 1.13.<br/>Confira [Versões do Kubernetes com suporte no AKS](/azure/aks/supported-kubernetes-versions) para obter a política de suporte de versão.|
|ARO (Red Hat OpenShift no Azure)|Implante o BDC em um ARO com versão igual ou superior à 4.3. Confira [Red Hat OpenShift no Azure](/azure/openshift/). <br><br> Suporte introduzido no SQL Server 2019 CU5.|

### <a name="host-os-for-kubernetes"></a>SO host para Kubernetes

|Plataforma|SO host|Versões com suporte|
|---------|---------|
|Kubernetes|Ubuntu|16.04|
|Kubernetes|Red Hat Enterprise Linux|7.3, 7.4, 7.5, 7.6|
|OpenShift|Red Hat Enterprise Linux/CoreOS |Confira [notas sobre a versão do OpenShift](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-about-this-release)|

### <a name="sql-server-editions"></a>Edições do SQL Server

|Edition|Observações|
|---------|---------|
|Enterprise<br/>Standard<br/>Desenvolvedor| A edição de cluster de Big Data é determinada pela edição da instância mestra do SQL Server. No momento da implantação, a Developer Edition é implantada por padrão. Você pode alterar a edição após a implantação. Confira [Configurar a instância mestra do SQL Server](./configure-sql-server-master-instance.md). |

## <a name="tools"></a>Ferramentas

|Plataforma|Versões com suporte|
|---------|---------|
|`azdata`|Como melhor prática, use a versão mais recente disponível. Na versão SQL Server 2019 CU5 e posteriores, `azdata` tem uma versão semântica independente do servidor. <br/><br/>Execute `azdata –-version` para validar a versão.<br/><br/>Confira o [Histórico de versões](#release-history) para ver a versão mais recente.|
|Azure Data Studio|Obtenha o build mais recente do [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md).|

Para obter uma lista completa, confira [Quais ferramentas são necessárias?](deploy-big-data-tools.md#which-tools-are-required)

## <a name="release-history"></a>Histórico de versões

A tabela a seguir lista o histórico de versões do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].

| Versão<sup>1</sup> | Versão do BDC  | `azdata` Versão <sup>2</sup> | Data de liberação |
|----------------------|--------------|-------------------------------|--------------|
| [CU6](#cu6)          | 15.0.4053.23 | 20.0.1                        | 04-08-2020   |
| [CU5](#cu5)          | 15.0.4043.16 | 20.0.0                        | 2020-06-22   |
| [CU4](#cu4)          | 15.0.4033.1  | 15.0.4033                     | 2020-03-31   |
| [CU3](#cu3)          | 15.0.4023.6  | 15.0.4023                     | 2020-03-12   |
| [CU2](#cu2)          | 15.0.4013.40 | 15.0.4013                     | 2020-02-13   |
| [CU1](#cu1)          | 15.0.4003.23 | 15.0.4003                     | 2020-01-07   |
| [GDR1](#rtm)         | 15.0.2070.34 | 15.0.2070                     | 2019-11-04   |

<sup>1</sup>As seguintes versões não estão disponíveis para o BDC:
- CU7
- CU8

<sup>2</sup>A versão `azdata` reflete a versão da ferramenta no momento do lançamento da CU. `azdata` também pode ser liberado de maneira independente da versão do servidor, portanto, você pode obter versões mais recentes ao instalar os pacotes mais recentes. As versões mais recentes são compatíveis com os CUs lançados anteriormente.

## <a name="how-to-install-updates"></a>Como instalar atualizações

Para instalar atualizações, confira [Como atualizar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-upgrade.md).

## <a name="cu6-july-2020"></a><a id="cu6"></a> CU6 (julho de 2020)

Versão CU6 (Atualização Cumulativa 6) do SQL Server 2019.

|Versão do pacote | Tag de imagem |
|-----|-----|
|15.0.4053.23 |[2019-CU6-ubuntu-16.04]

Essa versão inclui correções e melhorias secundárias. Os seguintes artigos incluem informações relacionadas a essas atualizações:

- [Gerenciar o acesso ao cluster de Big Data no modo do Active Directory](manage-user-access.md)
- [Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](deploy-active-directory.md)
- [Implantar o cluster de Big Data do SQL Server com alta disponibilidade](deployment-high-availability.md)
- [Configurar um cluster de Big Data do SQL Server](configure-cluster.md)
- [Configurar Apache Spark e Apache Hadoop em Clusters de Big Data](configure-spark-hdfs.md)
- [Propriedades de configuração da instância mestra do SQL Server.](reference-config-master-instance.md)
- [Propriedades de configuração do Apache Spark e do Apache Hadoop (HDFS)](reference-config-spark-hadoop.md)
- [O modelo RBAC do Kubernetes e o impacto sobre os usuários e as contas de serviço que gerenciam os BDC](kubernetes-rbac.md)

## <a name="cu5-june-2020"></a><a id="cu5"></a> CU5 (junho de 2020)

Versão CU5 (Atualização Cumulativa 5) do SQL Server 2019.

|Versão do pacote | Tag de imagem |
|-----|-----|
|15.0.4043.16 |[2019-CU5-ubuntu-16.04]

### <a name="added-capabilities"></a>Funcionalidades adicionadas

- Suporte para implantação de Clusters de Big Data no Red Hat OpenShift. O suporte inclui a plataforma de contêiner OpenShift implantada na versão local 4.3 e no Red Hat OpenShift no Azure. Confira [Implantar Clusters de Big Data do SQL Server no OpenShift](deploy-openshift.md)
- O modelo de segurança de implantação do BDC foi atualizado para que contêineres privilegiados implantados como parte do BDC não sejam mais *necessários*. Além de não privilegiados, os contêineres são executados como um usuário não raiz por padrão em todas as novas implantações usando o SQL Server 2019 CU5. 
- Suporte adicionado para implantação de vários Clusters de Big Data em um domínio Active Directory.
- A CLI do `azdata` tem uma versão semântica própria, independente do servidor. Qualquer dependência entre o cliente e a versão do servidor do azdata é removida. É recomendável usar a versão mais recente para o cliente e o servidor para garantir que você esteja se beneficiando dos aprimoramentos e correções mais recentes.
- Introduzidos dois novos procedimentos armazenados, sp_data_source_objects e sp_data_source_table_columns, para dar suporte à introspecção de determinadas fontes de dados externas. Eles podem ser usados por clientes diretamente por meio do T-SQL para descoberta de esquemas e para ver quais tabelas estão disponíveis para serem virtualizadas. Aproveitamos essas alterações no Assistente de Tabela Externa da [Extensão de Virtualização de Dados](../azure-data-studio/extensions/data-virtualization-extension.md) para o Azure Data Studio, que permite usar o SQL Server, o Oracle, o MongoDB e o Teradata para criar tabelas externas.
- Adicionado suporte para persistência de personalizações realizadas no Grafana. Anteriormente, os clientes do CU5 percebiam que as edições nas configurações do Grafana seriam perdidas ao reiniciar o pod `metricsui` (que hospeda o painel do Grafana). Esse problema está corrigido e todas as configurações agora são persistidas. 
- Corrigido o problema de segurança relacionado à API usada para coletar as métricas do pod e do nó usando o Telegraf (hospedado nos pods `metricsdc`). Como resultado dessa alteração, o Telegraf agora requer uma conta de serviço, uma função de cluster e associações de cluster para obtenção das permissões necessárias para coleta das métricas de pod e de nó. Confira [Função de cluster necessária para a coleta de métricas de pods e de nós](kubernetes-rbac.md#cluster-role-required-for-pods-and-nodes-metrics-collection) para obter mais detalhes.
- Adicionadas duas opções de recurso para controlar a coleta de métricas de pod e nó. Caso você esteja usando soluções diferentes para monitorar sua infraestrutura de Kubernetes, é possível desligar a coleção de métricas internas para nós de host e pods definindo *allowNodeMetricsCollection* e *allowPodMetricsCollection* como false no arquivo de configuração de implantação control.json. Para ambientes do OpenShift, essas configurações são definidas como false por padrão nos perfis de implantação internos, pois a coleta de métricas de pod e de nó exigia funcionalidades privilegiadas.

## <a name="cu4-april-2020"></a><a id="cu4"></a> CU4 (abril de 2020)

Versão CU4 (Atualização Cumulativa 4) para o SQL Server 2019. A versão do Mecanismo de Banco de Dados do SQL Server para essa versão é 15.0.4033.1.

|Versão do pacote | Tag de imagem |
|-----|-----|
|15.0.4033.1 |[2019-CU4-ubuntu-16.04]

## <a name="cu3-march-2020"></a><a id="cu3"></a> CU3 (março de 2020)

Versão CU3 (Atualização Cumulativa 3) para o SQL Server 2019. A versão do Mecanismo de Banco de Dados do SQL Server para essa versão é 15.0.4023.6.

|Versão do pacote | Tag de imagem |
|-----|-----|
|15.0.4023.6 |[2019-CU3-ubuntu-16.04]

### <a name="resolved-issues"></a>Problemas resolvidos

O SQL Server 2019 CU3 resolve os seguintes problemas de versões anteriores.

- [Implantação com repositório privado](#deployment-with-private-repository)
- [A atualização pode falhar devido ao tempo limite](#upgrade-may-fail-due-to-timeout)

## <a name="cu2-february-2020"></a><a id="cu2"></a> CU2 (fevereiro de 2020)

Versão CU2 (Atualização Cumulativa 2) para o SQL Server 2019. A versão do Mecanismo de Banco de Dados do SQL Server para essa versão é 15.0.4013.40.

|Versão do pacote | Tag de imagem |
|-----|-----|
|15.0.4013.40 |[2019-CU2-ubuntu-16.04]

## <a name="cu1-january-2020"></a><a id="cu1"></a> CU1 (janeiro de 2020)

Versão CU1 (Atualização Cumulativa 1) para o SQL Server 2019. A versão do Mecanismo de Banco de Dados do SQL Server para essa versão é 15.0.4003.23.

|Versão do pacote | Tag de imagem |
|-----|-----|
|15.0.4003.23|[2019-CU1-ubuntu-16.04]

## <a name="gdr1-november-2019"></a><a id="rtm"></a> GDR1 (novembro de 2019)

A GDR1 (Versão de Distribuição Geral 1) do SQL Server 2019 – apresenta a disponibilidade geral para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-nover.md)]. A versão do Mecanismo de Banco de Dados do SQL Server para essa versão é 15.0.2070.34.

|Versão do pacote | Tag de imagem |
|-----|-----|
|15.0.2070.34|[2019-GDR1-ubuntu-16.04]

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="known-issues"></a>Problemas conhecidos

### <a name="empty-livy-jobs-before-you-apply-cumulative-updates"></a>Esvaziar trabalhos do Livy antes de aplicar atualizações cumulativas

- **Versões afetadas**: Por meio da atualização cumulativa atual

- **Problema e impacto sobre o cliente**: Durante uma atualização, o sparkhead retorna o erro 404.

- **Solução alternativa**: Antes de atualizar o BDC, verifique se não há sessões ativas do Livy ou trabalhos em lotes. Siga as instruções em [Atualização de versão com suporte](deployment-upgrade.md#upgrade-from-supported-release) para evitar isso. 

   Se o Livy retornar um erro 404 durante o processo de atualização, reinicie o servidor Livy em ambos os nós do sparkhead. Por exemplo:

   ```console
   kubectl -n <clustername> exec -it sparkhead-0/sparkhead-1 -c hadoop-livy-sparkhistory -- exec supervisorctl restart livy
   ```

### <a name="big-data-cluster-generated-service-accounts-passwords-expiration"></a>Término das senhas das contas de serviço geradas pelo cluster de Big Data

- **Versões afetadas**: Todas as implantações de cluster de Big Data com integração do Active Directory, independentemente da versão

- **Problema e impacto sobre o cliente**: Durante a implantação do cluster de Big Data, o fluxo de trabalho gera um conjunto de [contas de serviço](active-directory-objects.md). Dependendo da política de término de senha definida no controlador de domínio, as senhas para essas contas podem expirar (o padrão é 42 dias). No momento, não há mecanismo para girar credenciais para todas as contas no BDC, portanto, o cluster se tornará inoperante assim que o período de término for atingido.

- **Solução alternativa**: Atualize a política de término das contas de serviço BDC para “A senha nunca expira” no controlador de domínio. Para obter uma lista completa dessas contas, confira [Objetos do Active Directory gerados automaticamente](active-directory-objects.md). Essa ação pode ser realizada antes ou depois do tempo de término. No último caso, o Active Directory reativará como senhas expiradas.

### <a name="credentials-for-accessing-services-through-gateway-endpoint"></a>Credenciais para acessar serviços por meio do ponto de extremidade do gateway

- **Versões afetadas**: Novos clusters implantados, começando com a CU5.

- **Problema e impacto sobre o cliente**: Para novos Clusters de Big Data implantados usando o SQL Server 2019 CU5, o nome de usuário do gateway não é **raiz**. Se o aplicativo usado para se conectar ao ponto de extremidade do gateway estiver usando as credenciais erradas, você verá um erro de autenticação. Essa alteração é um resultado da execução de aplicativos no cluster de Big Data como um usuário não raiz (um novo comportamento padrão começando com a versão 2019 CU5 do SQL Server: quando você implanta um novo cluster de Big Data usando a CU5, o nome de usuário do ponto de extremidade do gateway é baseado no valor passado pela variável de ambiente **AZDATA_USERNAME**. É o mesmo nome de usuário usado para os pontos de extremidade do controlador e do SQL Server. Isso afeta apenas as novas implantações; os Clusters de Big Data existentes implantados com qualquer uma das versões anteriores continuam usando **raiz**. Não há nenhum impacto nas credenciais quando o cluster é implantado para usar a autenticação do Active Directory. 

- **Solução alternativa**: O Azure Data Studio manipulará a alteração de credenciais de maneira transparente para a conexão realizada ao gateway para permitir uma experiência de navegação do HDFS no Pesquisador de Objetos. Você precisa instalar a [versão mais recente do Azure Data Studio](../azure-data-studio/download-azure-data-studio.md), que inclui as alterações necessárias que abordam esse caso de uso.
Para outros cenários em que você precisa fornecer credenciais para acessar o serviço por meio do gateway (por exemplo, fazer logon com `azdata`, acessar painéis da Web para Spark), é preciso verificar se as credenciais corretas são usadas. Se estiver direcionando um cluster existente implantado antes do CU5, você continuará usando o nome de usuário **raiz** para se conectar ao gateway, mesmo depois de atualizar o cluster para o CU5. Se você implantar um novo cluster usando o build do CU5, fará logon fornecendo o nome de usuário correspondente à variável de ambiente **AZDATA_USERNAME**.

### <a name="pods-and-nodes-metrics-not-being-collected"></a>Métricas de pods e de nós não sendo coletadas

- **Versões afetadas**: clusters novos e existentes que estão usando imagens da CU5

- **Problema e impacto sobre o cliente**: como resultado de uma correção de segurança relacionada à API que `telegraf` estava usando para coletar métricas de pod e de nó de host, os clientes podem perceber que as métricas não estão sendo coletadas. Isso é possível em implantações novas e existentes do BDC (após a atualização para a CU5). Como resultado da correção, o Telegraf agora requer uma conta de serviço com permissões de função para todo o cluster. A implantação tenta criar a conta de serviço e a função de cluster necessárias, mas se o usuário que está implantando o cluster ou executando a atualização não tiver permissões suficientes, a implantação/atualização continuará com um aviso e terá sucesso, mas as métricas de nó e de pod não serão coletadas.

- **Solução alternativa**: é possível pode pedir a um administrador para criar a função e a conta de serviço (antes ou depois da implantação/atualização) e o BDC as usará. [Este artigo](kubernetes-rbac.md#cluster-role-required-for-pods-and-nodes-metrics-collection) descreve como criar os artefatos necessários.

### <a name="azdata-bdc-copy-logs-command-failure"></a>Falha no comando `azdata bdc copy-logs`

- **Versões afetadas**: `azdata` versão *20.0.0*

- **Problema e impacto sobre o cliente**: a implementação do comando *copy-logs* supõe que a ferramenta cliente `kubectl` esteja instalada no computador cliente do qual o comando é emitido. Se você estiver emitindo o comando em um cluster BDC instalado no OpenShift, em um cliente em que apenas a ferramenta `oc` estiver instalada, você receberá um erro: *Ocorreu um erro ao coletar os logs: [WinError 2] O sistema não pôde localizar o arquivo especificado*.

- **Solução alternativa**: Instale a ferramenta `kubectl` no mesmo computador cliente e emita novamente o comando `azdata bdc copy-logs`. Confira [aqui](deploy-big-data-tools.md) as instruções de como instalar o `kubectl`.

### <a name="deployment-with-private-repository"></a>Implantação com repositório privado

- **Versões afetadas**: GDR1, CU1, CU2. Resolvido para CU3.

- **Problema e impacto sobre o cliente**: A atualização do repositório privado tem requisitos específicos

- **Solução alternativa**: Se usar um repositório privado para extrair previamente as imagens para implantar ou atualizar o BDC, verifique se as imagens de build atuais e as imagens de build alvo estão no repositório privado. Isso permitirá a reversão bem-sucedida, caso ela seja necessária. Além disso, se você tiver alterado as credenciais do repositório privado depois da implantação original, atualize o segredo correspondente no Kubernetes antes de atualizar. O `azdata` não é compatível com a atualização de credenciais por meio das variáveis de ambiente `AZDATA_PASSWORD` e `AZDATA_USERNAME`. Atualize o segredo usando [`kubectl edit secrets`](https://kubernetes.io/docs/concepts/configuration/secret/#editing-a-secret). 

Não há suporte para a atualização usando diferentes repositórios para builds atuais e alvo.

### <a name="upgrade-may-fail-due-to-timeout"></a>A atualização pode falhar devido ao tempo limite

- **Versões afetadas**: GDR1, CU1, CU2. Resolvido para CU 3.

- **Problema e impacto sobre o cliente**: Uma atualização pode falhar devido ao tempo limite.

   O seguinte exemplo de código mostra como poderia ser a falha:

   ```
   >azdata.EXE bdc upgrade --name <mssql-cluster>
   Upgrading cluster to version 15.0.4003

   NOTE: Cluster upgrade can take a significant amount of time depending on
   configuration, network speed, and the number of nodes in the cluster.

   Upgrading Control Plane.
   Control plane upgrade failed. Failed to upgrade controller.
   ```

   É mais provável que esse erro aconteça quando você atualiza o BDC no AKS (Serviço de Kubernetes do Azure).

- **Solução alternativa**: Aumente o tempo limite para a atualização. 

   Para aumentar os tempos limite de uma atualização, edite o mapa de configuração da atualização. Para editar o mapa de configuração da atualização:

   1. Execute o comando a seguir:

      ```bash
      kubectl edit configmap controller-upgrade-configmap
      ```

   2. Edite os seguintes campos:

       O **`controllerUpgradeTimeoutInMinutes`** designa o número de minutos que deverão ser aguardados para que o controlador ou o banco de dados do controlador conclua a atualização. O padrão é 5. Atualize para pelo menos 20.

       **`totalUpgradeTimeoutInMinutes`** : designa a quantidade combinada de tempo em que o controlador e o banco de dados do controlador concluem a atualização (atualização do `controller` + `controllerdb`). O padrão é 10. Atualize para pelo menos 40.

       **`componentUpgradeTimeoutInMinutes`** : designa a quantidade de tempo em que cada fase subsequente da atualização precisa ser concluída. O padrão é 30. Atualize para 45.

   3. Salvar e sair

   O script do Python abaixo é outra maneira de definir o tempo limite:

   ```python
   from kubernetes import client, config
   import json

   def set_upgrade_timeouts(namespace, controller_timeout=20, controller_total_timeout=40, component_timeout=45):
       """ Set the timeouts for upgrades

       The timeout settings are as follows

       controllerUpgradeTimeoutInMinutes: sets the max amount of time for the controller
           or controllerdb to finish upgrading

       totalUpgradeTimeoutInMinutes: sets the max amount of time to wait for both the
           controller and controllerdb to complete their upgrade

       componentUpgradeTimeoutInMinutes: sets the max amount of time allowed for
           subsequent phases of the upgrade to complete
       """
       config.load_kube_config()

       upgrade_config_map = client.CoreV1Api().read_namespaced_config_map("controller-upgrade-configmap", namespace)

       upgrade_config = json.loads(upgrade_config_map.data["controller-upgrade"])

       upgrade_config["controllerUpgradeTimeoutInMinutes"] = controller_timeout

       upgrade_config["totalUpgradeTimeoutInMinutes"] = controller_total_timeout

       upgrade_config["componentUpgradeTimeoutInMinutes"] = component_timeout

       upgrade_config_map.data["controller-upgrade"] = json.dumps(upgrade_config)

       client.CoreV1Api().patch_namespaced_config_map("controller-upgrade-configmap", namespace, upgrade_config_map)
   ```

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>O envio de trabalho do Livy do ADS (Azure Data Studio) ou da ondulação falha com o erro 500

- **Problema e impacto sobre o cliente**: Em uma configuração de HA, os recursos compartilhados do Spark `sparkhead` são configurados com várias réplicas. Nesse caso, você pode encontrar falhas com o envio de trabalho do Livy do ADS (Azure Data Studio) ou `curl`. Para verificar, `curl` para qualquer pod do `sparkhead` resulta em uma conexão recusada. Por exemplo, `curl https://sparkhead-0:8998/` ou `curl https://sparkhead-1:8998` retorna um erro 500.

   Isso acontece dos seguintes cenários:

   - Os pods ou processos de cada instância do ZooKeeper, são reiniciados algumas vezes.
   - Quando a conectividade de rede não é confiável entre o pod do `sparkhead` e os pods do ZooKeeper.

- **Solução alternativa**: Reiniciar ambos os servidores Livy.

   ```bash
   kubectl -n <clustername> exec sparkhead-0 -c hadoop-livy-sparkhistory supervisorctl restart livy
   ```

   ```bash
   kubectl -n <clustername> exec sparkhead-1 -c hadoop-livy-sparkhistory supervisorctl restart livy
   ```

### <a name="create-memory-optimized-table-when-master-instance-in-an-availability-group"></a>Criar uma tabela otimizada para memória quando a instância mestra em um grupo de disponibilidade

- **Problema e impacto sobre o cliente**: Você não pode usar o ponto de extremidade primário exposto para conectar-se a bancos de dados do grupo de disponibilidade (ouvinte) para criar tabelas otimizadas para memória.

- **Solução alternativa**: Para criar tabelas otimizadas para memória quando a instância mestra do SQL Server for uma configuração de grupo de disponibilidade, [conecte-se à instância do SQL Server](deployment-high-availability.md#instance-connect), exponha um ponto de extremidade, conecte-se ao banco de dados do SQL Server e crie as tabelas otimizadas para memória na sessão criada com a nova conexão.

### <a name="insert-to-external-tables-active-directory-authentication-mode"></a>Inserir no modo de autenticação do Active Directory de tabelas externas

- **Problema e impacto sobre o cliente**: Quando a instância mestra do SQL Server está no modo de autenticação do Active Directory, uma consulta que seleciona somente de tabelas externas, em que pelo menos uma das tabelas externas está em um pool de armazenamento e insere em outra tabela externa, a consulta retorna:

   ```
   Msg 7320, Level 16, State 102, Line 1
   Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "SQLNCLI11". Only domain logins can be used to query Kerberized storage pool.
   ```

- **Solução alternativa**: Modifique a consulta de uma das maneiras a seguir. Ingresse a tabela do pool de armazenamento em uma tabela local ou insira-a primeiro na tabela local e depois leia da tabela local para inseri-la no pool de dados.

### <a name="transparent-data-encryption-capabilities-can-not-be-used-with-databases-that-are-part-of-the-availability-group-in-the-sql-server-master-instance"></a>As funcionalidades de Transparent Data Encryption não podem ser usadas com bancos de dados que fazem parte do grupo de disponibilidade na instância mestra do SQL Server

- **Problema e impacto sobre o cliente**: Em uma configuração de HA, os bancos de dados com criptografia habilitada não podem ser usados após um failover, pois a chave mestra usada para criptografia é diferente em cada réplica. 

- **Solução alternativa**: Não há nenhuma solução alternativa para esse problema. É recomendável não habilitar a criptografia nessa configuração até que uma correção esteja em vigor.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
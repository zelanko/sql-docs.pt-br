---
title: Notas sobre a versão de Clusters de Big Data do SQL Server
titleSuffix: SQL Server big data clusters
description: Este artigo descreve as atualizações mais recentes e problemas conhecidos dos Clusters de Big Data do SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 03/31/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cd004554ad45db40beae958bdf0a7142b1b74bab
ms.sourcegitcommit: 2426a5e1abf6ecf35b1e0c062dc1e1225494cbb0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80517161"
---
# <a name="sql-server-2019-big-data-clusters-release-notes"></a>Notas sobre a versão de Clusters de Big Data do SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

As notas sobre a versão a seguir se aplicam a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Este artigo está dividido em seções para cada versão. Cada versão tem um link para um artigo de suporte que descreve as alterações da CU, bem como links para os downloads dos pacotes do Linux. O artigo também lista [problemas conhecidos](#known-issues) para as versões mais recentes do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC).

## <a name="supported-platforms"></a>Plataformas compatíveis

Nesta seção, há uma explicação sobre as plataformas compatíveis com o BDC.

### <a name="kubernetes-platforms"></a>Plataformas do Kubernetes

|Plataforma|Versões com suporte|
|---------|---------|
|Kubernetes|O BDC requer a versão mínima do Kubernetes 1.13. Confira a [política de suporte a distorção de versão e kubernetes do Kubernetes](https://kubernetes.io/docs/setup/release/version-skew-policy/) para a política de suporte à versão do Kubernetes.|
|AKS (Serviço de Kubernetes do Azure)|O BDC requer a versão mínima do AKS 1.13.<br/>Confira [Versões do Kubernetes com suporte no AKS](/azure/aks/supported-kubernetes-versions) para obter a política de suporte de versão.|

### <a name="host-os-for-kubernetes"></a>SO host para Kubernetes

|Plataforma|Versões com suporte|
|---------|---------|
|Red Hat Enterprise Linux|7.3, 7.4, 7.5, 7.6|
|Ubuntu|16.04|

### <a name="sql-server-editions"></a>Edições do SQL Server

|Edition|Observações|
|---------|---------|
|Enterprise<br/>Standard<br/>Desenvolvedor| A edição de cluster de Big Data é determinada pela edição da instância mestra do SQL Server. No momento da implantação, a Developer Edition é implantada por padrão. Você pode alterar a edição após a implantação. Confira [Configurar a instância mestra do SQL Server](../big-data-cluster/configure-sql-server-master-instance.md). |

## <a name="tools"></a>Ferramentas

|Plataforma|Versões com suporte|
|---------|---------|
|`azdata`|Deve ser a mesma versão secundária que a do servidor (a mesma instância mestra do SQL Server).<br/><br/>Execute `azdata –-version` para validar a versão.<br/><br/>Confira o [Histórico de versões](#release-history) para ver a versão mais recente.|
|Azure Data Studio|Obtenha o build mais recente do [Azure Data Studio](https://aka.ms/getazuredatastudio).|

## <a name="release-history"></a>Histórico de versões

A tabela a seguir lista o histórico de versões do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].

| Versão               | Versão         | Data de liberação |
|-----------------------|-----------------|--------------|
| [CU4](#cu4)           | 15.0.4033.1     | 2020-03-31   |
| [CU3](#cu3)           | 15.0.4023.6     | 2020-03-12   |
| [CU2](#cu2)           | 15.0.4013.40    | 2020-02-13   |
| [CU1](#cu1)           | 15.0.4003.23    | 2020-01-07   |
| [GDR1](#rtm)          | 15.0.2070.34    | 2019-11-04   |

## <a name="how-to-install-updates"></a>Como instalar atualizações

Para instalar atualizações, confira [Como atualizar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-upgrade.md).

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

       **`totalUpgradeTimeoutInMinutes`** : designa a quantidade combinada de tempo em que o controlador e o banco de dados do controlador concluem a atualização (atualização do controlador + banco de dados do controlador). O padrão é 10. Atualize para pelo menos 40.

       **`componentUpgradeTimeoutInMinutes`** : designa a quantidade de tempo em que cada fase subsequente da atualização precisa ser concluída.  O padrão é 30. Atualize para 45.

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

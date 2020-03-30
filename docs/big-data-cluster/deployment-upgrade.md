---
title: Atualizar para uma nova versão
titleSuffix: SQL Server Big Data Clusters
description: Saiba como atualizar Clusters de Big Data do SQL Server para uma nova versão.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2f8ca3e42221387470ee4fc4cbd6873b526bc8b7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77256859"
---
# <a name="how-to-upgrade-big-data-clusters-2019"></a>Como atualizar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O caminho de atualização depende da versão atual do BDC (Cluster de Big Data) do SQL Server. A atualização de uma versão com suporte, incluindo a GDR (versão de distribuição geral), CU (atualização cumulativa) ou atualização de QFE (Quick Fix Engineering), pode ser feita no local. Não há suporte para a atualização in-loco de uma CTP (versão prévia da tecnologia do cliente) ou da versão Release Candidate do BDC. Você precisa remover e recriar o cluster. As seguintes seções descrevem as etapas de cada cenário:

- [Atualização a partir da versão com suporte](#upgrade-from-supported-release)
- [Atualizar uma implantação BDC do CTP ou da versão Release Candidate](#update-a-bdc-deployment-from-ctp-or-release-candidate)

>[!NOTE]
>A primeira versão com suporte de Clusters de Big Data é o SQL Server 2019 GDR1.

## <a name="upgrade-release-notes"></a>Notas sobre a versão da atualização

Antes de continuar, confira as [notas sobre a versão da atualização para ver os problemas conhecidos](release-notes-big-data-cluster.md#known-issues).

## <a name="upgrade-from-supported-release"></a>Atualização a partir da versão com suporte

Esta seção explica como atualizar um BDC do SQL Server de uma versão com suporte (do SQL Server 2019 GDR1 em diante) para uma versão mais recente com suporte.

1. Faça backup da instância mestra do SQL Server.
2. Faça backup do HDFS.

   ```
   azdata bdc hdfs cp --from-path <path> --to-path <path>
   ```
   
   Por exemplo: 

   ```
   azdata bdc hdfs cp --from-path hdfs://user/hive/warehouse/%%D --to-path ./%%D
   ```

3. Atualizar `azdata`.

   Siga as instruções para instalar o `azdata`. 
   - [Windows Installer](deploy-install-azdata-installer.md)
   - [Linux com apt](deploy-install-azdata-linux-package.md)
   - [Linux com yum](deploy-install-azdata-yum.md)
   - [Linux com zypper](deploy-install-azdata-zypper.md)

   >[!NOTE]
   >Se `azdata` tiver sido instalado com `pip`, você precisará removê-lo manualmente antes da instalação com o Windows Installer ou o gerenciador de pacotes do Linux.

1. Atualize o Cluster de Big Data.

   ```
   azdata bdc upgrade -n <clusterName> -t <imageTag> -r <containerRegistry>/<containerRepository>
   ```

   Por exemplo, o script a seguir usa a marca de imagem `2019-CU1-ubuntu-16.04`:

   ```
   azdata bdc upgrade -n bdc -t 2019-CU1-ubuntu-16.04 -r mcr.microsoft.com/mssql/bdc
   ```

>[!NOTE]
>As marcas de imagem mais recentes estão disponíveis nas [Notas sobre a versão dos Clusters de Big Data do SQL Server 2019](release-notes-big-data-cluster.md).

>[!IMPORTANT]
>Se você usar um repositório privado para extrair previamente as imagens para implantar ou atualizar o BDC, verifique se as imagens de build atuais e >as imagens de build de destino estão no repositório privado. Isso permitirá a reversão bem-sucedida, caso ela seja necessária. Além disso, se você tiver alterado as >credenciais do repositório privado depois da implantação original, atualize as variáveis de ambiente DOCKER_PASSWORD e >DOCKER_USERNAME correspondentes. Não há suporte para a atualização usando diferentes repositórios privados para builds atuais e de destino.

### <a name="increase-the-timeout-for-the-upgrade"></a>Aumentar o tempo limite para a atualização

Um tempo limite poderá acontecer se determinados componentes não forem atualizados no tempo alocado. O seguinte exemplo de código mostra como poderia ser a falha:

   ```
   >azdata.EXE bdc upgrade --name <mssql-cluster>
   Upgrading cluster to version 15.0.4003

   NOTE: Cluster upgrade can take a significant amount of time depending on
   configuration, network speed, and the number of nodes in the cluster.

   Upgrading Control Plane.
   Control plane upgrade failed. Failed to upgrade controller.
   ```

Para aumentar os tempos limite de uma atualização, use os parâmetros **--controller-timeout** e **--component-timeout** para especificar valores maiores ao emitir a atualização. Essa opção está disponível apenas da versão SQL Server 2019 CU2 em diante. Por exemplo:

   ```bash
   azdata bdc upgrade -t 2019-CU2-ubuntu-16.04 --controller-timeout=40 --component-timeout=40 --stability-threshold=3
   ```
O **--controller-timeout** designa o número de minutos que você deverá aguardar para que o controlador ou o banco de dados do controlador conclua a atualização.
**--component-timeout** designa a quantidade de tempo em que cada fase subsequente da atualização precisa ser concluída.

Para aumentar os tempos limite de uma atualização antes da versão do SQL Server 2019 CU2, edite o mapa de configuração da atualização. Para editar o mapa de configuração da atualização:

Execute o comando a seguir:

   ```bash
   kubectl edit configmap controller-upgrade-configmap
   ```

Edite os seguintes campos:

   **controllerUpgradeTimeoutInMinutes** designa o número de minutos que deverão ser aguardados para que o controlador ou o banco de dados do controlador conclua a atualização. O padrão é 5. Atualize para pelo menos 20.
   **totalUpgradeTimeoutInMinutes**: designa a quantidade combinada de tempo em que o controlador e o banco de dados do controlador concluem a atualização (atualização do controlador + banco de dados do controlador). O padrão é 10. Atualize para pelo menos 40.
   **componentUpgradeTimeoutInMinutes**: designa a quantidade de tempo em que cada fase subsequente da atualização precisa ser concluída. O padrão é 30. Atualize para 45.

Salve e saia.

## <a name="update-a-bdc-deployment-from-ctp-or-release-candidate"></a>Atualizar uma implantação BDC do CTP ou da versão Release Candidate

Não há suporte para uma atualização in-loco de uma CTP ou da versão Release Candidate dos Clusters de Big Data do SQL Server. A seção a seguir explica como remover e recriar o cluster manualmente.

### <a name="backup-and-delete-the-old-cluster"></a>Fazer backup e excluir o cluster antigo

Não há atualização in-loco para clusters de Big Data implantados antes do SQL Server 2019 GDR1. A única maneira de atualizar para uma nova versão é remover o cluster manualmente e recriá-lo. Cada versão tem uma versão exclusiva do `azdata` que não é compatível com a versão anterior. Além disso, se uma imagem de contêiner for baixada em um cluster implantado com outra versão mais antiga, a imagem mais recente poderá não ser compatível com as imagens mais antigas no cluster. A imagem mais nova será capturada se você estiver usando a marca de imagem `latest` no arquivo de configuração de implantação nas configurações do contêiner. Por padrão, cada versão tem uma tag de imagem específica correspondente à versão de lançamento do SQL Server. Para fazer a atualização para a última versão, use as seguintes etapas:

1. Antes de excluir o cluster antigo, faça backup dos dados na instância mestra do SQL Server e no HDFS. Para a instância mestra do SQL Server, você poderá usar [Backup e restauração do SQL Server](data-ingestion-restore-database.md). Para o HDFS, você [pode copiar os dados com o `curl`](data-ingestion-curl.md).

1. Exclua o cluster antigo com o comando `azdata delete cluster`.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use a versão do `azdata` que corresponde ao cluster. Não exclua um cluster mais antigo com a versão mais recente do `azdata`.

   > [!Note]
   > A emissão de um comando `azdata bdc delete` resultará em todos os objetos criados dentro do namespace identificado com o nome do cluster de Big Data serem excluídos, mas não o próprio namespace. O namespace pode ser reutilizado para implantações subsequentes, desde que esteja vazio e nenhum outro aplicativo tenha sido criado dentro dele.

1. Desinstale a versão antiga do `azdata`.

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Instalar a versão mais recente do `azdata`. Os comandos a seguir instalam `azdata` da versão mais recente:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > Para cada versão, o caminho para a versão `n-1` do `azdata` muda. Mesmo que você tenha instalado o `azdata` anteriormente, precisará reinstalar com base no caminho mais recente antes de criar o cluster.

### <a name="verify-the-azdata-version"></a><a id="azdataversion"></a> Verificar a versão do azdata

Antes de implantar um novo cluster de Big Data, verifique se você está usando a última versão do `azdata` com o parâmetro `--version`:

```bash
azdata --version
```

### <a name="install-the-new-release"></a>Instalar a nova versão

Depois de remover o cluster de Big Data anterior e instalar o `azdata` mais recente, implante o novo cluster de Big Data usando as instruções de implantação atuais. Para obter mais informações, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md). Em seguida, restaure os bancos de dados ou os arquivos necessários.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md).

---
title: Implantar um cluster de Big Data do SQL Server com os notebooks do Azure Data Studio
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Use um notebook do Azure Data Studio para implantar um cluster de Big Data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: dfdf7dfd2ca5521bd80c4fdbf81e7b5c45d58b8d
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594221"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>Implantar um cluster de Big Data do SQL Server com os notebooks do Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornece uma extensão para o Azure Data Studio que inclui notebooks de implantação. Um notebook de implantação inclui documentação e código que você pode usar no Azure Data Studio para criar um cluster de Big Data do SQL Server.

Implementados inicialmente como um projeto de software livre, os [notebooks](notebooks-guidance.md) foram implementados no [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download). Você pode usar markdown de texto nas células de texto e um dos kernels disponíveis para escrever código nas células de código.

Você pode usar notebooks para implantar clusters de Big Data para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="prerequisites"></a>Prerequisites

Os pré-requisitos a seguir são necessários para também iniciar o notebook:

* Versão mais recente do [build do Azure Data Studio Insiders](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master) instalada

Além disso, a implantação do cluster de Big Data do SQL Server 2019 também requer:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI do Azure (se estiver implantando no Azure)](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)

## <a name="launch-the-notebook"></a>Iniciar o notebook

1. Iniciar o Azure Data Studio.

2. Na guia **Conexões**, selecione as reticências ( **...** ) e, em seguida, selecione **Implantar SQL Server...** .

   ![Implantar SQL Server](media/deploy-notebooks/deploy-notebooks.png)

3. Nas opções de implantação, selecione **Cluster de Big Data do SQL Server**.

4. No **Destino da Implantação**, em **Opções**, selecione **Novo cluster do Kubernetes do Azure** ou **Cluster existente do Serviço de Kubernetes do Azure**.

5. Aceitar os termos de privacidade e licença

6. Essa caixa de diálogo também verifica se as ferramentas necessárias para o tipo de implantação do SQL escolhido existem no host. O botão **Selecionar** não estará habilitado até que a verificação de ferramentas seja bem-sucedida.

7. Escolha o botão **Selecionar**. Essa ação inicia a experiência de implantação.

## <a name="set-deployment-configuration-template"></a>Definir modelo de configuração de implantação

Você pode personalizar as configurações do perfil de implantação seguindo as instruções abaixo.

### <a name="target-configuration-template"></a>Modelo de configuração de destino

Selecione o modelo de configuração de destino entre os modelos disponíveis. Os perfis disponíveis são filtrados dependendo do tipo de destino de implantação escolhido na caixa de diálogo anterior.

   ![Etapa 1 do modelo de configuração de implantação](media/deploy-notebooks/deployment-configuration-template.png)

### <a name="azure-settings"></a>Configurações do Azure

Se o destino de implantação for um novo AKS, informações adicionais, como ID de assinatura do Azure, grupo de recursos, nome do cluster do AKS, contagem de VMs, tamanho e outras informações adicionais, serão necessárias para criar o cluster do AKS.

   ![Configurações do Azure](media/deploy-notebooks/azure-settings.png)

Se o destino de implantação for um cluster Kubernetes existente, o assistente solicitará o caminho para o arquivo de configuração de *kube* para importar as configurações do cluster do Kubernetes. Verifique se o contexto do cluster apropriado está selecionado em um local em que o cluster de Big Data do SQL Server 2019 possa ser implantado.

   ![Contexto do cluster de destino](media/deploy-notebooks/target-cluster-context.png)

### <a name="cluster-docker-and-ad-settings"></a>Configurações de cluster, Docker e AD

1. Insira o nome do cluster para o BDC do SQL Server 2019, o nome de usuário do administrador e a senha.
Observação: A mesma conta é usada para o controlador e para o SQL Server.

   ![Configurações do cluster](media/deploy-notebooks/cluster-settings.png)

2. Insira as configurações do Docker conforme apropriado

   ![Configurações do Docker](media/deploy-notebooks/docker-settings.png)

3. Se a autenticação do AD estiver disponível, insira as configurações do AD

   ![Configurações do Active Directory](media/deploy-notebooks/active-directory-settings.png)

### <a name="service-settings"></a>Configurações de serviço

Esta tela tem entradas para várias configurações, como **Escala**, **Pontos de Extremidade**, **Armazenamento** e outras **Configurações de armazenamento avançadas**. Insira os valores apropriados e selecione **Avançar**.

#### <a name="scale-settings"></a>Configurações de dimensionamento

Insira o número de instâncias de cada um dos componentes no Cluster de Big Data.

Uma instância do Spark pode ser incluída junto com o HDFS. Ela é incluída no pool de armazenamento ou sozinha no Pool do Spark.

   ![Configurações de serviço](media/deploy-notebooks/service-settings.png)

Para obter mais informações sobre cada um desses componentes, você pode consultar [instância mestra](concept-master-instance.md), [pool de dados](concept-data-pool.md), [pool de armazenamento](concept-storage-pool.md) ou [pool de computação](concept-compute-pool.md).

#### <a name="endpoint-settings"></a>Configurações de ponto de extremidade

Os pontos de extremidade padrão foram preenchidos previamente. No entanto, eles podem ser alterados conforme apropriado.

   ![Configurações de ponto de extremidade](media/deploy-notebooks/endpoint-settings.png)

#### <a name="storage-settings"></a>Configurações de armazenamento

As configurações de armazenamento incluem classe de armazenamento e tamanho de declaração para Dados e Logs. As configurações podem ser aplicadas em Armazenamento, Dados e pool mestre do SQL Server.

   ![Configurações de armazenamento](media/deploy-notebooks/storage-settings.png)

#### <a name="advanced-storage-settings"></a>Configurações avançadas de armazenamento

Você pode adicionar configurações de armazenamento em **Configurações avançadas de armazenamento**

* Pool de armazenamento (HDFS)
* Pool de dados
* SQL Server Mestre

   ![Configurações avançadas de armazenamento](media/deploy-notebooks/advanced-storage-settings.png)

### <a name="summary"></a>Resumo

Esta tela resume todas as entradas fornecidas para implantar o Cluster de Big Data do SQL Server 2019. Os arquivos de configuração podem ser baixados usando o botão **Salvar arquivos de configuração**. Selecione **Script para o Notebook** para gerar script de toda a configuração de implantação em um Notebook. Quando o Notebook estiver aberto, selecione **Células de Execução** para iniciar a implantação do BDC do SQL Server 2019 no destino selecionado.

   ![Resumo](media/deploy-notebooks/deploy-sql-server-big-data-cluster-on-a-new-AKS-cluster.png)

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre a implantação, confira as [diretrizes de implantação para clusters de Big Data do SQL Server](deployment-guidance.md).

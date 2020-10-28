---
title: Monitorar cluster com o Azure Data Studio
titleSuffix: SQL Server Big Data Clusters
description: Monitorar cluster com o Azure Data Studio no Cluster de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4c4dc9956b8c3f9802feb839096195c09664d0d6
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378334"
---
# <a name="monitor-cluster-status-with-azure-data-studio"></a>Monitorar status do cluster com Azure Data Studio

Este artigo explica como exibir o status de um Cluster de Big Data usando o Azure Data Studio.

## <a name="use-azure-data-studio"></a><a id="datastudio"></a> Usar o Azure Data Studio

Depois de baixar o **build para insiders** mais recente do [Azure Data Studio](https://aka.ms/getazuredatastudio), você pode exibir pontos de extremidade de serviço e o status de um cluster de Big Data com o painel do cluster de Big Data do SQL Server. Alguns dos recursos a seguir estão disponíveis apenas no build para insiders do Azure Data Studio.

1. Primeiro, crie uma conexão com o cluster de Big Data no Azure Data Studio. Para obter mais informações, confira [Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md).

1. Clique com o botão direito do mouse no ponto de extremidade do cluster de Big Data e clique em **Gerenciar** .

   ![clicar com o botão direito do mouse em gerenciar](media/view-cluster-status/right-click-manage.png)

1. Selecione a guia **Cluster de Big Data do SQL Server** para acessar o painel do cluster de Big Data.

   ![Painel do cluster de Big Data](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Pontos de extremidade de serviço

É importante poder acessar facilmente os vários serviços em um cluster de Big Data. O painel do cluster de Big Data fornece uma tabela dos pontos de extremidade de serviço que permite ver e copiá-los.

![pontos de extremidade de serviço](media/view-cluster-status/service-endpoints.png)

Esses serviços listam os pontos de extremidade que podem ser copiados e colados quando você precisar do ponto de extremidade para se conectar a eles. Por exemplo, você pode clicar no ícone de copiar à direita do ponto de extremidade e colá-lo em uma janela de texto que solicita esse ponto de extremidade. O ponto de extremidade do Serviço de Gerenciamento do Cluster é necessário para executar o [notebook do status do cluster](#notebook).

### <a name="dashboards"></a>Painéis

A tabela de pontos de extremidade de serviço também expõe vários painéis para monitoramento:

- Métricas (Grafana)
- Logs (Kibana)
- Monitoramento de Trabalhos do Spark
- Gerenciamento de Recursos do Spark

Você pode clicar diretamente nesses links. Você será solicitado a autenticar ao acessar esses painéis. Para os painéis de métricas e logs, forneça as credenciais de administrador do controlador que você definiu no momento da implantação usando as variáveis de ambiente **AZDATA_USERNAME** e **AZDATA_PASSWORD** . Os painéis do Spark usarão as credenciais do gateway (Knox): a identidade do AD em um cluster integrado ao AD ou, se estiver usando a autenticação Básica no cluster, **AZDATA_USERNAME** e **AZDATA_PASSWORD** .

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

### <a name="cluster-status-notebook"></a><a id="notebook"></a> Notebook de Status do Cluster

1. Você também pode exibir o status do cluster de Big Data iniciando o notebook de Status do Cluster. Para iniciar o notebook, clique na tarefa **Status do Cluster** .

    ![inicialização](media/view-cluster-status/cluster-status-launch.png)

2. Antes de começar, você precisará dos seguintes itens:

    - Nome do cluster de Big Data
    - Nome de usuário do controlador
    - Senha do controlador
    - Pontos de extremidade do controlador

    O nome do cluster de Big Data padrão é **mssql-cluster** , a menos que você o tenha personalizado durante a implantação. É possível encontrar o ponto de extremidade do controlador no painel do cluster de Big Data na tabela Pontos de Extremidade do Serviço. O ponto de extremidade está listado como **Serviço de Gerenciamento do Cluster** . Se não conhecer as credenciais, peça ao administrador que implantou o cluster.

3. Clique em **Executar Células** na barra de ferramentas superior.

4. Siga o prompt para fornecer suas credenciais. Pressione ENTER depois de digitar cada credencial para o nome do cluster de Big Data, o nome de usuário do controlador e a senha do controlador.

    > [!Note]
    > Se você não tiver uma instalação de arquivo de configuração com seu Big Data, será solicitado que você informe o ponto de extremidade do controlador. Digite ou cole-o e pressione ENTER para continuar.

5. Se você tiver se conectado com êxito, o restante do notebook mostrará a saída de cada componente do cluster de Big Data. Quando quiser executar novamente uma determinada célula de código, passe o mouse sobre a célula de código e clique no ícone **Executar** .


## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).

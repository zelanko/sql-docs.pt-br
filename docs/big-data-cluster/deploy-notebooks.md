---
title: Implantar um cluster de Big Data do SQL Server com os notebooks do Azure Data Studio
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Use um notebook do Azure Data Studio para implantar um cluster de Big Data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d68baa615f384dd5afb665f29decb6d72113c5a3
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028568"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>Implantar um cluster de Big Data do SQL Server com os notebooks do Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornece uma extensão para o Azure Data Studio que inclui notebooks de implantação. Um notebook de implantação inclui documentação e código que você pode usar no Azure Data Studio para criar um cluster de Big Data do SQL Server.

Originalmente implementados como um projeto de software livre, os [notebooks](notebooks-guidance.md) foram implementados no [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download). Você pode usar markdown de texto nas células de texto e um dos kernels disponíveis para escrever código nas células de código.

Você pode usar notebooks para implantar clusters de Big Data para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="prerequisites"></a>Pré-requisitos

Os pré-requisitos a seguir são necessários para poder iniciar o notebook:

* Versão mais recente da [compilação do Azure Data Studio](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master) insiders instalada
* Extensão do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] instalada no Azure Data Studio

Além disso, a implantação do cluster de Big Data do SQL Server 2019 também requer:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI do Azure](/cli/azure/install-azure-cli)

## <a name="launch-the-notebook"></a>Iniciar o notebook

1. Inicie o Azure Data Studio insiders.

1. Na guia **Conexões**, clique em **...** e selecione **Implantar cluster de Big Data do SQL Server...** .

   ![IA e ML](media/deploy-notebooks/deploy-notebooks-1.png)

1. No **Destino da Implantação**, em **Opções**, selecione **Novo cluster do Kubernetes do Azure** ou **Cluster existente do Serviço de Kubernetes do Azure**.

1. Clique no botão **selecionar** .

1. Essa ação inicia uma caixa de diálogo para coletar a entrada do usuário, fornecer as informações necessárias e examinar os valores padrão.

1. Clique no botão **abrir bloco de anotações** .
Essa ação inicia o notebook apropriado. Para concluir a implantação, siga as instruções no notebook para implantar um cluster de Big Data para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] em um cluster novo ou existente do Serviço de Kubernetes do Azure.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre a implantação, confira as [diretrizes de implantação para clusters de Big Data do SQL Server](deployment-guidance.md).

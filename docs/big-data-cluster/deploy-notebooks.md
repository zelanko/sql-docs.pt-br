---
title: Implantar SQL Server Cluster de Big Data com blocos de anotações do Azure Data Studio
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Use um bloco de anotações do Azure Data Studio para implantar um cluster Big Data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f12a4f06ceb1c3a48b2b2fc661c59594e6d6cce3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426416"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>Implantar SQL Server Cluster de Big Data com blocos de anotações do Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]fornece uma extensão para Azure Data Studio que inclui blocos de anotações de implantação. Um bloco de anotações de implantação inclui documentação e código que você pode usar em Azure Data Studio para criar um cluster de Big Data SQL Server. 

Originalmente implementado como um projeto de software livre, os [blocos de anotações](notebooks-guidance.md) foram implementados no [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download). Você pode usar a redução de texto nas células de texto e um dos kernels disponíveis para escrever código nas células de código.

Você pode usar blocos de anotações para implantar Big Data clusters [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]para o.

## <a name="prerequisites"></a>Pré-requisitos
Os pré-requisitos a seguir são necessários para poder iniciar o bloco de anotações:

* Versão mais recente do [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download) instalada
* [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]extensão instalada no Azure Data Studio

Além disso, a implantação do SQL Server 2019 Big Data cluster também requer:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI do Azure](/cli/azure/install-azure-cli)

## <a name="launch-the-notebook"></a>Iniciar o bloco de anotações

1. Instale e inicie a [compilação do Azure Data Studio](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)insiders.
1.  Na guia **conexões** , clique em **...** e selecione **implantar SQL Server Cluster de Big Data...** .

   ![IA e ML](media/deploy-notebooks/deploy-notebooks-1.png)

1. No **destino de implantação**, em **Opções**, selecione **novo cluster do Azure kubernetes** ou **cluster do serviço kubernetes do Azure existente**.
1. Selecione **abrir bloco de anotações**.

Essa ação inicia o bloco de anotações apropriado. Para concluir a implantação, siga as instruções no bloco de anotações para implantar um cluster Big data [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] para o em um cluster do serviço kubernetes do Azure existente ou novo.

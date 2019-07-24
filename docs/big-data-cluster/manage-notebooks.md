---
title: Gerenciar SQL Server Cluster de Big Data com blocos de anotações do Azure Data Studio
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Use um bloco de anotações do Azure Data Studio para gerenciar e solucionar problemas de um cluster Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8d87b09878539cccd40191d870bf97487579dca2
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426396"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>Gerenciar clusters de Big Data para SQL Server com blocos de anotações do Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]fornece uma extensão para Azure Data Studio que inclui blocos de anotações de implantação. Um bloco de anotações de implantação inclui documentação e código que você pode usar em Azure Data Studio para gerenciar clusters Big Data para SQL Server.

Originalmente implementado como um projeto de software livre, os [blocos de anotações](notebooks-guidance.md) foram implementados no [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download). Você pode usar a redução de texto nas células de texto e um dos kernels disponíveis para escrever código nas células de código.

Você pode usar blocos de anotações para implantar Big Data clusters [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]para o.

## <a name="prerequisites"></a>Pré-requisitos

Os pré-requisitos a seguir são necessários para poder iniciar o bloco de anotações:

* Versão mais recente da [compilação do Azure Data Studio](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master) insiders
* [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]extensão instalada no Azure Data Studio

Além disso, a implantação do SQL Server 2019 Big Data cluster também requer:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI do Azure](/cli/azure/install-azure-cli)

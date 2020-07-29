---
title: Instalar o azdata
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar Clusters de Big Data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: dbb484c6858e9024fdbbaa4d12c15480d7314bc9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784267"
---
# <a name="install-azdata"></a>Instalar `azdata`

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

`azdata` é um utilitário de linha de comando escrito em Python para inicializar e gerenciar o cluster de Big Data por meio de APIs REST. 

## <a name="find-latest-version"></a>Localizar a versão mais recente

A lista de arquivos para a versão mais recente está sempre disponível em [https://aka.ms/azdata](https://aka.ms/azdata).

Para localizar sua versão instalada e ver se você precisar atualizá-la, execute `azdata --version`.

## <a name="os-specific-instructions"></a>Instruções específicas do SO

* [Instalar no Windows](deploy-install-azdata-installer.md)
* [Instalar no macOS](deploy-install-azdata-macos.md)
* Instalar no Linux ou [Subsistema Windows para Linux (WSL)](/windows/wsl/about/)
   * [Instalar com apt no Debian ou Ubuntu](deploy-install-azdata-linux-package.md)
   * [Instalar com o yum no RHEL, no Fedora ou no CentOS](deploy-install-azdata-yum.md)
   * [Instalar com o Zypper no openSUSE ou no SLE](deploy-install-azdata-zypper.md)
   * [Instalar do script](deploy-install-azdata-pip.md)

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).

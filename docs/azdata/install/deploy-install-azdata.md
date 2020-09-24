---
title: Instalar o azdata
titleSuffix: ''
description: Saiba como instalar a ferramenta azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 7939aa1575aaeec8edff33a9a9f7101a1014abc2
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914940"
---
# <a name="install-azdata"></a>Instalar `azdata`

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/azdata.md)]

`azdata` é um utilitário de linha de comando escrito em Python para inicializar e gerenciar serviços de dados por meio de APIs REST. 

## <a name="find-latest-version"></a>Localizar a versão mais recente

A lista de arquivos para a versão mais recente está sempre disponível em [https://aka.ms/azdata](https://aka.ms/azdata).

Para localizar sua versão instalada e ver se você precisar atualizá-la, execute `azdata --version`.

## <a name="os-specific-instructions"></a>Instruções específicas do SO

* [Instalar no Windows](../install/deploy-install-azdata-installer.md)
* [Instalar no macOS](../install/deploy-install-azdata-macos.md)
* Instalar no Linux ou [Subsistema Windows para Linux (WSL)](/windows/wsl/about/)
   * [Instalar com apt no Debian ou Ubuntu](../install/deploy-install-azdata-linux-package.md)
   * [Instalar com o yum no RHEL, no Fedora ou no CentOS](../install/deploy-install-azdata-yum.md)
   * [Instalar com o Zypper no openSUSE ou no SLE](../install/deploy-install-azdata-zypper.md)
   * [Instalar do script](../install/deploy-install-azdata-pip.md)

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="next-steps"></a>Próximas etapas

Usar o azdata com clusters de Big Data. Para isso, confira [O que são [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).

Usar o azdata com [serviços de dados habilitados o Azure Arc](/azure/azure-arc/data/)
